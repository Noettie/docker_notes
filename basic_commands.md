#First and Foremost: 
1. Create an acc with DockerHub
2.Open Play With Docker Platform (to play with docker)
3. Add a new instance

#List Docker images

docker images

#Show all images

docker images -a

#List full length image i.d

docker images --no-trunc

#List out images with filter

docker images --fliter=reference='image_name'

#Saving images that you created

docker export - Exports a containers filesystem as a tar archive
docker import - Import the contents from a tarball to create a filesystem image
docker save - Save one or two images to a tar archive 
docker load - Load an image from a tar archive of STDIN

#Display running and non running container
$ docker ps -a

#Clean docker host

$ docker rm -f $(docker ps -a -q)

#Stop a container

$ docker stop <container_id>

#Kill a container

$ docker kill <cointaner_id>

#Display docker host info

$ docker info

#Changing hostname of EC2 instance
$ sudo vim /etc/hostname
update hostname (e.g docker host)
restart the server: 
$ sudo init 6
Then connect to the server again
This helps in knowing whether you are at the container level or docker host level

#To clean up your host
docker system prune -a
#To keep a container in running status the backend

ctl + p & ctl + q

To access a web application as a contianer you should use port mapping .Execute following command:

$ docker run --name <websitename> <webserver_name> -p pupiphost:<default_web_port> -d <webserver_name>
  
  e.g : 
  
  $ docker run --name mynginx -p 7272:80 -d nginx
  
  -p : port mapping, -d: run in detached mode
  
  Steps to change the default webbage of a webserver:
  
  1. Go to the underlying system of the container using the command:
  
  $ docker exec -it mynginx /bin/bash 
  
  This command takes you to the container Operating system.
  
  2. Identify which file to target by finding the default nginx webpage index.html :
  
  # /usr/share/nginx/html
  
  3. cd into the html using the default webpage path above 
  4. cat the html file. The contents of the default webpage will be present
  5. Change the entire contents to the contents of your own web page using  and paste your own html code: 
   $ cat > html
  
  To run jenkins as a container:
 1. $ docker run --name myjenkins -d -p 8080:8080 jenkins/jenkins:2.53
  $docker ps -a
  
 2. Use the following to get the access to the underlying OS:
  
  docker exec -it myjenkins /bin/bash
  
  3. cat the path given to access the password
  
  4. Copy and paste the password 
  
  For automatic port assignment use the -P flag , e.g :
  
  $ docker run --name myhttpd -d -P httpd
  
  -p (small caps) is for manual port assignment
  
  Creating a database as a container e.g
  
  1. $ docker run --name mydb -d -e MYSQL_ROOT_PASSWORD=12345 mysql
  
  2. Connect to the data through the underlying OS:
  
  $ docker exec -it mydb /bin/bash
  
  3. Gain access to the db using:
  
  mysql -u root -p
  
  4. Enter the environment password
  
  #To mount a volume to the container use the following:
  
  $ docker run --name myalpine -it -v /mydata alpine
  
 $ ls
  
  cd mydata
  
  add the files you want saved
  When the container is removed all data is lost exept from the mydata file
  
  #To retrieve the data:
  
  cd /
  cd var
  cd lib
  cd docker
  cd volumes
  ls
  ls -lt
  check the newly created file
  cd int it
  ls
  cd _data
  
 path_to_mount_volume:          /var/lib/docker/volumes/
  
  #Docker Volumes Container
  Mountaing a volume and sharing it with several containers
  
  $ docker run --name c1 -it -v /shared_drive alpine
  
  $ docker run --name c2 -it ---voumes-from c1 busybox
  
  ls 
  cd shared_drive
  ls
  create files
  
  Working collaboratively on a project
  Step to take:
  
  1. Download customized image :
  $ docker run --name project1 -it alpine
  2. Install required packages
  $ apk update
  $ apk add git
  mkdir project2022
  cd project2022
  git clone 
  cd ..
  apk add maven
  exit 
  All prerequirements for project1 installed
  
  docker ps -a
  docker commit project1 project2022
  docker images
  
  image should be present on hub.docker.com
  
  Next step is to push image to hub.docker.com
  
  $ docker login enter
  
  and enter username $ password
  
  $ docker tag project2022 <docker_hub_username/project2022>
  $ docker images
  $ docker rmi project2022
  $ docker push <docker_hub_username/project2022>
  
  #Creating customized docker image
  
  #Use DOCKERFILE
  
  Write a dockerfile with keyword FROM
  
  Example:
  
  FROM ubuntu
  MAINTAINER nothando
  RUN apt update
  RUN apt install -y git 
  RUN apt install -y maven
  RUN apt install -y tree
  RUN apt install -y default-jdk   (java)
  
  crl+ C / save and quit (:wq!)
  
  Execute the command:
  
  docker build -t myimage .   (the . means in the pwd)
  
  Result is a customized image with all packages installed
  
  If more than one dockerfile exists use:
  
  $ docker build -f <dockerfile_name> -t <image_name> .
  
  
  
  
  
 
  
  
  
  
  
  

