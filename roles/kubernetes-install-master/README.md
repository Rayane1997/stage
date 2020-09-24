
kubernetes-install-master
===========================

first we need to set the firewall. The master communicates with the nodes using several ports. 

|Protocol |	Direction	|Port Range |	Purpose |	Used By |
|----------------------|----------------|-------------------|--------------------------------|--------------|
| TCP |	Inbound	| 6443 |	Kubernetes API server| All |
| TCP |	Inbound |	2379-2380 |	etcd server client API |	kube-apiserver, etcd |
| TCP | Inbound	| 10250 |	Kubelet API	| Self, Control plane|
| TCP | Inbound |	10251	| kube-scheduler |	Self |
| TCP |	Inbound |	10252 |	kube-controller-manager |	Self |

To set up the firewall i create a firewalld service from an xml file. The xml file is kept in the roles under the files directory.
i then initialize the cluster as the root user, to use kubectl command as a non root user you need to copy the config file in the $HOME/.kube directory 
as we start from a new machine before copying the config file the roles check if the user exist if the user exist it add him to the sudo users and if not it create the user.to assure communication between the container and the outside we need an CNI (The Container Networking Interface). we choose to use flannel. finally we can add nodes to the cluster, to add them we'll need to past the join command on the nodes. we can't just past the command between two hosts. we save the command as a fact and then past it on a file in the localhost. therefore the last playbook will be able to use the command on the nodes.



Role Variables
--------------

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|user|xxxxxxx| user to have access to kubectl in order to run command |
|password|xxxxxxx| password for the user only if the user need to be created |
 
Dependencies
------------

roles :  
  + preparation
  + deploiement 
  + kubernetes-set-depedencies


Source
-------
  
  - https://www.linuxtechi.com/install-kubernetes-1-7-centos7-rhel7/
  - https://computingforgeeks.com/install-kubernetes-cluster-on-centos-with-kubeadm/
  - https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-cluster-using-kubeadm-on-centos-7


