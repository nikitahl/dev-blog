---
layout: post
permalink: style-range-input-css
title: Styling range input with CSS and JavaScript for better UX
date: 2021-04-23T07:36:11.678Z
updated: 2023-07-13T18:22:14.468Z
description: A complete guide to style range input with CSS and JavaScript to
  make your UI consistent, more usable and visually appealing
tags: [css, javascript, html]
---

To style the range input with CSS you'll need to apply styles to two pseudo-elements: [`::-webkit-slider-thumb`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-slider-thumb) and [`::-webkit-slider-runnable-track`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-slider-runnable-track). Find out how you can apply custom styling and make the range input more functional and appealing.

Contents of the article:

1. [Accent color](#accent-color)
2. [CSS selectors for the range input](#css-selectors-for-the-range-input)
3. [Improving usability](#improving-usability)
4. [A sprinkle of JavaScript](#a-sprinkle-of-javascript)
5. [Range input for RTL direction](#range-input-for-rtl-direction)
6. [Demo](#custom-range-input-demo)

The `input` element with a type of range is a native HTML form UI element that allows users to select a value by dragging a slider over a range field.

The default browser styling for this element is very basic and doesn’t provide enough information to the user which might confuse one. Also, the appearance of the range input element is different across browsers.

**Range input HTML**:

```html
<input type="range">
```

**Result:**

<input type="range">

<style>
  .image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
  .image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
  .image-grid figure{margin:0 10px 10px;flex:1 0 47%}
</style>

**Range input appearance on different browsers**:

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/html-elements/range-chrome.png" alt="Range Input on Chrome" loading="lazy">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/range-edge.png" alt="Range Input on Edge" loading="lazy">
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/range-firefox.png" alt="Range Input on Firefox" loading="lazy">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/range-safari.png" alt="Range Input on Safari" loading="lazy">
    <figcaption>Safari</figcaption>
  </figure>
</div>

Luckily there are ways you can improve that using nothing but native CSS and JavaScript.

## Accent color

One simple way to customize the appearance of the range input without any specific selectors or additional HTML is to change the color of the range.

To do so you can define the [`accent-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/accent-color) property for the `input[type="range"]` selector which will update the color of the track and thumb.

```css
input[type="range"] {
  accent-color: coral;
}
```

**Result:**

<input type="range" style="accent-color:coral">

## CSS selectors for the range input

The range input widget consists of two parts the **thumb** and the **track**. Each one of these parts has its own pseudo-class selector for styling with a vendor suffix for cross-browser support.

**Thumb**:

`input[type="range"]::-webkit-slider-thumb`

`input[type="range"]::-moz-range-thumb`

`input[type="range"]::-ms-thumb`

**Track**:

`input[type="range"]::-webkit-slider-runnable-track`

`input[type="range"]::-moz-range-track`

`input[type="range"]::-ms-track`

```css
input[type="range"] {
  -webkit-appearance: none;
  margin-right: 15px;
  width: 200px;
  height: 7px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 5px;
  background-image: linear-gradient(#ff4500, #ff4500);
  background-size: 70% 100%;
  background-repeat: no-repeat;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background: #ff4500;
  cursor: ew-resize;
  box-shadow: 0 0 2px 0 #555;
  transition: background .3s ease-in-out;
}

input[type=range]::-webkit-slider-runnable-track  {
  -webkit-appearance: none;
  box-shadow: none;
  border: none;
  background: transparent;
}
```

To indicate the selected value, we can add a color from the start of the track up until the thumb. To do that we can use the `background-image` property with the `linear-gradient()` value. The `background-size` property will be used to set the size, which can later be [updated with JavaScript](#a-sprinkle-of-javascript).

## Improving usability

The default range input doesn’t specify any values selected. Which makes it hard for users to understand what value is currently selected.

While the [hash marks and labels](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range#adding_hash_marks_and_labels) on the range input are a great way to aid users visually, this feature is yet to become available.

However, there are a few ways you can improve that with some additional HTML and JavaScript:

1. Specify the output element to display the selected value
2. Specify the number input that is synced to the range input

### Specify the output element to display the selected value

The `output` element on the side of the range input will display the selected value. You'll have to add an `id` attribute for the `output` element, and an `oninput` attribute for the range input with a short function as a value, that will update the `output` element contents.

```html
<input type="range" min="0" max="100" oninput="rangevalue.value=value"/>
<output id="rangevalue">50</output>
```

### Specify the number input that is synced to the range input

To take it a step further you can add a number input next to the range element.

That way the user will see the selected value and will have an option to modify it via the number input, which can be a better experience especially for mobile users.

```html
<input type="range" value="50" min="0" max="100" id="range" oninput="rangevalue.value=value"/>
<input type="number" id="rangevalue" value="50" oninput="range.value=value">
```

## A sprinkle of JavaScript

To finalize we’ll need some JavaScript code to make it all work. The `oninput` attribute is already updating value based on a target element.

But to update the selected area of the range input we need to calculate the ratio and apply that value to the input `background-size` property.

**💡 NOTE: the `value` property of the range input is a string type, if you want to use is as a [numeric value](/number-value-from-input-javascript) you should use `valueAsNumber` property.**

```javascript
const rangeInputs = document.querySelectorAll('input[type="range"]')
const numberInput = document.querySelector('input[type="number"]')

function handleInputChange(e) {
  let target = e.target
  if (e.target.type !== 'range') {
    target = document.getElementById('range')
  } 
  const min = target.min
  const max = target.max
  const val = target.value
  
  target.style.backgroundSize = (val - min) * 100 / (max - min) + '% 100%'
}

rangeInputs.forEach(input => {
  input.addEventListener('input', handleInputChange)
})

numberInput.addEventListener('input', handleInputChange)
```

## Range input for RTL direction

To make the above solution of custom range input work for RTL (right to left) web pages, you must make some adjustments for both CSS and JavaScript.

The recommended way to set the text direction of a block or a whole page is to use the [`dir`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#dir){:target="_blank"} attribute.

```html
<html dir="rtl">
  ...
</html>
```

Once the `dir` attribute is set, we can specify the following selector for the range input `[dir="rtl"] input[type="range"]`.

Now to set the same value for the RTL direction, we must revet the background colors and the value. So for the 70% range, it will look as follows:

```css
[dir="rtl"] input[type="range"] {
  /* Used to be gradient color, the current progress */
  background: #ff4500;

  /* Used to be background color, the track */
  background-image: linear-gradient(#fff, #fff);

  /* 30% is the difference between the max and the current value (100 - 70) */
  background-size: 30% 100%;
  background-repeat: no-repeat;
}
```

As for the JavaScript, we need to add a condition for the change handler function, to calculate the correct value: *max - current*.

```javascript
function handleInputChange(e) {
  let target = e.target
  if (e.target.type !== 'range') {
    target = document.getElementById('range')
  } 
  const min = target.min
  const max = target.max
  const val = target.value
  let percentage = (val - min) * 100 / (max - min)
  
  // condition to check whether the document has RTL direction
  // you can move it to a variable, if document direction is dynamic
  if (document.documentElement.dir === 'rtl') {
    percentage = (max - val) 
  }
  
  target.style.backgroundSize = percentage + '% 100%'
}
```

## Custom range input Demo

You can find a full demo with a complete code examples on CodePen:

<p class="codepen" data-height="400" data-theme-id="dark" data-default-tab="result" data-user="tippingpointdev" data-slug-hash="bGgLqLY" style="height: 360px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Range Input with values (Pure HTML, CSS, JS)">
  <span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/bGgLqLY">
  Range Input with values (Pure HTML, CSS, JS)</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
