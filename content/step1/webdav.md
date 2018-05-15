---
title: "Creating an Alias to a WebDAV Share"
linkTitle: "WebDAV"
date: 2018-05-10T15:26:41-07:00
draft: False
---

Create a new ScramFS alias called `webdav_share` that points to a new folder, `secure.scramfs` (the folder need not exist yet):

```
$ scramfs alias create my_webdav_share -e --store-local-key --create -p secure.scramfs -t webdav
```

ScramFS will prompt you first for the URL of the WebDAV share, then for share login credentials. Enter both:

```
$ scramfs alias create my_webdav_share -e --store-local-key --create -p secure.scramfs -t webdav
Server URL: http://localhost:8080/webdav
Username: admin
Password: 
```

If ScramFS can connect to the URL and you provided good credentials, it will prompt you to set a password for your new encrypted folder (enter it twice to confirm):

```
$ scramfs alias create my_webdav_share -e --store-local-key --create -p secure.scramfs -t webdav
Server URL: http://localhost:8080/webdav
Username: kent
Password: 
Set new encryption password for alias my_webdav_share: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://my_webdav_share". We recommend that you do "scramfs alias test my_webdav_share"
```

Because the command included `--create` option, ScramFS created the new directory for you:

![WebDAV folder](/images/webdav_folder.png)

Finally, to make sure ScramFS can write data to the folder, run the `alias test` command:

```
$ scramfs alias test my_webdav_share
my_webdav_share (read): PASS
my_webdav_share (write): PASS
```

Looks good! Now you're ready to encrypt and backup local data to your WebDAV share.