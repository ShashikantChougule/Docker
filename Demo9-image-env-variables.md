# Create an image to set environment variables in it
===========================================================

# Image with ubuntu os files, curl command, own folder
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


RUN mkdir /home/Codes

ENV USER Joker-Canvas
ENV SHELL /bin/bash
ENV LOGNAME Joker-Canvas

CMD ["bash"]


# build the image and run the container
$ docker build -t imgenv:1.0 .

$ docker run -d --name c1 imgenv

$ docker exec -it c1 sh
# ls
# env
# echo $USER
# echo $LOGNAME

