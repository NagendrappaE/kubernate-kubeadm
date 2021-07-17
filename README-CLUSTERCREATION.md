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

kubeadm init --apiserver-advertise-address=172.31.19.233 --pod-network-cidr=192.168.1.1/16  --node-name=master --ignore-preflight-errors=ALL
  or 
  kubeadm init --apiserver-advertise-address=172.31.19.233 --node-name=master --ignore-preflight-errors=ALL


5.execute the network pluguins
https://docs.projectcalico.org/getting-started/kubernetes/quickstart

kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml



5. copy the  generated as below in all the salves (worker nodes)

kubeadm join phase kubelet-start 172.31.19.233:6443 --token 5elq8r.vwacp93fxtienb1x --discovery-token-ca-cert-hash sha256:4bb764dfce2ab7798fd98e89050774157ff4396a745a961be858e78eeca491e4

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

6.kubectl get nodes

