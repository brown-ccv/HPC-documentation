---
title: CIFS
date: '2019-01-31 22:06:09 +0000'
project: Oscar
section: Connecting to Oscar
weight: 0
icon: check
---

# CIFS \(Local Mount\)

CCV users can access their home, data, and scratch directories as a local mount on their own Windows, Mac, or Linux system using the Common Internet File System \(CIFS\) protocol \(also called Samba\). This allows you to use applications on your machine to open files stored on Oscar. It is also a convenient way to move files between Oscar and your own machine, as you can drag and drop files.

{% hint style="info" %}
To use CIFS you will need to be on the Brown network. On campus use the 'Brown' wifi network. Off campus use the [Brown VPN client](https://vpn.brown.edu).
{% endhint %}

Users should ensure that the date and time are set correctly on their machine. Now you are ready to mount your CCV directories locally. Instructions for each of the various operating systems are given below.

{% hint style="warning" %}
If you have problems with `smb://smb.ccv.brown.edu`

You can use the old CIFS mount`smb://oscarcifs.ccv.brown.edu.`[`Documentation here`](cifs-non-ad-local-mount.md)
{% endhint %}

## macOS

1. In the Finder, press "Command + K" or select "Connect to Server..."

   from the "Go" menu.

2. For "Server Address", enter `smb://smb.ccv.brown.edu`

   and click "Connect".

3. Enter your AD username and password.
4. You may choose to add your login credentials to your keychain so you will not need to enter this again.

**Optional.** If you would like to automatically connect to the share at startup:

1. Open "System Preferences" \(leave the Finder window open\).
2. Go to "Accounts" &gt; "\(your account name\)".
3. Select "Login Items".
4. Drag your data share from the "Finder" window to the "Login Items" window.

## Linux

1. Install the `cifs-utils` package:

   ```bash
   CentOS/RHEL:   $ sudo yum install cifs-utils
   Ubuntu:        $ sudo apt-get install cifs-utils
   ```

2. Make a directory to mount the share into:

   ```bash
   $ sudo mkdir /mnt/rdata
   ```

3. Create a credentials file and add your AD account information:

   ```bash
   $ sudo gedit /etc/cifspw

   username=<user>
   password=<password>
   ```

4. Allow only root access to the credentials files:

   ```bash
   $ sudo chmod 0600 /etc/cifspw
   ```

5. Add an entry to the `fstab`:

   ```bash
   $ sudo gedit /etc/fstab
   ```

6. The `fstab` entry is the single line:

   ```bash
   //smb.ccv.brown.edu/<user> /mnt/rdata cifs credentials=/etc/cifspw,vers=2.0,nounix,uid=<localUser> 0 0
   ```

7. Change `<localUser>` to the login used on your Linux workstation.
8. Mount the share:

   ```bash
   $ mount -a
   ```

## Windows

1. Right-click "Computer" and select "Map Network Drive"
2. Select an unassigned drive letter
3. Enter `\\smb.ccv.brown.edu\<user>` as the Folder
4. Check "Connect using different credentials"
5. Click "Finish"
6. Enter your AD user name. If your computer is not in Active Directory \(AD\), you should enter your username in the format **ad\username**
7. Enter your AD password and click "OK"

You can now access your home directory through Windows Explorer with the assigned drive letter. Your data and scratch directories are available as the subdirectories \(`~/data` and `~/scratch`\) of your home directory.

