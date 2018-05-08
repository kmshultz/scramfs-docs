---
title: "Step1_s3"
date: 2018-05-07T11:37:10-07:00
draft: true
---

{{%excerpt%}}
### Step 1: Create an Encrypted Folder in Dropbox

First, create a new ScramFS alias called `<ALIAS>` that points to a new Dropbox folder, `secure.scramfs`:

```
$ scramfs alias create <ALIAS> -e --store-local-key --create -p secure.scramfs -t dropbox
Use "my files" or "shared"? [M/s]: M
Access token [press Enter to obtain the new one]: 
```

At the first prompt, enter **M** or **s**, depending on where in Dropbox you want to store your data.

Next, press enter **Enter**, causing ScramFS to open Dropbox in your web browser. Sign in to Dropbox if you haven't already, then click **Allow** to let ScramFS access Dropbox:

![Choose Google account](/images/dropbox_allow.png)

Then return to your shell and set a password for your new encrypted folder (enter it twice to confirm):

```
$ scramfs alias create <ALIAS> -e --store-local-key --create -p secure.scramfs -t dropbox
Use "my files" or "shared"? [M/s]: M
Authentication token [press Enter to obtain the new one]: 
Set new encryption password for alias <ALIAS>: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://<AlIAS>". We recommend that you do "scramfs alias test <ALIAS>"
```

Now you should be able to [see your new encrypted folder](https://www.dropbox.com/home/secure.scramfs):

![secure.scramfs](/images/dropbox_dir.png)

Finally, to make sure ScramFS can write data to the folder, run the `alias test` command:

```
$ scramfs alias test <ALIAS>
dropbox (read): PASS
dropbox (write): PASS
```

Looks good! Now you're ready to encrypt and backup local data to your Dropbox account.
{{% /excerpt%}}
