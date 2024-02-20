---
layout: post
permalink: text-gradient-with-css
title: Text gradient with pure CSS
date: 2023-03-29T19:20:12.133Z
description: Text with a gradient background effect is a nice way to display headings on your website, and it can be done with pure CSS
tags: [css]
---

Text with a gradient background effect is a nice way to display headings on your website, and it can be done with pure CSS.

The text can be contained in any HTML tag, whether it's a heading `h1` to `h6`, paragraph `p`, or even a `div`.

For the sake of example let's use the `h2` tag.

```html
<h2>Hello World!</h2>
```

To apply a gradient for a text we'll need to use a `background-image` property with a gradient and a `background-clip` property with `text` value to specify where the background extension limit is. Also to make the gradient visible, we need to set the transparent color.

<p class="note">💡  NOTE: For Chrome-based browsers the <code>text</code> value is only supported by <code>-webkit-background-clip</code> (and not by <code>background-clip</code>).</p>

```css
h2 {
  background-image: linear-gradient(45deg,#ff7200,#5c00ff);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
```

**Result:**
<style>
  .gradient-text {
    position: relative;
    margin: 0;
    font-size: 45px;
    background-image: linear-gradient(45deg,#ff7200,#5c00ff);
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
  }

  .gradient-text--hover:hover {
    background-image: linear-gradient(45deg,#5c00ff,#ff7200);
  }

  .gradient-text--hover-smooth::before {
    content: 'Hello World!';

    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    background-image: linear-gradient(45deg,#5c00ff,#ff7200);

    transition: opacity 0.5s ease-in-out;
    opacity: 0;
  }

  .gradient-text--hover-smooth:hover::before {
  opacity: 1;
}
</style>
<h2 class="gradient-text">Hello World!</h2>

That's it. The [`background-clip` property](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip){:target="_blank"} is supported in all modern browsers:

<figure class="figure-centered">
  <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip#browser_compatibility" target="_blank" rel="noreferrer noopener">
    <img class="shadow" src="/images/browser-support/background-clip-browser-support.webp" loading="lazy" alt="Browser support for CSS background-clip property">
  </a>
</figure>

## Hover state

To go a bit further, you can add a hover effect by changing the gradient via the `background-image` property. You can reverse the gradient colors.

```css
h2:hover {
  background-image: linear-gradient(45deg,#5c00ff, #ff7200);
}
```

**Result:**

<h2 class="gradient-text gradient-text--hover">Hello World!</h2>

<p class="note">💡  NOTE: However in CSS you cannot transition gradients. If you want to add a smooth gradient transition on hover, you'll have to implement a <a href="https://keithjgrant.com/posts/2017/07/transitioning-gradients/" target="_blank" rel="noreferrer noopener">solution with pseudo-classes</a> as described by Keith J. Grant.</p>

To apply a smooth transition, set your text tag to `position: relative`.

For the pseudo-element, make it absolutely position, and have the same gradient properties, but most important it's `content` property should be equal to the actual text.

Finally, on hover, you change the `opacity`.

```css
h2 {
  position: relative;

  background-image: linear-gradient(45deg,#ff7200,#5c00ff);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

h2::before {
  content: 'Hello World!';

  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  background-image: linear-gradient(45deg,#5c00ff,#ff7200);

  transition: opacity 0.5s ease-in-out;
  opacity: 0;
}

h2:hover::before {
  opacity: 1;
}
```

**Result:**

<h2 class="gradient-text gradient-text--hover-smooth">Hello World!</h2>

## Demo

You can find a full demo with a complete code example on my CodePen:

<p class="codepen" data-height="340" data-default-tab="result" data-slug-hash="zYJXwOa" data-user="nikitahl" style="height: 340px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/zYJXwOa">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
