---
layout: post
permalink: css-aspect-ratio
title: Aspect ratio with CSS aka the padding hack
date: 2021-01-22T09:41:17.020Z
description: Aspect ratio is a great way to give a consistent and appealing look
  to your media content. This guide explains how to implement an aspect ratio
  with CSS.
tags:
  - css
---

When working with media whether it's an image or a video, sometimes you have to preserve its initial proportions (aspect ratio). In this guide, I'll try to explain how exactly you can achieve such a result with CSS.

## What is the aspect ratio?

Usually, when talking about an [aspect ratio](https://en.wikipedia.org/wiki/Aspect_ratio_(image)) it implies a display or a screen. It's a ratio of width to height. Most popular are *16:9* (standard for HDTV) and *4:3* (standard TV). So for the *16:9* aspect ratio, it means that the ratio is 16 units of width to 9 units of height.

In order to implement aspect ratio in CSS, the so-called *"padding hack"* must be used. This means that a `padding-top` or `padding-bottom` property must be set on an element with the calculated percentage value that represents the aspect ratio.

## Calculation

In order to calculate the value for the padding property, you'll need to make a division of the ratio values and multiply it by 100%.

E.g.: 

* *16:9* aspect ratio will result in `9 / 16 * 100% = 56.25%`;
* *4:3* aspect ratio will result in `3 / 4 * 100% = 75%`;
* *1:1* aspect ratio will result in `1 / 1 * 100% = 100%`.

So to apply it for a `div` element:

```css
.aspect-ratio--16-9 {
  overflow: hidden;
  padding-top: 56.25%;
  background-image: linear-gradient(45deg, #7f14c1, #80fbfb);
}
```

The resulted element below will now always maintain the *16:9* aspect ratio no matter the screen size:

<style>
  .demo-box { margin: 0 0 30px }
  .aspect-ratio--16-9 {
    overflow: hidden;padding-top: 56.25%;background-image: linear-gradient(45deg,#7f14c1, #80fbfb);
  }
  .aspect-ratio--image {
    overflow: hidden;padding-top: 56.25%;background: url("") no-repeat center;background-size: cover;
  }
  .video-container, .embed-container {
  position: relative;padding-top: 56.25%;
  }
  .video, .embed-vimeo {
    position: absolute;top: 0;left:0;width:100%;height: 100%;object-fit: cover;margin:0 !important;
  }
</style>

<div class="aspect-ratio--16-9 demo-box"></div>

## Use cases

### Images

Images comes with a fixed size thus fixed aspect ratio. Consider following image, its size is 1920x1585.

<figure>
  <img class="shadow lozad" data-src="/images/misc/city-skyline.jpg" alt="City Skyline">
  <noscript>
    <img class="shadow" src="/images/misc/city-skyline.jpg" alt="City Skyline">
  </noscript>
  <figcaption>
    <span>Photo by <a href="https://unsplash.com/@karlkoehler?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Karl Köhler</a> on <a href="https://unsplash.com/s/photos/skyline?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
  </figcaption>
</figure>

If you change its width or height to match the desired aspect ratio, the image will become skewed as it has a fixed aspect ratio.

However, you can set the image as a background for a `div` container, and provide the container with an aspect ratio.

```css
.aspect-ratio--16-9 {
  overflow: hidden;
  padding-top: 56.25%;
  background: url('city-skyline.jpg') no-repeat center;
  background-size: cover;
}
```

The image will lose its initial size but will take up the remaining space evenly and maintain the aspect ratio.

**NOTE: Setting an image as a background is not a good practice to display an image as it is not friendly to assistive technologies. The background image should be set only for [decorative purposes](https://www.w3.org/WAI/GL/2016/WD-WCAG20-TECHS-20160105/F39).**

**Result**:

<div class="aspect-ratio--image demo-box lozad" data-background-image="/images/misc/city-skyline.jpg"></div>

### Videos

Videos are another media format that requires proper styling on a page in order to have a more appealing display. Today the standard video aspect ratio is *16:9* (recommended by [YouTube](https://support.google.com/youtube/answer/6375112?co=GENIE.Platform%3DDesktop&hl=en) and [Vimeo](https://vimeo.com/blog/post/aspect-ratios-explained/)).

To give your video an aspect ratio we'll use the *"padding hack"* along with some other properties.

The markup consists of a container `div` and a `video` element inside it and will look as follows:

```html
<div class="video-container">
  <video class="video" src="runner.mp4" controls />
</div>
```

The container will have a `padding-top` property for the aspect ratio. The `video` element has to have `position: absolute` in order to fit inside the container. Also the `object-fit: cover` and the `height: 100%` properties have to be applied in order for the `video` element to fill up the empty space.

```css
.video-container {
  position: relative;
  padding-top: 56.25%;
}

.video {
  position: absolute;
  top: 0;
  left:0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

**Result**:

<div class="video-container demo-box">
  <video class="video lozad" data-src="/videos/runner.mp4" controls />
</div>

<p class="figcaption">
  <span>Video by <a href="https://pixabay.com/pt/users/coverr-free-footage-1281706/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=10809">Coverr-Free-Footage</a> from <a href="https://pixabay.com/pt/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=10809">Pixabay</a></span>
</p>

### Embeds

Embeds are a popular way to include images and videos from a 3rd party websites, like Vimeo for videos or Pinterest for images. Embed is an `iframe` element. In this case to give an `iframe` an aspect ratio, we can use the same approach as for videos.

In the example below let's embed a Vimeo video. Markup:

```html
<div class="embed-container">
  <iframe class="embed-vimeo" src="https://player.vimeo.com/video/82931517" width="640" height="360" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
</div>
<p>
  <a href="https://vimeo.com/82931517">Light Goes On</a> from <a href="https://vimeo.com/dariustwin">Darren Pearson</a> on <a href="https://vimeo.com">Vimeo</a>.
</p>
```

CSS will be the same as for video:

```css
.embed-container {
  position: relative;
  padding-top: 56.25%;
}

.embed-vimeo {
  position: absolute;
  top: 0;
  left:0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

**Result**:

<div class="embed-container demo-box">
  <iframe class="embed-vimeo lozad" data-src="https://player.vimeo.com/video/82931517" width="640" height="360" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
</div>
<p class="figcaption">
  <a href="https://vimeo.com/82931517">Light Goes On</a> from <a href="https://vimeo.com/dariustwin">Darren Pearson</a> on <a href="https://vimeo.com">Vimeo</a>.
</p>

## The CSS aspect-ratio property

CSS has an [`aspect-ratio`](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio) property that can be used natively to avoid the *"padding hack"*. This property does essentialy what you'd expect it to do, apply aspect ratio to an element.

The `aspect-ratio` property was officially released in [Chrome 88](https://twitter.com/smashingmag/status/1351902173307744256) while for [other browsers](https://caniuse.com/mdn-css_properties_aspect-ratio) it is unavailable or available only under a flag (you'll have to manually enable it via browser settings).

So instead of the `padding-top` property you can use the `aspect-ratio`.

Example:

```css
.aspect-ratio-container {
  aspect-ratio: 16 / 9;
}
```

## Conclusion

Use the *"padding-hack"* approach to showcase your content in an appealing way. It will always scale along with the user's viewport and maintain a consistent aspect ratio. It works across all browsers.

On the other hand, keep an eye on the `aspect-ratio` CSS property as it will be the future way to go. You can already experiment with it.