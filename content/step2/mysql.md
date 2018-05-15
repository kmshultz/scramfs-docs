---
title: "Backing Up And Encrypting A MySQL Database"
linkTitle: "MySQL"
date: 2018-05-10T15:12:05-07:00
draft: false
---

There's no need to dump your database to disk before moving it to the encrypted directory—you can dump it, encrypt it, and back it up all in one step!

Suppose your database is called `wordpress`, is located at 172.17.0.2, and is accessible via user `wpadmin` and password `foobar`. Here's how to back up and encrypt it:

```
$ mysqldump -h172.17.0.2 -uwpadmin -pfoobar wordpress | scramfs save scramfs://<ALIAS>/wordpress_db_1
```
