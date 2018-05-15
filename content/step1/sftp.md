---
title: "Creating An Alias To An SFTP Server"
linkTitle: "SFTP"
date: 2018-05-10T15:26:45-07:00
draft: true
---

Create a new ScramFS alias called `my_sftp_server` that points to a new folder on the server, `secure.scramfs` (the folder need not exist yet):

```
$ scramfs alias create my_sftp_server -e --store-local-key --create -p secure.scramfs -t sftp
```

ScramFS will prompt you first for the server host and port:

```
$ scramfs alias create my_sftp_server -e --store-local-key --create -p secure.scramfs -t sftp
Server address: localhost
Server port [default: 22]: 
```

Then for the SFTP server credentials:

```
$ scramfs alias create my_sftp_server -e --store-local-key --create -p secure.scramfs -t sftp
Server address: localhost
Server port [default: 22]: 
Username: admin
Password: 
```

If ScramFS can connect to the server and you provided good credentials, it will prompt you to set a password for your new encrypted folder (enter it twice to confirm):

```
$ scramfs alias create my_sftp_server -e --store-local-key --create -p secure.scramfs -t sftp
Server address: localhost
Server port [default: 22]: 
Username: kent
Password: 
Set new encryption password for alias my_sftp_server: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://my_sftp_server". We recommend that you do "scramfs alias test my_sftp_server"
```

Because the command included `--create` option, ScramFS created the new directory for you. Login to your SFTP server to see it:

```
$ sftp admin@192.168.1.99
Password:
Connected to 192.168.1.99.
sftp> ls -a secure.scramfs
secure.scramfs/.        secure.scramfs/..       secure.scramfs/.access
```

That `.access` file is where ScramFS stores the encryption key and other alias metadata.

Finally, to make sure ScramFS can write data to the folder, run the `alias test` command:

```
$ scramfs alias test my_sftp_server
my_webdav_share (read): PASS
my_webdav_share (write): PASS
```

Looks good! Now you're ready to encrypt and backup local data to your SFTP server.
