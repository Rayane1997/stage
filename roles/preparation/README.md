Preparation
=========

this roles prepare the remote machine for the installation of docker. First it checks if there's enough space where in the docker directory. Directory that you need to set in the vars fail before to run the script. the image and the container can rapidly takes a lot of spaces so we'll need a minimum of 1 gb of free disk space.
Best practice : put all the data in a seperate disk

there is still no docker packages availible for centos 8 we need to download so we have to install from the repository. 

here we use the X86_64 repodata 

the installation of docker-io is necessary because it's a prerequisite to install docker we can install docker-io and docker in the same time only if we use the --nobest parameters not supported by ansible so we had to find a workaround. that's why we install the docker-io.rpm be always aware to have the latest versions.

Requirements
------------
hosts file confgured and a connection to internet to download the packages

Role Variables
--------------
|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| directory_docker | /var/lib/docker | where the docker directory need to be installed|
| mount_on  |    / |  where the directory docker is mount (you can use a df -h /path_to_docker-directory/ to see where it's mount)  |
| espace_disk |     1   |  minimum  free disk space on the docker directory. image can take rapdily a lot of space. to avoid to avoid any inconveniance set up the var to at least 1 gb  |





Source
-------

https://docs.docker.com/engine/install/centos
https://linuxconfig.org/how-to-install-docker-in-rhel-8
https://docs.ansible.com/
