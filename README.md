### 1. Part 1 k8s exam, yaml inside the folder part1:

1. Deploy a pod named nginx-pod using the nginx:alpine image. Name: nginx-pod-yourname Image: nginx:alpine 
```
kubectl run nginx-pod --image=nginx:alpine
```
2. Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg. Pod Name: messaging Image: redis:alpine Labels: tier=msg
```
kubectl run messaging --image=redis:alpine --labels=tier=msg 
```
