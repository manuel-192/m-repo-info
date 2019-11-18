# Instructions for using Manuel's repos

## Latest changes
- 2019-11-18: Manuel's repos can now be added with a script, see the <b>Overview</b> below.
- 2019-08-29: IMPORTANT: Renamed repo server addresses so that the "assets" word in the end is now "$arch".
- 2019-08-05: Repo [antergos-m] has moved to [m-m].
- 2019-08-04: Antergos users may find a new home at https://endeavouros.com. Many Antergos users have already moved there.
- 2019-08-04: IMPORTANT: repos are now under construction due to Antergos shutdown.
  This means any repo can be changed to another place or even be totally removed.
  Please continue looking at this page for more info in the near future!
- 2019-07-29: IMPORTANT: changed SigLevel of each repo from **Required** to **PackageRequired**.<br>
  You MUST make the same change in your /etc/pacman.conf.<br>
  This was due to inadequate support from pacman for database signatures.

## Overview
Currently there are the following repos available:

Name | Purpose | Link | Special remarks
---- | ------- | ---- | ---------------
m-more | Selection of AUR packages and more | [m-more](../../../m-more) | -
m-m | Packages created by Manuel | [m-m](../../../m-m) | -

The following three steps
1. edit /etc/pacman.conf
2. install a gpg key
3. update system

show you how to start using the repos.<br><br>
Note: you can now use a small script to add Manuel's repositories to your system:
<pre>
wget -q https://github.com/manuel-192/m-more/raw/master/PKGBUILDs/mirrorlist-m/install-mirrorlist
bash install-mirrorlist
</pre>

## Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions:
```
# Place the following repo definitions preferably in the end of the file since these packages
# shouldn't conflict with other repos.

# Selection of prebuilt AUR packages and more:
[m-more]
Server = https://github.com/manuel-192/$repo/releases/download/$arch

# Packages created and published by Manuel:
[m-m]
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
You may write to https://forum.endeavouros.com about any issues with these repos.
<br><br>
<b>DISCLAIMER</b>: <u>use these packages at your own risk!</u><br>I have no way of
guaranteeing the safety of these packages.
I build and sign (using name <i>manuel-192</i>) them,
and transfer them here using the best safety practices I know of.
