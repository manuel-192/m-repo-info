# Instructions to set up the all Manuel's repos
Currently there are three repos available:

Name | Purpose
---- | -------
antergos-m | Packages created by Manuel
antergos-maur | A selection of AUR packages
antergos-mup | Packages to update some Antergos packages

The following instructions show how to get started with the repos.

## Edit /etc/pacman.conf
Add all (or a selection) of the following repo definitions:
```
# Prebuilt and up to date AUR packages for Antergos.
# Place this before the [antergos] repo definition since these packages are meant to replace
# matching packages of the Antergos repo.
[antergos-mup]
Server = https://github.com/manuel-192/antergos-mup/raw/master
SigLevel = Required


# Packages created and published by Manuel.
# Place this repo preferably in the end of the file since these packages shouldn't conflict with other repos.
[antergos-m]
Server = https://github.com/manuel-192/antergos-m/raw/master
SigLevel = Required


# Selection of prebuilt packages from AUR.
# Place this repo preferably in the end of the file since these packages shouldn't conflict with other repos.
[antergos-maur]
Server = https://github.com/manuel-192/antergos-maur/raw/master
SigLevel = Required
```
## Add the maintainer's gpg key to your system (but only if you trust these packages!)
Run the following commands (unless you haven't already done so):
```
sudo pacman-key --recv-keys A1F1B5187D25904B
sudo pacman-key --lsign-key A1F1B5187D25904B
```
That's it! Now the new packages are available for you. Use pacman or similar tools to manage them.
## Last but not least
Update your repos system system:
```
sudo pacman -Syyu
```
This command should show also the new package database files (that you added) including the corresponding \<database\>.sig file.
