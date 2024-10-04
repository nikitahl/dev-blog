---
layout: post
permalink: simple-css-carousel-slider
title: Simple carousel-like slider with pure CSS
date: 2024-10-04T09:08:12.102Z
description: Learn how to create a sleek, autoplaying CSS-only carousel that smoothly scrolls through items and pauses on hover, without the need for any JavaScript or controls.
tags: [css]
---

In this article, I'll show you how to build a simple yet elegant CSS-only carousel slider for smooth, automatic scrolling.

Unlike [other carousels](/scroll-snap-css) that allow users to manually scroll, this one will autoplay infinitely, pausing on hover.

It won’t have any controls; it will just scroll smoothly from side to side, highlighting specific items.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/css-carousel.gif" alt="CSS carousel example">
</figure>

## Markup

I will wrap the carousel element inside a wrapper that spans the full width of the page. This wrapper is essential for properly positioning the carousel and ensuring it takes up the entire page width.

Let’s use a `section` element with a class name of `carousel-section`, as it may also contain other content, such as text and images.

```html
<section class="carousel-section">
  <div class="css-carousel">
    ...
  </div>
</section>
```

For the sake of this example, I'll use plain images as carousel slides, but any other content can be used as well.

```html
<section class="carousel-section">
  <div class="css-carousel">
    <figure>
      <img src="img-1.png" alt="First slide">
    </figure>
    <figure>
      <img src="img-2.png" alt="Second slide">
    </figure> 
    <figure>
      <img src="img-3.png" alt="Third slide">
    </figure> 
    <!-- Add more images below ... -->
  </div>
</section>
```

Once you've added the necessary markup, make sure to include enough slide elements so that the carousel has sufficient content to scroll through.

## Styles

To make this carousel function properly, the first step is to add `overflow: hidden` to the wrapper element.

```css
.carousel-section {
  overflow: hidden;
}
```

For the carousel element, the slides need to align horizontally and occupy the full width. We'll use `display: flex` along with a few other rules to improve its appearance.

```css
.css-carousel {
  display: flex;
  align-items: stretch;
  gap: 3px;
}
```

We'll need to specify both the width and height for the image elements.

```css
.css-carousel img {
  display: inline-block;
  margin: 0;
  padding: 0;
  width: 400px;
  height: 100%;
}
```

The objective of this carousel is to scroll infinitely. We can make it move from one end to the other, looping back continuously.

The trickiest part is specifying the correct value at which the carousel will scroll. This value represents the portion of the carousel that extends outside the viewport.

To calculate this <u>offset</u> value, we'll use a mathematical formula. The final value must be negative, as the carousel will start moving to the left along the X-axis.

```
O - offset
SW - slide width
SC - slice count
VW - viewport width (in percent)

O = -(SW × SC) - VW
```

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/carousel-structure.webp" alt="Carousel structure on a page">
  <figcaption>Carousel structure on a page</figcaption>
</figure>

We'll use [CSS custom properties (variables)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties){:target="_blank"} and the [`calc()`](https://developer.mozilla.org/en-US/docs/Web/CSS/calc){:target="_blank"} function to compute the offset value.

<p class="note">
💡 NOTE: To make the offset value negative, we’ll subtract it from 0.
</p>

```css
:root {
  --slide-count: 6; /* number of slides in the carousel */
  --slide-width: 400px; /* width of a single slide */
  --carousel-edge-pos:
      calc( 0% - ((var(--slide-width) * var(--slide-count)) - 100%) ); /* formula to calulate the offset value */
}
```

Lastly, we'll add an animation to the carousel element and enable it to pause on hover.

The animation will manipulate the `translateX` property, causing the carousel to move horizontally.

```css
.css-carousel {
  /* ... */
  -webkit-overflow-scrolling: touch;
  animation: scroll 40s linear alternate infinite;
  animation-play-state: running;
}

.css-carousel:hover {
  animation-play-state: paused;
}

@keyframes scroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(var(--carousel-edge-pos));
  }
}
```

Complete CSS code:

```css
:root {
  --slide-count: 6; /* number of slides in the carousel */
  --slide-width: 400px; /* width of a single slide */
  --carousel-edge-pos:
      calc( 0% - ((var(--slide-width) * var(--slide-count)) - 100%) ); /* formula to calulate the offset value */
}

.carousel-section {
  overflow: hidden;
}

.css-carousel {
  display: flex;
  align-items: stretch;
  gap: 3px;

  -webkit-overflow-scrolling: touch;
  animation: scroll 40s linear alternate infinite;
  animation-play-state: running;
}

.css-carousel:hover {
  animation-play-state: paused;
}

.css-carousel img {
  display: inline-block;
  margin: 0;
  padding: 0;
  width: var(--slide-width);
  height: 100%;
}

@keyframes scroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(var(--carousel-edge-pos));
  }
}
```

## Demo

You can find a full demo with a complete code example on my CodePen. The demo also includes additional styling to enhance the appearance and functionality of the carousel:

<p class="codepen" data-height="438.140380859375" data-default-tab="result" data-slug-hash="NWQxvJN" data-pen-title="Untitled" data-preview="true" data-user="nikitahl" style="height: 438.140380859375px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/NWQxvJN">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
