---
title:  Postgres in Docker
layout: post
author: alameenkhader
author_email: alameenkhader@gmail.com
date: 2017-02-01 02:44:26 +0530
title_image: postgres-in-docker.jpg
---

### DOCKER PG_DUMP

    sudo docker exec <container name> pg_dump -U postgres -F t <database name> > <database_name>_pg_dump
    # example:
    # sudo docker exec myapp-db pg_dump -U postgres -F t myapp_dev > myapp_dev_pg_dump

### DOCKER PG_RESTORE

    sudo docker exec -i <container name> pg_restore -C --clean --no-acl --no-owner -U postgres -d <database name> < /path/to/pg_dump
    # example:
    # sudo docker exec -i myapp-db pg_restore -C --clean --no-acl --no-owner -U postgres -d myapp_dev < myapp_dev_pg_dump
