---
layout: post
permalink: toggle-switch-button-css
title: Toggle switch button with Pure CSS
date: 2023-06-28T20:14:02.112Z
description: A toggle switch button is a recognizable part of the User Interface. These days it is common beyond smartphones and widely used on the web.
tags: [css]
---

A toggle switch button is a recognizable part of the User Interface. These days it is common beyond smartphones and widely used on the web.

It's great way to let users know whether something can be enabled or disabled. E.g. toggle switch is a great control to enable the [dark mode](/dark-mode).

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 10px;flex:1 0 47%}
.switch-toggle-container{position:relative;display:inline-block}
.switch-toggle-input{opacity:0;position:absolute;z-index: -1}
.switch-toggle {
  position: relative;
  display: inline-block;
  margin: 0 0 10px;
  width: 50px;
  height: 30px;
  background: #ddd;
  border-radius: 50px;
  transition: background .2s ease-in-out;
  cursor: pointer;
}
.switch-toggle::after {
  content: '';
  position: absolute;
  top: 2px;
  left: 2px;
  width: 26px;
  height: 26px;
  background: #fff;
  border-radius: 50px;
  box-shadow: 0 0 3px 1px rgba(0,0,0,0.15);
  transition: left .2s ease-in-out, width .2s ease-in-out, transform .2s ease-in-out;
}
.switch-toggle--labels::after  {
  content: 'Off';
  display: inline-flex;
  justify-content: center;
  align-items: center;
  font-size: 11px;
  color: #444;
}
.switch-toggle-input:checked + .switch-toggle--labels::after {
  content: 'On';
}
.switch-toggle-input:checked + .switch-toggle {
  background: #30e16b;
}
.switch-toggle-container:active .switch-toggle-input:not([disabled]) + .switch-toggle::after {
  width: 34px;
}
.switch-toggle-input:checked + .switch-toggle::after {
  left: calc(100% - 2px);
	transform: translateX(-100%);
}
.switch-toggle-input:disabled + .switch-toggle {
  cursor: not-allowed;
  background: #eaeaea;
}
.switch-toggle-input:disabled + .switch-toggle::after {
  background: #f8f8f8;
}
.switch-toggle-input:focus + .switch-toggle,
.switch-toggle-container:active .switch-toggle-input:not([disabled]) + .switch-toggle {
  outline: 2px solid #5195fe;
  outline-offset: 2px;
}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/ios-toggle-switch.webp" alt="iOS toggle switch">
    <figcaption>iOS toggle switch</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/android-toggle-switch.webp" alt="Android toggle switch">
    <figcaption>Android toggle switch</figcaption>
  </figure>
</div>

In this article, I’ll show you how you can implement a toggle switch button with pure HTML and CSS. The following solution will create an iOS-like feel and will ensure the same appearance across browsers as well as easy-to-use inside forms.

## Markup

You can use any HTML element, but in this case, we're going to use the checkbox element for the toggle switch.

```html
<input class="switch-toggle" type="checkbox">
```

Using a checkbox over let's say `button`, `div`, or a `span`, gives you a few advantages:

1. You can use it in conjunction with a `label` element (improved accessibility)
2. You can use pure CSS to style it (states controlled via selectors)
3. You can easily get the value of the toggle control when working with [forms](/get-all-form-elements)

However in order to properly display the toggle switch and make it more accessible, we'll need to specify additional HTML.

Let's wrap the checkbox inside the `label` tag. It will serve as a click area and the `span` will represent the track and thumb of a switch.

```html
<label class="switch-toggle-container">
  <input class="switch-toggle-input" type="checkbox">
  <span class="switch-toggle"></span>
</label>
```

## Styles

First, we'll need to hide the checkbox by making it transparent and outside of [document flow](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow){:targe="_blank"}.

By hiding it that way, we still can use its native state for navigation via `focus` state.

```css
.switch-toggle-input {
  opacity: 0;
  position: absolute;
  z-index: -1;
}
```

Next, we need to set `position` and `display` styles for the `label` tag, in order to position our toggle switch.

```css
.switch-toggle-container {
  position: relative;
  display: inline-block;
}
```

Then to give a toggle switch its distinct appearance, we'll need to style the `span` element. The `span` will represent the track and its `::after` pseudo-element will represent the thumb.

<p class="note">
  💡 NOTE: You can use the following styles to create a toggle switch control from a <code>button</code> or any other HTML tag.
</p>

```css
.switch-toggle {
  position: relative;
  display: inline-block;
  margin: 0 0 10px;
  width: 50px;
  height: 30px;
  background: #ddd;
  border-radius: 50px;
  transition: background .2s ease-in-out;
  cursor: pointer;
}

.switch-toggle::after {
  content: '';
  position: absolute;
  top: 2px;
  left: 2px;
  width: 26px;
  height: 26px;
  background: #fff;
  border-radius: 50px;
  box-shadow: 0 0 3px 1px rgba(0,0,0,0.15);
  transition: left .2s ease-in-out,
              width .2s ease-in-out,
              transform .2s ease-in-out;
}
```

To make the thumb move on click, we'll use the `:checked` pseudo-class on the checkbox `input` and an [adjacent sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_combinator){:target="_blank"} (`+`) to select `span`.


```css
.switch-toggle-input:checked + .switch-toggle {
  background: #30e16b;
}

.switch-toggle-input:checked + .switch-toggle::after {
  left: calc(100% - 2px);
	transform: translateX(-100%);
}
```

For the disabled toggle let's set dimmed gray colors with a proper cursor.

```css
.switch-toggle-input:disabled {
  pointer-events: none;
}

.switch-toggle-input:disabled + .switch-toggle {
  cursor: not-allowed;
  background: #eaeaea;
}

.switch-toggle-input:disabled + .switch-toggle::after {
  background: #f8f8f8;
}
```

For accessibility, we can add an outline, on focus state.

```css
.switch-toggle-input:focus + .switch-toggle::before,
.switch-toggle-container:active .switch-toggle-input:not([disabled]) + .switch-toggle::before {
  outline: 2px solid #5195fe;
  outline-offset: 2px;
}
```

Finally, for iOS-like feel, we can add a little transition for the thumb when it's moving. On click, the thumb will grow as it moves to the opposite side and then get back to its original size.

```css
.switch-toggle-container:active .switch-toggle-input:not([disabled]) + .switch-toggle::after {
  width: 34px;
}
```

**Result:**

<label class="switch-toggle-container">
  <input class="switch-toggle-input" type="checkbox">
  <span class="switch-toggle"></span>
</label>

## Text

You can also add text to your toggle switch control, to provide additional indication whether it is on or off.

To do so we'll specify the `content` property for the pseudo-element and display it accordingly.

```css
.switch-toggle::after  {
  content: 'Off';
  display: inline-flex;
  justify-content: center;
  align-items: center;
  font-size: 11px;
  color: #444;
}

.switch-toggle-input:checked + .switch-toggle::after {
  content: 'On';
}
```

**Result:**

<label class="switch-toggle-container">
  <input class="switch-toggle-input" type="checkbox">
  <span class="switch-toggle switch-toggle--labels"></span>
</label>

## Demo

You can find a full demo with a complete code examples on my CodePen:

<p class="codepen" data-height="350" data-default-tab="result" data-slug-hash="rNQyVYY" data-user="nikitahl" style="height: 350px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/rNQyVYY">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
