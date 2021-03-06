---
title:  Docker Cheat Sheet
layout: post
date: 2017-02-01 02:44:26 +0530
description: List of docker commands
---

### List all docker images

    sudo docker image ls
    # OR
    docker images

### Remove a docker image

    sudo docker rmi  <IMAGE ID>

### List all containers

    sudo docker container ls

### Stop all containers

    docker stop $(docker ps -a -q)

### Remove a docker container

    sudo docker rm <ID>

### Remove all Exited containers

    sudo docker ps -a | grep Exit | cut -d ' ' -f 1 | xargs sudo docker rm

### Remove all orphan images

    sudo docker rmi $(docker images --filter "dangling=true" -q --no-trunc)


### How to load with mysql dump

    sudo docker exec -i <container-name> mysql -uroot -ppassword -D<databasename> --force < /path/to/dump.sql

    ## example:
    ## sudo docker exec -i myblog-db mysql -uroot -ppassword -Dmyblog --force < /home/alameen/myblog.sql

### How to copy/rename/tag an image

    sudo docker tag <IMAGE_Id> <new_name_or_tag>

    ##example:
    ## sudo docker tag myblog-web latest

## Troubleshoot


Sometimes you may find it difficult to remove a container. Then manually remove the container would help

    # stop docker
    sudo /etc/init.d/docker stop
    # list containers in your machine
    sudo ls /var/lib/docker/containers
    # Identify the container you want to remove
    sudo rm -r /var/lib/docker/containers/<contaner-id>
    # start docker
    sudo /etc/init.d/docker start
