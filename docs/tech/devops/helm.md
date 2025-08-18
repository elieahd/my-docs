`HELM` is a package manager for `Kubernetes`.
It simplifies deploying, upgrading and managing `Kubernetes` application.

#### Main concepts

`Chart` contains all the `Kubernetes` manifests needed to deploy an app.

Structure of a chart:

- `Chart.yaml` : metadata (name, version, description)
- `values.yaml` : default configuration values
- `templates/` : parameterized `Kubernetes` YAML files

`HELM` uses Go templating `{{ ... }}` to generate `Kubernetes` manifests dynamically.

#### Getting started

##### 1. Install `HELM` cli

##### 2. Setup `HELM` charts in a project with the command `helm create`

This command creates a chart directory along with the common files and directories used in a chart.

For example :

```sh
helm create devops/helm
```

It will create a directory structure that looks something like this:

```
devops/helm
├── .helmignore    # Contains patterns to ignore when packaging Helm charts.
├── Chart.yaml     # Information about your chart
├── values.yaml    # The default values for your templates
├── charts/        # Charts that this chart depends on
└── templates/     # The template files
    └── tests/     # The test files
```

##### 3. Setup your templates

Define your `Kubernetes` manifests in the `HELM` chart that you have just created.

So under `devops/helm` (our previous created chart), you will define under `/templates/` the manifests :

- `deployment.yaml`
- `service.yaml`
- `ingress.yaml`
- ...

Let's take an example of a manifest : `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Values.app }}-{{ .Values.env }}
  labels:
    app.kubernetes.io/name: {{ .Values.app }}-{{ .Values.env }}
    app.kubernetes.io/component: {{ .Values.app }}-{{ .Values.env }}
    environment: {{ .Values.env }}
spec:
  replicas: {{ .Values.replicas }}
  selector:
    matchLabels:
    app.kubernetes.io/name: {{ .Values.app }}-{{ .Values.env }}
    app.kubernetes.io/component: {{ .Values.app }}-{{ .Values.env }}
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  template:
    metadata:
      labels:
        app.kubernetes.io/name: {{ .Values.app }}-{{ .Values.env }}
        app.kubernetes.io/component: {{ .Values.app }}-{{ .Values.env }}
        environment: {{ .Values.env }}
    spec:
      containers:
        - image: https://hub.docker.com/my-namespace/{{ .Values.app }}:{{ .Values.tag }}
          imagePullPolicy: Always
          name : {{ .Values.app }}-{{ .Values.env }}-cn
          resources:
            limits:
              cpu: {{ .Values.resources.limits.cpu }}
              memory: {{ .Values.resources.limits.memory }}
            requests:
              cpu: {{ .Values.resources.requests.cpu }}
              memory: {{ .Values.resources.requests.memory }}
            # ... simplified for documentation purpose
        {{- if .Values.filebeat.enabled }}
        - image: https://hub.docker.com/elastic/filebeat:8.19.2
          imagePullPolicy: Always
          name : {{ .Values.app }}-{{ .Values.env }}-filebeat-cn
          resources:
            limits:
              cpu: 20m
              memory: 200Mi
            requests:
              cpu: 5m
              memory: 200Mi
            # ... simplified for documentation purpose
        {{- end }}
```

##### 4. Configuration via `values.yaml`

The `values.yaml` file allows you to centralize and override configurations without editing your template files directly.

Here is an example of a `values.yaml` for the app `audit`

- `HOMOL` environment values : `/audit/devops/homol/values.yaml`

```yaml
app: audit
env: homol
replicas: 1

resources:
  limits:
    cpu: 200m
    memory: 200Mi
  requests:
    cpu: 50m
    memory: 200Mi

filebeat:
  enabled: false
```

- `PROD` environment values : `/audit/devops/homol/values.yaml`

```yaml
app: audit
env: prod
replicas: 2

resources:
  limits:
    cpu: 500m
    memory: 500Mi
  requests:
    cpu: 200m
    memory: 500Mi

filebeat:
  enabled: true
```

##### 5. Deployment

Traditionally you would have used `kubectl` to deploy to a `Kubernetes` cluster, by using the command `kubectl apply`

Now that you are using `HELM` you would need to switch that up to use `HELM` cli `upgrade` command :

```sh
helm upgrade --install ${app} devops/helm \
     -f audit/devops/${env}/values.yaml
     --set image.tag=${tag}
     --namespace=${namespace}
     --wait
```

The `tag` value is being passed during deployment time, since the image tag will change everytime you build/push an docker image into your registry

##### Attention point

If you have existing `Kubernetes` manifests in a cluster, and wan to migrate them to use a `HELM` chart, you will need to add some labels and annotations prior to the migration.

`HELM` won't know how to manage an existing `Kubernetes` manifests without the following :

labels :

```yaml
app.kubernetes.io/managed-by: Helm
```

annotations :

```yaml
meta.helm.sh/release-name: ...
meta.helm.sh/release-namespace: ...
```

### Resources

- [Getting Started](https://helm.sh/docs/chart_template_guide/getting_started/)
- [Introduction à Helm](https://blog.stephane-robert.info/docs/conteneurs/orchestrateurs/outils/helm/)
