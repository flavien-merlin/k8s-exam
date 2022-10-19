### k8s exam Deployment :

1. Create a deployment called webapp with image nginx with 5 replicas
```
kubectl create deploy web app —image=nginx —dry-run=client -o yaml > webapp.yaml 
edit webapp.yaml
kubeclt edit deploy webapp.yaml
```
2. Get the deployment rollout status
```
kubectl rollout status deploy webapp
```
3. Get the replicaset that created with this deployment
```
kubectl get rs -l app=webapp
```
4. EXPORT the yaml of the replicaset and pods of this deployment
```
kubectl get rs -l app=webapp -o yaml
kubectl get po -l app=webapp -o yaml
```
5. Delete the deployment you just created and watch all the pods are also being deleted 
```
kubectl delete deploy webapp 
kubectl get po -l app=webapp -w
```
6. Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version 
```
kubectl create deploy webapp-flav --image=nginx:1.17.1 --dry-run=client -o yaml > webapp2.yaml
edit and add port to webapp2.yaml
kubectl describe pod webapp-flav-676d554496-wrzsb | grep -i image
```
7. Update the deployment with the image version 1.17.4 and verify 
```
kubectl set image deploy/webapp-flav nginx=nginx:1.17.4
kubectl describe deploy webapp-flav | grep -I image
```
8. Check the rollout history and make sure everything is ok after the update 
```
kubectl rollout history deploy webapp-flav 
kubectl get deploy webapp-flav --show-labels 
kubectl get rs -l app=webapp-flav 
kubectl get po -l app=webapp-flav
```
9. Undo the deployment to the previous version 1.17.1 and verify Image has the previous version  
```
kubectl rollout undo deploy webapp-flav
kubectl describe deploy webapp-flav | grep Image
```
10.  Update the deployment with the wrong image version 1.100 and verify something is wrong with the deployment
 ```
 kubectl set image deploy/webapp-flav nginx=nginx:1.100
 kubectl rollout status deploy webapp-flav 
 kubectl get pods
 kubectl rollout undo deploy webapp-flav
 kubectl rollout status deploy webapp-flav
 kubectl get pods
 kubectl rollout history deploy webapp-flav --revision=7
 kubectl set image deploy/webapp-flav nginx=nginx:latest
 kubectl rollout history deploy webapp-flav
```
11.  Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas and target CPU of 85% and verify hpa is created and replicas are increased to 10 from 1 
```  
kubectl autoscale deploy webapp-flav --min=10 --max=20 --cpu-percent=85
kubectl get hpa
kubectl get pod -l app=webapp-flav
```
12.  Clean the cluster by deleting deployment and hpa you just created
 ```
 kubectl delete deploy webapp-flav
 kubectl delete hpa webapp-flav
 ```
13.  Create a job and make it run 10 times one after one (run > exit > run >exit ..) using the following configuration:
```
kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am from job" > hello-job.yaml	
edit hello-job.yaml
```
