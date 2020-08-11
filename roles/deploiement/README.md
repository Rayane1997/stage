deploiements
=========

 to install docker we first want the docker directory to be installed where we want to. In order to do that we have to modified the docker daemon so he knows whete to install itself. since docker is not installed we still don't have any reportory docker. the first step is to create the directory then we creqte the daemon file and finaly we had { "data-root" : "{{directory_docker}}" } this will tell to docker daemon to install itself in our docker directory and not the /var/lib/docker/


Role Variables
--------------
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|  directory_docker: | /var/lib/docker  |  specifiy the docker directory |
 
Dependencies
------------

roles : preparation



Source
-------
https://medium.com/developer-space/how-to-change-data-docker-folder-configuration


