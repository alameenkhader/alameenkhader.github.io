---
title:  Postgres in Docker
layout: post
date: 2017-04-01 02:44:26 +0530
description: List of helpful commands when running postgres in docker
---

### DOCKER PG_DUMP

    # Login to the docker container
    sudo docker exec -it <container name> bash
    # Generate the dump
    pg_dump -h localhost -p 5432 -U <database username> -d <database name> > dump
    # Copy the dump from the container to the host machine
    docker cp <container name>:/dump .

    # example:
    # sudo docker exec -it db bash
    # pg_dump -h localhost -p 5432 -U postgres -d myapp_database > dump
    # docker cp db:/dump .

### DOCKER PG_RESTORE

    sudo docker exec -i <container name> pg_restore -C --clean --no-acl --no-owner -U postgres -d <database name> < /path/to/pg_dump
    # example:
    # sudo docker exec -i myapp-db pg_restore -C --clean --no-acl --no-owner -U postgres -d myapp_dev < myapp_dev_pg_dump

