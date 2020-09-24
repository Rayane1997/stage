Docker deployement with ansible
=================================

This project provides the following roles :
+ create-lvm : creation of a dedicated lvm
+ preparation : Installation of docker on remote virtual machine/servers
+ deploiement : Installation of docker engineChange the docker directory
+ registry : configuration of a private registry 
+ registry_hosts : configure the hosts to comunicate with the docker-distribution
+ kubernetes-init : set dependencies for kubernetes
+ kubernetes-install-master : set up all the requirement to initialize the cluster and then copy the join command in a file
+ kubernetes-install-worker : set the firewall rules for the worker and then run the join command 

Supports only centos and redhat operating systems

docker.yml : install docker

registy.yml : configure the registry

access_registry.yml : configure the acces to the registry 

kubernetes-set-depedencies.yml : set depedencies for kubernetes

kubernetes-master.yml : init the cluster

kubernetes-nodes.yml : join the nodes to the cluster

requirement
-------------
5 vm : 4 centos(or redhat) 8 and 1 centos(or redhat) 7

the vm running on centos 7 will be used as our private registry and can also serve as a dns server.
we need 3 vms for the cluster kubernetes one master and two worker and finally a bootsrap to deploy our ansible playbook.

free disk availible on each vm


how to
=========
ansible connect to remote host in ssh. To be able to use the ansible script you need to create a private and a public key :
       
    - ssh-keygen -t rsa 
 
when the both key are created you'll need to copy the public key on the remote host. the playbook connect as root so be careful to copy it as root when you use the ssh-copy-id :
 
       - ssh-copy-id root@ip_hosts

modified the host file /etc/ansible/hosts , add the ip addresses of the remote hosts :

    vi /etc/ansible/hosts

         [registry]
         registry_ip or common_name 
         [master]
         masterVM_ip or common_name
         [worker]
         workerVM_ip or common_name
         [docker:children]
         master
         worker
    

you can also create it on your directory. if you do it this way you'll nedd to add -i path_to_file when ever you run an ansible playbook 

        - ansible-playbook docker.yml -i hosts


once all of that is done you can run the ansible playbook. 
    
from here i will assume that you're already in the git directory named stage


LVM creation
-------------

the 2 first playbook start by creating a dedicated lvm. Here are the variables necessary for the creation.
the lvm created will bee used to contain the docker data in the docker machines and the images, necessary to run containers, for the registry

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| mount_point  |  /data-docker |   directory where the docker data or the images will be held  |
| physical_device | /dev/sdb |  free disk used to contained the data   |
|volumegroup_name| docker00 | name of the volume group|
|lv_name| test | logical volume name|

if neccesarry change the vars:

    - vi roles/create_lvm/vars/main.yml
    



docker.yml 
----------

the first playbook to run is the docker.yml. the playbook install docker on the remote hosts but before you run the playbook check the vars.  
    
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| directory_docker | /data-docker/docker | where the docker directory need to be installed|
| mount_point  |  /data-docker |  where the directory docker is mount (you can use a df -h /path_to_docker-directory/ to see where it's mount)  |
| espace_disk  |   1   |  minimum  free disk space on the docker directory. image can take rapdily a lot of space. to avoid to avoid any inconveniance set up the var to at least 1 gb  |

note: we want the directory docker to be installed on the lvm so be carreful where you install  the directory_docker (check the LVM creation) 

if neccesarry change the vars:

    - vi roles/preparation/vars/main.yml
    - vi roles/deploiement/vars/main.yml
    
finally you can run the playbook :
    
    - ansible-playbook docker.yml

registry.yml
-----------
  
 before your run the playbook don't forget to check the lvm creation's variables. 
    
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|common_name_registry| XXXXXXX| common name for the self signed certificate. need to be the hostname of the registry server |
|name_org| XXXXXXX| name of the organisation for the certificate|
|path_prvkey| /etc/pki/tls/private/registry.key| path to the private key|
|path_csr | /etc/pki/tls/registry.csr| path to the csr file |
|path_cert | /etc/pki/tls/registry.crt | path to the certificate |
|directory_registry| /var/lib/registry | directory where the image will be kept |
|path_auth | /etc/docker-distribution/dockerpasswd | path to  the http authentification  file |
|passwd| Rayane1997| password for htpasswd |
|user_auth| dock | username for the authetification|
   
first you need to complete the value for all the non defined variable shown here with XXXX

       - vi roles/registry/vars/main.yml
       
then run the playbook :

       - ansible-playbook registry.yml --ask-vault-pass
       
       password for vault ==> stage123
       
       

access-registry.yml
-------------------

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|ip_registry|xxxxxxx| ip address of the registry server only necessary if the dns vars is set to true|
|cert_name|registry.crt| name of the certificat|
|dns|true|set to false if you have a dns service. if true  it add the ip address of the registry server to the hosts file|

first you need to complete the value for the non defined variable shown here with XXXX

       - vi roles/registry-hosts/vars/main.yml
then run the playbook :

       - ansible-playbook access-registry.yml
       
       
now you can pull and push  images from your registry. to see how you can do it read the http.md

kubernetes-set-depedencies.yml
-------------------

this roles set all depencies in order to set up the kubernetes cluster. all you need to do is run the playbook.

run the playbook :

       - ansible-playbook kubernetes-set-depedencies.yml
       

kubernetes-master.yml
-------------------

this roles configure the master and copy the command needed for the workers to join the cluster 

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|user|xxxxxxx| user to have access to kubectl in order to run command |
|password|xxxxxxx| password for the user only if the user need to be created |

first you need to complete the value for the non defined variable shown here with XXXX

       - vi roles/kubernetes-install-master/vars/main.yml
       
because this playbook contain a password the vars file need to be crypted:

       - ansible-vault encrypt roles/kubernetes-install-master/vars/main.yml
         then enter a password 
         
         don't forget the password you'll need it to run your playbook
         
then run the playbook :

       - ansible-playbook kubernetes-master.yml --ask-vault-pass



kubernetes-nodes.yml
-------------------
this roles set up the firewall and then run the command to join the cluster. all you need to do is run the playbook.

run the playbook :

       - ansible-playbook kubernetes-nodes.yml


    
    


