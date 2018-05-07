---
title: "Getting Started"
date: 2018-04-18T13:10:38-07:00
draft: false
weight: -30
---

Before we consider the many use cases for ScramFS CLI, let's get acquainted with it. This page shows how to:

1. Create an encrypted directory
2. Add a file to it
3. Verify the file's integrity after encryption and after decryption
4. Backup the directory's encryption key
5. Automatically encrypt your files

If you haven't done so already, [download a trial version of ScramFS CLI](https://scramfs.com/download/). Then make sure `scramfs` is in your shell's `PATH`:

```
$ which scramfs
/usr/local/bin/scramfs
```

Your own `scramfs` may be located in a different path than above, depending on your operating system.

### Step 1: Create an Encrypted Directory

Before ScramFS can encrypt any data, you must tell it where to store the data. 

The simplest type of encrypted store is a local directory. Here's the command to create an encrypted local directory (don't run it just yet):

```
$ scramfs alias create secure_directory --create -e -p ~/secure.scramfs
```

An **alias** is a simple name that refers to the location of an encrypted store. Here we're creating an alias called `secure_directory` that refers to a new directory, `~/secure.scramfs`. (You don't need to create the directory yourself; ScramFS will do that for you since we added `--create`.) Any time you interact with this directory—to list its contents, add a file, read a file, etc—you need the alias name.

But not _only_ the alias name. Run the command now:

```
$ scramfs alias create secure_directory --create -e -p ~/secure.scramfs
Set new encryption password for alias secure_directory:
```

An alias encompasses both the location of encrypted store _and_ its encryption key. The `-e` option tells ScramFS to prompt us for a password, which it will use to protect the alias's auto-generated encryption key. Think of a strong password and enter it twice to confirm:

```
$ scramfs alias create secure_directory --create -e -p ~/secure.scramfs
Set new encryption password for alias secure_directory: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://secure_directory". We recommend that you do "scramfs alias test secure_directory"
```

You have just created your first alias with ScramFS! Before adding data to the encrypted directory, test the alias, providing its password when prompted:

```
$ scramfs alias test secure_directory
Enter encryption password for alias secure_directory: 
secure_directory (read): PASS
secure_directory (write): PASS
```

{{% notice warning %}}
**Never write your password down—not on paper, not in a file—and never lose it.** If you do lose it, you will NOT be able to recover the data in the encrypted directory.
{{% /notice %}}

Now let's add some data.

### Step 2: Encrypt a File

First, create a file outside of the encrypted directory:

```
$ echo "foo" > bar.txt
```

Then use ScramFS to copy it to the encrypted directory:

```
$ scramfs cp bar.txt scramfs://secure_directory/
Enter encryption password for alias secure_directory: 
```

That command probably looks familiar. ScramFS commands are named similarly to the common UNIX commands for interacting with the filesystem. Here's another one:

```
$ scramfs ls scramfs://secure_directory
Enter encryption password for alias secure_directory: 
bar.txt
```

Now try to examine the directory without ScramFS:

```
$ ls -l ~/secure.scramfs/
total 128
-rw-r--r--  1 kent  staff  64432 Apr 24 13:45 ꆽ糕鸊萣审㨗涯尞ᚼ鲮㚒鬞䨂䱸涍ᙡ來ഛ
```

We can see that the file is there, but ScramFS has obfuscated its name. And is that file really 64 kilobytes? Check the size of the unencrypted file:

```
$ ls -l bar.txt
-rw-r--r--  1 kent  staff  4 Apr 24 13:54 bar.txt
```

It's really just 4 bytes, so it turns out ScramFS has also obfuscated its size.

Now what about the file's contents?

### Step 3: Verify the Integrity of the File

First let's look at the file's contents:

```
$ scramfs cat scramfs://secure_directory/bar.txt
Enter encryption password for alias secure_directory: 
foo
```

Looks good. But for larger files, we cannot quickly verify the integrity of the data by glancing at the contents. Thankfully, you can use ScramFS to calculate a hash:

```
$ scramfs checksum --md5 scramfs://secure_directory/bar.txt
Enter encryption password for alias secure_directory: 
d3b07384d113edec49eaa6238ad5ff00  scramfs://secure_directory/bar.txt
```

Then calculate a hash of the unencrypted file:

```
$ md5 bar.txt
MD5 (bar.txt) = d3b07384d113edec49eaa6238ad5ff00
```

Great—the checksums match.

{{% notice note %}}
Your `md5` command might be named `md5sum`, depending on your operating system.
{{% /notice %}}

Finally, copy the encrypted file back to your (unencrypted) working directory using a different filename:

```
$ scramfs cp scramfs://secure_directory/bar.txt bar-decrypted.txt
Enter encryption password for alias secure_directory:
```

Then compare the checksum of the original to that of the decrypted copy:

```
$ md5 bar.txt bar-decrypted.txt 
MD5 (bar.txt) = d3b07384d113edec49eaa6238ad5ff00
MD5 (bar-decrypted.txt) = d3b07384d113edec49eaa6238ad5ff00
```

### Step 4: Backup the Encryption Key

In Step 1, you were warned never to lose the password for `secure_directory`. Similarly, you must never lose the encryption key that the password protects. The encryption key is stored with the rest of the alias metadata, which ScramFS generated when you ran `scramfs alias create`.

Suppose you have a network disk mounted at `/mnt/backup`. You can run the following to backup the encryption key for `secure_directory`:

```
$ scramfs key backup secure_directory backup/
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

<Bit about restoring from backup>

### Step 5: Automatically Encrypt your files

Suppose you want to periodically back up and encrypt your files. How can you do that automatically, given that ScramFS requires your alias password every time you run it?

By creating a password-less key file. Here's how to do that:

```
$ scramfs key storelocal secure_directory
Input password: 
A local copy of the encryption key successfully stored.
```

Now you can access the encrypted directory without a password:

```
$ scramfs ls scramfs://secure_directory
bar.txt
```

<Bit about scripting backups>