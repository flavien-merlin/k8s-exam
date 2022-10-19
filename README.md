### 1. Part 1 k8s exam, yaml inside the folder part1:

1. Deploy a pod named nginx-pod using the nginx:alpine image. Name: nginx-pod-yourname Image: nginx:alpine 
```
kubectl run nginx-pod --image=nginx:alpine
```
2. Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg. Pod Name: messaging Image: redis:alpine Labels: tier=msg
```
kubectl run messaging --image=redis:alpine --labels=tier=msg 
```
3. Create a namespace named apx-x998-yourname
```
kubectl create namespace apx-x998-flav
```
4. Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname
```
kubectl get node -o json > /tmp/nodes-flav.json
```
5. Create a service messaging-service to expose the messaging application within the cluster on port 6379.
```
kubectl expose pod messaging --port=6379 --name=messaging-svc
```
6. Create a service messaging-service to expose the messaging application within the cluster on port 6379.
```
kubectl create service clusterip messaging —tcp=6379:6379  --dry-run=client -o yaml > msg-svc.yaml
```
7. Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas
```
kubectl create deploy hr-web-app --image=kodekloud/webapp-color --replicas=2
```
8. Create a static pod named static-busybox on the master node that uses the busybox image and the command sleep 1000
```
kubectl run static-busybox —restart=Never --image=busybox  -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```
9. Create a POD in the finance-yourname namespace named temp-bus with the image redis:alpine
```
kubectl create namespace finance-flav 
kubectl -n finance-flav run temp-bus --image=redis:alpine
```
10. Create a Persistent Volume with the given specification 
```
pv-analytics.yaml
```
11. Create a Pod called redis-storage-yourname with image: redis:alpine with a Volume of type emptyDir that lasts for the life of the Pod.
```
redid-storage-flav.yaml
```
12. Create this pod and attached it a persistent volume called pv-1  a. Make sure the PV mountPath is hostbase : /data  
```
storageclass.yaml 
pv1.yaml
pvc.yaml
nginx-pod-pv.yaml
```
13. Create a new deployment call Nginx-deploy, with image Nginx:1.16 and 1 replicas Record the version. Next upgrade the deployment to version 1.17 using rolling update. Make sure that the version upgrade is recorded in the resource annotation. 
```
Nginx-deploy.yaml > kubectl create -f nginx-deploy.yaml --record kubectl set image deploy Nginx-deploy nginx=nginx:1.17 —record 
kubectl rollout history deploy Nginx-deploy
```
14. Create an nginx pod called nginx-resolver using image nginx, expose it internally with a service called nginx-resolver-service. Test that you are able to look up the service and pod names from within the cluster. Use the image: busybox:1.28 for dns lookup. Record results in /root/nginx-yourname.svc and /root/nginx-yourname.pod 
```
kubectl run nginx-resolver --image=nginx  --labels=app=nginx-resolver
kubectl expose pod nginx-resolver --port=80   --target-port=80 --protocol=TCP --name=nginx-resolver-service --type=ClusterIP
kubectl get svc nginx-resolver-service
kubectl exec -it dns -- nslookup 10.104.124.10 > nginx.svc 
kubectl get pod nginx-resolver -o wide
kubectl exec -it dns -- nslookup 10.1.0.18 > nginx.pod
```
15. Create a static pod on node01 called nginx-critical with image nginx. Create this pod on node01 and make sure that it is recreated/restarted automatically in case of a failure. 
```
on node01 create in /etc/kubernetes/manifests/nginx-critical.yaml
Nginx-critical.yaml
```
16. Create a pod called multi-pod with two containers. Container 1, name: alpha, image: nginx Container 2: beta, image: busybox, command sleep 4800. 
```
multi-pod.yaml
```
