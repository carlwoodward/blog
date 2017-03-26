---
title: Working on old projects
layout: post
---

With side projects like [Revisit](http://revisit.io), if you are like me then you tend to update them once or twice a year.

Every attempt leads to the painful realisation that the version of every dependency has moved on. First thought is to try to upgrade the project. 4 hours later when the project is very broken and no end is insight you realise that this process isn't working. Most likely, it's time to give up, but it's actually quite easy to Rsync the whole server into a Vagrant machine and have a working version with all dependencies.

First create vagrant machine with a linux distro that matches the server:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "66.33.33.61"
end
```

Then run `vagrant ssh` to login to the vagrant machine.

Run the following. NOTE: change /home/user/.ssh to your user ssh directory and change root@111.111.111.111 to your server.

```
sudo rsync -aAXvP --exclude={/boot/,/dev/,/etc/fstab,/etc/modprobe*,/etc/modules/,/lost+found/,/etc/mtab,/etc/network*,/etc/sysconfig/ip*,/etc/sysconfig/kernel,/etc/sysconfig/network*,/lib/modules/,/media/,/mnt/,/proc/,/run/,/sys/,/tmp/,/var/lib/lxcfs/,/var/lock/,/home/user/.ssh} root@111.111.111.111:/ /
```

This command comes from the [Digital Ocean Downgrade guide](https://www.digitalocean.com/community/tutorials/how-to-downgrade-digitalocean-droplets).

Reboot the machine and then you should be able to access the machine in the same way as the server. E.g. http://66.33.33.61. You may need to remove any SSL config but everything will match what is on the server (including the database). Be careful because this server will have production data.

If you've ever tried to share a directory with vagrant to do work with a server that watches the disk e.g. rails, nodejs, elixir, then you have probably run into issues with changes not being picked up and forcing the server to reload. A fix for this is to use sshfs and mount the directory from inside vagrant. To do this on a mac first [install Fuse](http://osxfuse.github.io/).

Run `vagrant ssh-config` to get the port that vagrant ssh is running on. Also 

```
mkdir TEMP_LOCAL_DIRECTORY
sshfs -p PORT vagrant@127.0.0.1:DIRECTORY_ON_SERVER TEMP_LOCAL_DIRECTORY
```

From here you can ssh onto the vagrant instance and run your app in development, make changes in the mounted directory, and deploy changes easily once finished.

For bonus points take a backup on the vagrant instance so you don't have to go through is again:

```
vagrant halt
vagrant package
```
