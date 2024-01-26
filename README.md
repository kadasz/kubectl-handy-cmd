# My kubectl cheat sheet

List of kubectl commands which I've found useful for on a daily basis because may come in handy for sure.


### To get IP addresses of pods
`
kubectl get pods -o custom-columns=ip:.status.podIP -n namespace
`

### Lists external IP adress of all nodes
`
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}'
`

### Lists all node of names with external IP address 
`
kubectl get nodes -o custom-columns=NODE:.metadata.name,'IP:.status.addresses[?(@.type=="InternalIP")].address'
`
