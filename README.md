# Instructions for using Manuel's repos

## Latest changes
- 2019-08-04: IMPORTANT: repos are now under construction due to Antergos shutdown.
  This means any repo can be changed to another place or even be totally removed.
  Please continue looking at this page for more info in the near future!
- 2019-07-29: IMPORTANT: changed SigLevel of each repo from **Required** to **PackageRequired**.<br>
  You MUST make the same change in your /etc/pacman.conf.<br>
  This was due to inadequate support from pacman for database signatures.

## Overview
Currently there are the following repos available:

Name | Purpose | Link | Status
---- | ------- | ---- | ------
m-more | Selection of AUR packages and more | [m-more](../../../m-more) | changing mirror
antergos-m | Packages created by Manuel | [antergos-m](../../../antergos-m) | changing name and mirror
antergos-maur | A selection of AUR packages | [antergos-maur](../../../antergos-maur) | removed
antergos-mup | Packages to update some Antergos packages | [antergos-mup](../../../antergos-mup) | removed

The following three steps
1. edit /etc/pacman.conf
2. install a gpg key
3. update system

show you how to start using the repos.

## Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions (note: removed obsolete repos):
```
# Selection of prebuilt AUR packages and more.
# Place this repo preferably in the end of the file since these packages
# shouldn't conflict with other repos.
[m-more]
#Include = /etc/pacman.d/manuel-mirrorlist
Server = https://github.com/manuel-192/$repo/releases/download/assets
SigLevel = PackageRequired

# Packages created and published by Manuel.
# Place this repo preferably in the end of the file since these packages
# shouldn't conflict with other repos.
[antergos-m]
#Include = /etc/pacman.d/manuel-mirrorlist
Server = https://github.com/manuel-192/$repo/releases/download/assets
SigLevel = PackageRequired
```
Note that you may also write a mirrorlist file with the following contents:
```
# contents of file /etc/pacman.d/manuel-mirrorlist:
Server = https://github.com/manuel-192/$repo/releases/download/assets
```
and uncomment the "#Include = ..." lines from the repo definitions above.

## Add the maintainer's gpg key to your system
but only if you trust the maintainer and these packages!<br><br>
Run the following commands (unless you haven't already done so):
```
sudo pacman-key --recv-keys A1F1B5187D25904B
sudo pacman-key --lsign-key A1F1B5187D25904B
```
You should see token **manuel-192** inside the output of the these last commands.
If not, check that the added key was correct.

That's it! The hard part is done, and now the new repos are available for your package manager.

## Update your system
Last but not least, update your repos and packages:
```
sudo pacman -Syyu
```
This command should show also the new package database files that you added.
## Troubleshooting
In case of any error, please check that you have copied the repo definitions exactly as they are above. And check that the installed gpg key was correct.<br>
You can see what gpg keys you have installed with:
```
gpg --list-keys --keyid-format LONG
```
You may write to https://forum.antergos.com about any issues with these repos.
<br><br>
<b>DISCLAIMER</b>: <u>use these packages at your own risk!</u> I have no way of
guaranteeing the safety of these packages.
I build and sign (using name <i>manuel-192</i>) them,
and transfer them here using the best safety practices I know of.
