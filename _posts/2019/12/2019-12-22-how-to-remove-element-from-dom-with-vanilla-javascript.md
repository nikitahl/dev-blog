---
layout: post
title: How to remove HTML element from DOM with vanilla JavaScript in 4 ways
description: An overview of 4 ways how to remove HTML element from DOM with vanilla JavaScript. Plus jsperf performance tests.
tags: [javascript]
comments: true
---

Vanilla JavaScript allows you to remove elements from DOM in several ways. In this article, I'll show you how it can be achieved and also provide performance tests for each one.

1. [removeChild() method](#1-removechild-method)
2. [remove() method](#2-remove-method)
3. [innerHTML property](#3-innerhtml-property)
4. [outerHTML property](#4-outerhtml-property)
5. [Performance tests with jsperf](#performance-tests-with-jsperf)

## 1. removeChild() method

As the name states, this method will remove the child element from the selected element.

HTML:
```html
<div id="container">
  <div id="child-1"></div>
  <div id="child-2"></div>
</div>
```
JavaScript:
```javascript
const container = document.getElementById("container")
const childOne = document.getElementById("child-1")

container.removeChild(childOne)
```
If you're willing to remove all children, you can use the following pattern:

```javascript
while (container.firstChild) {
  container.removeChild(container.firstChild);
}
```

This approach is **fully cross-browser**, read full docs on [removeChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild){:target="blank"}.

## 2. remove() method

The `removeChild` method will remove the selected element from the DOM tree.

HTML:
```html
<div id="container">
  ...
</div>
```
JavaScript:
```javascript
const container = document.getElementById("container")

container.remove()
```
This method is **not supported by Internet Explorer** browser. Find out more about [remove method on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove){:target="blank"}.

## 3. innerHTML property

Unlike previous methods, this *property's* purpose isn't really to remove element. `innerHTML` property will get or set the HTML markup contained within the element.

But you can utilize this property to *"remove"* any elements within the container, by setting the value to an empty string.

HTML:
```html
<div id="container">
  <div id="child-1"></div>
  <div id="child-2"></div>
</div>
```
JavaScript:
```javascript
const container = document.getElementById("container")

container.innerHTML = ""
```

This property is **fully cross-browser**, read full docs on [innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML){:target="blank"}.

## 4. outerHTML property

Similar to `innerHTML` the `outerHTML` property allows you to get the given element as a serialized string with all the descendant elements.

Again you can utilize this property to set the value to an empty string.

HTML:
```html
<div id="container">
  <div id="child-1"></div>
  <div id="child-2"></div>
</div>
```
JavaScript:
```javascript
const container = document.getElementById("container")

container.outerHTML = ""
```

This property is **fully cross-browser**, read full docs on [outerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/outerHTML){:target="blank"}.

## Performance tests with jsperf

I've created a [test on jsperf.com](https://jsperf.com/remove-elements-from-dom) to compare the performance of each of those methods.

For each test case, a container will be populated with a defined HTML code that will contain ten `p` elements. All `p` elements from that HTML code will be removed using one of the four ways described above.

Tested in:
* **Chrome 78.0.3904 / Mac OS X 10.15.1**
* **Firefox 71.0.0 / Mac OS X 10.15.0**
* **Safari 13.0.3 / Mac OS X 10.15.1**

All three browsers show that <u>for this test case</u> the `innerHTML` is the fastest way to remove multiple HTML elements from DOM.

<style>
figure {
  margin: 0 0 30px
}
</style>

<figure>
  <img class="shadow lozad" data-src="/images/remove-elements-from-dom/remove-elements-from-dom-chrome-test.png" alt="Remove elements from DOM Chrome browser test results">
  <noscript>
    <img class="shadow" src="/images/remove-elements-from-dom/remove-elements-from-dom-chrome-test.png" alt="Remove elements from DOM Chrome browser test results">
  </noscript>
  <figcaption>Results for Chrome</figcaption>
</figure>

<figure>
  <img class="shadow lozad" data-src="/images/remove-elements-from-dom/remove-elements-from-dom-firefox-test.png" alt="Remove elements from DOM Firefox browser test results">
  <noscript>
    <img class="shadow" src="/images/remove-elements-from-dom/remove-elements-from-dom-firefox-test.png" alt="Remove elements from DOM Firefox browser test results">
  </noscript>
  <figcaption>Results for Firefox</figcaption>
</figure>

<figure>
  <img class="shadow lozad" data-src="/images/remove-elements-from-dom/remove-elements-from-dom-safari-test.png" alt="Remove elements from DOM Safari browser test results">
  <noscript>
    <img class="shadow" src="/images/remove-elements-from-dom/remove-elements-from-dom-safari-test.png" alt="Remove elements from DOM Safari browser test results">
  </noscript>
  <figcaption>Results for Safari</figcaption>
</figure>