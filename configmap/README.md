### k8s exam configMap :



1. Create a file called config.txt with two values key1=value1 and key2=value2 and verify the file
```
cat >> config.txt << EOF
key1=value1
key2=value2
EOF

cat config.txt
```
2.  Create a configmap named keyvalcfgmap and read data from the file config.txt and verify that configmap is created correctly
```
kubectl create cm keyvalcfgmap --from-file=config.txt
kubectl get cm keyvalcfgmap -o yaml
```
3.  Create an nginx pod and load environment values from the above configmap keyvalcfgmap and exec into the pod and verify the environment variables and delete the pod
```
kubectl run nginx-flav --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yml
edit yaml to match configmap : nginx-pod.yml
kubectl create -f nginx-pod.yml
kubectl exec -it nginx-flav -- env
kubectl delete po nginx
```
