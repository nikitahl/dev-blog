---
layout: post
permalink: how-to-lazy-load-codepen-and-caniuse-embeds
title: How to lazy load CodePen and CanIUse embeds
date: 2024-02-27T19:50:17.102Z
description: CodePen and CanIUse embeds that are often used on blog posts require the load of a lot of resources, and usually, this is done on the initial page load.
tags: [javascript, performance]
---

CodePen and CanIUse embeds that are often used on blog posts require the load of a lot of resources, and usually, this is done on the initial page load.

1. [Problem with embeds](#problem-with-embeds)
2. [Solution is to lazy load](#solution-is-to-lazy-load)

## Problem with embeds

This poses a significant performance issue, particularly when the embed isn't immediately visible on the page. And I'm not just referring to [CodePen](https://blog.codepen.io/documentation/embedded-pens/){:target="_blank"} and [CanIUse](https://caniuse.bitsofco.de/){:target="_blank"}; this applies to any third-party embed on the page.

While CodePen offers some [optimization](https://blog.codepen.io/documentation/embedded-pens/#pen-previews){:target="_blank"} options, such as using the *Click-to-Load* feature on an embed or employing the `loading="lazy"` attribute on an `iframe` to [defer the load](/defer-css-and-javascript), further optimization is still possible.

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:30px 0}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 30px;flex:0 0 47%}
.vertical{width:60%}
</style>
<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/dev-tools/codepen-embed-resources.webp" alt="CodePen embed resources">
    <figcaption>CodePen embed resources</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/dev-tools/caniuse-embed-resources.webp" alt="CanIUse embed resources">
    <figcaption>CanIUse embed resources</figcaption>
  </figure>
</div>

The number of resources loaded depends on the content of an embed, and in some cases, it can be substantial, such as numerous and/or large images.

These resources are deemed [render-blocking](https://web.dev/render-blocking-resources/){:target="_blank"}, implying that loading them during the initial page load significantly [impacts the page's speed](https://web.dev/articles/lcp){:target="_blank"}, a [critical aspect](https://web.dev/learn/performance/why-speed-matters){:target="_blank"} of web page performance.

I've encountered this issue for some time, as I incorporate many of these embeds on my blog to showcase my work and offer information about browser support for a feature.

## Solution is to lazy load

I decided to write a custom script to [lazy load](/lazy-load-images) these embeds and optimize my blog posts for load speed.

The solution is quite simple: utilize the [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API){:target="_blank"} to determine if the embed is sufficiently close to the edge of the screen to initiate resource downloading.

The first step involves pasting the embed HTML code, but excluding the `script` tag. The `script` contains code to fetch the necessary resources for the embed.

So in case of CanIUse, the HTML will appear as follows:

```html
<p style="background:pink;padding:50px 0;" class="ciu_embed" data-feature="mdn-css__properties__-webkit-text-stroke-width" data-periods="future_1,current,past_1" data-accessible-colours="false">
  Data on support for the <a href="https://caniuse.com/text-stroke" target="_blank">-webkit-text-stroke-width</a> feature across the major browsers
</p>
```

Next, we'll need to write a small JavaScript snippet to properly handle embed lazy loading.

The following JavaScript code will verify if the embed element is within 400px of the edge of the screen and will then append the embed script to the `body` element, thereby triggering the resource download.

Below is my JavaScript snippet with comments for explanation:

```javascript
// Get all CodePen and CanIUse embeds
const embeds = document.querySelectorAll(".codepen, .ciu_embed");

// Execute further code only if embeds exist on the page
if (embeds.length) {
  // Set flags if resources for embeds are already loaded
  let isCpLoaded = false;
  let isCiuLoaded = false;

  // Specify options for IntersectionObserver
  // rootMargin is the top and bottom margin that represents
  // the value to the edge of the screen of the embed
  const options = {
    root: null,
    rootMargin: "400px 0px", 
    threshold: 0
  };

  // Create the Intersection Observer from the IntersectionObserver constructor
  const intersectionObserver = new IntersectionObserver((entries, observer) => {
    entries.forEach((entry) => {
      // Ensure if the element is intersecting the edge of the screen
      if (entry.isIntersecting) {
        // Define the embed element
        const embed = entry.target;
        // Define the script source variable
        let src = "";
        // Based on the condition set the source variable equal to embed script path
        // do it only once, because we don't need to run the code multiple times,
        // once the resourses have already loaded
        if (!isCiuLoaded && embed.classList.contains("ciu_embed")) {
          isCiuLoaded = true;
          src = "https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/public/caniuse-embed.min.js";
        } else if (!isCpLoaded && embed.classList.contains("codepen")) {
          isCpLoaded = true;
          src = "https://cpwebassets.codepen.io/assets/embed/ei.js";
        }
        // Execute further code only if the script source is available
        if (src) {
          // Create a script element and assign src and async attributes
          var script = document.createElement("script");
          script.src = src;
          script.async = true;
          // Append the script before the closing body tag
          document.body.appendChild(script);
          // For the CanIUse embeds run additional code
          if (embed.classList.contains("ciu_embed")) {
            // CanIUse embed script is wrapped inside a "DOMContentLoaded" event
            // so we need to trigger this event oursevles in order for the script to execute
            // NOTE: trigger this event at your own risk,
            // because many JavaScript libraries rely on this event
            // and it might produce an unwanted results.
            script.onload = function(params) {
              var customEvent = new CustomEvent("DOMContentLoaded");
              document.dispatchEvent(customEvent);
            }
          }
        }
      }
    })
  }, options);

  // Call observer for each embed
  embeds.forEach((embed) => {
    intersectionObserver.observe(embed);
  });
}
```
