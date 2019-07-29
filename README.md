# Instructions for using Manuel's repos

## Latest changes
- 2019-07-29: IMPORTANT: changed SigLevel of each repo from **Required** to **PackageRequired**.<br>
  You MUST make the same change in your /etc/pacman.conf.<br>
  This was due to inadequate support from pacman for database signatures.

## Overview
Currently there are the following repos available:

Name | Purpose | Link
---- | ------- | ----
antergos-m | Packages created by Manuel | [antergos-m](../../../antergos-m)
antergos-maur | A selection of AUR packages | [antergos-maur](../../../antergos-maur)
antergos-mup | Packages to update some Antergos packages | [antergos-mup](../../../antergos-mup)
m-more | Selection of the above and more | [m-more](../../../m-more)

The following three steps
1. edit /etc/pacman.conf
1. install a gpg key
1. update system

show how to start using the repos.

## Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions:
```
# Prebuilt and up to date AUR packages for Antergos.
# Place this before the [antergos] repo definition since these packages are meant to replace
# matching packages of the Antergos repo.
[antergos-mup]
Server = https://github.com/manuel-192/antergos-mup/raw/master
SigLevel = PackageRequired

# Packages created and published by Manuel.
# Place this repo preferably in the end of the file since these packages
# shouldn't conflict with other repos.
[antergos-m]
Server = https://github.com/manuel-192/antergos-m/raw/master
SigLevel = PackageRequired

# Selection of prebuilt packages from AUR.
# Place this repo preferably in the end of the file since these packages
# shouldn't conflict with other repos.
[antergos-maur]
Server = https://github.com/manuel-192/antergos-maur/raw/master
SigLevel = PackageRequired

# m-more contains a selection of the above and some more packages.
[m-more]
Server = https://github.com/manuel-192/m-more/releases/download/mirror
SigLevel = PackageRequired
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

That's it! The hard part is done, and now the new repos are available for your package manager.

## Update your system
Last but not least, update your repos and packages:
```
sudo pacman -Syyu
```
This command should show also the new package database files (that you added) including the corresponding \<database\>.sig file.
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
