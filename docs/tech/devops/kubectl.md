# My most used K8S commands

## Deployments
```sh
kubectl get deployments -n <namespace>
```

You can hide headers with `--no-headers`
```sh
kubectl get deployments 
    --no-headers
    -n <namespace>
```

You can select custom columns, for example to show deployments with available replicas
```sh
kubectl get deployments
  -o custom-columns="NAME:.metadata.name, REPLICAS:.status.availableReplicas"
  -n <namespace>
```

## Cron Jobs
```sh
kubectl get cronjobs -n <namespace>
```

You can check the last scheduled time, last successful time and suspended info for all cron jobs with : 

```sh
kubectl get cronjobs 
   -o custom-columns="NAME:.metadata.name, LAST_SCHEDULED:.status.lastScheduleTime, LAST_SUCCESSFUL=.status.lastSuccessfulTime, ON_HOLD:.spec.suspend"
   -n <namespace> 
```

## Jobs
```sh
kubectl get jobs -n <namespace>
```

You can get the latest jobs sorted by creation timestamp for a given cron job (by filtering by label)

```sh
kubectl get jobs 
    -l app.kubernetes.io/component=<cron-job-name>
    --sort-by=.metadata.creationTimestamp
    -n <namespace>
```

To return the latest job status for a given cron job, you can run the following command 

```sh
kubectl get jobs 
    -l app.kubernetes.io/component=<cron-job-name>
    --sort-by=.metadata.creationTimestamp
    -o jsonpath='{.items[-1].status.conditions[-1].type}'
    -n <namespace>
```

Trigger/Launch job

```sh
kubectl create job <job-name> 
    --from=cronjob/<cron-job-name>
    -n <namespace>
```

## Pods 
```sh
kubectl get pods -n <namespace>
```

You can get logs of a given pod 

```sh
kubectl get logs <pod-name> -n <namespace>
```

Tip : You can save terminal output with `command > file.txt`, for example 
```sh
kubectl get logs <pod-name> -n <namespace> > pod-logs.txt
```
Or you can even append it into an existing file with `command >> existing-file.txt`, for example  
```sh
kubectl get logs <pod-name> -n <namespace> >> pod-logs.txt
```

You can get more details about the pods with the following command : 
```sh
kubectl describe pod <pod-name> -n <namespace>
```
