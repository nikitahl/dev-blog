---
layout: post
permalink: input-clear-button
title: How to create a button to clear the input field
date: 2023-04-10T12:00:12.133Z
description: It's a good idea to allow users to clear the input with push of a button. Lets look at how you can add a clear button to the input field.
tags: [html, css]
---

It's a good idea to allow users to clear the input with push of a button. Lets look at how you can add a clear button to the input field.

The first thing you need to know is that the `input` tag with the `type="search"` has a clear button by default.

```html
<input type="search" placeholder="Search..." />
```

The default clear button will appear once user has typed something in to the input field.

<style>
.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
.image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/search-input-chrome.webp" alt="Search input on Chrome">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/search-input-firefox.webp" alt="Search input on Firefox">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/search-input-safari.webp" alt="Search input on Safari">
    <figcaption>Safari</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/search-input-edge.webp" alt="Search input on Edge">
    <figcaption>Edge</figcaption>
  </figure>
</div>

## Markup

However it's not working in all browsers, Firefox doesn't have such functionality.

Also you may want to add clear button to other `input` types, like `text`, `email`, etc.

To add a button we'll need to slightly modify the HTML.

<p class="note">
💡 NOTE: If it's a <code>search</code> type input, be aware that you might want to display a <a href="/search-icon-inside-input">search icon</a> as well.
</p>

One way to do that is if it's a standalone `input` field, you can wrap it in a `form` tag. Or if it's a single input already inside a `form` you can add a [`button` tag with reset type](/html-button-types).

For close (cross) charachter we'll use an [HTML entity](/special-characters-and-symbols-with-html-entities), times symbol - "×". It's a simple and quick way to show a close character. Ofcourse you can also use a font or an SVG.

The reset button, will reset all form values, in this particular case it will clear the one and only `input` field. The main benefit is that you don't need to add any additional JavaScript to clear the field. Form reset is a native behavior.

```html
<form class="clear-input-container">
  <input class="clear-input" type="text">
  <button
    class="clear-input-button"
    type="reset"
    aria-label="Clear input"
    title="Clear input"
  >×</button>
</form>
```

If you have a specific `input` you want to clear, the idea is similar. Wrap `input` tag inside a `div` and add a button.

```html
<div  class="clear-input-container">
  <input class="clear-input" type="text">
  <button
    class="clear-input-button"
    aria-label="Clear input"
    title="Clear input"
  >×</button>
</div>
```

In both cases, `input` and `button` are contained in a single wrapper element.

## Styling

Whether you choose to use `form` or `div` element as a container the CSS will be the same.

First we need to set container element to have a `position: relative`, so that we can align the clear button later.

And set it to `display: inline-block` so that it takes the size (width and height) of the `input`.

```css
.clear-input-container {
  position: relative;
  display: inline-block;
}
```

The clear button has to be positioned reative to the container with `position: absolute`. Now we can set it to be at the end of the `input`, which is right side for LTR direction.

Additionally to positioning properties, we need to style the visual appearance of the button.

```css
.clear-input-button {
 /* button position */
  position: absolute;
  right: 4px;
  top: 4px;
  bottom: 0;
  /* button appearane */
  justify-content: center;
  align-items: center;
  width: 16px;
  height: 16px;
  appearance: none;
  border: none;
  border-radius: 50%;
  background: gray;
  margin: 0;
  padding: 2px;
  color: white;
  font-size: 13px;
  cursor: pointer;
  /* hide the button initially */
  display: none;
}

.clear-input-button:hover {
  background: darkgray;
}
```

We'll hide the button to make it visible only when use input a value. We'll add a custom class with JavaScript to the `input` field if if has a value.

And we'll set some styles to show the clear button with the touched input.

```css
.clear-input--touched:focus + .clear-input-button,
.clear-input--touched:hover + .clear-input-button,
.clear-input--touched + .clear-input-button:hover {
  display: inline-flex;
}
```

## Functionality

To make the button visible on `input` value change lets add an event listener, which will add a custom class name. and toggle on focus (if there's a value)

```javascript
const input = document.querySelector(".clear-input")

const handleInputChange = (e) => {
  if (e.target.value && !input.classList.contains("clear-input--touched")) {
    input.classList.add("clear-input--touched")
  } else if (!e.target.value && input.classList.contains("clear-input--touched")) {
    input.classList.remove("clear-input--touched")
  }
}

input.addEventListener("input", handleInputChange)
```

Finally, we need to clear the input on button click.

If you're using the `form` with a button type `reset`, then you don't need additional JavaScript.

Otherwise lets add an event listener for clear button.

```javascript
const input = document.querySelector(".clear-input")
const clearButton = document.querySelector(".clear-input-button")

const handleButtonClick = (e) => {
  input.value = ''
  input.focus()
  input.classList.remove("clear-input--touched")
}

clearButton.addEventListener("click", handleButtonClick)
```

As you can see from the code above, on button click, we set the input value to an empty string.

Additionally, we leave input focused and remove the `clear-input--touched` class to hide the clear button.

## Demo

You can find a full demo with a complete code examples on my CodePen:

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="yLRyPLY" data-user="nikitahl" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/yLRyPLY">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
