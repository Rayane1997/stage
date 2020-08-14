Docker deployement with ansible
=================================

This project provides the following roles :

+ preparation : Installation of docker on remote virtual machine/servers
+ deploiement : Installation of docker engineChange the docker directory
+ registry : configuration of a private registry 
+ registry_hosts : configure the hosts to comunicate with the docker-distribution

Supports only centos and redhat operating systems

docker.yml : install docker

registy.yml : configure the registry

access_registry.yml : configure the acces to the registry using registry-hosts roles




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
         [docker]
         dockerVM_ip or common_name
    
    once all of that is done you can run the ansible playbook. there are 3.
    
docker.yml 
----------

the first playbook to run is the docker.yml. the playbook install docker on the remote hosts but before you run the playbook check the vars. from here i will assume that you're already int the git directory named stage 
    
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| directory_docker | /var/lib/docker | where the docker directory need to be installed|
| mount_on  |    / |  where the directory docker is mount (you can use a df -h /path_to_docker-directory/ to see where it's mount)  |
| espace_disk |     1   |  minimum  free disk space on the docker directory. image can take rapdily a lot of space. to avoid to avoid any inconveniance set up the var to at least 1 gb  |

if neccesarry change the vars:

    - vi roles/preparation/vars/main.yml
    
then you can run the playbook :
    
    - ansible-playbook docker.yml

registry.yml
-----------
    
   
    
    
    


    
    
note to myself : you need to use inventory groups. Inventory grou can be really useful to run tasks only on the hosts you want. the docker-distribution(private-registry) need to be under the registry group and the docker machine under docker group

Example 
----------------

 example of how to use the ssh-keygen ans ssh :

    - ssh-keygen -t rsa 
    - ssh-copy-id root@ip_hosts
    
 example of hosts file :
    
    [registry]
    registry_ip or common_name 
    [docker]
    dockerVM_ip or common_name 
    
 example of command to run the script :
 
    - ansible-playbook docker.yml
    

