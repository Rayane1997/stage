Run http container
=================================

in order to run an http container , we will start by write a docker file. A docker file create a personalised image from an source image. 

first create a directory 

     mkdir http
     
then create the dockerfile. the docker file build your image adding layer
     
     vi http/Dockerfile
     
     from docker_image
     WORKDIR /usr/local/apache2/htdocs #directory where the index.html is kept
     COPY    index.html /usr/local/apache2/htdocs/
     VOLUME /usr/docker
  
  
once the docker file is created you can build your image and create a personalized message in the index file. but before enter in the directory
  
        cd http
        echo " bonjour , le conteneur est en marche"  > index.html
        Docker build -t http:pull .

 verified if you image is created 
        
        dovker image ls --all

finally run a new container and link the port 80 of the container to a port in your vms
    
    - docker run -d -p 8080:80 http:pull
    
 the -d parameters keep the container running in the background
 
 to verify if your service is running you can do a curl http://ip_address:8080
   

source
------------
https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker/
https://linuxhint.com/dockerfile_volumes/
