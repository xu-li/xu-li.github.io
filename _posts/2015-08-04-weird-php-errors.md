---
layout: post
title: Weird PHP errors
category: php
tags: php, centos, apc
---

After I deployed a new version onto our QA server, I was getting errors like _Cannot redeclare class_ and _Class XXX not found_ in a 3rd-party lib.

Weird, I haven't made any changes in those files.

After hours of investigation, I found out that it was APC on the server which caused this issue, and solved it by restarting apache.
