---
linkTitle: "Dropbox"
slug: "dropbox"
title: "How To Backup And Encrypt MySQL in Dropbox"
date: 2018-05-07T11:33:33-07:00
draft: false
parent: main
---

<h5 style="text-align: center;"><i>Got 10 minutes? You can backup and encrypt your MySQL Database in Dropbox!</i></h5>

#### Step 1: Create an Encrypted Folder in Dropbox
```
$ scramfs alias create my_dropbox -e --store-local-key --create -p secure.scramfs -t dropbox
```
[Read more about this step.](../../../step1/dropbox/)

#### Step 2: Dump Your Database To the Encrypted Folder
```
$ mysqldump -h172.17.0.2 -uwpadmin -pfoobar wordpress | scramfs save scramfs://my_dropbox/wordpress_db_1
```
[Read more about this step.](../../../step2/dropbox/)
