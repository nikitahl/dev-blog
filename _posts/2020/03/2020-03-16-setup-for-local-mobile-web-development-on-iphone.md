---
layout: post
title: Set up a local environment for mobile web development on iPhone/iPad
description: Connect iPhone/iPad to a MAC and set up a local environment for mobile web development
tags: [development, tips]
comments: true
---

Set up a local environment to develop and debug a web project for an iPhone/iPad device.

This will allow you to inspect elements, use browser console and other development tools that are available in the [Safari browser](https://developer.apple.com/safari/tools/){:target="blank"} right on your mobile device.

**NOTE: This manual will work only for Apple devices. This means that you have to have a MAC computer and an iPhone/iPad.**

1. [Setting up a mobile device (iPhone/iPad)](#1-setting-up-a-mobile-device-iphoneipad)
2. [Setting up a MAC](#2-setting-up-a-mac-iphoneipad)
3. [Entering Inspector](#3-entering-inspector)
4. [Tips](#4-tips)

<style>
.image-container {display: flex;justify-content: center;margin: 0 0 20px;flex-direction:column}
.image {width: 90%margin: 0}
.image-vert img {width:50%}
</style>

## 1. Setting up a mobile device (iPhone/iPad)

Before connecting a mobile device to a MAC, you'll need to enable the **Web Inspector**. This will allow you to use your MAC Safari Developer Tools on your mobile device.

On a mobile device go to:

**Settings > Safari > Advanced > Web Inspector**

and enable the Web Inspector switch.

<figure class="image-container image-vert">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/iphone-enable-inspect-element.jpg" alt="Enable inspect element on iPhone">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/iphone-enable-inspect-element.jpg" alt="Enable inspect element on iPhone">
  </noscript>
  <figcaption>Enable inspect element on iPhone</figcaption>
</figure>

## 2. Setting up a MAC (iPhone/iPad)

You'll need to enable Develop menu in order to access Dev tools if you haven't already.

Open up Safari browser go to **Preferences** and tick _Show Develop menu in menu bar_ checkbox.

<figure class="image-container">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/mac-enable-devtools.png" alt="Enable developer tools on a MAC">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/mac-enable-devtools.png" alt="Enable developer tools on a MAC">
  </noscript>
  <figcaption>Enable inspect element on iPhone</figcaption>
</figure>

## 3. Entering Inspector

Connect your device to a computer via cable.

**NOTE: you might need to click on trust this computer button if you haven't already**

Open the Safari browser on your device and go to a webpage. Now open a Safari browser on your computer and click on a Develop in a menu. Hover over _Develop_ in the menu and you'll see your device's name and a web page. Click on it and the inspector will open.

<figure class="image-container">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/mac-open-iphone-inspector.png" alt="Open web inspector on a MAC">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/mac-open-iphone-inspector.png" alt="Open web inspector on a MAC">
  </noscript>
  <figcaption>Open web inspector on a MAC</figcaption>
</figure>

At this point, you can use element inspector and other tools just like you do on a computer.

<figure class="image-container image-vert">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/iphone-safari-website.jpg" alt="iPhone web page on Safari">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/iphone-safari-website.jpg" alt="iPhone web page on Safari">
  </noscript>
  <figcaption>iPhone web page on Safari</figcaption>
</figure>

<figure class="image-container">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/mac-iphone-inspector.png" alt="MAC iPhone web inspector">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/mac-iphone-inspector.png" alt="MAC iPhone web inspector">
  </noscript>
  <figcaption>MAC iPhone web inspector</figcaption>
</figure>

## 4. Tips

A quick tip while debugging you might want to clear browser cache, to do that go to:

**Settings > Safari > Clear History and Website Data**

and click **Clear History and Data**.

<figure class="image-container image-vert">
  <img class="image shadow lozad" data-src="/images/connect-iphone-to-mac/iphone-clear-browser-cache.jpg" alt="iPhone clear browser cache">
  <noscript>
    <img class="shadow" src="/images/connect-iphone-to-mac/iphone-clear-browser-cache.jpg" alt="iPhone clear browser cache">
  </noscript>
  <figcaption>iPhone clear browser cache</figcaption>
</figure>