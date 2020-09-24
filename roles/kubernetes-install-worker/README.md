kubernetes-install-worker
-----------

first we need to set the firewall. The master communicates with the nodes using several ports. 

|Protocol |	Direction	|Port Range |	Purpose |	Used By |
|----------------------|----------------|-------------------|--------------------------------|--------------|
| TCP | Inbound	| 10250 |	Kubelet API	| Self, Control plane|
|TCP	|Inbound	|30000-32767	|NodePort Services |	All|

To set up the firewall i create a firewalld service from an xml file. The xml file is kept in the roles under the files directory.

once the firewall is set up, we can then join the nodes to the cluster. The playbook copy the file on the tmp directory (be sure to have a temporary directory) and then execute it. 

Dependencies
------------

roles :  
  + preparation
  + deploiement 
  + kubernetes-set-depedencies
  + kubernetes-install-master


Source
-------
  
  - https://www.linuxtechi.com/install-kubernetes-1-7-centos7-rhel7/
  - https://computingforgeeks.com/install-kubernetes-cluster-on-centos-with-kubeadm/
  - https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-cluster-using-kubeadm-on-centos-7

