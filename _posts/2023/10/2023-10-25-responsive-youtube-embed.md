---
layout: post
permalink: responsive-youtube-embed
title: How to Create a Responsive YouTube Embed with Custom CSS for Adjustable Size
date: 2023-10-25T20:03:02.112Z
description: YouTube embeds are a great addition to a web page. In this guide, I'll show you how to make them responsive with a sprinkle of CSS.
tags: [css]
---

YouTube embeds are a great addition to a web page. In this guide, I'll show you how to make them responsive with a sprinkle of CSS.

By default, YouTube provides the following HTML code for video embeds.

```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/Ukg_U3CnJWI?si=9aST45sr3a1mrjKJ"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen
  >
</iframe>
```

<figure>
  <img class="shadow" loading="lazy" src="/images/misc/youtube-embed-code.webp" alt="YouTube embed code">
  <figcaption>YouTube embed code</figcaption>
</figure>

If you use the code above in your code, the YouTube video will remain at the fixed size of 560x315px no matter the viewport size.

It may look fine on larger screens but it won't fit on smaller screens:

<figure>
  <img class="shadow" loading="lazy" src="/images/misc/youtube-default-embed-on-mobile.webp" alt="YouTube embed with fixed size on mobile viewport">
  <figcaption>YouTube embed with fixed size on mobile viewport</figcaption>
</figure>

The problem is caused by the size attributes `width` and `height` on the `iframe` element.

There are a few ways how you can solve it.

## 1. Using the aspect-ratio property

First you need to remove the `width` and `height` attributes from the `iframe` and give it a custom class name e.g. `yt-embed`.

```html
<iframe
  class="yt-embed"
  src="https://www.youtube.com/embed/Ukg_U3CnJWI?si=9aST45sr3a1mrjKJ"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen
  >
</iframe>
```

Next you'll need to set the [`aspect-ratio`](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio){:target="_blank"} property for the `iframe` along with the 100% width.

```css
.yt-embed {
  aspect-ratio: 16 / 9;
  width: 100%;
}
```

The `aspect-ratio` property is a modern CSS way to set the size of a container. It is supported by all modern browsers.

<figure>
  <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio#browser_compatibility" target="_blank" rel="noreferrer noopener">
    <img class="shadow" src="/images/browser-support/css-aspect-ratio-browser-support.webp" alt="CSS aspect-ratio property browser support" loading="lazy">
  </a>
</figure>

<p class="note">💡 NOTE: Today the standard video aspect ratio is <em>16:9</em> (recommended by <a href="https://support.google.com/youtube/answer/6375112?co=GENIE.Platform%3DDesktop&amp;hl=en">YouTube</a> and <a href="https://vimeo.com/blog/post/aspect-ratios-explained/">Vimeo</a>).</p>

## 2. Using the padding hack

If for some reason you can't use the `aspect-ratio` property to make your ember responsive, you can use the so-called "padding hack".

Using this approach you'll need to wrap the `iframe` into a `div` element and you can leave the `width` and `height` attributes.

```html
<div class="yt-container">
  <iframe
    class="yt-embed"
    width="560"
    height="315"
    src="https://www.youtube.com/embed/Ukg_U3CnJWI?si=9aST45sr3a1mrjKJ"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen
    >
  </iframe>
</div>
```

To make it work in CSS you'll need to set the container `div` to `position: relative` with the `padding-top` (for aspect ratio) and the iframe to `position: absolute` and 100% of the size.

```css
.yt-container {
  position: relative;
  padding-top: 56.25%;
}

.yt-embed {
  position: absolute;
  top: 0;
  left:0;
  width: 100%;
  height: 100%;
}
```

## Conclusion

Your go-to solution should be using the modern CSS approach with the `aspect-ratio` property. The code is small and straightforward.

However, the “padding hack” approach is useful if you have to deal with older browsers where the `aspect-ratio` property is not supported. Also, it’s good to know if you come across it in the existing code base.

You can read more about the padding hack and aspect-ratio in my detailed [article](/css-aspect-ratio).
