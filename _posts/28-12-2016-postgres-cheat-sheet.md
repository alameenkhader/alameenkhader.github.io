---
layout: post
title:  "Postgres Cheat Sheet"
date:   2017-01-01 02:44:26 +0530
categories: Postgres
---

### PG Restore
`pg_restore --verbose --clean --no-acl --no-owner -h localhost -U myuser -d mydb latest.dump`

### PG Dump
`PGPASSWORD=mypassword pg_dump -Fc --no-acl --no-owner -h localhost -U myuser mydb > mydb.dump`

### Install package
`sudo apt-get install postgresql postgresql-contrib`

#### Install pgAdmin III - a handy GUI for PostgreSQL
`sudo apt-get install pgadmin3`

####Setup
#####Login to postgres sql prompt
`sudo -u postgres psql postgres`
#####Change the postgres user password
`\password postgres`
#####Exit the posgreSQL prompt
`Control+D`

###Basics
####Login as a different user
`psql -U <username> -h 127.0.0.1 <database-name>`
####Create a database
`sudo -u postgres createdb mydb`
Create a user
`CREATE USER <username> WITH PASSWORD '<password>';`
List all the users
`\du`
Grant a database to the user
`GRANT ALL PRIVILEGES ON DATABASE "<databasename>" to <username>;`
Drop database
`sudo -u postgres dropdb mydb`
Run the psql prompt to use the database mydb
`sudo -u postgres psql mydb`
List all the databases
`\list`
Switch databases
`\connect <database-name>`
Create a table
```
    CREATE TABLE weather (
      city            varchar(80),
      temp_lo         int,           -- low temperature
      temp_hi         int,           -- high temperature
      prcp            real,          -- precipitation
      date            date
    );
  ```
Drop a table
`DROP TABLE tablename;`
List alll the database tables
`\dt`
Import Database dump
`psql -U username -h localhost -d database_name < path/to/your/file.sql`

## PG Restore
`pg_restore -U postgres -d dbname filename`

#Trouble Shoot
##`FATAL:  Peer authentication failed for user "uuser"`
1. vi /etc/postgresql/9.1/main/pg_hba.conf
2. Change
   `# TYPE DATABASE USER ADDRESS METHOD`
   `local  all      all          peer`
   To
   `# TYPE DATABASE USER ADDRESS METHOD`
   `local  all      all          md5`
3. sudo service postgresql restart

## Compile php again for psql?
1. sudo apt-get install php5-pgsql
2. sudo /etc/init.d/apache2 restart

## Unable to login as postgres user from phpgadmin
1. sudo vi /etc/postgresql/9.3/main/pg_hba.conf
2. Find the lines
```
# Database administrative login by Unix domain socket
local   all             postgres                    ident
```
The last word may be `ident`, `md5` or `all`, whatever change it to to `trust`
3. Restart `sudo /etc/init.d/postgres restart`
4.

## Upgrage from 9.3 to 9.4

1. Package repo (for apt-get)
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" >> /etc/apt/sources.list.d/postgresql.list'
```

2. `sudo apt-get update`
3. `sudo apt-get install postgresql-9.4 postgresql-server-dev-9.4 postgresql-contrib-9.4`
4. `sudo pg_lsclusters`
5. `sudo /etc/init.d/postgresql stop`
6. `sudo pg_dropcluster --stop 9.3 main`
7. `sudo pg_dropcluster 9.3 main` # Optional
8. `sudo pg_dropcluster --stop 9.4 main`
9. `sudo pg_createcluster 9.4 main`
10. `sudo service postgresql restart 9.4`

References: https://medium.com/@tk512/upgrading-postgresql-from-9-3-to-9-4-on-ubuntu-14-04-lts-2b4ddcd26535#.othub6c58
            https://gist.github.com/tamoyal/2ea1fcdf99c819b4e07d#file-gistfile1-sh-L65

#### References
* [heroku] [Heroku]

[heroku]: https://devcenter.heroku.com/articles/heroku-postgres-import-export
