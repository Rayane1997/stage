Registry
=========
This role configure the docker VM to be able to communicate with the registry server. docker search the ceritificates unde the directory "/etc/docker/certs.d/registry_name:port/" .to make it work we need to create this directory and copy the certificates.if you have a dns server you can set the dns vars to false so ansible skip the first step. the first command add the ip address of the registry's hostname to the hosts.conf so you're not forced to write the ip address.

once it all done you can access to the docker registry:
 + pull an image from the dockerhub
 + tag the image as myregistry:5000/http .  When the first part of the tag is a hostname and port, Docker interprets this as the location of a registry, when pushing.
 + login to the docker registry
 + push the tagged image
 
nom even if you don't have acces to internet you'll be able to pull you're imagie frome your private registry

to the docker registry using "docker login registry_name:5000"


Requirements
------------

docker installed


Role Variables
--------------

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|ip_registry|192.168.234.54| ip address of the registry server only necessary if the dns vars is set to true|
|cert_name|registry.crt| name of the certificat|
|dns|True|set to false if you have a dns server|

 




Dependencies
------------
registry role


Example Playbook
----------------

Including an exemple to push your image:

   + docker pull httpd
   + docker tag httpd myregistry.local:5000/httpd
   + docker login docker-distribution-01.example.com:5000:
   
    name:
    password:
    
   + docker push myregistry.local:5000/httpd
   
source
------------------

https://www.centlinux.com/2019/04/configure-secure-registry-docker-distribution-centos-7.html


