---
layout: post
permalink: text-selection-color-css
title: Text selection color CSS
date: 2021-08-12T19:19:02.919Z
description: You can make a custom text selection color with pure CSS to match
  the theme color of your web app.
tags:
  - css
---

You can make a custom text selection color with pure CSS to match the theme color of your web app. To do so you’ll need to use a [`::selection` pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/::selection).

**Example**:

```css
::selection {
  background-color: mediumpurple;
  color: white;
}
```

To support the older versions of **Firefox** browser (version 61 and below) use the vendor prefix:

```css
::-moz-selection {
  background-color: mediumpurple;
  color: white;
}
```

<figure>
  <img class="shadow" src="/images/misc/document-text-selection-color.png" alt="Document text selection color" loading="lazy">
  <figcaption>Whole document text selection color</figcaption>
</figure>

When used on its own the `::selection` pseudo-element will apply the selection color to the whole document. In case you want to make a selection color for a specific part of the page apply it in combination with the element selector.

**Example**:

```css
/* Will apply selection color only for heading 2 elements */
h2::selection {
  background-color: tomato;
  color: mintcream;
}
```

<figure>
  <img class="shadow" src="/images/misc/heading-text-selection-color.png" alt="Heading text selection color" loading="lazy">
  <figcaption>Heading text selection color</figcaption>
</figure>

However, note that only the following CSS properties can be used with `::selection`:

* `color`
* `background-color`
* `text-decoration` and its associated properties
* `text-shadow`
* `stroke-color`, `fill-color` and `stroke-width`

In particular, `background-image` is ignored.

**Browser support for `::selection` pseudo-element**:

<p class="ciu_embed" data-feature="css-selection" data-periods="future_1,current,past_1" data-accessible-colours="false">
<picture>
<source type="image/webp" srcset="https://caniuse.bitsofco.de/image/css-selection.webp">
<source type="image/png" srcset="https://caniuse.bitsofco.de/image/css-selection.png">
<img src="https://caniuse.bitsofco.de/image/css-selection.jpg" alt="Data on support for the css-selection feature across the major browsers from caniuse.com">
</picture>
</p>

<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/public/caniuse-embed.min.js"></script>