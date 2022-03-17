---
layout: post
permalink: defer-css-and-javascript
title: Modern way to defer CSS and JavaScript resources to improve page load speed
description: Learn how to defer CSS and JavaScript resources to improve page load speed using only HTML code
tags: [performance]
---

To improve your page load speed you can defer CSS and JavaScript resources by tweaking only the HTML code of the page.

1. [Defer CSS](#defer-css)
2. [Defer Media](#defer-media)
3. [Defer JavaScript](#defer-javascript)

Resources like CSS, fonts, and JavaScript are considered [render-blocking](https://web.dev/render-blocking-resources/). This means that the browser takes time to load them before actually rendering the contents of the page.

So the larger the file size of these resources the longer it takes to load them, the longer it takes for the user to see the contents of the page.

To check your page load speed and render-blocking resources you can use the [Lighthouse](https://developers.google.com/web/tools/lighthouse/) tool right in the browser (Chrome). This is one of the [essential tools](/tools-for-frontend-developers#web-performance) to measure web performance.

To prevent render-blocking resources from slowing down your page, you can implement the small HTML changes listed below to tackle this issue.

## Defer CSS

The proper way to handle CSS load is to split your styles into critical and non-critical CSS.

* **critical** - these styles are required to show immediate content, the one user sees once the page loads ([above the fold](https://www.abtasty.com/blog/above-the-fold/)).
* **non-critical** - these styles are used for the content that is not immediately visible (below the fold), thus can be loaded later.

For critical CSS you can define styles in the `style` tag at the head of your page:

```html
<style type="text/css">
  .site-headline {
    font-size: 42px;
    font-weight: 600;
    color: #444;
    line-height: 1.75;
    letter-spacing: 0.3px;
  }
</style>
```
And then load the rest of the styles asynchronously, by adding additional attributes for the `link` tag.

```html
<link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
```

To break it down:

1. The [`preload`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload) value of the `rel` attribute tells the browser to load resources as soon as requires for the rendering of the page.
2. The [`as`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link#attr-as) attribute specifies the type of content being loaded by the `<link>`.
3. The `onload` attribute processes CSS loading. After it sets the `onload` handler to `null` to avoid repeated calling and changes the `rel` attribute value.

**NOTE: Use a `noscript` tag with a standard `link` as a fallback solution for cases when JavaScript is not executed.**

```html
<noscript><link rel="stylesheet" href="styles.css"></noscript>
```

## Defer Media

You can lazy load media, to further improve the load speed of your page. Lazy load means media like images will load only when a user scrolls near it.

### Images and iframes

You can add a [`loading="lazy"`](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading#images_and_iframes) attribute for `img` or `iframe` tag.

```html
<img src="funny-cat.png" alt="Funny cat" loading="lazy">
<iframe src="https://youtu.be/AActXSWxsRo" title="Lazy Loading images" loading="lazy"></iframe>
```

### Video and audio

For [`video`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video#attr-preload) and [`audio`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio#attr-preload) tags you can add a `preload="none"` attribute.

**NOTE: The `preload="none"` will not work with the `autoplay` attribute.**

```html
<video preload="none">
  <source src="funny-cat.webm" type="video/webm">
  <source src="funny-cat.mp4" type="video/mp4">
</video>
```

While it is better to use native HTML attributes to defer images and other media, they still lack full browser support and customizability (e.g. you cannot lazy load a background image). You can check how to implement lazy loading in my [article](/lazy-load-images) explaining it in detail.

## Defer JavaScript

To avoid deferring scripts, you should include them just before the closing `body` tag. But that's not always the case. You may want to fetch data or include analytics before or during the content rendering.

To defer scripts you can use one of two HTML attributes:
* `defer`
* `async`

The [`defer`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-async) attribute means the script will "load in the background" and it will not block content rendering. The script will execute on [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event) event.

```html
<p>...content before script...</p>

<script defer src="scripts/fetch-data.js"></script>

<!-- visible immediately -->
<p>...content after script...</p>
```

The [`async`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-defer) attribute means the script will be loaded in parallel with the content rendering and will be immediately available for execution.

```html
<!-- Google Analytics is usually added like this -->
<script async src="https://google-analytics.com/analytics.js"></script>
```

For more details and the differences between the `defer` and `async` attributes I highly recommend the [javascript.info article](https://javascript.info/script-async-defer).
