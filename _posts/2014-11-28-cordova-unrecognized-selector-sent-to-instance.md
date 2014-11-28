---
layout: post
title: Cordova unrecognized selector sent to instance
category: cordova
tags: cordova, phonegap, plugin development
---

It has been a long time since last time I make a cordova plugin. Today, an annoying exception occured to me.

> \[XXX initWithWebView:\]: unrecognized selector sent to instance

After digging into the Cordova source code, I found that it was caused by the mis-configuration of class name in plugin.xml.

~~~
    <platform name="ios">
        <config-file target="config.xml" parent="/*">
            <feature name="Parse">
                <param name="ios-package" value="YOUR_OBJECTIVE_C_CLASS_NAME" onload="true" />
            </feature>
        </config-file>
    </platform>
~~~

