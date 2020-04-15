# Instructions for using Manuel's repos

## Important changes
- 2020-04-15: In your file **/etc/pacman.conf** you **must** change repo **[m-more]** to **[m-more2]** due to the repo move operation today.
- 2020-03-28: Repo address https://github.com/manuel-192/$repo/raw/master/repo is removed now. Please use the **mirrorlist-m** package as instructed below!
- 2020-03-03: **SigLevel** for Manuel's repos is now recommended to be set to **Required**.

## Overview
Currently there are the following repos available:

Name | Purpose | Link | Special remarks
---- | ------- | ---- | ---------------
m-more2 | Selection of AUR packages and more | [m-more2](../../../m-more2) | Moved from [m-more] at 2020-Apr-15!
m-m | Packages created by Manuel | [m-m](../../../m-m) | -

The following steps
1. edit /etc/pacman.conf
2. install a gpg key
3. update system
4. install mirrorlist-m
5. final touch

are needed to start using the repos.

## Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions (note the comment character '#'
at the beginning of the **Include** lines - it will be removed in the last step):
```
# Place the following repo definitions preferably in the end of the file since these packages
# shouldn't conflict with other repos.

# Selection of prebuilt AUR packages and more:
[m-more2]
SigLevel = Required
#Include = /etc/pacman.d/mirrorlist-m
Server = https://github.com/manuel-192/$repo/releases/download/$arch

# Packages created and published by Manuel:
[m-m]
SigLevel = Required
#Include = /etc/pacman.d/mirrorlist-m
Server = https://github.com/manuel-192/$repo/releases/download/$arch
```
## Add the maintainer's gpg key to your system
but only if you trust the maintainer and these packages!<br><br>
Run the following commands (unless you haven't already done so):
```
sudo pacman-key --recv-keys A1F1B5187D25904B
sudo pacman-key --lsign-key A1F1B5187D25904B
```
You should see token **manuel-192** inside the output of the these last commands.
If not, check that the added key was correct.

## Update your system
Update your repos and packages:
```
sudo pacman -Syyu
```
This command should also show the new package database files that you added.

## Install mirrorlist-m
```
sudo pacman -S mirrorlist-m
```
## Final touch
Remove the comment character (#) from the Include line(s) as noted above.<br>
Also, you *should* remove the **Server** line for the [m-m] and [m-more2].<br>
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
