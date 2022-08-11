---
layout: post
permalink: custom-bullet-points-css
title: Create cool custom bullet points with CSS
description: To make your lists stand out and look even fancier you can introduce a custom bullet points with pure CSS.
tags: [css]
---

Lists are a great way to showcase structured data. To make them look even fancier you can introduce a custom bullet points with pure CSS.

There are quite a few ways to make [lists in HTML](https://www.w3schools.com/HTML/html_lists.asp). But in this article I'm going to focus mainly on unordered list, as they're more often requires appearance customization.

<style>
  .bullet-image {
    list-style-image: url('/images/misc/double-caret-right.png');
  }
  .bullet-image li::before,
  .bullet-marker li::before {
    display: none;
  }
  .bullet-emoji li:before {
    all: unset;
    content: '🔹';
  }
  .bullet-entity li:before {
    content: '✔';
    font-size: 15px;
    color: limegreen;
    line-height: 1.7;
    padding-right: 10px;
  }
  .bullet-bg li {position:relative}
  .bullet-bg li:before {
    content: '';
    position: absolute;
    left: 23px;
    top: 6px;
    width: 15px;
    height: 15px;
    background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='gold'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
  }
  .bullet-marker li::marker {
    content: '✅ ';
    font-size: 15px;
}
</style>

## Defaults

By default bullet points are displayed for unordered lists - `ul` tag. Usually they are in a circle shape. But you can set some predefined values to change their appearance.

Use a `list-style-type` property with one of the following values:

* circle
* disc (this is often a default appearance)
* disclosure-closed
* disclosure-open
* square

All of the values are self explanatory. You can always make a quick experiment inside the [Dev Tools](/cool-chrome-dev-tools-tricks-you-might-not-know-about/).

  <figure>
    <img class="shadow" src="/images/misc/default-bullet-points-types.png" alt="Default bullet points types" loading="lazy">
    <figcaption>Default bullet points types in Chrome browser</figcaption>
  </figure>

## Images

You can also set the image to appear as the bullet point with the `list-style-image` property.

```css
ul {
  list-style-image: url('double-caret-right.png');
}
```
**Result:**
<ul class="bullet-image">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

However `list-style-type` and `list-style-image` has its own limitations. You cannot control the size or the color of the bullets.

## Pseudo element

To make an even more fancy appearance of the bullet points you can use pseudo-elements.

### before and after

The traditional way to do so is to declare a `before` pseudo-element on a `li` tag.

```css
ul li::before {
  content: '🔹';
}
```

**Result:**

<ul class="bullet-emoji">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

The best part is that now you can control different properties of the bullet point. Like content, size, color, position.

For content you can use emojies, special characters ([html entities](/special-characters-and-symbols-with-html-entities/), and fonts.

Since content is interpreted as text, you can set font related rules like `font-size`, `color`, `line-height` and etc.

```css
ul li::before {
  content: '✔';
  font-size: 15px;
  color: limegreen;
  line-height: 1.7;
  padding-right: 10px;
}
```

**Result:**

<ul class="bullet-entity">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

Another way to customize your bullet points is to set images as a background, this works well for SVG type images. You can even set an SVG image as an [encoded](/using-svg-background-image-with-css-code-only) piece of code, meaning no file needed.

The benefit of this approach is that unlike `list-style-image` property you can control image size and position.

```css
ul li {
  position: relative;
}

ul li:before {
  content: '';
  position: absolute;
  left: 23px;
  top: 6px;
  width: 15px;
  height: 15px;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='gold'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}
```

**Result:**

<ul class="bullet-bg">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

### marker

A modern and a semantic way to customize your bullet points is to use [`marker` pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/::marker). It selects a marker box of a list item, that way you have `before` and `after` pseudo-elements saved for later usage.

It acts the same way as `before` and `after` pseudo elements. You can set the `content` property for custom bullet type. And then use font related rules to set the appearance of the bullet, `color`, `font-size`, etc.

```css
ul li::marker {
  content: '✅ ';
  font-size: 15px;
}
```

**Result:**

<ul class="bullet-marker">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

For list styling it is recommended use the `marker` pseudo-element it is supported by [all modern browsers](https://caniuse.com/css-marker-pseudo).



