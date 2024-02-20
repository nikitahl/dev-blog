---
layout: post
permalink: outline-text-with-css
title: A simple way to add an outline to text with pure CSS
date: 2023-12-20T20:08:02.112Z
description: Adding a cool outline effect to your text is quite simple with just a few lines of CSS.
tags: [css]
---

Adding a cool outline effect to your text is quite simple with just a few lines of CSS.

Previously, you needed to use hacks, such as adding several `box-shadow` properties, to achieve such a result.

But with modern CSS to add an outline effect you’ll need to use only three CSS properties `-webkit-text-fill-color`, `-webkit-text-stroke-width` and `-webkit-text-stroke-color`.

```css
.outline-text {
  -webkit-text-fill-color: #fff;
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: #262626;
}
```

**Result:**

<style>
  .outline-text {
    -webkit-text-fill-color: #fff;
    -webkit-text-stroke-width: 1px;
    -webkit-text-stroke-color: #262626;
    font-size:3.5em;
    font-family: Helvetica, sans-serif;
    line-height: 1.2;

    transition: -webkit-text-stroke-color .2s ease-in-out;
  }
  .outline-text-hover:hover {
    -webkit-text-stroke-color: #f00;
  }
</style>

<strong class="outline-text">Outline Text</strong>

These properties are pretty self-explanatory:

* [`-webkit-text-fill-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-text-fill-color){:target="_blank"} - adds a fill color for the text
* [`-webkit-text-stroke-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-text-stroke-color){:target="_blank"} - specifies the outline color of the text
* [`-webkit-text-stroke-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-text-stroke-width){:target="_blank"} - specifies the outline width of the text

## Hover effect

They also work well with CSS transitions, so you can apply one on hover effect.

```css
  .outline-text {
    -webkit-text-fill-color: #fff;
    -webkit-text-stroke-width: 1px;
    -webkit-text-stroke-color: #262626;

    transition: -webkit-text-stroke-color .2s ease-in-out;
  }

  .outline-text:hover {
    -webkit-text-stroke-color: #f00;
  }
```
**Result:**

<strong class="outline-text outline-text-hover">Outline Text with Hover Effect</strong>

## Browser support

These three properties are fully supported by all modern browsers.

<p class="ciu_embed" data-feature="mdn-css__properties__-webkit-text-fill-color" data-periods="future_1,current,past_1" data-accessible-colours="false">
Data on support for the <a href="https://caniuse.com/text-stroke" target="_blank">-webkit-text-fill-color</a> feature across the major browsers
</p>

<p class="ciu_embed" data-feature="mdn-css__properties__-webkit-text-stroke-color" data-periods="future_1,current,past_1" data-accessible-colours="false">
Data on support for the <a href="https://caniuse.com/text-stroke" target="_blank">-webkit-text-stroke-color</a> feature across the major browsers
</p>

<p class="ciu_embed" data-feature="mdn-css__properties__-webkit-text-stroke-width" data-periods="future_1,current,past_1" data-accessible-colours="false">
Data on support for the <a href="https://caniuse.com/text-stroke" target="_blank">-webkit-text-stroke-width</a> feature across the major browsers
</p>