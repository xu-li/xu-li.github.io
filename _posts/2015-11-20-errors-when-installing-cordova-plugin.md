---
layout: post
title: A few errors occured when installing a cordova plugin
category: cordova
tags: cordova, corodva plugin
---

### TypeError: Object.keys called on non-object

<!--more-->

~~~
Saving plugin to package.json file
Error happened [TypeError: Object.keys called on non-object]
TypeError: Object.keys called on non-object
    at Function.keys (native)
    at Object.getPluginFromFetchJsonByLocator (/usr/local/lib/node_modules/ionic/node_modules/ionic-app-lib/lib/state.js:734:26)
    at Object.savePlugin (/usr/local/lib/node_modules/ionic/node_modules/ionic-app-lib/lib/state.js:670:36)
    ...
~~~

This is due to the wrong format in package.json. You can find out which plugin is causing this issue by adding console.log(lookupPlugin); in the for loop in /usr/local/lib/node_modules/ionic/node_modules/ionic-app-lib/lib/state.js at line 730.

### The module "ConfigParser" has been factored into "cordova-common". Consider update your plugin hooks.

You can fix it by replacing
~~~
context.requireCordovaModule('cordova-lib/src/configparser/ConfigParser')
~~~
with
~~~
context.requireCordovaModule('cordova-common').ConfigParser
~~~.
