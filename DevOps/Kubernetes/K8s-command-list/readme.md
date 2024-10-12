Check the status of nodes, pods, master components, network, and more

# Node Commands
```
kubectl get nodes
kubectl describe nodes
kubectl get nodes -o wide
kubectl top nodes
kubectl cordon <node-name>
kubectl uncordon <node-name>
kubectl drain <node-name>
kubectl taint nodes <node-name> key=value:NoSchedule
kubectl get pod --all-namespaces -o wide
kubectl get nodes --show-labels
```

# Pod Commands
```
kubectl get pods
kubectl describe pod <pod-name>
kubectl get pods -n <namespace>
kubectl get pods -o wide
kubectl logs <pod-name>
kubectl logs <pod-name> -f
kubectl exec -it <pod-name> -- /bin/bash
kubectl port-forward <pod-name> <local-port>:<pod-port>
kubectl delete pod <pod-name>
kubectl get pods --field-selector status.phase=Running
```

# Service Commands

```
kubectl get services
kubectl describe service <service-name>
kubectl get svc -o wide
kubectl get endpoints
kubectl get services --all-namespaces
kubectl port-forward svc/<service-name> <local-port>:<service-port>
kubectl expose deployment <deployment-name> --port=<port> --target-port=<target-port>
kubectl get ing
kubectl describe ing <ingress-name>
kubectl get networkpolicies
```

# Deployment Commands
```
kubectl get deployments
kubectl describe deployment <deployment-name>
kubectl scale deployment <deployment-name> --replicas=<number>
kubectl rollout status deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name>
kubectl get replicasets
kubectl get jobs
kubectl get cronjobs
kubectl delete deployment <deployment-name>
kubectl apply -f <deployment-file>.yaml
```

# Namespace Commands
```
kubectl get namespaces
kubectl create namespace <namespace-name>
kubectl delete namespace <namespace-name>
kubectl config set-context --current --namespace=<namespace-name>
kubectl describe namespace <namespace-name>
kubectl get all -n <namespace-name>
kubectl get pods -n <namespace-name> --show-labels
kubectl apply -f <namespace-file>.yaml
kubectl delete all --all -n <namespace-name>
kubectl get resourcequotas -n <namespace-name>
```

# ConfigMap and Secret Commands
```
kubectl get configmaps
kubectl describe configmap <configmap-name>
kubectl create configmap <configmap-name> --from-file=<file>
kubectl delete configmap <configmap-name>
kubectl get secrets
kubectl describe secret <secret-name>
kubectl create secret generic <secret-name> --from-literal=<key>=<value>
kubectl delete secret <secret-name>
kubectl get secrets -n <namespace-name>
kubectl apply -f <configmap-secret-file>.yaml
```

# Master Component Commands
```
kubectl get componentstatuses
kubectl get cs
kubectl describe pod kube-apiserver -n kube-system
kubectl describe pod kube-controller-manager -n kube-system
kubectl describe pod kube-scheduler -n kube-system
kubectl get pods -n kube-system
kubectl logs kube-apiserver -n kube-system
kubectl logs kube-controller-manager -n kube-system
kubectl logs kube-scheduler -n kube-system
kubectl top pods -n kube-system
```

# Network Commands
```
kubectl get networkpolicies
kubectl describe networkpolicy <policy-name>
kubectl get pod <pod-name> -o jsonpath='{.status.hostIP}'
kubectl get svc -o jsonpath='{.items[*].spec.clusterIP}'
kubectl run netshoot --image=nicolaka/netshoot --rm -it -- /bin/bash
kubectl exec -ti netshoot -- nc -zv <service-name> <port>
kubectl get nodes -o json | jq '.items[].status.addresses[] | select(.type=="InternalIP")'
kubectl get pods --field-selector status.phase=Running -o wide
kubectl get endpoints <service-name>
kubectl get pods --selector app=<app-name>
```

# Cluster Commands
```
kubectl cluster-info
kubectl get events
kubectl top nodes
kubectl api-versions
kubectl api-resources
kubectl get resourcequotas
kubectl get limitranges
kubectl version
kubectl describe nodes <node-name>
kubectl get pv
```

# Maintenance and Troubleshooting Commands
```
kubectl get pod --all-namespaces --field-selector=status.phase!=Running
kubectl get events --sort-by='.metadata.creationTimestamp'
kubectl describe pod <pod-name> -n <namespace-name>
kubectl edit deployment <deployment-name>
kubectl patch deployment <deployment-name> -p '{"spec":{"replicas":<new-replicas>}}'
kubectl delete pod --force --grace-period=0 <pod-name>
kubectl rollout history deployment/<deployment-name>
kubectl logs <pod-name> --previous
kubectl wait --for=condition=ready pod/<pod-name> --timeout=60s
kubectl proxy
```

# Additional Commands
```
kubectl cp <pod-name>:<source-path> <destination-path>
kubectl get statefulsets
kubectl scale statefulset <statefulset-name> --replicas=<number>
kubectl get storageclasses
kubectl describe storageclass <storage-class-name>
```