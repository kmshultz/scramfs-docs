---
title: "Step 4: Backing Up The Encryption Key"
date: 2018-05-10T14:18:53-07:00
draft: false
weight: -40
---

In Step 1, you were warned never to lose the password for `secure_directory`. Similarly, you must never lose the encryption key that the password protects. The encryption key is stored with the rest of the alias metadata, which ScramFS generated when you ran `scramfs alias create`.

Suppose you have a network disk mounted at `/mnt/backup`. You can run the following to backup the encryption key for `secure_directory`:

```
$ scramfs key backup secure_directory /mnt/backup/
Input password: 
Input backup password: 
Confirm backup password: 
Key successfully backed up.
```

For the first password prompt, enter the alias password. For the next password prompt (and the confirmation prompt after it), enter a different password (or the same, if you wish) to protect the backup.

Now you have a file `.backup` on your network disk. It's encrypted using the new password you chose above:

```
$ cat /mnt/backup/.backup 
? UȾ^?R??15?u3??~s
????"?.^???5?Ȃ????/hdy???OW?4??x#l????????4՗?
```