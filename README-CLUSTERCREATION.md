#Clustor creation

1.create 3 server with all trafic should be allowed 
a)master 
b)slave/worker 1(node)
c)slave /worker node2(node)

2.install the docker  in all the servers

3.install kubeadm
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

4.create cluster inmaster server

172.31.19.233 --ip address of master

kubeadm init --apiserver-advertise-address=172.31.19.233 --pod-network-cidr=192.168.0.0/16  --node-name=master --ignore-preflight-errors=ALL
  or 
  kubeadm init --apiserver-advertise-address=172.31.19.233 --node-name=master --ignore-preflight-errors=ALL


5.execute the network pluguins
https://docs.projectcalico.org/getting-started/kubernetes/quickstart

kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml



#5. copy the  generated as below in all the salves (worker nodes)



sudo kubeadm join 172.31.41.121:6443 --token x119h3.3e0ga6ez7po4geab --discovery-token-ca-cert-hash sha256:96556e50638e89870d58aceb727d4b36221ce0c820a0a6570f1bb05ee597b166 --ignore-preflight-errors=ALL

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

6.kubectl get nodes

####if u get erro#######

kubectl get nodes
The connection to the server 172.31.1.189:6443 was refused - did you specify the right host or port?
ubuntu@ip-172-31-1-189:~$ export KUBECONFIG=/etc/kubernetes/admin.conf



#####################CLEAN UP Cluster################

1.reset kubeadm

kubeadm reset


2.
kubectl drain master --delete-emptydir-data --force --ignore-daemonsets

3.

kubectl delete node master

