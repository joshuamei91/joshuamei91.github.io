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

- [Access restricted remote server from local machine through port forwarding](https://www.howtogeek.com/168145/how-to-use-ssh-tunneling/)
  ``` bash
  # this tells the ssh server to forward traffic from local port to restricted remote server 
  ssh -L local_port:restricted_remote_server:remote_port username@accessible_ssh_server
  
  # if the restricted server app (eg. on port 1234) is running on the same ssh server
  ssh -L local_port:localhost:1234 username@accessible_ssh_server
  ```

## Tidbits

### Package management
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

### User/Permissions management
- [Create user](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/): `useradd -m -u <uid> -g <group> <username>` (`-m`: create home dir)
  > To login after creating user, change user password (below)
- Change own password: `passwd`, change someone else's password: `passwd <username>`
- Check user database: `cat /etc/passwd`
- [Create user group](https://www.geeksforgeeks.org/groupadd-command-in-linux-with-examples/): `groupadd <groupname>`
- [Change file permissions](https://kb.iu.edu/d/abdb): eg. `chmod a+rwx myfile`
  | Access class| Operator   | Access Type | 
  | ----------- | -----------| ----------- |
  | u (user)    | + (add)    | r (read)    |
  | g (group)   | - (remove) | w (write)   |
  | o (other)   | = (exact)  | x (execute) |
  | a (all)
- [Change file owner](https://linuxize.com/post/linux-chown-command/): eg. `chown <username> myfile` or `chown -R <username> DIRECTORY`

### Network
- [List open ports](https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/): `netstat -tulpn | grep LISTEN`
  
### SFTP ([ref](https://docs.oracle.com/cd/E36784_01/html/E36830/remotehowtoaccess-15.html))
- Copy file from remote directory to local directory: `get myfile`
- Copy file from local directory to remote directory: `put myfile`
- Delete file from remote directory: `delete myfile`

### Others
- Add executable to path: add executable binary or create symlinks in `/usr/local/bin`
- Get detailed info about files: `ls -l` or `ll` (alias for `ls -l`)

## Concepts

- [SELinux](https://www.redhat.com/en/topics/linux/what-is-selinux)