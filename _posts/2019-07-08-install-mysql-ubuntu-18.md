---
title: How to install MySQL - ubuntu 18.04
layout: post
date: 2019-07-08 02:44:26 +0530
description: Easy steps to install mysql in ubuntu 18.04
---

MySQL is the favorite relational database management system for all the beginners. Easy to install and work with. This article explains  how to install MySQL in Ubuntu 18.04.

Since this is our first time using apt in this session, lets refresh our local package index

        sudo apt-get update

## Install MySQL

        sudo apt-get install mysql-server -y

Lets check the installation

        al@al:~$ mysql --version
        mysql  Ver 14.14 Distrib 5.7.26, for Linux (x86_64) using  EditLine wrapper

To implement the security recommendations

       sudo mysql_secure_installation

This will take you through a series of prompts where you can
* set a password for root accounts.
* remove root accounts that are accessible from outside the local host.
* remove anonymous-user accounts.
* remove the test database.






