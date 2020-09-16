kubernetes-init
=========


This role install all the depedencies necessary for kubernetes to work. 
  + First we disabled selinux. selinux can be sometimes really useful but in here it can cause some problem. So in order to avoid any issues i rather disabled it.
  + disable swap. If memory swapping is allowed to occur on a host system, this can lead to performance and stability issues within Kubernetes. kubelet won't run unless swap memmory is disabled
  + enable forwarding packets from one bridge port to another
  
  once all the depedencies are set we proceed to the creation of a repo to install kubeadm and kubelet
  

Depedencies
------------

docker installed (you need to first run all the plabook necessary to use docker)


Source
------
https://www.tecmint.com/install-a-kubernetes-cluster-on-centos-8/
