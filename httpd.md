Run http container
=================================

in order to run an http container , we will start by write a docker file. A docker file create a personalised image from an source image. 

the docker file will contain 3 tasks:
  + workdir : define the working directory of a Docker container at any given time |  WORKDIR  "directory within the container"
  + copy: allow us to copy a file or a directory from our machine directly to the docker container | COPY "source in your machine" "destination in the container"
  + volume: create a new persistent volume in your docker machine for each of the containers created from this image  | VOLUME "directory"
save it as DockerFile
  
   example of a dockerfile :

    - from docker_image
    - WORKDIR /usr/local/apache2/htdocs #directory where the index.html is kept
    - COPY    index.html /usr/local/apache2/htdocs/
    - VOLUME /usr/docker
  
  
once the docker file is created you can build your image using -t to named it and create a personalized message in the index file.
  
  example  : 
   - echo " bonjour , le conteneur est en marche"  > index.html
   -  Docker build -t http
   
finally run a new container and link the port 80 of the container to a port in your vms
   
   example  : 
    - docker run -d -p 8080:80 http
    
 the -d parameters keep the container running in the background
 
 to verify if your service is running you can do a curl http://ip_address:8080
   

source
------------
https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker/
https://linuxhint.com/dockerfile_volumes/
