---
layout: post
permalink: flip-box-card-css
title: How to create a flip box card with CSS
date: 2023-04-26T19:49:12.133Z
description: Learn how to create a cool looking card with flip effect on hover with pure CSS.
tags: [css]
---

Learn how to create a cool-looking card with a flip effect on hover with pure CSS.

As an example, we'll make a card that will look like a box with a heading and background image, and on hover, it will flip and show a backside with background color and text.

<style>
.flipbox {
  position: relative;
  width: 300px;
  height: 200px;
  margin: 30px auto;
  perspective: 1000px;
}

.flipbox .card {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  border-radius: 3px;
  box-shadow: 1px 5px 13px 2px rgba(0,0,0,0.3);
  color: #fff;
  text-align: center;
  backface-visibility: hidden;
  transition: transform .5s ease-in-out;
  transform-style: preserve-3d;
}

.flipbox-front {
  transform: rotateY(0deg);
  background: url("https://plus.unsplash.com/premium_photo-1674593231084-d8b27596b134?crop=entropy&cs=srgb&fm=jpg&ixid=MnwzMjM4NDZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2ODI1MzU1OTc&ixlib=rb-4.0.3&q=85") no-repeat center;
  background-size: cover;
}

.flipbox-back {
  transform: rotateY(180deg);
  padding: 10px;
  font-size: 17px;
  line-height: 1.5;
  background: #9e8ed9;
}

.flipbox:hover .flipbox-front {
  transform: rotateY(-180deg);
}

.flipbox:hover .flipbox-back {
  transform: rotateY(0deg);
}

.flipbox h2 {
  margin: 0;
  font-size: 30px;
  text-shadow: 2px 2px rgba(0,0,0,0.2);
}
</style>
<div class="flipbox">
  <div class="card flipbox-front">
    <h2>Hello, World!</h2>
  </div>
  <div class="card flipbox-back">
    <p>PER ASPERA <br>AD ASTRA</p>
  </div>
</div>

## Markup

To begin with, we need to create the markup for both sides, let's name them the front side and the back side.

Inside a `div` with a `flipbox` class, we'll make two more: `flipbox-front` and `flipbox-back`. Each of them will hold some content.

```html
<div class="flipbox">
  <div class="card flipbox-front">
    <h2>Hello, World!</h2>
  </div>
  <div class="card flipbox-back">
    <p>PER ASPERA <br>AD ASTRA</p>
  </div>
</div>
```

## Styling

Now for the styling. First, we'll set the dimensions of our flip card. Apart from that, we'll also need to specify the [`perspective` property](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective){:target="_blank"}. It will give some depth (3D perspective) when flipping the box.

```css
.flipbox {
  position: relative;
  width: 300px;
  height: 200px;
  margin: 80px auto;
  perspective: 1000px;
}
```

Next, we need to position each side relative to our flip box. As well as to set the [`backface-visibility` property](https://developer.mozilla.org/en-US/docs/Web/CSS/backface-visibility){:target="_blank"} to [hide the backside](https://codepen.io/nikitahl/pen/LYOGKvj) of each card and [`transform-style` property](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-style){:target="_blank"} for the 3D effect.

```css
.card {
  /* car position relative to flip box */
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;

  /* card styling */
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 3px;
  box-shadow: 1px 5px 13px 2px rgba(0,0,0,0.3);
  color: #fff;

  /* hide backside and position for 3D space */
  backface-visibility: hidden;
  transform-style: preserve-3d;

  /* make a smooth transition */
  transition: transform .5s ease-in-out;
}
```

Each card will have a background style along with a `transform` property that will change on the hover effect. We'll rotate the backside by 180 degrees, thus on the other side.

```css
.flipbox-front {
  transform: rotateY(0deg);
  background: url("https://plus.unsplash.com/premium_photo-1674593231084-d8b27596b134?crop=entropy&cs=srgb&fm=jpg&ixid=MnwzMjM4NDZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2ODI1MzU1OTc&ixlib=rb-4.0.3&q=85") no-repeat center;
  background-size: cover;
}

.flipbox-back {
  transform: rotateY(180deg);
  padding: 10px;
  font-size: 17px;
  line-height: 1.5;
  background: #9e8ed9;
}
```

Finally let's set a hover effect on a `flipbox` element where we'll change the `transform` property for each side.

```css
.flipbox:hover .flipbox-front {
  transform: rotateY(-180deg);
}

.flipbox:hover .flipbox-back {
  transform: rotateY(0deg);
}
```

## Demo

You can find a full demo with a complete code examples on my CodePen:

<p class="codepen" data-height="444" data-default-tab="result" data-slug-hash="LYgyyoy" data-user="nikitahl" style="height: 444px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/LYgyyoy">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
