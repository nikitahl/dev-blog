---
layout: post
permalink: scroll-snap-css
title: Create beautiful carousels with scroll snap CSS property
date: 2023-02-24T12:30:24.232Z
description: You can create beautiful carousels with a fancy and smooth snap effect by implementing a CSS-only solution.
tags: [css]
---

You can create beautiful carousels with a fancy and smooth snap effect by implementing a CSS-only solution.

The scroll snap effect means that each time a user finishes scrolling an element will be snapped to the edge of the scroll container.

This effect looks especially good on mobile devices, both for vertical and horizontal scrolling.

## CSS snap properties

To add a basic scroll snap for a container with the scroll you’ll need to define one single property.

```css
.scroll-container {
  scroll-snap-type: x mandatory;
}
```

> The [`scroll-snap-type` CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-type) sets how strictly snap points are enforced on the scroll container in case there is one.

There are a few options available for the `scroll-snap-type` property.

To specify the axis use `x` - horizontal or `y` - vertical value, and for behavior use `mandatory` - will always snap to the next element after the scroll action, `proximity` - will snap to the next element when the scroll ends in the near proximity of a snap point.

For the child elements, you should specify the `scroll-snap-align` which will set the snap position of the element. The values can be `start`, `end`, or `center`.
```css
.scroll-child {
  scroll-snap-align: start;
}
```
You can apply additional properties to customize the scroll behavior.

For the scroll container, you can add a `scroll-padding`. This property will create an offset by the edge of the scroll container. It comes in handy when there is an overlying element, like a sticky header.

```css
.scroll-container {
  scroll-snap-type: y mandatory;
  scroll-padding: 30px;
}
```

For child elements, you can add a `scroll-margin`. This property represents the outset from the corresponding edge of the scroll container.

```css
.scroll-child {
  scroll-snap-align: start;
  scroll-margin: 10px;
}
```

The scroll snap properties are fully supported by all modern browsers:

<figure class="figure-centered">
  <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-type#browser_compatibility" target="_blank" rel="noreferrer noopener">
    <img class="shadow" src="/images/browser-support/scroll-snap-browser-support.webp" loading="lazy" alt="Scroll snap browser support">
  </a>
  <figcaption>Scroll snap browser support</figcaption>
</figure>

## Creating a carousel

For this example, we’ll create a small horizontal carousel that will showcase a list of cards with programming courses.

The HTML structure of a carousel is pretty simple. A `div` container with child elements.

```html
<div class="carousel">
  <div class="carousel-item"></div>
  <div class="carousel-item"></div>
  <div class="carousel-item"></div>
</div>
```

<p class="note">💡 NOTE: for accessibility concerns, you can use <code>role="list"</code> on a <code>div</code> and <code>role="listitem"</code> for child elements. However, it is recommended to <a href="/why-it-is-important-to-write-semantic-html">use semantic elements</a> like <code>ul</code> or <code>ol</code> lists.</p>

The carousel will have a fixed width, explicit `overflow` property with `scroll` value, some paddings, and a flex display, to order items horizontally. To make space between the items the `gap` property of 10px is applied.

The item will have a `flex` property set to define the width and a few others to make it look fancy. To compensate for the gap, and align the item lets set a `scroll-margin` with a `5px`.

```css
.carousel {
  /* appearance */
  display: flex;
  gap: 10px;
  width: 580px;
  max-width: 90%;
  margin: 50px auto;
  padding: 10px;
  overflow-x: scroll;
  /* snap */
  scroll-snap-type: x mandatory;
}

.carousel-item {
  /* appearance */
  flex: 1 0 250px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px 1px #ccc;
  color: #444;
  /* snap */
  scroll-snap-align: start;
  scroll-margin: 5px;
}

```
 
## Demo

The end result with complete code can be viewed on CodePen:

<p class="codepen" data-height="450" data-default-tab="result" data-slug-hash="RwYRBBz" data-user="nikitahl" style="height: 450px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/RwYRBBz">
  Carousel</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
