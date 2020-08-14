Registry
=========

This role install and configure a docker-distribution. Docker-distribution is only availible on centos 7. So before trying to install the packages we first ensure that the centos versions si 7.  We then install the required packages. You're not forced to create a self signed certificate to have access to your registry. Adding this to the docker daemon { "insecure-registries" : ["myregistrydomain.com:5000"]} will be enough but that's really not secure. Indeed by default docker use https to connect to docker registry. but with the insecure registry http is used. This eliminate the need of CA signed certificate for internal use or to trust self signed certificate in all docker nodes. Here we'll create the self-signed certificate be carreful that the common name match exactly your vm's hostname. To secure even more the registry you have the choice betweeen three authentification method : 1- htpasswd 2- silly 3- token

Here i used htpasswd, htpasswd provides a simple authentication scheme that checks for the user credential hash in an htpasswd formatted file.

the configuration file for the docker distribution is kept in the templates. finally the script set the firewall to let tcp communication on port 5000.

note: the images must be kept in a dedicated volume

Requirement
------------
Vm with docker installed to push and pull image

Role Variables
--------------

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
|common_name_registry| XXXXXXX| common name for the self signed certificate. need to be the hostname of the registry server |
|name_org| XXXXXXX| name of the organisation for the certificate|
|path_prvkey| /etc/pki/tls/private/registry.key| path to the private key|
|path_csr | /etc/pki/tls/registry.csr| path to the csr file |
|path_cert | /etc/pki/tls/registry.crt | path to the certificate |
|directory_registry| /var/lib/registry | directory where the image will be kept |
|path_auth | /etc/docker-distribution/dockerpasswd | path to  the http authentification  file |
|passwd| XXXXXXX| password for htpasswd |
|user_auth| XXXXXXX| username for the authetification|

first you need to go complete the vars file and add all the non defined variable

        


Source
-------

https://github.com/docker/distribution/blob/master/docs/configuration.md

https://www.centlinux.com/2019/04/configure-secure-registry-docker-distribution-centos-7.html

https://computingforgeeks.com/install-and-configure-docker-registry-on-centos-7/

