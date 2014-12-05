---
layout: post
title: Simulator session timed out
category: cordova
tags: cordova, phonegap, iOS, simulator
---

One of my friends asked me for helping her with this issue when running simulator:

<!--more-->

~~~
Session could not be started: Error Domain=DTiPhoneSimulatorErrorDomain Code=2 "Simulator session timed out." UserInfo=0x7f8b62c0c660 {NSLocalizedDescription=Simulator session timed out.}
Error: /XXX/XXX/XXXXX/platforms/ios/cordova/run: Command failed with exit code 1
    at ChildProcess.whenDone (/usr/local/lib/node_modules/cordova/node_modules/cordova-lib/src/cordova/superspawn.js:135:23)
    at ChildProcess.emit (events.js:98:17)
    at maybeClose (child_process.js:756:16)
    at Process.ChildProcess._handle.onexit (child_process.js:823:5)
~~~

A quick google takes me to [here](http://forum.ionicframework.com/t/running-cordova-emulate-ios-problem/1165), and none of the solutions there works.

A few facts:

1. It is an ionic project
2. Simulator works in xcode
3. ```ionic emulate ios``` and ```ionic run ios``` both return that error
4. ```ionic platform add ios``` was run as root.

Solution:

1. Remove the platform. ```ionic platform rm ios```
2. Open a new terminal window(which will run as current user)
3. Add the platform ```ionic platform add ios```
4. Run the project.```ionic run ios```

Other possible issues:

1. When I try to run ```ionic platform add ios```, it fails when using a non-root user. I have to remove the npm_cache folder at ```~/.cordova/lib/```.

Happy hybriding!
