# My kubectl cheat sheet

List of kubectl commands which I've found useful for on a daily basis because may come in handy for sure.


### To get IP addresses of pods
```
kubectl get pods -o custom-columns=IP:.status.podIP 
```

### To get Name and Images of pods
```
kubectl get pods -o custom-columns=Name:.metadata.name,Image:..spec.containers[*].image
```

### To get Name and Worker IP of pods
```
kubectl get pods -o custom-columns=Name:.metadata.name,WorkerIP:.status.hostIP
```

### To get a list of all pods without pods from openshift-* namespaces
```
kubectl get pods -A --field-selector=metadata.namespace!=openshift-* -o wide
```

### Rolling updates and Rollbacks 
```
kubectl create -f app-deployment.yml
kubectl get deployments
kubectl apply -f app-deployment.yml
kubectl set image deployment/app-deployment nginx=nginx:1.25.1
kubectl rollout status deployment/app-deployment
kubectl rollout history deployment/app-deployment
kubectl rollout undo deployment/app-deployment
```

### Lists external IP adress of all nodes
```
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}'
```

### Lists all node of names with external IP address 
```
kubectl get nodes -o custom-columns=NODE:.metadata.name,'IP:.status.addresses[?(@.type=="InternalIP")].address'
```

### To get token from secret
```
kubectl -n jenkins get secret jenkins-token -o jsonpath="{.data.token}"|base64 -d; echo
```


### StatefulSet - rolling update, scale up and down 
```
kubectl rollout restart sts name_sts
kubectl scale --replicas=0 sts name_sts
kubectl scale --replicas=1 sts name_sts
```
