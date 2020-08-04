Preparation
=========

this roles install the containerd.io packet neccessaey to install docker it also check if there is enough space because images can rapidly takes a lot of spaces.

Requirements
------------


Role Variables
--------------
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| mount_on  |    / |  where the directory docker is mount  |
| espace_disk |     1   |  minimum availible space in GB for docker to be installed  |



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

Source
-------

https://docs.docker.com/engine/install/centos
https://linuxconfig.org/how-to-install-docker-in-rhel-8
https://docs.ansible.com/
