---
layout: post
permalink: smooth-scroll-to-anchor
title: Full page navigation with smooth scroll to anchor (CSS and JavaScript solution)
date: 2021-06-24T21:24:28.237Z
description: Create a full page navigation with smooth scroll to anchor. It can
  be done with pure CSS or JavaScript solution.
tags: [css, javascript]
---

A smooth scroll to anchor is a common concept for single-page applications. It features a sliding animation effect that helps the user to understand what’s currently is happening on the device screen. There are two ways you can implement it:

1. [CSS solution](#smooth-scroll-with-css);
2. [JavaScript solution](#smooth-scroll-with-javascript);
3. [Libraries](#smooth-scroll-with-library).

## Smooth scroll with CSS

The easiest way to achieve a smooth scroll effect is to add a CSS rule called [`scroll-behavior`](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior) to the whole document (the `html` tag).

However, this rule is applicable for any scrollable container, so you can add this feature only to a specified part of your page.

The full-page navigation with a smooth scroll effect to the anchor would look as follows:

**HTML**:

```html
<nav>
  <a href="#section-one">One</a>
  <a href="#section-two">Two</a>
  <a href="#section-three">Three</a>
</nav>

<section id="section-one">Section one</section>
<section id="section-two">Section two</section>
<section id="section-three">Section three</section>
```

**CSS**:

```css
html {
  scroll-behavior: smooth;
}
```

**Demo on CodePen**:

<p class="codepen" data-height="440" data-default-tab="result" data-slug-hash="WNpVpVd" data-user="tippingpointdev" style="height: 440px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/WNpVpVd">
  Smooth scroll navigation</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

Now if you have a fixed header, it’s a good idea to add a [scroll-margin](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-margin) property that will define the offset of the visible element that is being scrolled to. So for our navigation, we can set the `scroll-margin-top` property to all of the sections that will be equal to the height of the navbar, e.g. 50px.

```css
.section {
  scroll-margin-top: 50px;
}
```

**Browser support for `scroll-behavior`**:
<p class="ciu_embed" data-feature="css-scroll-behavior" data-periods="future_1,current,past_1" data-accessible-colours="false"> <picture> <source type="image/webp" srcset="https://caniuse.bitsofco.de/image/css-scroll-behavior.webp"> <source type="image/png" srcset="https://caniuse.bitsofco.de/image/css-scroll-behavior.png"> <img src="https://caniuse.bitsofco.de/image/css-scroll-behavior.jpg" alt="Data on support for the css-scroll-behavior feature across the major browsers from caniuse.com"> </picture> </p>

## Smooth scroll with JavaScript

JavaScript has a built-in [`scrollIntoView()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView) method to scroll to any element, even if it doesn’t have the `id` attribute. This can be useful in custom cases, like reacting to an event.

This method is being called upon the target element:

```javascript
const textElement = document.getElementById("text")

textElement.scrollIntoView()
```

One of the options this method accepts is the `behavior` property, which can be set to `smooth`. This will make scrolling to an element smooth and appealing.

```javascript
const textElement = document.getElementById("text")

textElement.scrollIntoView({behavior: "smooth"})
```

**Browser support for `scrollIntoView` method**:
<p class="ciu_embed" data-feature="scrollintoview" data-periods="future_1,current,past_1" data-accessible-colours="false"> <picture> <source type="image/webp" srcset="https://caniuse.bitsofco.de/image/scrollintoview.webp"> <source type="image/png" srcset="https://caniuse.bitsofco.de/image/scrollintoview.png"> <img src="https://caniuse.bitsofco.de/image/scrollintoview.jpg" alt="Data on support for the scrollintoview feature across the major browsers from caniuse.com"> </picture> </p>

## Smooth scroll with Library

To make your user experience better and more consistent across different browsers, you can use a library for smooth scrolling. Libraries will cover all the major browsers

* <https://github.com/cferdinandi/smooth-scroll> (NOTE: this library has been archived)
* <https://github.com/iamdustan/smoothscroll>

## Conclusion

If you’re implementing a simple web page with straightforward logic like on-page navigation, the CSS solution should be your choice.

The JavaScript approach on the other hand can be used to scroll to any element (even without the id attribute).

The drawback for both approaches is the lack of full browser support or only partial support. Fortunately, there are some JS libraries that are able to handle that for you. On the other hand, 3rd party library is a dependency to manage in the long run and some issues can still arise since this is not a native behavior.
