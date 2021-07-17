# kubernate-kubeadm
#installing kubedm  in AWS
1.i have created 3 ec2 instances in AWS
   a)master 
   b)slave   node1
   c)slave node2

2.install docker  on servers 
   sudo apt  update
   sudo apt  install docker.io
   
3.installe kubedam on master and nodes   
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

4.creating clustor on master node

 kubeadm init --apiserver-advertise-address=<<private ip address of server>> --pod-network-cidr=<<network range>> --node-name=<<node name>>
   
   kubeadm init --apiserver-advertise-address=172.31.19.233 --pod-network-cidr=192.168.0.0/16 --node-name=master
   
  note:min cpu is 2 gives error in server(execute the below if eror comes)
   
    kubeadm init --apiserver-advertise-address=172.31.19.233 --pod-network-cidr=192.168.0.0/16 --node-name=master --ignore-preflight-errors=NumCPU,Mem

   
   5.after success creation of clustier gives as below  
   
   #########
   
   Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.31.19.233:6443 --token 9zlxoz.2hed3rbg7dlov5zc \
	--discovery-token-ca-cert-hash sha256:181cdcaa104b0e58a555f3776f29b245807542042b54ed6e6261a3761dd7f8bb 
   
   ###########
   
 6. join the slave nodes to master by running the below at slave nodes
   
   Then you can join any number of worker nodes by running the following on each as root:

 kubeadm join 172.31.19.233:6443 --token 9zlxoz.2hed3rbg7dlov5zc --discovery-token-ca-cert-hash sha256:181cdcaa104b0e58a555f3776f29b245807542042b54ed6e6261a3761dd7f8bb
   
   
 7 . get the status by below comand at master
	
	kubectl get all --all-namespaces
	
	kubectl get nodes   -->u should get the nodes

#8.The connection to the server localhost:8080 was refused - did you specify the right host or port?

	
	 mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf
#9. shows master not ready
	
###################################delete node
	
	kubectl drain master --delete-local-data --force --ignore-daemonsets
	
	
