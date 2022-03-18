# kubectl
```SH
kubectl config get-contexts #get all contexts in your config file .kube\config
kubectl get namespace #get all namespace (isolating groups of resources within a single cluster)
kubectl config view #get the config
kubectl describe deployment  | Select-String ^Replicas # get replica deployment info
kubectl describe pods # get pods info
kubectl get pods #get all pods
kubectl logs {PodName} #get logs for a pod
```

# kubectx
```SH
kubectx {MyContext} #switch context
```

# helm
```SH
helm ls #list releases
helm uninstall {ReleaseName} #uninstall a release
```