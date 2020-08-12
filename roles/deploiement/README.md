deploiements
=========

To install docker we first need the docker directory to be installed where we want to. In order to do that we have to modified the docker daemon so he knows where to install itself. Since docker is not installed we still don't have any directory docker. therefor, the first step is to create the directory then we'll be able to create the daemon file and finaly we had { "data-root" : "{{directory_docker}}" } this will tell to the docker daemon to install itself in our docker directory and not the /var/lib/docker/


Role Variables
--------------
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|  directory_docker: | /usr/lib/docker  |  specifiy the docker directory |
 
Dependencies
------------

roles : preparation


Source
-------
https://medium.com/developer-space/how-to-change-data-docker-folder-configuration


