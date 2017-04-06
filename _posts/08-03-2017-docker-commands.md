---
layout: post
title:  "Docker Commands"
date:   2017-03-08 02:44:26 +0530
categories: Docker
---
Remove a docker image
sudo docker rmi  <IMAGE ID>

Remove a docker container
sudo docker rm <ID>

Docker: remove all Exited containers
sudo docker ps -a | grep Exit | cut -d ' ' -f 1 | xargs sudo docker rm

List all images
`sudo docker image ls` or `docker images`

List all containers
sudo docker container ls

sudo docker build -t demo .
sudo docker run -it -p 4567:4567 demo

sudo chmod 757 -R .

docker-compose build
docker-compose up
docker-compose run web rake db:create
docker ps

## How to load with mysql dump
sudo docker exec -i pizza-ranch-db mysql -uroot -ppassword -Dpizza_live --force < /home/alameen/Desktop/pizzaranch_feb22.sql

## Docker copy/rename/tag an image
sudo docker tag <IMAGE_Id> new_name_or_tag
