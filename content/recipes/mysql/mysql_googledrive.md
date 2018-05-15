---
linkTitle: "Google Drive"
slug: "googledrive"
title: "How To Backup And Encrypt MySQL to Google Drive"
date: 2018-04-18T13:39:02-07:00
draft: false
---

#### Step 1: Create an Encrypted Folder in Google Drive
```
$ scramfs alias create my_googledrive -e --store-local-key --create -p secure.scramfs -t googledrive
```

[Read more about this step.](../../../step1/googledrive/)

#### Step 2: Dump Your Database To the Encrypted Folder
```
$ mysqldump -h172.17.0.2 -uwpadmin -pfoobar wordpress | scramfs save scramfs://my_googledrive wordpress_db_1
```

[Read more about this step.](../../../step2/mysql/)