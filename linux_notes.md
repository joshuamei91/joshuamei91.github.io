---
layout: page
title: Linux Notes
permalink: /linux-cheatcheet/
---

## Useful workflows
- Download package and its dependencies from Windows

``` bash
# Run in WSL
yumdownloader --assumeyes -destdir=/var/rpm_dir/mypackages --resolve <package_name>
scp /var/rpm_dir/mypackages user@ip:/home/offline/server
yum install /home/offline/server/*.rpm
```
- Mount USB

``` bash
lsblk # find out what the drive is called. look for something like /dev/sdb1
mkdir /media/usb # (optional) can use /mnt if nothing is mounted there
mount /dev/sdb1 /media/usb
unmount /media/usb
```
- Check network interface

``` bash
sudo nmcli
# if disconnected
sudo nmtui
sudo reboot
```

## Tidbits
- Check CentOS version: `rpm -q centos-release`
- Check package for dependencies: `rpm -qpR <package.rpm>`
- List repositories: `yum repolist` or `yum repolist enabled`
- Remove a package: `yum remove <package_name>`
- Remove installed packages from a specific repository: 

``` bash
# this will remove all installed packages, dependencies and the repository itself
yum remove $(yum list installed | grep <repo_name> | awk '{ print $1 }')
```
- Remove a single package: `rpm -e --nodeps PACKAGE`
  > Danger: Do not remove python as yum depends on it. This command can cause applications to crash or misbehave

- Install using rpm if there is no yum: `rpm -i <package.rpm>`
  > If yum is broken because python was removed, download the python package and install via rpm
  
- View variables like $releasever

``` bash
# CentOS 6 & 7
python -c 'import yum, json; yb = yum.YumBase(); print json.dumps(yb.conf.yumvar, indent=2)'
```