# To install Docker on AWS EC2 instance
   - Create an EC2 instance on AWS and Connect to it
   - Follow the link to install docker:
    https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html`
   - Use putty to connect to the instance
   

$ touch Dockerfile

# Build Docker image
Syntax:
   # docker build -t img_from .

# Scenario 1: We want to build an image based on ubuntu os and run the bash command on startup.

ARG CODE_VERSION=16.04

FROM ubuntu:${CODE_VERSION}

RUN apt-get update -y

CMD ["bash"]


=============================================================================

# Scenario 2: We want to build an image based on ubuntu and install curl command in it. Then remove temp files from the /var/lib/apt/lists/* directory. Then, we need to set the environment variables 

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


RUN mkdir /home/Codes

ENV USER Joker-Canvas
ENV SHELL /bin/bash
ENV LOGNAME Joker-Canvas

CMD ["bash"]

# Build the image
$ docker build -t img_run_env .

# Run container
$ docker run -itd --name c2 img_run_env
$ docker exec -it c2 bash
$ # ls
$ # echo $USER
$ # echo $SHELL
$ # echo $LOGNAME
$ # cd /home
$ /home# ls
$ /home# exit

=================================================================================

# Scenario 3: Build an ubuntu image and install nginx in it

FROM ubuntu:16.04

RUN apt-get update && apt-get install nginx -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


EXPOSE 80


CMD ["nginx", "-g", "daemon off;"]



$ docker build -t img_expose .

$ docker run -itd --name web1 -p 8080:80 img_expose

$ curl http://localhost:8080



# To create an python image to run python application
=============================================================
## Steps
1. OS- Ubuntu
2. Update apt repo
3. Install dependencies using apt
4. Install Python dependencies using pip
5. Copy source code to  /opt folder
6. Run the web server using "flask" command

## Now to install dependencies:
   # Debain, Ubuntu, Mint and other flavors of Linux
        - use 'apt' application to install from repository
        - Example: sudo apt install/update app-name
   # Redhat, Centos, and Fedora
        - use 'yum'
        - Example: sudo yum install app-name

## Implementation
1. Create a dockerfile
2. Add instructions into it
3. Build the image
4. push the image to docker hub registry


A Dockerfile is a file that contain steps to create the container
Two main components of Dockerfile are:
   # INSTRUCTION
   # ARGUMENT

   # INSTRCUTIONS - FROM, RUN, COPY, ENTRYPOINT, CMD, and so on

   You pass arguments to the instructions

# Start image building from a base image


# Lets build a python image
https://dockerlabs.collabnix.com/beginners/dockerfile/lab_dockerfile_python.html




# Searching of Images
=====================================
1. docker search ubuntu
2. docker search --filter "is-official=true" registry
3. docker search --format "table {{.Name}}\t{{.Description}}\t{{.IsOfficial}}" ubuntu

# Listing Images
=======================================
1. docker images 
2. docker image ls
3. docker images ubuntu:16.04


# You can create repository on Dockerhub
============================================
$ docker login
$ docker tag nginx:latest priya12345/repo-nginx:cc-nginx
$ docker image push priya12345/repo-nginx:cc-nginx



# To run Java Spring Boot Rest API in Docker
# Steps:
   1. Build a Jar
   2. Setup the pre-requisites for Running the jar
      - openjdk:8-jdk-alpine
      - docker run -itd openjdk:8-jdk-alpine
      - docker container ls
      - docker container exec keen_leakey ls /tmp
      - docker container cp *.jar keen_leakey:/tmp
      - docker container exec keen_leakey ls /tmp
      - docker container commit --change='CMD ["java", "-jar", "/tmp/hello-world-rest-api.jar"]' keen_leakey priya12345/restapi:1.0

      - docker run -p 8080:8080 priya12345/restapi:1.0
      

   3. Copy the jar
   4. Run the jar


====================================================================

To push an image on docker repository
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname

docker push priya123456/myrepo:tagname

# myubuntu is a tag to the image
$ docker tag img_ubuntu:mywork priya123456/myrepo:myubuntu
$ docker login
# username - dockerid
# password - 
$ docker push priya123456/myrepo:myubuntu


Login into Dockerhub
$ docker pull priya123456/myrepo:myubuntu
$ docker run -it --name c1 priya123456/myrepo:myubuntu


