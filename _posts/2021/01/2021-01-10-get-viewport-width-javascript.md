---
layout: post
permalink: viewport-size-with-javascript
title: A complete guide to get viewport, device and document sizes with JavaScript
date: 2021-01-15T07:21:23.793Z
description: A complete guide explaining the difference between device, viewport
  and document, as well as providing ways to get the sizes (width and height)
tags: [javascript]
---

JavaScript provides a native API to get the width and height of a viewport. But it's important to understand the difference between what sizes you are getting as it may cause you some trouble.

When making calculations you have to distinguish between **viewport**, **device**, and **document**. Because at times the values of all three may be the same. However they may sound and look as if they are the same, but really these are three different concepts.

## Viewport size

In web development terms the [viewport](https://www.w3.org/TR/2011/REC-CSS2-20110607/visuren.html#viewport) is treated the same as the browser window, **including the rendered scrollbar** if any. 

**MDN** distinct two types of viewports:

* [Layout viewport](https://developer.mozilla.org/en-US/docs/Glossary/layout_viewport) - the area which is available to be seen;
* [Visual viewport](https://developer.mozilla.org/en-US/docs/Glossary/visual_viewport) - the portion of the viewport that is currently visible (e.g. zoomed area on a mobile device).

When we're talking about the viewport for the most part we're talking about the Layout viewport. There are 2 ways to get the width and height of the viewport (Layout viewport):

### 1. innerWidth and innerHeight properties

The [`innerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerWidth) property returns the interior width of the window in pixels (including the width of the scroll bar, if one is present).

```javascript
const viewportWidth = window.innerWidth
```

The [`innerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight) property returns the interior height of the window in pixels (including the height of the scroll bar, if one is present).

```javascript
const viewportHeight = window.innerHeight
```

Both properties return the integer value and are read-only.

**Browser Support:** [innerWidth](https://caniuse.com/?search=innerWidth) and [innerHeight](https://caniuse.com/?search=innerHeight) supported by all browsers.

### 2. outerWidth and outerHeight properties

The [`outerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerWidth) read-only property returns the width of the outside of the browser window. It represents the width of the whole browser window including sidebar (if expanded), window chrome and window resizing borders/handles.

```javascript
const browserWidth = window.outerWidth
```

The [`outerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerHeight) read-only property returns the height in pixels of the whole browser window, including any sidebar, window chrome, and window-resizing borders/handles.

```javascript
const browserHeight = window.outerHeight
```

Both properties return the integer value and are read-only.

**Browser Support:** [outerWidth](https://caniuse.com/?search=outerWidth) and [outerHeight](https://caniuse.com/?search=outerHeight) supported by all browsers.

## Device size

The device size is often referred to as a screen or display size. This is the size of an actual area of the device where users see the content. Unlike viewport or document size the values of the screen (display) remain unaltered.

To get the size of the screen the [`window.screen`](https://developer.mozilla.org/en-US/docs/Web/API/Window/screen) property can be used. It is a part of the [Screen API](https://developer.mozilla.org/en-US/docs/Web/API/Screen). The `screen` property returns an object that contains data about the current screen.

Some of the properties of the `screen` object can be utilized to get the size of the screen.

`screen.width` property returns a screen width in pixels. The returned value is an integer and read-only.

```javascript
const screenWidth = window.screen.width
```

`screen.height` property returns a screen height in pixels. The returned value is an integer and read-only.

```javascript
const screenHeight = window.screen.height
```

**Browser support**: [Screen API](https://caniuse.com/mdn-api_screen) supported in all browsers.

## Document size

The following ways will get the size of the document. Now the difference from the viewport is that the **document can be larger than the viewport** itself. Also, other things need to be considered. But let's move step by step.

To get the size of the document you need to get the `html` element that represents the document. The `document.documentElement` property returns the root element of the current document, that is `html`.

### 1. clientWidth and clientSize properties

While the [`clientWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth) property returns the inner width of an element in pixels. Initially, it includes paddings but excludes borders, margins, and scrollbars. But for `html` element it's a [special case](https://www.w3.org/TR/2016/WD-cssom-view-1-20160317/#dom-element-clientwidth) and the **viewport width** is returned (in pixels), **excluding scrollbar width**.

```javascript
const documentWidth = document.documentElement.clientWidth
```

The [`clientHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight) property returns the inner height of an element. Just like with the `clientWidth`, the `clientHeight` is a [special case](https://www.w3.org/TR/2016/WD-cssom-view-1-20160317/#dom-element-clientheight) when used on the `html` element. And it returns the **viewport height** (in pixels), **excluding scrollbar height**.

```javascript
const documentHeight = document.documentElement.clientHeight
```

When using these properties the scrollbar width and height are excluded - this is another thing to consider I mentioned before.

**Note: even if the `html` element has the CSS width or height rules applied, the clientWidth and clientHeight properties will always return viewport width and height (without scrollbars).** 

**Browser Support:** [clientWidth](https://caniuse.com/?search=clientWidth) and [clientHeight](https://caniuse.com/?search=clientHeight) supported by all browsers.

### 2. offsetWidth and offsetHeight properties

The [`HTMLElement.offsetWidth`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetWidth) property can be used on an `html` element to determine the width of the document. **Note**: that the document width can be larger than the viewport width.

The `HTMLElement.offsetWidth` read-only property returns the integer value of the width of an element. `offsetWidth` includes any borders, padding, and vertical scrollbars (if rendered).

```javascript
const documentWidth = document.documentElement.offsetWidth
```

The [`HTMLElement.offsetHeight`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight) property can be used on an `html` element to determine the height of the document. **Note**: that the document height can be larger than the viewport height.

The `HTMLElement.offsetHeight` read-only property returns the integer value of the height of an element. `offsetHeight` includes any borders, padding, and horizontal scrollbars (if rendered).

```javascript
const documentHeight = document.documentElement.offsetHeight
```

**Browser Support:** [offsetWidth](https://caniuse.com/mdn-api_htmlelement_offsetwidth) and [offsetHeight](https://caniuse.com/mdn-api_htmlelement_offsetheight) supported by all browsers.

### 3. scrollWidth and scrollHeight properties

The [`scrollWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollWidth) property returns the width of an element, including the part that is not visible on the screen due to overflow. This is a read-only integer value that includes the element's padding, but not its border, margin, or vertical scrollbar (if present).

```javascript
const documentWidth = document.documentElement.scrollWidth
```

The [`scrollHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight) property returns the height of an element, including the part that is not visible on the screen due to overflow. This is a read-only integer value that includes the element's padding, but not its border, margin, or horizontal scrollbar (if present).

```javascript
const documentHeight = document.documentElement.scrollHeight
```

**Browser Support:** [scrollWidth](https://caniuse.com/mdn-api_element_scrollwidth) and [scrollHeight](https://caniuse.com/mdn-api_element_scrollheight) supported by all browsers.

## Final thoughts

To help you understand and remember the difference think of it this way, you have a laptop (**device**) on which you open the browser (**viewport**) to view the web page (**document**).

Device size is always fixed, while viewport and document can change in size.