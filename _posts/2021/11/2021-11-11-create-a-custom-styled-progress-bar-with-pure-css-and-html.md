---
layout: post
permalink: progress-bar-css
title: Create a custom-styled progress bar with Pure CSS and HTML
date: 2021-11-11T12:29:41.016Z
description: A progress bar can be styled using pure CSS and a sprinkle of HTML
  for more appealing and cross-browser friendly view.
tags:
  - css
  - html
---

A progress bar is a nice way to showcase the completion state of something. The default HTML element looks inconsistent across different browsers. Fortunately, there’s a way to give a custom style for the progress bar element.

<style>
.container li p {margin: 0}
.container ol ol {margin: 0}
progress {display:inline-block;margin:0 0 20px}
.styled {-webkit-appearance:none}
.styled::-webkit-progress-bar {background-color: aliceblue}
.styled::-webkit-progress-value {background-color: coral}
.styled::-moz-progress-bar {background-color: coral}
.pseudo {
  position: relative;
}
.pseudo::before,
.pseudo::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
}
.pseudo::before {
  width: 100%;
  background: burlywood;
}
.pseudo::after {
  width: 75%;
  background: brown;
}
.progress-element {width: 200px}
.progress-element .progress-container {display: block}
.progress-container progress {opacity:0}
.progress-container {
  position: relative;
  display: inline-block;
  background: #eee;
  height: 20px;
  border-radius: 6px;
  overflow: hidden;
}
.progress-container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 75%;
  background: turquoise;
}
.progress-label {
  position: relative;
}
.progress-label::after {
  content: "75%";
  position: absolute;
  top:0;
  right: 0;
}
.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px}
.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
.image-grid figure{margin: 0 10px 10px;flex: 1 0 47%}
</style>

