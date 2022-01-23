---
layout: post
permalink: resize-element-javascript
title: How to resize element with JavaScript
date: 2021-10-27T19:43:36.781Z
description: JavaScript has a native and easy-to-use API to listen for element
  resize. ResizeObserver is a modern approach to handle element resize.
tags:
  - js
---

JavaScript has a native and easy-to-use API to listen for element resize. `ResizeObserver` is a modern approach to handle element resize.

However, depending on your requirements and UI behavior you may want to consider using one of the following approaches for handling element resize:

1. [ResizeObserver](#resizeobserver-api)
2. [Resize EventListener](#resize-eventlistener)
3. [CSS media queries](#css-media-queries)

## ResizeObserver API

The most optimal way to listen for element resize is the [`ResizeObserver`](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver) API. Unlike the window `resize` event that always listens for the whole window viewport resizing, the `ResizeObserver` will only report changes to a target element if it has changed.

```javascript
const navbarResizeHandler = function (entries) {
  for (let entry of entries) {
    console.log(entry)
    // entry object properties:
    // borderBoxSize
    // contentBoxSize
    // contentRect
    // devicePixelContentBoxSize
    // target
  }
}

const navbarResizeObserver = new ResizeObserver(navbarResizeHandler)
const navbar = document.querySelector(".navbar")

navbarResizeObserver.observe(element)
```

Use this approach for single HTML elements that you wish to react to resize. It is more optimal than using a window `resize` event. E.g. you have a navigation bar element with some items in it, and you want to collapse it to the hamburger button if it doesn’t fit into the viewport anymore.

**ResizeObserver browser support**: <https://caniuse.com/resizeobserver>

## Resize EventListener

For a more generic approach, you can always use the window [`resize` event](https://developer.mozilla.org/en-US/docs/Web/API/Window/resize_event). This event will fire every time the document viewport (window) has been resized.

```javascript
function handleWindowResize (e) {
  // handle resizing
}

window.addEventListener("resize", handleWindowResize)
```

One of the problems with this approach is performance. However, there is a way to optimize the `resize` event so it’s not called every time the window resizes. You can implement a [throttle or debounce](https://redd.one/blog/debounce-vs-throttle).

A **throttle** means the function will be called once per N amount of time. Any additional function calls within the specified time interval are ignored.

A **debounce** means function will be called after N amount of time passes since its last call.

Use resize event for when you need to handle global changes to the viewport size and not just separate elements.

**Window resize event browser support**: <https://caniuse.com/mdn-api_window_resize_event>

## CSS media queries

A worthy mention would be CSS media queries. You might want to reconsider using JavaScript resize at all, quite possible that the desired result can be achieved with CSS.

```css
@media screen and (min-width: 600px) {
  /* styles for devices wider than 600px */
}
```

This approach is not as dynamic as a JavaScript one, but you don’t waste any resources running script. So instead of toggling a class name with JavaScript, you can specify a breakpoint and add CSS rules to match your case. On window resize these rules will be applied at a given breakpoint.

**CSS Media Queries browser support: <https://caniuse.com/css-mediaqueries>**