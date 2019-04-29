---
layout: post
title: docker command
author: Mizuha Ki
date: 2019-04-18
categories:
- computer science
- ubuntu
- docker
tags:
- computer science
- ubuntu
- docker
- blog
---

## images import and export
- sudo docker images
- sudo docker save -o **.tar image_name
- sudo docker load --input **.tar

## new docker 
- sudo docker images
- sudo docker run ....

## enter container
- docker exec -ti container_name bash (recommend)
- docker attach container_name 

## frequent command
- docker images
- docker ps -a
- docker tag image_id image_name
- docker rmi image_name
- docker container rm
- docker container kill
- docker container start
- docker container stop
- docker container rename
