---
layout: post
permalink: html-button-types
title: "What are the HTML button types and how are they different? "
date: 2021-10-13T19:52:16.173Z
description: There are 3 HTML button types, each of them has its own purpose. In
  this article, we’ll inspect each one of them and see how they are different.
tags:
  - html
---

There are 3 types of buttons in HTML, each of them has its own purpose. In this article, we’ll inspect each one of the HTML button types and see how they are different.

## Button tag

For the button element, one of two HTML tags can be used: `input` and `button`.

```html
<button>Click here</button>
```

If an `input` tag is used a `type` attribute has to be specified in order for it to appear as a button. As well as a `value` attribute to display the text on the button.

```html
<input type="button" value="Click here" />
```

Both approaches will render a button to a page that will look the same by default, no matter the button type value. However, each browser displays a button in a slightly different way.

<style>.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}.image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}</style>

<div class="image-grid">
  <figure>
    <img class="shadow lozad" data-src="/images/button-styles/buttons-chrome.png" alt="Buttons on Chrome">
    <noscript>
      <img class="shadow" src="/images/button-styles/buttons-chrome.png" alt="Buttons on Chrome">
    </noscript>
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/button-styles/buttons-edge.png" alt="Buttons on Edge">
    <noscript>
      <img class="shadow" src="/images/button-styles/buttons-edge.png" alt="Buttons on Edge">
    </noscript>
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/button-styles/buttons-firefox.png" alt="Buttons on Firefox">
    <noscript>
      <img class="shadow" src="/images/button-styles/buttons-firefox.png" alt="Buttons on Firefox">
    </noscript>
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/button-styles/buttons-safari.png" alt="Buttons on Safari">
    <noscript>
      <img class="shadow" src="/images/button-styles/buttons-safari.png" alt="Buttons on Safari">
    </noscript>
    <figcaption>Safari</figcaption>
  </figure>
</div>

Both `button` and `input` share some common attributes:

1. `disabled`
2. `autofocus`
3. `tabindex`

### The difference between button and input tags

While `button` and `input` (when displayed as a button) do essentially the same thing, some differences exist.

1. The [`input` tag cannot have pseudo-element](https://www.scottohara.me/blog/2014/06/24/pseudo-element-input.html), while button can;
2. The `input` tag has some unique attributes for additional functionality:

   1. The [`accesskey`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/accesskey) attribute which allows the user to trigger a button using a key or combination of keys on the keyboard;
3. The `input` tag can have a `label` tag attached to it.

**NOTE: It is [advised](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button) to use the button tag over input when possible. As button tag is fully [accessible](https://www.deque.com/blog/accessible-aria-buttons/) and semantic out of the box.**

## Button types

To set the button type, use the according attribute:

* `button` - a regular button, doesn’t do anything unless specified (e.g. JavaScript event)
* `submit` - submits form data to the server
* `reset` - resets the values from fields

```html
<button type="button">Apply now</button>

<button type="submit">Submit</button>

<button type="reset">Reset</button>
```

or

```html
<input type="button" value="Apply now" />

<input type="submit" value="Submit" />

<input type="reset" value="Reset" />
```

## Button behavior

The `type` attribute defines button behavior inside the form. Visually different button types look the same and don’t have many differences.

Inside the form, once clicked the button will perform an action by default specified by the `type` attribute. If the button is inside the form and has no attribute specified it will act as a `submit` type button. If the button is inside the form and it has a `button` attribute, it will not trigger any actions, unless specified by JavaScript.

Outside the form, each button type acts as a regular button, this means on click nothing will happen.

**Example**:

```html
<form action="">
  <input type="text" placeholder="Your name" required>
  <input type="email" placeholder="email@example.com" required>
  <input type="number" value="42">

  <input type="submit" value="Submit" />
  <input type="reset" value="Reset" />
  <button type="button">Button</button>
</form>
```

**Result**:

<form style="margin: 0 0 30px">

<input type="text" placeholder="Your name" required>

<br><br>

<input type="email" placeholder="email@example.com" required>

<br><br>

<input type="number" value="42">

<br><br>

<input type="submit" value="Submit" />

<br><br>

<input type="reset" value="Reset" />

<br><br>

<button type="button">Button</button>

</form>

## Browser Support

<https://caniuse.com/mdn-html_elements_button>

<https://caniuse.com/mdn-html_elements_button_type>

<https://caniuse.com/mdn-html_elements_input_input-button>

<https://caniuse.com/mdn-html_elements_input_input-submit>

<https://caniuse.com/mdn-html_elements_input_input-reset>