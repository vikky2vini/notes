## Docker

#### Tweaks
##### Allow host machine to share sound card
1. Edit /etc/pulse/default.pa
2. Add or uncomment: load-module module-native-protocol-tcp
3. Restart pulseaudio: pulseaudio -k

#### Commands
###### Show basic information about docker:
  `# docker info`

###### Show docker containers that are running:
  `# docker ps`

###### Show all containers that have ever been run:
  `# docker ps -a`

###### Search for a docker container in the docker hub:
  `# docker search <searchterm>`

###### Pull down a container from the docker hub:
  `# docker pull training/sinatra`

###### Run a docker container, remove it when it's finished:
  `# docker run --rm ubuntu:latest /bin/bash`

###### Make two containers able to talk to each-other:
  `# docker run --link container-a --name container-b myimage`

###### Use environment variables:
  `# docker run -d --name pengdb -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_DB docker.io/postgres`

###### Run a docker container with an interactive shell:
  `# docker run -it ubuntu:latest /bin/bash`
    Note: If the container doesn't exist locally, it will search the hub

###### Run a docker container as a daemon:
  `# docker run -it ubuntu:latest /bin/bash`

Run a docker container as a daemon, and redirect port (localport:containerport):
  `# docker run -d -p 8080:80 training/sinatra`

###### Start a previous (uncommitted) container (and continue where it left off):
  `# docker start <containerID>`

###### Committing changes to a docker container:
  `# docker run -t -i centos:centos6 /bin/bash`
  Make changes, then grab the container ID (part of the host name in the shell)
  `$ exit`
  `# docker commit 4ff1c0d3e9bd centos6:withupdates`

###### Attach to a container that is already running:
  `# docker attach <containerID>`

###### Detach from a running container"
  Press CTRL+P CTRL+Q

###### Stop a daemonized container:
  `# docker stop daemon_dave`

###### See what's happening inside a daemonized container:
  `# docker logs <ContainerID>`

###### Follow the output of a daemonized container:
  `# docker logs -f <ContainerID>`

###### Display the last 10 lines of a daemonized container's output:
  `# docker logs --tail 10 <ContainerID>`

###### Display the output of a daemonized container with timestamps:
  `# docker logs --ft <ContainerID>`

###### Run a container, but specify its name:
  `# docker run --name bob_the_container -i -t ubuntu /bin/bash`
  Now the container can be referred to by its name rather than its ID.

###### Execute a command inside a container:
  `# docker exec -it MYCONTAINER1 /usr/bin/top`

###### Add a new background task to a running container:
  `# docker exec -d daemon_dave touch /etc/new_config_file`

###### Run a command against a docker image:
  `# docker run ubuntu:latest /bin/echo "Hello from your Docker container"`

###### Inspect a container (good for finding its IP):
  `# docker inspect <containerID>`

###### Inspecting a container's processes:
  `# docker top <containerID>`

###### Mount a local directory to a container:
  `# docker run -itv /local/dir:/mnt/myvolume jay:testhtml /bin/bash`

###### Make resources from one container available in another:
  `# docker run -d -i -t --volumes-from DATA1 --name DATA2 jay:centos6 /bin/bash`
  `# docker run -d -i -t -v /data/ --name DATA1 jay:centos6 /bin/bash`

###### Delete all previously run and stopped containers:
  `# docker rm `docker ps -a -q``

###### Delete containers older than 7 days ago:
  `# ocker ps -a |grep 'week' | awk '{print $1}' | xargs docker rm`

###### Delete a non-running container (stop it with 'docker stop' or 'docker kill' first):
  `# docker rm <container id>`

###### Delete all containers:
  `# docker rm `docker ps -a -q` or docker rm $(docker ps -a -q)`

###### Delete all images:
 `# docker rmi $(docker imagesx -q)`

###### Remove an image:
  `# docker rmi <imageID>`

###### Better way to find a container's IP address:
  `# docker inspect <containerID> |grep IPAddress |cut -d ":" -f2 | cut -d "\"" -f2`

###### Starting a registry from a docker container:
  `# docker run -p 5000:5000 registry`

###### Add a resource for a Docker file to the container:
  `ADD testfile.html /var/www/html/testfile.html`

###### To build a container from a Dockerfile, cd into the directory containing the Dockerfile and execute:
  `# docker build -t <jay:name> .`
* In this example, the `-t` is for tag, so it's giving it a new name of `jay:name`.
* The `-t` parameter will probably overwrite another container if it has the same tag.

#### Misc
###### Note about ufw firewall:
  * Change `DEFAULT_FORWARD_POLICY` to `Accept` in `/etc/default/ufw`

###### Sample startup script (reference this in /root/.bashrc:
    #!/bin/bash

    rm -rf /run/httpd/*
    exec /usr/sbin/apachectl -D FOREGROUND


##### Sample Dockerfile:
    FROM centos:centos6
    MAINTAINER Jay <somebody@somewhere.net>

    RUN yum -y update; yum clean all
    RUN yum -y install httpd vim
    RUN echo "This is our new Apache Test Site" >> /var/www/html/index.html

    EXPOSE 80

    RUN echo "/sbin/service httpd start" >> /root/.bashrc
