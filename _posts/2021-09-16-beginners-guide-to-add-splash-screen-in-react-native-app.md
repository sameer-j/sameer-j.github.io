---
layout: post
author: Sameer
title: Beginners guide to add splash screen in react native app
date: 2021-09-16T14:15:41.128Z
thumbnail-img: /assets/img/posts/react_native_logo.png
category: react native
summary: Simplest steps to add splash screen on a react native app
keywords: reactnative splashscreen
thumbnail: /assets/img/posts/react_native_logo.png
permalink: /blog/react-native-splash-screen/
---
In this tutorial I will show how to add splash screen in a react native app, for android specifically. Last tested with react native v0.65.

## Splash Screen

In simplest words, splash screen is like a starting screen of your mobile app that shows up just before the first screen of your app shows up. 

***\[Splash screen GIF here]***

This is a common thing in apps, be it native apps in android or ios and hybrid apps using React Native, Cordova etc. It acts as a dummy screen to show your user while it takes time to startup. You can choose to add a nice animation for it. 

In this tutorial I will show how to add splash screen in a react native app, for android specifically.

## Setting splash screen on Android

First we need to setup splash screen on native android side. Splash screen on Android side leverages setting a theme with splash image. Theme is loaded before the MainActivity in android. 

1. First, get a splash screen image for your app and copy it in the following location\
   `"android/app/src/main/res/drawable/splash.png"`. Create "drawable" folder if it doesn't exist.
2. reate a color for the background in "`android/app/src/main/res/values/colors.xml"` file with following code:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <color name="primary">#000</color>
   </resources>
   ```
3. Create a **background_splash.xml** file in drawable folder with the following code:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <layer-list xmlns:android="http://schemas.android.com/apk/res/android">

       <item
           android:drawable="@color/primary"/>
       <item
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:drawable="@drawable/splash"
           android:gravity="center" />
   </layer-list>

   ```
4. Create a new "SplashTheme" style in "`android/app/src/main/res/values/styles.xml"` :

   ```xml
   ....
   <style name="SplashTheme" parent="Theme.AppCompat.Light.NoActionBar">
       <item name="android:background">@drawable/background_splash</item>
       <item name="android:statusBarColor">@color/primary</item>
       <item name="android:textColor">#000</item>
   </style>
   ....
   ```
5.

#### Reference

* [Implementing the Perfect Splash Screen in Android](https://medium.com/geekculture/implementing-the-perfect-splash-screen-in-android-295de045a8dc)

See that white flash between your splash screen and home page? Thats the time ...

## Handling splash screen flash for react native apps



## Troubleshooting common issues

* jest tests failing with "Cannot use import statement outside a module" or "Cannot read property 'hide' of undefined"

  * as "react-native-splash-screen" is a native plugin, its not available during jest test run. You need to mock the library in your test file.

    ```javascript
    jest.mock('react-native-splash-screen', () => ({
      hide: jest.fn(),
      show: jest.fn(),
    }));
    ```

    \
    Reference: <https://github.com/crazycodeboy/react-native-splash-screen/issues/166#issuecomment-362774112>

Code for this tutorial is available at <https://github.com/sameer-j/RNSplashScreenDemo>

References: