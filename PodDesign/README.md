### k8s exam : Pod Design Questions:

1. Type the command for:
```
kubectl get pod —show-labels
```
2. Create 5 nginx pods in which two of them is labeled env=prod and  
```
kubectl run nginx-dev1 —image=nginx --labels=env=dev 
kubectl run nginx-dev2 —image=nginx --labels=env=dev
kubectl run nginx-dev3 —image=nginx --labels=env=dev
kubectl run nginx-prod1 —image=nginx --labels=env=prod
kubectl run nginx-prod2 —image=nginx --labels=env=prod
```
3. Verify all the pods are created with correct labels
``` 
kubectl get pod —show-label
```
4. Get the pods with label env=dev
```
kubectl get pod -l env=dev
```
5. Get the pods with label env=dev and also output the labels
```
kubectl get pods -l env=dev --show-labels
```
6. Get the pods with label env=prod
```
kubectl get pod -l env=prod
```
7.  Get the pods with label env=prod and also output the labels
```
kubectl get pod -l env=prod —show-labels
```
8.  Get the pods with label env
```
kubectl get pod -L env
```
9.  Get the pods with labels env=dev and env=prod
```
kubectl get pod -l 'env in (dev,prod)'
```
10.  Get the pods with labels env=dev and env=prod and output the labels as well	
```
kubectl get pod -l 'env in (dev,prod)' —show-labels
```
11. Change the label for one of the pod to env=uat and list all the pods to verify
```
kubectl label pod/nginx-dev1 env=uat --overwrite 	
kubectl get pod —show-labels
```
12.   Remove the labels for the pods that we created now and verify all the labels are removed 
```
kubectl label pod nginx-dev{1..3} env-
kubectl label pod nginx-prod{1..2} env-
kubectl get pod --show-labels
```
13.  Let’s add the label app=nginx for all the pods and verify (using kubectl)
```
kubectl label pod nginx-dev{1..3} app=nginx
kubectl label pod nginx-prod{1..2} app=nginx
kubectl get po --show-labels
```
14.  Get all the nodes with labels (if using minikube you would get only master node)	
```
kubectl get nodes --show-labels
```
15.	 Label the worker node nodeName=nginxnode
```
kubectl label node flav-worker nodeName=nginxnode
```
16.  Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode
```
kubectl create -f nginx.yml
```
17.  Verify the pod that it is scheduled with the node selector on the right node... fix it if it’s not behind scheduled. 
```
kubectl describe po nginx | grep Node-Selector
```
18.  Verify the pod nginx that we just created has this label 
```
kubectl describe po nginx | grep Labels
```
