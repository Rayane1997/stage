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


Example 
----------------

Including an example of how to use the ssh-keygen ans ssh :

    - ssh-keygen -t rsa 
    - ssh-copy-id root@iphosts

