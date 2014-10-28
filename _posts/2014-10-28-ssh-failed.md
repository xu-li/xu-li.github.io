---
layout: post
title: SSH Failed
category: server
tags: server, ssh, centos
---

I tried to ssh to a new installed server last Friday using Putty, and it gave me the error, "Network error: Connection refused.". But it had been working when using DHCP!

What happened?

<!--more-->

## Firewall?

Checking the firewall settings, and it seems to be okay.

## sshd?

Checking the ports, and it seems to be okay.

## IP Address?

Yes, I typed it correctly.

## IP Address!

Finally, I found out that the IP Address has been used by another computer! It took me almost two hours to figure that out. WTF!
