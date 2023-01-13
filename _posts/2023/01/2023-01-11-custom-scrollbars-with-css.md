---
layout: post
permalink: custom-scrollbars-with-css
title: Create custom scrollbars with pure CSS
date: 2023-01-13T09:00:24.232Z
description: To make your UI consistent across different browsers you can create custom scrollbars on your website with a sprinkle of pure CSS
tags: [css]
---

To make your UI consistent across different browsers you can create custom scrollbars on your website with a sprinkle of pure CSS. However there are some exceptions, let's find out more below.

The way scrollbars appear in UIs has evolved over the years. And each system has its own way of displaying scrollbars. A WebDesignMuseum has captured this evolution and shared it in a tweet:

<figure class="figure-centered">
  <a href="https://twitter.com/WebDesignMuseum/status/1455910134639579151" target="_blank" rel="noreferrer noopener">
    <img class="shadow" src="/images/misc/webdesignmuseum-scrollbars-tweet.png" loading="lazy" alt="Web Design Museum scrollbars tweet">
  </a>
  <figcaption>Interactive evolution of the scrollbar via Web Design Museum</figcaption>
</figure>

A scrollbar has the following structure.

<figure class="figure-centered">
  <img class="shadow" src="/images/misc/scrollbar-structure.png" loading="lazy" alt="Scrollbar structure">
  <figcaption>Scrollbar structure</figcaption>
</figure>

Each part of the structure can be styled via pseudo-class. Now, these pseudo-classes are only supported by browsers like [Chrome, Edge, and Safari](https://caniuse.com/mdn-css_selectors_-webkit-scrollbar){:target="blank"}. Firefox has a slightly different approach that we’ll look at in a moment. But first, let's explore the way to style the scrollbar in all the other browsers.

You can set all scrollbars on the page to a root element by using the [`::-webkit-scrollbar`](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-scrollbar){:target="blank"} pseudo-class without any additional selector:

```css
/* Scrollbar width */
::-webkit-scrollbar {
  width: 8px;
}

/* Scrollbar track */
::-webkit-scrollbar-track {
  background: #2a2a2a;
  box-shadow: inset 0 0 3px rgba(0, 0, 0, 0.5);
}

/* Scrollbar handle (thumb) */
::-webkit-scrollbar-thumb {
  border-radius: 5px;
  background-image: linear-gradient(orangered, rebeccapurple);
}

/* Scrollbar handle on hover */
::-webkit-scrollbar-thumb:hover {
  background-image: linear-gradient(tomato, purple);
}
```

The `::-webkit-scrollbar` pseudo-classes allow you to use almost any CSS property, thus you can make your scrollbar look really fancy.

On the other hand, the scrollbar styling on Firefox differs from the previous example and is much more scarce in options. To apply styles for the scrollbar in the Firefox browser you can use the `scrollbar-width` and `scrollbar-color` [properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Scrollbars){:target="blank"}.

```css
:root {
  scrollbar-color: rebeccapurple #222;
  scrollbar-width: thin;
}
```
As you can see the `scrollbar-color` property accepts two colors. The first value applies to the thumb of the scrollbar, and the second to the track. The values can be only colors (names, hex, rbg, etc.), that means you cannot use gradients.

The `scrollbar-width` property accepts values like `auto`, `thin`, and `none`. That means that the browser will define the width, which means less customization options for you.

The [`scrollbar-width`](https://caniuse.com/mdn-css_properties_scrollbar-width){:target="blank"} and [`scrollbar-color`](https://caniuse.com/mdn-css_properties_scrollbar-color){:target="blank"} properties are only supported by FireFox.

## Demo

You can check out a full solution with code and live example on my CodePen:

<p class="codepen" data-height="300" data-default-tab="result" data-slug-hash="abjWrjW" data-user="nikitahl" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/abjWrjW">
  Scrollbar properties</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>


## A cross-browser solution

Although CSS solution to style the scrollbar has its limitations at the moment, like full cross-browser support and possibly a lack of additional options. You can create some really nice solutions with a little bit of JavaScript.

There are quite a few JavaScript libraries that allow you to create fully customized cross-browser and cross-platform scrollbars. 

Below I’ve prepared a list of popular Open Source libraries for custom scrollbars:

1. [FakeScroll](https://github.com/yairEO/fakescroll){:target="blank"}
2. [jScrollPane](https://github.com/vitch/jScrollPane){:target="blank"}
3. [gemini-scrollbar](https://github.com/noeldelgado/gemini-scrollbar){:target="blank"}
4. [OverlayScrollbars](https://github.com/KingSora/OverlayScrollbars){:target="blank"}
5. [SimpleBar](https://github.com/Grsmto/simplebar){:target="blank"}
6. [react-scrollbars-custom](https://github.com/xobotyi/react-scrollbars-custom){:target="blank"}




