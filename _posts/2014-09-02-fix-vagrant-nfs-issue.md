---
layout: post
title: Fix a vagrant nfs issue
category: code
tags: vagrant, nfs
---

Today, when I tried to ```vagrant up``` a local box as what I usually do, it failed to mount nfs folder. After a lot of googling, I fixed that by simply restarting the network adapter.

<!--more-->

### Environment

- Host: Mac OS X 10.9.4
- Guest: Ubuntu 12.04 LTS
- vagrant 1.6.3
- virtualbox 4.3.8
- NFS enabled
- Private network

### Error

~~~
==> default: Mounting NFS shared folders...
The following SSH command responded with a non-zero exit status.
Vagrant assumes that this means the command failed!

mount -o 'vers=3,udp' 192.168.50.1:'/Users/xuli/Projs/PHP/test' /vagrant

Stdout from the command:



Stderr from the command:

stdin: is not a tty
mount.nfs: mount to NFS server '192.168.50.1:/Users/xuli/Projs/PHP/test' failed: timed out, giving up
~~~

### Solution

~~~ bash
# vboxnetX is the name of Host-only Adapter.
# You can find that in VirtualBox(Settings -> Network -> Adapter 2).
sudo ifconfig vboxnetX down
sudo ifconfig vboxnetX up
~~~

### Helpful resources

- [https://github.com/mitchellh/vagrant/issues/1093](https://github.com/mitchellh/vagrant/issues/1093)
- [https://github.com/mitchellh/vagrant/issues/1744](https://github.com/mitchellh/vagrant/issues/1744)
- [https://github.com/mitchellh/vagrant/issues/1941](https://github.com/mitchellh/vagrant/issues/1941)
