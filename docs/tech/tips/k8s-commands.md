# Some K8S commands

```sh
kubectl config get-contexts         # List all contexts
kubectl config use-context <name>   # Switch context
kubectl cluster-info                # Show cluster master and services
kubectl version                     # Show client and server version

kubectl get pods                    # List pods in current namespace
kubectl get pods -A                 # List pods in all namespaces
kubectl describe pod <name>         # Detailed pod info
kubectl logs <pod>                  # Show logs from pod
kubectl logs <pod> -c <container>   # Logs for specific container in pod
kubectl exec -it <pod> -- bash      # Exec into pod (if bash is available)
kubectl delete pod <pod>            # Delete a pod

kubectl get deployments             # List deployments
kubectl describe deployment <name>  # Deployment details
kubectl rollout status deployment <name> # Check rollout status
kubectl rollout undo deployment <name>   # Rollback deployment
kubectl delete deployment <name>    # Delete a deployment

kubectl get ns                     # List namespaces
kubectl get secrets                # List secrets
kubectl describe secret <name>    # Secret details
kubectl get configmaps            # List ConfigMaps
kubectl describe configmap <name> # ConfigMap details

kubectl get events                 # Show recent events
kubectl top pod                    # Show pod CPU/mem usage (metrics-server required)
kubectl describe node <node>      # Node status and issues
kubectl get all                    # Show all resources in current namespace
```

Try `k9s`
and context 
