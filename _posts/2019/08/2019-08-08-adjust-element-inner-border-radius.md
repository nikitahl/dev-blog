---
layout: post
title: How to adjust the element's inner border radius
description: Two simple solutions on how to adjust the element's inner border radius with CSS
updated: 2023-04-14T09:35:10.124Z
tags: [css]
comments: true
---

An element's inner border-radius is the value a developer cannot directly affect. However, some tricks can be implemented in order to achieve the same smooth border curve result.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/border-radius.webp" alt="Element's border radiuses">
  <figcaption>Element's border radiuses</figcaption>
</figure>

The element's inner border-radius is formed via formula:

```
IBR: Inner Border Radius
OBR: Outer Border Radius
BW: Border Width

IBR = OBR - BW
```

<blockquote>
	The padding edge (inner border) radius is the outer border radius minus the corresponding border thickness.
	<br />
	&mdash;<cite><a href="https://www.w3.org/TR/css-backgrounds-3/#corner-shaping
" target="_blank">Corner Shaping</a></cite>

</blockquote>

<style>
.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
.image-grid figure{margin: 0 10px 10px;flex: 1 0 30%;}
@media screen and (max-width: 640px) {
  .image-grid figure{flex: 0 0 50%;}
}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/no-inner-radius.webp" alt="Zero inner radius">
    <figcaption>Zero inner radius</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/slight-inner-radius.webp" alt="Slight inner radius">
    <figcaption>Slight inner radius</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/exact-inner-radius.webp" alt="Exact inner radius">
    <figcaption>Exact inner radius</figcaption>
  </figure>
</div>

Therefore there might be cases when the inner border-radius will differ from the outer one. Usually, this will happen when the `border-width` is greater than the `border-radius`, this will result in a right angle.

Luckily if you know how the inner border-radius is formed, you can apply certain changes that will help you to smooth out the looks of the inner border-radius.

There are a few ways to achieve that. Let's say there's an element with some content inside it.

HTML:
```html
<div class="content">
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
</div>
```

CSS:
```css
.content {
  border: 13px solid #333;
  border-radius: 10px;
}
```

Result:
<div style="border: 13px solid #333;border-radius: 10px">
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
</div>


## 1. Add a box-shadow property
For this trick, the `border` property must be removed and `box-shadow` must be added instead.

HTML:
```html
<div class="content">
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
</div>
```

CSS:
```css
.content {
  box-shadow: 0 0 0 13px #333;
  border-radius: 10px;
}
```

Result:
<div style="border-radius: 10px;box-shadow: 0 0 0 13px #333">
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
</div>

**NOTE:** `box-shadow` property goes outside the element's box model, this means that the element might get larger in size.

## 2. Add a container for content
Although the `box-shadow` gets the job done it is a bit hacky fix. Another more proper way to fix it is to add a wrapper for the content and set the `border-radius` property for it.
The value should be equal to a [CSS `calc()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/calc){:target="blank"}. The parameter for this function should be the expression based on the formula given above.

To actually make the inner border-radius effect a `background` property with a value equal to the border color must be set to the `.content` element.

For the `p` element, a `background` property must be set as well.

HTML:
```html
<div class="content">
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
</div>
```

CSS:
```css
.content {
  border: 13px solid #333;
  border-radius: 10px;
  background: #333;
}

.content p {
  border-radius: calc(13px - 10px);
  background: #fff;
  margin: 0;
}
```

Result:
<div style="border: 13px solid #333;border-radius: 10px;background: #333">
  <p style="border-radius: calc(13px - 10px);background: #fff;margin: 0">Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
</div>


## What about gradient?

If you wish to use a [gradient for your border](/gradient-border-css) then you should set a `background` property for the `.content` with `linear-gradient` as the `border-color` and the `padding` property as the `border-width`.

CSS:
```css
.content {
  border-radius: 10px;
  background: linear-gradient(45deg, purple, orange);
  padding: 10px;
}

.content p {
  border-radius: calc(13px - 10px);
  background: #fff;
  margin: 0;
}
```

Result:
<div style="border-radius: 10px;background: linear-gradient(45deg, purple, orange);padding: 10px;">
  <p style="border-radius: calc(13px - 10px);background: #fff;margin: 0">Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
</div>