1. [Styling the progress](#styling-the-progress)

   1. [Accent color](#accent-color)
   2. [Non-standard styling](#non-standard-styling)
   3. [Pseudo-elements](#pseudo-elements)
2. [Cross-browser friendly solution](#cross-browser-friendly-solution)
3. [Animating a progress bar with CSS](#animating-a-progress-bar-with-css)
4. [Demo](#demo)

To display a progress bar a [`progress` tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress) is used, along with some attributes. The `max` attribute represents the maximum `value` of the progress bar. The `value` attribute represents the current value of the progress element.

```html
<progress value="75" max="100">75%</progress>
```

**Result:**

<progress value="75" max="100">75%</progress>

Default progress bar appearance across different browsers:

<div class="image-grid">
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/progress-bar-chrome.png" alt="Progress bar on Chrome">
    <noscript>
      <img class="shadow" src="/images/html-elements/progress-bar-chrome.png" alt="Progress bar on Chrome">
    </noscript>
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/progress-bar-edge.png" alt="Progress bar on Edge">
    <noscript>
      <img class="shadow" src="/images/html-elements/progress-bar-edge.png" alt="Progress bar on Edge">
    </noscript>
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/progress-bar-firefox.png" alt="Progress bar on FireFox">
    <noscript>
      <img class="shadow" src="/images/html-elements/progress-bar-firefox.png" alt="Progress bar on FireFox">
    </noscript>
    <figcaption>FireFox</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/progress-bar-safari.png" alt="Progress bar on Safari">
    <noscript>
      <img class="shadow" src="/images/html-elements/progress-bar-safari.png" alt="Progress bar on Safari">
    </noscript>
    <figcaption>Safari</figcaption>
  </figure>
</div>

If no `value` attribute is specified the progress element will show up with the loading animation:

```html
<progress></progress>
```

**Result:**

<progress></progress>

## Styling the progress

### Accent color

You can set the color of the current progress by defining the [`accent-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/accent-color) property.

```css
progress {
  accent-color: coral;
}
```

**Result:**

<progress style="accent-color:coral" value="75" max="100">75%</progress>

The `accent-color` property is a new thing and can be used to [style form elements](https://www.smashingmagazine.com/2021/09/simplifying-form-styles-accent-color/) as well. However, at the time this article is written, it is lacking full [browser support](https://caniuse.com/mdn-css_properties_accent-color). So you shouldn’t rely on it much right now, but worth knowing about this property, to use it in the future.

### Non-standard styling

Currently, there are some non-standard pseudo-elements available to style the `progress` tag parts. It is recommended not to use these selectors in production as the behavior is not consistent and may change in the future. But it’s worth knowing that these kinds of properties exist.

For these properties to work, first thing you’ll need to set the `appearance` of the progress element to `none`.

```css
progress {
  -webkit-appearance: none;
}
```

The first one is the [`::-webkit-progress-bar`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-progress-bar) pseudo-element. It represents the entire progress element. You can use it to set the background color. Will only work in browsers based on Blink or WebKit.

```css
::-webkit-progress-bar {
  background-color: aliceblue;
}
```

To style the actual value use the [`::-webkit-progress-value`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-progress-value) selector for Blink or WebKit based browsers and [`::-moz-progress-bar`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-progress-bar) for Firefox browser.

```css
::-webkit-progress-value {
  background-color: coral;
}

::-moz-progress-bar {
  background-color: coral;
}
```

**Result:**

<progress class="styled" value="75" max="100">75%</progress>

### Pseudo-elements

The progress element can also be styled with pseudo-elements, `::before` representing the background and `::after` representing the progress bar. However, pseudo-elements for the progress element are not supported by all browsers (Safari and Firefox don’t have support).

```css
progress {
  position: relative;
}

progress::before,
progress::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
}

progress::before {
  width: 100%;
  background: burlywood;
}

progress::after {
  width: 75%;
  background: brown;
}
```

**Result:**

<progress class="pseudo" value="75" max="100">75%</progress>

## Cross-browser friendly solution

To make the progress bar look and behave the same way in all browsers you’ll need to wrap it in a `div`. The `div` will replace the appearance of the progress bar.

```html
<div class="progress-container">
  <progress value="75" max="100">75%</progress>
</div>
```

First, you need to hide the progress element by setting its `opacity` to 0.

```css
progress {
  opacity: 0;
}
```

Then, add the desired styles to the `div`. If you want it to take up the same width as the progress element, set the display property to `inline-block`. Otherwise, the `div` will span 100% of the container, and its width should be controlled via `width` property.

```css
.progress-container {
  position: relative;
  display: inline-block;
  background: #eee;
  height: 20px;
  border-radius: 6px;
  overflow: hidden;
}
```

To display the progress value we’ll use the `::before` pseudo-element.

```css
.progress-container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 75%;
  background: turquoise;
}
```

**Result:**

<div class="progress-container">
  <progress value="75" max="100">75%</progress>
</div>

For the progress bar to be more descriptive let’s add a label and a numeric value. The `p` tag will represent the label, and its pseudo-element will display a numeric value.

```html
<div class="progress-element">
  <p class="progress-label">HTML</p>
  <div class="progress-container">
    <progress max="100" value="75">75%</progress>
  </div>
</div>
```

```css
.progress-label {
  position: relative;
}

.progress-label::after {
  content: "75%";
  position: absolute;
  top:0;
  right: 0;
}
```

**Result:**

<div class="progress-element">
  <p class="progress-label">HTML</p>
  <div class="progress-container">
    <progress max="100" value="75">75%</progress>
  </div>
</div>

## Animating a progress bar with CSS

If you want to animate progress value on page load, you can add a CSS animation to the pseudo-element.

First, let’s create a `keyframe` for progress value animation. Since we will animate the width of the pseudo-element, the value will represent the progress percentage:

```css
@keyframes progress-animation {
  to {
    width: 75%;
  }
}
```

Then we need to set the pseudo-element width to 0 and then specify the `animation` property.

```css
.progress-container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  background: turquoise;
  width: 0;
  animation: progress-animation .7s ease-in forwards;
}
```

Finally to complete the animation we need to animate the percentage value stored in the pseudo-element. There’s a way to animate the numeric value using the [CSS counter](https://css-tricks.com/animating-number-counters/).

**NOTE: Animating numeric values using CSS is [not supported](https://caniuse.com/mdn-css_selectors_after_animation_and_transition_support) by all browsers! So as a workaround you can set pseudo-elements' content value to a progress value (e.g. "75%") without animation.**

```css
@property --num {
  syntax: '<integer>';
  initial-value: 0;
  inherits: false;
}

.progress-label::after {
  counter-reset: num var(--num);
  content: counter(num) '%';
  position: absolute;
  top:0;
  right: 0;
  animation: progress-text 1s ease-in forwards;
}

@keyframes progress-text {
  to {
    --num: 75;
  }
}
```

## Demo

The end result can be viewed on CodePen:

<p class="codepen" data-height="370" data-default-tab="result" data-slug-hash="KKvBmYd" data-user="tippingpointdev" style="height: 370px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/KKvBmYd">
  Styled progress bar</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>