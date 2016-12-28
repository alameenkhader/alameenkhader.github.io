---
layout: post
title:  "Postgres Cheetsheet"
date:   2016-12-28 02:44:26 +0530
categories: Postgres
---

### pr_restore
`pg_restore --verbose --clean --no-acl --no-owner -h localhost -U myuser -d mydb latest.dump`

### pg_dump
`PGPASSWORD=mypassword pg_dump -Fc --no-acl --no-owner -h localhost -U myuser mydb > mydb.dump`
## Rspec

#### References
* [heroku] [Heroku]

[heroku]: https://devcenter.heroku.com/articles/heroku-postgres-import-export
