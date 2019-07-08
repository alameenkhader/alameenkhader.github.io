---
title: How to install phpPgAdmin - ubuntu 18.04
layout: post
date: 2018-09-18 02:44:26 +0530
description: phpPgAdmin is one of the best Postgres GUI tools. This artilcle explains how to install phpPgAdmin in Ubuntu 18.04.
---

phpPgAdmin is one of the best Postgres GUI tools. This artilcle explains how to install phpPgAdmin in Ubuntu 18.04.

Since this is our first time using apt in this session, lets refresh our local package index

    sudo apt update

## Install Apache

    sudo apt-get install apache2

## Install PHP

    sudo apt-get install php libapache2-mod-php

Lets check the installation

    al@al:~$ php -v
    PHP 7.2.10-0ubuntu0.18.04.1 (cli) (built: Sep 13 2018 13:45:02) ( NTS )
    Copyright (c) 1997-2018 The PHP Group
    Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
        with Zend OPcache v7.2.10-0ubuntu0.18.04.1, Copyright (c) 1999-2018, by Zend Technologies


## Install php-pgsql and phpPgAdmin

    sudo apt-get install php-pgsql phppgadmin

Lets check the installation, go to `localhost/phppgadmin` ![localhost/phppgadmin](/public//images/posts/phppgadmin-installed.png)

## Trobleshoot

1. `Login disallowed for security reasons.`

![Login disallowed for security reasons](/public/images/posts/phppgadmin-login-disabled.png)

   Open phpgadmin config file

    sudo nano /etc/phppgadmin/config.inc.php

   Find the line `$conf['extra_login_security'] = true;` and change the value to false so you can login to phpPgAdmin with user postgres. Please note that this is only for your local environment for development purposes.




