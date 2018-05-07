---
title: "Step1_googledrive"
date: 2018-05-07T11:27:57-07:00
draft: true
---

{{%excerpt%}}
### Step 1: Set Up An Alias For Your Google Drive

First, create a new ScramFS alias called `google_drive` that points to a new Google Drive directory, `secure.scramfs`:

```
$ scramfs alias create google_drive -e --store-local-key --create -p secure.scramfs -t googledrive
Use "my files" or "shared"? [M/s]: M
Access token [press Enter to obtain the new one]: 
```

At the first prompt, enter **M** or **s**, depending on where in Google Drive you want to store your data.

Next, press enter **Enter** twice, which causes ScramFS to open your web browser to a Google Authentication page: 

![Choose Google account](/images/google_account_prompt.png)

Choose or enter the Google account where you want to store your encrypted data, and close the browser window.

Then, set a password for your new encrypted directory (enter it twice to confirm):

```
$ scramfs alias create google_drive -e --store-local-key --create -p secure.scramfs -t googledrive
Use "my files" or "shared"? [M/s]: M
Access token [pre
Refresh token [press Enter to obtain the new one]: 
Set new encryption password for alias google_drive: 
Confirm encryption password: 
Alias successfully created. You can access the alias using "scramfs://google_drive". We recommend that you do "scramfs alias test google_drive"
```

Run the `alias test` command to make sure the alias is working:

```
$ scramfs alias test google_drive
google_drive (read): PASS
google_drive (write): PASS
```

Looks good! Now you're ready to encrypt and backup any data to your Google Drive.
{{% /excerpt%}}
