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



