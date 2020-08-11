Docker deployement with ansible
=================================

This project provides the following :

+ Installation of docker on remote virtual machine/servers
+ Installation of docker engine
+ Change the docker directory
+ configuration of a private registry 

Supports only centos and redhat operating systems


Requirement
============
ansible connect to remote host in ssh. To be able to use the ansible script you need to create a private key and a public key , you can use the ssh-keygen command. when the bot key are created you'll need to copy the public key on the remote. My script connect as root so be careful when you use the ssh-copy-id.

In the hosts file add the ip address of the remote hosts you have two posibilieties:
    - create an hosts file in the same directory as the docker.yml (main script) but you'll have to add -i hosts when you run your playbook  
      ansible-playbook docker.yml -i hosts
    - add on the hosts file located /etc/ansible/hosts the ip addresses
    note : you need yo use inventory groups the docker-distribution(private-registry) need to be under the registry and the docker machine 


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
    

