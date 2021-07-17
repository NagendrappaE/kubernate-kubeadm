**#Kubernate spring boot deployment using kubeadm  with one master and 2 worker nodes(slave1,slave2)



#1 we need to deploy the docker image on  worker node(slave node)

#2 create deployment at master 

kubectl create deployment helloworld --image amanfiet/spring-docker-demo:latest --replicas=3

3.create the service 

helloworld -->deployment name

kubectl create service nodeport helloworld --tcp 8080:8080


4.finally access the application

do kubectl get svc

ubuntu@ip-172-31-41-121:~$ kubectl get svc
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
helloworld   NodePort    10.101.73.11   <none>        8080:30519/TCP   9s
kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP          37m


  18.118.107.102 ---master servcer public IP  and 
  
http://18.118.107.102:30519/data
