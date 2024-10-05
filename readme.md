#       Docker commands

*    `docker ps` lists all running Docker containers.

*    `usermod -aG docker <username>` adds the specified user to the Docker group, 
       allowing them to   run Docker commands without `sudo`.

*    `docker images` displays a list of all locally stored Docker images.

*    `docker pull nginx` downloads the latest Nginx image from Docker Hub to your local machine.

*    `docker create <image>:tag` creates a new container from the specified image and tag but does not start it.

*    `docker ps -a`: Lists all Docker containers, including both running and stopped ones.

*    `docker start <container ID>` starts a stopped container specified by the container ID.

*    `docker run` creates and starts a new container from a specified image, running it in the foreground. (docker run = docker pull + docker create <CID> + docker start
docker run effectively combines the actions of docker pull (downloading the image if not already available), docker create (creating a container from the image), and docker start (starting the container))

*    `docker rm <container ID>` removes the specified container from the Docker host, but only if it is stopped.

*    `docker rm -f <container ID>` forcefully removes the specified container, stopping it if it is currently running.

*    `docker rmi <image ID>` removes the specified image from the local Docker host, deleting it if no containers are using it.

*    `docker rmi -a -q <image ID>` removes all images matching the specified image ID, using the `-a` option to target all tags and `-q` to only show the image IDs without additional output.

*    docker rm `docker image -a -q` removes all locally stored Docker images by executing the    inner command to get all image IDs and passing them to `docker rmi`.

*   docker rm `docker ps -a -q` removes all stopped containers by executing the inner command to list all container IDs and passing them to `docker rm`.

*    `docker run -d nginx` starts a new Nginx container in detached mode, allowing it to run in the background.

# Q. How can you access docker container from internet ?
# A. By enabling the port, we need to open host port that can redirect traffic to container