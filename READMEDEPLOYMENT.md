**#Kubernate spring boot deployment using kubeadm  with one master and 2 worker nodes(slave1,slave2)



#1 we need to deploy the docker image on  worker node(slave node)

#2 create deployment at master 

kubectl create deployment helloworld --image amanfiet/spring-docker-demo:latest --replicas=3

3.
