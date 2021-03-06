# Instructions for using Manuel's repos

## Important changes
Date | Description
:--- | :---
2020.Apr.20 | Moved AUR packages from repo [m-more2] to a new repo [m-aur].
2020.Apr.20 | Moved package source of mirrorlist-m to repo [m-m] from repo [m-more2].
2020.Apr.15 | In your file **/etc/pacman.conf** you **must** change repo **[m-more]** to **[m-more2]** due to the repo move operation today.
2020.Mar.28 | Repo addresses have been changed. Please install the **mirrorlist-m** package as instructed below!

## Overview
Currently the following repos are available:

Name | Purpose | Link | Special remarks
:---- | :------- | :---- | :---------------
m-m | Packages created by Manuel | [m-m](../../../m-m) | -
m-more2 | Additional open source packages | [m-more2](../../../m-more2) | Moved from [m-more] at 2020-Apr-15!
m-aur | Selection of AUR packages | [m-aur](../../../m-aur) | New repo.

## Steps
The following steps
1. edit /etc/pacman.conf
2. install a gpg key
3. update system
4. install mirrorlist-m
5. final touch

are needed to start using the repos. Details are below.

### 1. Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions (note the comment character '#'
at the beginning of the **Include** lines - it will be removed in the last step):
```
# Place the following repo definitions preferably in the end of the file since these packages
# shouldn't conflict with other repos.

# Packages created and published by Manuel:
[m-m]
SigLevel = Required
#Include = /etc/pacman.d/mirrorlist-m
Server = https://github.com/manuel-192/$repo/releases/download/$arch

# Selection of prebuilt AUR packages:
[m-aur]
SigLevel = Required
#Include = /etc/pacman.d/mirrorlist-m
Server = https://github.com/manuel-192/$repo/releases/download/$arch

# Additional open source packages:
[m-more2]
SigLevel = Required
#Include = /etc/pacman.d/mirrorlist-m
Server = https://github.com/manuel-192/$repo/releases/download/$arch
```
### 2. Add the maintainer's gpg key to your system
but only if you trust the maintainer and these packages!<br><br>
Run the following commands (unless you haven't already done so):
```
sudo pacman-key --recv-keys A1F1B5187D25904B
sudo pacman-key --lsign-key A1F1B5187D25904B
```
You should see token **manuel-192** inside the output of the these last commands.
If not, check that the added key was correct.

### 3. Update your system
Update your repos and packages:
```
sudo pacman -Syyu
```
This command should also show the new package database files that you added.

### 4. Install mirrorlist-m
```
sudo pacman -S mirrorlist-m
```
### 5. Final touch
Remove the comment character (#) from the Include line(s) as noted above.<br>
Also, you *should* remove the **Server** line for the [m-m], [m-aur] and [m-more2].<br>
Then both repos should have lines looking like this:
```
SigLevel = Required
Include = /etc/pacman.d/mirrorlist-m
```
Then update again:
```
sudo pacman -Syy
```

## Troubleshooting
In case of any error, please check that you have copied the repo definitions exactly as they are above. And check that the installed gpg key was correct.<br>
You can see what gpg keys you have installed with:
```
gpg --list-keys --keyid-format LONG
```
You may write to https://forum.endeavouros.com about any issues with these repos.
<br><br>
<b>DISCLAIMER</b>: <u>use these packages at your own risk!</u><br>I have no way of
guaranteeing the safety of these packages.
I build and sign (using name <i>manuel-192</i>) them,
and transfer them here using the best safety practices I know of.
