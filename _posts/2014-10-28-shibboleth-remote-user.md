---
layout: post
title: REMOTE_USER is empty when using Shibboleth
category: server
tags: server, shibboleth, apache, REMOTE_USER
---

I have installed shibd and configured shibboleth SP correctly.But I couldn't get ```$_SERVER['REMOTE_USER']``` using PHP.

For troubleshooting, you may try the following:

<!--more-->

1. What's inside the logs(native.log, shibd.log, shibd_warn.log)?
2. Have you already setup the REMOTE_USER in shibboleth2.xml?
3. Is the attribute available, and if that attribute has been set in attribute-map.xml?
4. What will you see after visiting /Shibboleth.sso/Session? Is the attribute in there?
5. Is the script under ```AuthType Shibboleth``` protection?

Finally, I found out that #5 is the reason why ```$_SERVER['REMOTE_USER']``` is empty!
