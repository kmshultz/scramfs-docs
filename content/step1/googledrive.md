---
title: "Creating An Alias To Google Drive"
linkTitle: "Google Drive"
date: 2018-05-07T11:27:57-07:00
draft: false
weight: -30
---

Create a new ScramFS alias called `google_drive` that points to a new Google Drive folder, `secure.scramfs`:

```
$ scramfs alias create google_drive -e --store-local-key --create -p secure.scramfs -t googledrive
Use "my files" or "shared"? [M/s]: M
Access token [press Enter to obtain the new one]: 
```

At the first prompt, enter **M** or **s**, depending on where in Google Drive you want to store your data.

Next, press enter **Enter** twice, causing ScramFS to open a Google Accounts page in your web browser:

![Choose Google account](/images/google_account_prompt.png)

Choose or enter the Google account where you want to store your encrypted data, then close the browser window.

Then return to your shell and set a password for your new encrypted folder (enter it twice to confirm):

```
$ scramfs alias create google_drive -e --store-local-key --create -p secure.scramfs -t googledrive
Use "my files" or "shared"? [M/s]: M
Access token [pre
Refresh token [press Enter to obtain the new one]: 
Set new encryption password for alias google_drive: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://google_drive". We recommend that you do "scramfs alias test google_drive"
```

Now you should be able to see your new encrypted folder in [Google Drive](https://drive.google.com):

![secure.scramfs](/images/google_drive_dir.png)

Finally, to make sure ScramFS can write data to the folder, run the `alias test` command:

```
$ scramfs alias test google_drive
google_drive (read): PASS
google_drive (write): PASS
```

Looks good! Now you're ready to encrypt and backup local data to your Google Drive.
