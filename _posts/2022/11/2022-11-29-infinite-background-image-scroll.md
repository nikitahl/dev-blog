---
layout: post
permalink: infinite-background-image-scroll
title: Seamless infinite background image scroll animation with CSS
description: To create a non-stop background image scroll animation (without cuts, breaks, or jumps) will require a quite simple solution. 
tags: [css]
---

CSS allows you to create really cool stuff, like infinite background image scroll animation. And it will require a relatively simple solution.

In this example, we’ll create a section with a background image that will scroll horizontally from right to left.

To create a non-stop background image scroll animation (without cuts, breaks, or jumps) you'll need to create a container for the animation itself and set a background image you’re willing to scroll.

**HTML:**

```html
<div class="container"></div>
```

Since the container will be empty we’ll need to set its dimensions `width` and `height` properties. Additionally `max-width` property so it adapts for mobile screens and `margin` to center it.

```css
.container {
  width: 500px;
  height: 300px;
  max-width: 80%;
  margin: 10px auto;
}
```

Next, let’s specify the background image via the `background` property and its size. We’ll need the fixed size, to later move it by the same amount via `animation`.

The background image should also have a `repeat-x` value set and the size to match the container dimensions.

```css
background: url(https://images.unsplash.com/photo-1667937026547-1b7cce7525b7?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwzMjM4NDZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2Njk3NTIzNzE&ixlib=rb-4.0.3&q=80) repeat-x;
background-size: 500px 300px;
```

We’ll be animating the `background-position` property with the [`@keyframe` rule](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes){:target="blank"}. Inside the `@keyframe` rule for animation, we’ll set the single step `to` (or `100%`).

This means it will animate the background from the initial `background-position` value to  `-500px 0`, hence moving the background 500px to the left.

```css
@keyframes scroll {
  to {
    background-position: -500px 0;
  }
}
```
As for the container, we can specify the `animation` shorthand property. For smooth non-stop animation make sure to set the `timing-function` to `linear` and the `iteration-count` to `infinite`.

```css
animation: scroll 4s linear infinite;
```

The final code looks as follows:

```css
.container {
  width: 500px;
  height: 300px;
  margin: 50px auto;

  background: url(https://images.unsplash.com/photo-1667937026547-1b7cce7525b7?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwzMjM4NDZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2Njk3NTIzNzE&ixlib=rb-4.0.3&q=80) repeat-x;
  background-size: 500px 300px;
  
  animation: scroll 4s linear infinite;
}


@keyframes scroll {
  to {
    background-position: -500px 0;
  }
}
```

## Demo

Working demo with code can be found on CodePen:

<p class="codepen" data-height="485.27618408203125" data-default-tab="result" data-slug-hash="poKOJpa" data-user="nikitahl" style="height: 485.27618408203125px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/poKOJpa">
  Background image scroll</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

