Preparation
=========

this roles install the containerd.io packet neccessaey to install docker it also check if there is enough space because images can rapidly takes a lot of spaces.

Requirements
------------

?

Role Variables
--------------
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|  directory_docker: | /var/lib/docker  |  specifies the docker directory specifies the docker directory  |
 

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

Source
-------
https://medium.com/developer-space/how-to-change-data-docker-folder-configuration


