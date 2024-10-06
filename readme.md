#       Docker commands

*    Docker Image == Bare minimum OS + App run time + system packages and dependencies + App code (conatiner is the running istance of docker image)

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



 Q. How can you access docker container from internet ?
 A. By enabling the port, we need to open host port that can redirect traffic to container


*  `docker run -d -p <host-port>:<container-port>` starts a new container in detached mode, mapping a specified port on the host to a port on the container.

*  `docker logs <container ID>` retrieves and displays the logs from the specified container, showing its output and any error messages.

* `docker logs -f <container ID>` streams the logs of the specified container in real-time, allowing you to see new log entries as they are generated.

*  `docker inspect <container or image ID>` provides detailed information about a specified container or image in JSON format, including its configuration and state.

* `docker exec -it <container ID> bash` opens an interactive bash shell in the specified running container, allowing you to execute commands inside it.

* `docker images -f <filter>` lists Docker images with optional filters applied, allowing you to narrow down the results based on specific criteria, such as dangling images or specific labels.

* `docker tag <source-image> <target-image>` creates a new tag for an existing Docker image, allowing you to reference it by a different name or version, typically used for versioning or preparing images for pushing to a registry. 

* `docker login -u <username>` prompts for the password and logs the user into a Docker registry with the specified username, allowing access to private repositories.

* `docker push <username>/<image-name>:<tag>` uploads a local Docker image to the specified repository on Docker Hub, making it accessible to others or for use on different systems.

*  " DOCKERFILE ------>> It is the declarative way of creating custom images "

* docker build -t url/username/image-name:tag . ---> will check for the dockerfile

# DOCKER INSTRUCTIONS

* FROM 
  -----
  FROM shuould be the first instruction to represent the base OS.
  FROM image-name:tag(The `FROM` instruction in a Dockerfile specifies the base image to use for the new image, defining the starting point for the build process.)

* RUN
  ------
  We will use RUN instruction to install the packages and configure them.
  run instruction will execute at the time of image creation.(The `RUN` instruction in a Dockerfile executes a command in the shell during the image build process, allowing you to install packages or modify the file system of the image.)

* CMD
  ----
  CMD instruction run at the time of container creation (The `CMD` instruction in a Dockerfile specifies the default command to run when a container is started from the image, which can be overridden by command-line arguments when running the container.)


* LABEL
  ------
  The `LABEL` instruction in a Dockerfile adds metadata to an image in the form of key-value pairs, which can be used for documentation, organization, or management purposes.

* EXPOSE 
  -----
  The `EXPOSE` instruction in a Dockerfile informs Docker that the container listens on specified network ports at runtime, serving as documentation for users and other developers, but it does not actually publish the ports.

* ENV
  ----
  The `ENV` instruction in a Dockerfile sets environment variables in the container, which can be accessed by applications running inside the container and can also influence the behavior of the image.

* ENTRYPOINT
  ----------
  The `ENTRYPOINT` instruction in a Dockerfile specifies a command that will always run when a container is started from the image, allowing you to configure a container to behave like a standalone executable. It can be combined with `CMD` to provide default arguments.
    * CMD instruction can be overridden
    * we cant override entrypoint , if you try to over ride it will be append
    *   CMD/ENTRYPOINT
         -----------
    * we can mix the CMD and entrypoint for better result
    * CMD is used to supply default arguments to ENTRYPOINT
    * we can always override defailt args from the run time.

* USER
  -----
  Q what is the best practices in docker? A. It's best practice to avoid running containers with root access to enhance security, as it minimizes the potential impact of vulnerabilities or breaches by restricting permissions. Instead, create and use a non-root user within the container.
  * The `USER` instruction in a Dockerfile sets the username or UID (and optionally the group or GID) to use when running the container, allowing you to specify a non-root user for improved security.

* WORKDIR
  -------
  The `WORKDIR` instruction in a Dockerfile sets the working directory for any subsequent `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions, making it easier to manage file paths within the container. If the directory does not exist, it will be created.

* ARGS
  ----
  The `ARG` instruction in a Dockerfile defines a variable that users can pass at build-time to the Docker build process, allowing for dynamic configuration of the image. Unlike environment variables set with `ENV`, `ARG` variables are not available in the running container.
  
     1. **ARG** defines build-time variables; in this Dockerfile, `version`, `COURSE`, `TRAINER`, and `Duration` are specified, with a default version of `8` for the base image.
  
    2. **ENV** sets environment variables for the container; here, `Duration` is made available to applications running inside the container.
