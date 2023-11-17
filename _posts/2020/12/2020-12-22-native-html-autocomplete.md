---
layout: post
permalink: html-autocomplete
title: Native HTML autocomplete with dropdown for input field from list
date: 2020-12-23T21:37:59.290Z
updated: 2023-11-17T10:52:10.124Z
description: A definitive guide how to implement a simple native HTML autocomplete field with dropdown from list using just HTML code
tags: [html]
---

Did you know that you can create a native HTML autocomplete field with dropdown? Yes, it is possible with just a few lines of code.

## Markup

It works as follows. We'll need to use an `input` element with a [`list` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-list) that will act as an autocomplete field.

Next we need to assign it a `list` attribute that should have the value of an `id` attribute of the `datalist` element.

The [`datalist` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist) contains a set of predefined `option` elements that act as suggestions for our autocomplete `input` element.

The complete HTML code will look as follows:

```html
<label for="language-field">Choose a programming language:</label>
<input list="languages" id="language-field" name="language-field" />

<datalist id="languages">
  <option value="C">
  <option value="C#">
  <option value="C++">
  <option value="JavaScript">
  <option value="JAVA">
  <option value="PHP">
  <option value="Perl">
  <option value="Python">
  <option value="Ruby">
  <option value="Rust">
</datalist>
```

**Result:**

<p><label for="language-field">Choose a programming language:</label> <input list="languages" id="language-field" name="language-field" /><datalist id="languages"><option value="C"></option><option value="C#"></option><option value="C++"></option><option value="JavaScript"></option><option value="JAVA"></option><option value="PHP"></option><option value="Perl"></option><option value="Python"></option><option value="Ruby"></option><option value="Rust"></option></datalist></p>

*Click on the label or input and start typing.*

## Appearance and behavior

The appearance of the autocomplete `input` field and the suggestion box will differ depending on the browser and the operating system. So that's an important thing to keep in mind when designing an interface.

<style>
  .image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px}
  .image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
  .image-grid figure{margin: 0 10px 10px;flex: 1 0 47%}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/html-elements/datalist-chrome.png" alt="Datalist on Chrome" loading="lazy">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/datalist-edge.png" alt="Datalist on Edge" loading="lazy">
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/datalist-firefox.png" alt="Datalist on Firefox" loading="lazy">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/datalist-safari.png" alt="Datalist on Safari" loading="lazy">
    <figcaption>Safari</figcaption>
  </figure>
</div>

### CSS

The `input` field is a common form element and it is easy to style consistently across different browsers, similar to the [select element](/how-to-custom-style-select-tag-with-css-only). 

By default, the `datalist` element has a style of `display: none`. So when a user clicks on the `input` field the dropdown shown is not the `datalist` element, but instead a list preview rendered by the browser.

That means to make the dropdown look consistent across different browsers additional functionality has to be added, like custom JavaScript and CSS.

To change the appearance of the arrow, you'll need to hide it and then you can use [encoded SVG as a background image](/using-svg-background-image-with-css-code-only).

```css
input#language-field::-webkit-calendar-picker-indicator {
  display: none;
}

input#language-field {  
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='292.4' height='292.4'%3E%3Cpath fill='%23333' d='M287 69.4a17.6 17.6 0 0 0-13-5.4H18.4c-5 0-9.3 1.8-12.9 5.4A17.6 17.6 0 0 0 0 82.2c0 5 1.8 9.3 5.4 12.9l128 127.9c3.6 3.6 7.8 5.4 12.8 5.4s9.2-1.8 12.8-5.4L287 95c3.5-3.5 5.4-7.8 5.4-12.8 0-5-1.9-9.2-5.5-12.8z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 8px center;
  background-size: 9px;
}
```

### JavaScript

The `datalist` element has no particular [Web API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDataListElement) attached to it, so you'll just have to use default JavaScript methods to manipulate your autocomplete field and dropdown list.

This means that in order to customize the appearance and behavior of it, you'll have to sacrifice native behavior.

## Browser Compatibility

The `datalist` is a [semantic HTML element](/why-it-is-important-to-write-semantic-html) and is supported in all modern browsers. However some issues may occur if you're willing to support older browsers, please refer to the `datalist` compatibility table.

<p class="ciu_embed" data-feature="datalist" data-periods="future_1,current,past_1,past_2" data-accessible-colours="false">
<picture>
<source type="image/webp" srcset="https://caniuse.bitsofco.de/image/datalist.webp">
<source type="image/png" srcset="https://caniuse.bitsofco.de/image/datalist.png">
<img src="https://caniuse.bitsofco.de/image/datalist.jpg" alt="Data on support for the datalist feature across the major browsers from caniuse.com">
</picture>
</p>

## Final thoughts

All in all in my opinion, while the default styling and functionality are left untouched the HTML autocomplete is a pretty unique paradigm in web development. However, it lacks some flexibility and customization which can make it a rare use case.

<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/public/caniuse-embed.min.js"></script>