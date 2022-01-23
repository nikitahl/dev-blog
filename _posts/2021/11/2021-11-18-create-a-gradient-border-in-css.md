---
layout: post
permalink: gradient-border-css
title: Create a gradient border in CSS
date: 2021-11-18T20:22:13.094Z
description: Create a beautiful gradient border in CSS using one of three
  approaches. In this article I'll show you each one in detail.
tags:
  - css
---

To show gradients for a border with CSS you can use the `border-image` property. It allows setting gradient values in the same way as the `background-image` property.

<style>
.box {position:relative;display:inline-block;padding:10px 20px}
.gradient-border {
  border: 5px solid;
  border-image: linear-gradient(45deg, purple, orange) 1;
}
.gradient-border-pseudo {
  background: #fff;
  margin: 5px;
  border-radius: 5px;
}
.gradient-border-pseudo::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  margin: -5px;
  border-radius: inherit;
  background-image: linear-gradient(45deg, purple, orange);
}
.gradient-border-mask::before {
content:"";
position:absolute;
top:0;
left:0;
right:0;
bottom:0;
border-radius: 50px;
border: 5px solid transparent;
background: linear-gradient(45deg,purple,orange) border-box;-webkit-mask:
linear-gradient(#fff 0 0) padding-box,
linear-gradient(#fff 0 0);-webkit-mask-composite: destination-out;
mask-composite: exclude;
}
.gradient-border-bg {
  background: linear-gradient(#fff, #fff) padding-box,
              linear-gradient(45deg, slateblue, coral) border-box;
  border: 5px solid transparent;
  border-radius: 50px;
}
</style>

Besides the `border-image` property, you should specify additional properties to actually show border gradient.

* `border-width`
* `border-style`
* `border-image-source`
* `border-image-slice`

We can combine these properties into a shorthand syntax `border-width` with `border-style` into `border` and `border-image-source` with `border-image-slice` into `border-image`.

```css
.gradient-border {
  border: 5px solid;
  border-image: linear-gradient(45deg, purple, orange) 1;
}
```

**Result**:

<p class="box gradient-border">Hello World!</p>

Now you have a nice -ooking gradient border. And you can use all types of gradients: `linear-gradient`, `radial-gradient` and `conic-gradient`.

However, there’s a drawback to this approach. You cannot use `border-radius` property, as it is not supported with the `border-image` property. But there are a few workarounds.

## Pseudo element

### Positioning trick

For this approach, we need to add a gradient as a `background-image` for the pseudo-element. Additionally, we need to set its position to `absolute` and set a negative margin, that will represent the border width. Give it a negative `z-index` to make it below the main element. And finally, make it inherit `border-radius` from the main element.

For the initial element, we need to set the required `border-radius`. Set background color, to match the `body` background. Optionally we give it a margin to make it within the boundaries of the container because pseudo-element has a negative margin.

```css
.gradient-border-pseudo {
  position: relative;
  padding: 10px 20px;
  background: #fff;
  margin: 5px;
  border-radius: 5px;
}

.gradient-border-pseudo::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  margin: -5px;
  border-radius: inherit;
  background-image: linear-gradient(45deg, purple, orange);
}
```

**Result**:

<p class="box gradient-border-pseudo">Hello World!</p>

### Masking trick

For this solution, we’ll also use the pseudo-element, but instead of positioning it with `z-index`, we will use the [`mask`](https://developer.mozilla.org/en-US/docs/Web/CSS/mask) property to clip the background.

> The `mask` CSS shorthand property hides an element (partially or fully) by masking or clipping the image at specific points.
>
> \- MDN

While the mask property may [lack full support](https://caniuse.com/css-masks), you can use this approach for the gradient border.

We'll set the element's background as a gradient. And then using `mask` property we'll specify two more gradient backgrounds (same color as `body`). The first one will mask (cover) the area within the padding boundaries, and the second one will mask (cover) the area all the way up to the border.

Additionally, we need to set the [`mask-composite`](https://developer.mozilla.org/en-US/docs/Web/CSS/mask-composite) property to exclude the top layer from the bottom in order to see the border.

```css
.gradient-border-mask {
  position: relative;
  padding: 15px 20px;
}

.gradient-border-mask::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-radius: 50px; 
  border: 5px solid transparent;
  background: linear-gradient(45deg,purple,orange) border-box;
  -webkit-mask:
    linear-gradient(#fff 0 0) padding-box, 
    linear-gradient(#fff 0 0);
  -webkit-mask-composite: destination-out;
  mask-composite: exclude;
}
```

**Result**:

<p class="box gradient-border-mask">Hello World!</p>

## Background clip

To avoid additional styles for pseudo-element you can use the `background-image` property in combination with [`background-clip`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip) property.

> The `background-clip` CSS property sets whether an element's background extends underneath its border box, padding box, or content box.
>
> \- MDN

Essentially we’re going to clip the background in the similar way we did with the `mask` property.

First, we’ll need to pass two gradients values for the `background-image`. One will represent the background of the element with the according color, and the second one will represent the border with gradient.

For each of the gradients, we’ll specify the `background-clip` property.

For the first one, the value will be `padding-box`, so the background will extend up until the border.

For the second one, the value will be `border-box`, which means that the background will extend to the outside edge of the border.

Finally we need to specify a transparent border color and `border-radius`, and it’s done.

```css
.gradient-border-bg {
  background: linear-gradient(#fff, #fff) padding-box,
              linear-gradient(45deg, slateblue, coral) border-box;
  border: 5px solid transparent;
  border-radius: 50px;
}
```

**Result**:

<p class="box gradient-border-bg">Hello World!</p>

## Demo

Complete examples with code available on CodePen:

<p class="codepen" data-height="360" data-default-tab="result" data-slug-hash="gOxqZqy" data-user="tippingpointdev" style="height: 360px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/gOxqZqy">
  Untitled</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>