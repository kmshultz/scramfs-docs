---
title: "Creating An Alias To A Local Directory"
linkTitle: "Local Directory"
date: 2018-05-10T15:26:36-07:00
draft: false
weight: -60
---

The simplest type of alias is a local directory. Here's the command to create an encrypted local directory. Create a new ScramFS called `secure_directory` that points to a new local folder, `~/secure.scramfs` (the directory need not exist yet):

```
$ scramfs alias create secure_directory --create -e -p ~/secure.scramfs
```

ScramFS will prompt you for a password, which it uses to encrypt the directory. Choose a password and enter it twice to confirm:

```
$ scramfs alias create secure_directory --create -e -p ~/secure.scramfs
Set new encryption password for alias secure_directory: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://secure_directory". We recommend that you do "scramfs alias test secure_directory"
```

Because the command included `--create` option, ScramFS created the directory for you:

```
$ ls -la secure.scramfs/
total 136
drwx------   4 kent  staff    128 Apr 24 13:45 .
drwxr-xr-x+ 77 kent  staff   2464 May 10 14:43 ..
-rw-r--r--   1 kent  staff     82 Apr 22 17:05 .access
```

That `.access` file is where ScramFS stores the encryption key and other alias metadata.

Finally, run the `alias test` command to confirm the alias is working:

```
scramfs alias test secure_directory
google_drive (read): PASS
google_drive (write): PASS
```

Looks good! Now you're ready to add some files to the new encrypted directory.