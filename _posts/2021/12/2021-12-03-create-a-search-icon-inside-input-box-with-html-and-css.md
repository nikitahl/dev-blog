---
layout: post
permalink: search-icon-inside-input
title: Create a search icon inside input box with HTML and CSS
date: 2021-12-03T07:22:16.317Z
description: "You can display a search icon inside input box in different ways
  with simple HTML and CSS code "
tags:
  - css
  - html
---

Displaying a search icon inside an input box is a nice way to indicate to the user that it is indeed a search input.

<style>
.image-grid {display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 10px;flex:1 0 46%}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/google-search-input.png" alt="Google search input">
    <noscript>
      <img class="shadow" src="/images/resources/google-search-input.png" alt="Google search input">
    </noscript>
    <figcaption>Google search input</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/duckduckgo-search-input.png" alt="Duckduckgo search input">
    <noscript>
      <img class="shadow" src="/images/resources/duckduckgo-search-input.png" alt="Duckduckgo search input">
    </noscript>
    <figcaption>Duckduckgo search input</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/twitter-search-input.png" alt="Twitter search input">
    <noscript>
      <img class="shadow" src="/images/resources/twitter-search-input.png" alt="Twitter search input">
    </noscript>
    <figcaption>Twitter search input</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/codepen-search-input.png" alt="CodePen search input">
    <noscript>
      <img class="shadow" src="/images/resources/codepen-search-input.png" alt="CodePen search input">
    </noscript>
    <figcaption>CodePen search input</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/gmail-search-input.png" alt="Gmail search input">
    <noscript>
      <img class="shadow" src="/images/resources/gmail-search-input.png" alt="Gmail search input">
    </noscript>
    <figcaption>Gmail search input</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/vimeo-search-input.png" alt="Vimeo search input">
    <noscript>
      <img class="shadow" src="/images/resources/vimeo-search-input.png" alt="Vimeo search input">
    </noscript>
    <figcaption>Vimeo search input</figcaption>
  </figure>
</div>

## Markup

The HTML for our search box with an icon will consist of a `form`, `input`, and `button` elements.

```html
<form>
  <input type="search" placeholder="Search...">
  <button type="submit">Search</button>
</form>
```

The `form` will act as a wrapper, as well as will react to the `submit` event.

The `input` element should have a `type` attribute equal to the `search` value. It will ensure a [better usability](https://css-tricks.com/better-form-inputs-for-better-mobile-user-experiences/#using-the-correct-input-type) on mobile devices. The keyboard with a layout suited for [search](https://better-mobile-inputs.netlify.app/?android=false&autocomplete=on&inputmode=search&type=search) will be shown.

**NOTE: To improve UX you can also specify an input placeholder e.g. “Search…”. This will give a user an additional hint that this is indeed a search input.**

Finally, the `button` `type` attribute should have a `submit` value. The [proper button type](/html-button-types) will ensure the `form` can be submitted via button click without additional events for this button. The button will also act as an icon.

## Styling

First, we’ll need to set the `form` element `display` property value to `flex`. This will allow us to properly align `input` and `button` elements.

We'll also set a `border` property to wrap elements closer together.

```css
form {
  color: #555;
  display: flex;
  padding: 2px;
  border: 1px solid currentColor;
  border-radius: 5px;
}
```

Next, we need to set styles for our search input box. It should span the full width of the container element, as well as have some visually appealing properties.

```css
input[type="search"] {
  border: none;
  background: transparent;
  margin: 0;
  padding: 7px 8px;
  font-size: 14px;
  color: inherit;
  border: 1px solid transparent;
  border-radius: inherit;
}

input[type="search"]::placeholder {
  color: #bbb;
}
```

Finally, let’s add some styling to the submit button. We will hide the text of the button with `text-indent` and `overflow` properties, and display in its place a magnifying glass icon.

To display the icon we can use [encoded svg as a background](/using-svg-background-image-with-css-code-only) image.

```css
button[type="submit"] {
  text-indent: -999px;
  overflow: hidden;
  width: 40px;
  padding: 0;
  margin: 0;
  border: 1px solid transparent;
  border-radius: inherit;
  background: transparent url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' class='bi bi-search' viewBox='0 0 16 16'%3E%3Cpath d='M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z'%3E%3C/path%3E%3C/svg%3E") no-repeat center;
  cursor: pointer;
  opacity: 0.7;
}

button[type="submit"]:hover {
  opacity: 1;
}
```

The last touch is to set the `:focus` state on `input` and `button` elements:

```css
button[type="submit"]:focus,
input[type="search"]:focus {
  box-shadow: 0 0 3px 0 #1183d6;
  border-color: #1183d6;
  outline: none;
}
```

## No button example

If you're willing to show an icon inside an input without it being a button, just remove the submit button from the form.

```html
<form class="nosubmit">
  <input class="nosubmit" type="search" placeholder="Search...">
</form>
```

You can leave existing form and input styles but in this case, set the icon as a background for the input.

```css
form.nosubmit {
  border: none;
  padding: 0;
}

input.nosubmit {
  width: 260px;
  border: 1px solid #555;
  display: block;
  padding: 9px 4px 9px 40px;
  background: transparent url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' class='bi bi-search' viewBox='0 0 16 16'%3E%3Cpath d='M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z'%3E%3C/path%3E%3C/svg%3E") no-repeat 13px center;
}
```

## Demo

<p class="codepen" data-height="300" data-default-tab="result" data-slug-hash="WNZbWGe" data-user="tippingpointdev" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
<span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/WNZbWGe">
Untitled</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>

<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>