# Instructions for using Manuel's repos

## Important changes
Date | Description
:--- | :---
2023-Feb-11 | IMPORTANT: repos were changed, manual intervention required!<br>Repo `m-more2` needs a special mirror definition as the first one.<br>See the contents of file `/etc/pacman.conf` below (Step: Final touch).
2021-Sep-09 | IMPORTANT: Please update package `mirrorlist-m` because of repo location change.<br>Otherwise file `/etc/pacman.d/mirrorlist-m` must be changed manually.<br>This change was caused by pacman update to version 6.0.1 that fixed the broken 6.0.0.
2021-Jun-02 | IMPORTANT: Manual intervention is required because repo locations had to be changed<br>after pacman v6. See **New repo settings at 2021-Jun-02** below.
2020-Apr-20 | Moved AUR packages from repo [m-more2] to a new repo [m-aur].
2020-Apr-20 | Moved package source of mirrorlist-m to repo [m-m] from repo [m-more2].
2020Apr-15 | In your file **/etc/pacman.conf** you **must** change repo **[m-more]** to **[m-more2]** due to<br>the repo move operation today.
2020-Mar-28 | Repo addresses have been changed. Please install the **mirrorlist-m** package as instructed below!

## Overview
Currently the following repos are available:

Name | Purpose | Link | Additinal remarks
:---- | :------- | :---- | :---------------
m-m | Packages created by Manuel | [m-m](../../../m-m) | -
m-more2 | Additional open source packages | [m-more2](../../../m-more2) | Special (e.g. large) packages.
m-aur | Selection of AUR packages | [m-aur](../../../m-aur) | -

## Steps to set up
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
# Place the following repo definitions preferably in the end of the file
# since these packages shouldn't conflict with other repos.

[m-m]
SigLevel = Required
Server = https://raw.githubusercontent.com/manuel-192/$repo/master/repo
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

Change Manuel's repos in file `/etc/pacman.conf` to look like this (2023-Feb-11):

```
[m-m]
SigLevel = Required
Include = /etc/pacman.d/mirrorlist-m

[m-more2]
SigLevel = Required
Server = https://github.com/manuel-192/$repo/releases/download/$arch
Include = /etc/pacman.d/mirrorlist-m

[m-aur]
SigLevel = Required
Include = /etc/pacman.d/mirrorlist-m
```
(If you don't want to use all of the Manuel's repos, simply comment those out, or remove their lines.)

Then update again:
```
sudo pacman -Syyu
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
I build and sign (using name <i>manuel-192</i> or <i>manuel</i>) them,
and transfer them here using the best safety practices I know of.
