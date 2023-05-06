---
layout: post
permalink: 4-ways-to-get-the-width-and-height-of-an-element-with-vanilla-javascript
title: 4 Ways To Get the Width and Height of an Element with Vanilla JavaScript
date: 2020-10-12T07:42:38.868Z
description: A definitive guide explaining how to get the dimensions (width and
  height) of an HTML element with plain Vanilla JavaScript.
tags:
  - javascript
---
This guide will explain to you how to get the width and height of an HTML element with plain Vanilla JavaScript.

The contents of the article:

1. [The Box Model](#the-box-model);
2. [offsetHeight and offsetWidth properties](#1-offsetheight-and-offsetwidth-properties);
3. [clientHeight and clientWidth properties](#2-clientheight-and-clientwidth-properties);
4. [getBoundingClientRect() method](#3-getboundingclientrect-method);
5. [getComputedStyle() method](#4-getcomputedstyle-method).

## The Box Model

Before we move forward a small explanation about what is the Box Model and how it affects element dimensions (width and height).

You can think of an HTML element as a box. This box consists of several parts:

> Every box is composed of four parts (or areas), defined by their respective edges: the content edge, padding edge, border edge, and margin edge.
>
> [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

<figure>
  <img class="shadow" src="/images/misc/css-box-model.jpg" alt="CSS Box Model" loading="lazy">
  <figcaption>CSS Box Model</figcaption>
</figure>

Depending on what CSS `box-sizing` property is applied to the current element the element height and width can vary.

> The `box-sizing` CSS property sets how the total width and height of an element is calculated.
>
> [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)

By default, every element’s `box-sizing` property is set to the `content-box.` This means that if you set an element's width to `100px`, then the element's content box will be `100px` wide. And the width of any border or padding will be added to the final rendered width, making the element wider than `100px`.

<figure>
  <img class="shadow" src="/images/dev-tools/div-box-padding-border.jpg" alt="Content Box" loading="lazy">
  <figcaption>Content Box</figcaption>
</figure>

The `border-box` on the other hand, tells the browser to account for any `border` and `padding` in the values, you specify for an element's `width` and `height`. If you set an element's width to `100px`, that `100px` will include any `border` or `padding` you've added.

<figure>
  <img class="shadow" src="/images/dev-tools/div-box-paddin-border-box-sizing.jpg" alt="Border Box" loading="lazy">
  <figcaption>Border Box</figcaption>
</figure>

You should keep in mind what `border-box` property is set to an HTML element when getting its width and height, as it may produce some unexpected results.

Moving on to how to actually get the width and height of an element with Vanilla JavaScript.

You can use one of the following Vanilla JavaScript properties and methods depending on your needs. Each one of these approaches has its own unique trait and could be used in different situations.

## 1. offsetHeight and offsetWidth properties

[`offsetHeight`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight) and [`offsetWidth`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetWidth) properties will get the height and width of an element, including paddings and borders. The returned value is an integer and read-only.

```javascript
const element = document.querySelector('.element');

element.offsetWidth;
// integer value of element’s content width + horizontal paddings and borders (if any)

element.offsetHeight;
// integer value of element’s content height + vertical paddings and borders (if any)
```

## 2. clientHeight and clientWidth properties

[`clientHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight) and [`clientWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth) properties will get the height and width of an element, including paddings but excluding borders. The returned value is an integer and read-only.

```javascript
const element = document.querySelector('.element');

element.clientWidth;
// integer value of element’s content width + horizontal paddings (if any)

element.clientHeight;
// integer value of element’s content height + vertical paddings (if any)
```

**NOTE: These properties will round the value to an integer.**

## 3. getBoundingClientRect() method

The [`getBoundingClientRect()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect) method returns an object holding the size of an element and its position relative to the viewport. To get the width and height of the element you should use the corresponding property names.

The `width` and `height` properties of the `getBoundingClientRect()` method will return the value based on the CSS `box-sizing` property of the element. E.g. if the `box-sizing` is set to `border-box`, then the `width` and `height` will include paddings and borders.

```javascript
const element = document.querySelector('.element');

element.getBoundingClientRect().width;
// integer value of element’s width (the width is calculated based on box-sizing property value)

element.getBoundingClientRect().height;
// integer value of element’s height (the height is calculated based on box-sizing property value)
```

## 4. getComputedStyle() method

The global [`getComputedStyle()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle) method returns an object containing the values of all CSS properties of an element. Each CSS value is accessible through a corresponding property and is of a string type.

Just like the method above the `width` and `height` properties of the `getComputedStyle()` method will return the value based on the CSS `box-sizing` property of the element. E.g. if the `box-sizing` is set to `border-box`, then the `width` and `height` will include paddings and borders.

```javascript
const element = document.querySelector('.element');

window.getComputedStyle(element).width;
// string value of element’s content width with pixel units attached

window.getComputedStyle(element).height;
// string value of element’s content height with pixel units attached
```

To get the integer value just wrap it in a `parseInt()` method:

```javascript
parseInt(window.getComputedStyle(element).height); // integer value
```