KUBECTL
===
```
# show URL of the dashboard
echo http://`kubectl -n kube-system get svc kubernetes-dashboard | tail -n1 | sed 's/  */ /g' | cut -f3 -d' '`

# list all contexts
kubectl config get-contexts
# swithch to context
kubectl config use-context minikube

# show current context
kubectl config current-context
# show namespace in the current context
kubectl config view | grep namespace:
# switch namespace:
kubectl config set-context $(kubectl config current-context) --namespace=ns0

# show pods for all namespaces:
kubectl get pods --all-namespaces
# show pods for certain namespace
kubectl get pods --namespace=jx

# get all resources in the namespace
kubectl get all
# show all resources types
kubectl api-resources
# show all API versions
kubectl api-versions

# delete (typically) all resources
kubectl delete ds,rs,svc,deploy,po,rc --all

# re-encrypt all secrets
kubectl get secrets --all-namespaces -o json | kubectl replace -f -

# port-forward:
kubectl port-forward --namespace default svc/my-rabbit 5672:5672

# nodes:
kubectl get nodes
kubectl get nodes -o yaml
```

