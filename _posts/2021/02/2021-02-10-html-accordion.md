---
layout: post
permalink: native-html-accordion
title: Pure HTML accordion with details and summary elements
date: 2021-02-17T14:08:50.492Z
updated: 2024-10-03T18:35:10.124Z
description: A modern way to create a pure HTML accordion widget on a page using nothing but the semantic elements
tags: [html]
---

The [accordion](https://en.wikipedia.org/wiki/Accordion_(GUI)) is a UI paradigm that consists of several stacked blocks. Each block consists of a label and a content section, clicking on a label either *expands* or *collapses* the section. 

For a long time, such behavior was only available with a JavaScript implementation or with some [CSS workarounds](https://codepen.io/raubaca/pen/PZzpVe). Until HTML5 came along and introduced the `details` and `summary` tags that can be used to create a pure HTML accordion.

The [`details`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/details) tag serves as a wrapper for an interactive widget that can be open or closed. A user has to click on the label which is represented by the [`summary`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/summary) tag to open or close the widget. 

Now you can create a pure HTML accordion using nothing but these two tags. It's a great way to utilize [semantic HTML](/why-it-is-important-to-write-semantic-html) and make an accessible and easily recognizable widget.

```html
<details>
    <summary>What is HTML?</summary>
    <p>HTML (HyperText Markup Language) is the most basic building block of the Web. It defines the meaning and structure of web content.</p>
</details>
<details>
    <summary>What is CSS?</summary>
    <p>Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML.</p>
</details>
<details>
    <summary>What is JavaScript?</summary>
    <p>JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions.</p>
</details>
```

**Result:**

<style>
  details { padding: 3px}
  .details-container { margin-bottom: 15px}
  summary { padding: 5px; cursor:pointer} 
  .image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
  .image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
  .image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}
</style>

<div class="details-container ">

  <details>
      <summary>What is HTML?</summary>
      <p>HTML (HyperText Markup Language) is the most basic building block of the Web. It defines the meaning and structure of web content.</p>
  </details>
  <details>
      <summary>What is CSS?</summary>
      <p>Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML.</p>
  </details>
  <details>
      <summary>What is JavaScript?</summary>
      <p>JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions.</p>
  </details>

</div>

## Styling and Behavior

Default styling looks pretty similar across the browsers. One particular feature about HTML accordion is that by default the `summary` tag has a small triangle that changes it direction based on the state of the widget.

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/html-elements/details-chrome.png" alt="Details element on Chrome" loading="lazy">
    <figcaption>Crome</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/details-edge.png" alt="Details element on Edge" loading="lazy">
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/details-firefox.png" alt="Details element on Firefox" loading="lazy">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/details-safari.png" alt="Details element on Safari" loading="lazy">
    <figcaption>Safari</figcaption>
  </figure>
</div>

The triangle shape inherits the color from the `color` property of the summary element or the closest parent wich has this property set.

Also you can target the opened state of the widget with the `[open]` atrtibute selector:

```css
details[open] {
  box-shadow: 0 2px 5px 0 #666;
}
```

The `summary` tag is focusable so `summary:focus` selector can be used to target this state:

```css
summary:focus {
  color: #005fcc;
}
```

If you're willing to customize the appearance of the arrow there's a `::-webkit-details-marker` pseudo-element that will hide the arrow:

```css
summary::-webkit-details-marker {
  display: none;
}
```

To insert another symbol to replace the arrow you can use an [encoded SVG image as a background](/using-svg-background-image-with-css-code-only).

<p class="note">
  💡 NOTE: Unfortunately, at this time there's no built-in way to animate the transition between open and closed.
</p>

## Events and API

The `details` element has an `open` property attached to its DOM object, which you can read and modify. Modifying it will result in triggering the open or close of the widget.

```javascript
const details = document.querySelector('details')
details.open = true // will expand the widget
```

Additionally, the `details` element supports `toggle` event. It reacts whenever the widget is collapsed or expanded:

```javascript
const details = document.querySelector('details')

details.addEventListener('toggle', (e) => {
  console.log(e.target.open) // will log true or false based on the state
})
```

## Show a single section

To add more functionality and create a collapsible HTML accordion, you can assign the same `name` attribute value to each of the `details` elements.

This will make it function like a classic accordion, where only one section is visible at a time, and the others collapse.

```html
<div class="details-container">
  <details class="details" name="technology">
      <summary>What is HTML?</summary>
      <p>HTML (HyperText Markup Language) is the most basic building block of the Web. It defines the meaning and structure of web content.</p>
  </details>
  <details class="details" name="technology">
      <summary>What is CSS?</summary>
      <p>Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML.</p>
  </details>
  <details class="details" name="technology">
      <summary>What is JavaScript?</summary>
      <p>JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions.</p>
  </details>
</div>
```

**Result:**

<div class="details-container">
  <details class="details" name="web-technology">
      <summary>What is HTML?</summary>
      <p>HTML (HyperText Markup Language) is the most basic building block of the Web. It defines the meaning and structure of web content.</p>
  </details>
  <details class="details" name="web-technology">
      <summary>What is CSS?</summary>
      <p>Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML.</p>
  </details>
  <details class="details" name="web-technology">
      <summary>What is JavaScript?</summary>
      <p>JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions.</p>
  </details>
</div>

<!-- <script>
  var details = Array.from(document.querySelectorAll('.details'));
  details.forEach((detail) => {
    detail.addEventListener('click', (e) => {
      var active = details.find(d => d.open);
      if (!e.currentTarget.open && active) {
        active.open = false;
      }
    });
  });
</script> -->

## Browser Support

Both `details` and `summary` elements are [supported in all browsers](https://caniuse.com/details) except IE.