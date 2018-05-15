---
title: "Creating An Alias To Microsoft OneDrive"
linkTitle: "Microsoft OneDrive"
date: 2018-05-10T15:26:50-07:00
draft: false
---

Create a new ScramFS alias called `my_onedrive` that points to a new OneDrive folder, `secure.scramfs`:

```
$ scramfs alias create my_onedrive -e --store-local-key --create -p secure.scramfs -t googledrive
Use "my files" or "shared"? [M/s]: M
Access token [press Enter to obtain the new one]: 
```

At the first prompt, enter **M** or **s**, depending on where in OneDrive you want to store your data.

Next, press enter **Enter**, causing ScramFS to open OneDrive in your web browser. Sign in to your Microsoft Live account if you haven't already, then click **Yes** to let ScramFS access OneDrive:

![Choose Google account](/images/onedrive_allow.png)

After you have logged in, return to your shell and set a password for your new encrypted folder (enter it twice to confirm):

```
$ scramfs alias create my_onedrive -e --store-local-key --create -p secure.scramfs -t onedrive
Use "my files" or "shared"?  [M/s]: M
Access token [press Enter to obtain the new one]: 
Refresh token [press Enter to obtain the new one]: 
Set new encryption password for alias my_onedrive: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://my_onedrive". We recommend that you do "scramfs alias test my_onedrive"
```

Now you should be able to see your new encrypted folder in [OneDrive](https://onedrive.live.com/):

![secure.scramfs](/images/onedrive_folder.png)

Finally, to make sure ScramFS can write data to the folder, run the `alias test` command:

```
$ scramfs alias test my_onedrive
google_drive (read): PASS
google_drive (write): PASS
```

Looks good! Now you're ready to encrypt and backup local data to your OneDrive.
