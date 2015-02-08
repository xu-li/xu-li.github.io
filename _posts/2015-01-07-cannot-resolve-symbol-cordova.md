---
layout: post
title: Cannot resolve symbol 'CordovaActivity'
category: cordova
tags: cordova, phonegap, android, android studio
---

After I imported a cordova project into Android Studio, symbols of cordova classes cannot be resolved.

<!--more-->

## Softwares:

* Android Studio: 1.0.2
* Ionic: 1.3.0-beta1

## Problem:

Somehow, android studio cannot figure out the library project.

## How to solve this:

1. ```ionic platform add android```
2. Open android studio, and choose _Import Non-Android Studio Project_
3. Select the root folder(usually _platform/android_)
4. Use Gradle Wrapper? _YES_
5. Change gradle plugin version from _0.10.+_ to _1.0.0_ in both _build.gradle_ files
6. Change _buildToolsVersion_ from _19.0.0_ to _19.1.0_ in both _build.gradle_ files
7. Remove the for loop in _dependencies_ section of _build.gradle_, then add ```compile project(':CordovaLib')```
8. Remove the for loop in _settings.gradle_, then add ```include ':CordovaLib'```
9. Resync the gradle, and it should work
