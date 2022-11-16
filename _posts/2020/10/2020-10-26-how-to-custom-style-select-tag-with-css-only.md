---
layout: post
permalink: how-to-custom-style-select-tag-with-css-only
title: Select tag custom styles with CSS only
date: 2020-10-27T14:08:12.231Z
description: A simple and cross-browser consistent solution to give a to custom
  style to a select tag with CSS only
tags:
  - css
---
The `select` tag is one of the most confusing and hard to style form elements in HTML. Luckily there is a simple and cross-browser consistent solution to give custom styles for `select` tag using only CSS.

1. [The problem with styling select tag](#the-problem-with-styling-select-tag)
2. [The CSS solution](#the-css-solution)
3. [Final result](#final-result)
4. [The future of select tag styling](#the-future-of-select-tag-styling)

## The problem with styling select tag

`select` is one of those HTML tags that have different appearances across browsers.

<style>
.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}

.image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}

</style>

<div class="image-grid">
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/select-tag-chrome.png" alt="Select tag on Chrome">
    <noscript>
      <img class="shadow" src="/images/resources/select-tag-chrome.png" alt="Select tag on Chrome">
    </noscript>
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/select-tag-firefox.png" alt="Select tag on Firefox">
    <noscript>
      <img class="shadow" src="/images/resources/select-tag-firefox.png" alt="Select tag on Firefox">
    </noscript>
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/select-tag-safari.png" alt="Select tag on Safari">
    <noscript>
      <img class="shadow" src="/images/resources/select-tag-safari.png" alt="Select tag on Safari">
    </noscript>
    <figcaption>Safari</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/select-tag-edge.png" alt="Select tag on Edge">
    <noscript>
      <img class="shadow" src="/images/resources/select-tag-edge.png" alt="Select tag on Edge">
    </noscript>
    <figcaption>Edge</figcaption>
  </figure>
</div>

That’s the main reason why developers applying custom styles for `select` tag. A [study has shown](https://www.gwhitworth.com/surveys/controls-components/) that the `select` tag is the number one form control developers are creating a custom style for. The same study shows that the reasons for custom styling `select` tag in the first place are:

* Browser inconsistencies;
* Couldn’t change the appearance sufficiently.

## The CSS solution

To apply custom style for a `select` tag, you’ll need the CSS only approach, no additional HTML, or JavaScript. That means that native behavior and accessibility are preserved and less code is used which is good.

Let’s take the basic `select` tag markup.

**HTML:**

```html
<select>
  <option value="pen">Pen</option>
  <option value="pineapple">Pineapple</option>
  <option value="apple">Apple</option>
  <option value="pen">Pen</option>
  <option value="pen">PenPineappleApplePen</option>
</select>
```

As for the CSS, we’ll reset basic styles first.

**CSS:**

```css
select {
  box-sizing: border-box;

  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;

  background-color: transparent;
  border: none;
  padding: 0;
  margin: 0;
  width: 100%;

  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 1.3;

  cursor: default;
}
```

**NOTE: the** `appearance` **rule will remove the dropdown arrow. However, it is not [supported](https://caniuse.com/#search=appearance) by the IE browser.**

If you need to reset default styling for the IE browser, add the following rule:

```css
select::-ms-expand {
  display: none;
}
```

*Source: [StackOverflow.com](https://stackoverflow.com/questions/20163079/remove-select-arrow-on-ie/20163273#20163273)*

Now that we’ve removed the default dropdown arrow, we can add a custom one. It can be achieved via an [encoded background SVG image](/using-svg-background-image-with-css-code-only). This solution is cross-browser-friendly. And since it’s SVG you can further customize it if needed.

```css
select {
  padding: 5px 10px 5px 8px;
  border: 1px solid #999;
  border-radius: 5px;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='292.4' height='292.4'%3E%3Cpath fill='%23333' d='M287 69.4a17.6 17.6 0 0 0-13-5.4H18.4c-5 0-9.3 1.8-12.9 5.4A17.6 17.6 0 0 0 0 82.2c0 5 1.8 9.3 5.4 12.9l128 127.9c3.6 3.6 7.8 5.4 12.8 5.4s9.2-1.8 12.8-5.4L287 95c3.5-3.5 5.4-7.8 5.4-12.8 0-5-1.9-9.2-5.5-12.8z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 8px center;
  background-size: 9px;
  color: #333;
}
```

Next, let's add styles for pseudo-classes `:hover` and `:focus`. For the `:focus` state we’ll add the `box-shadow` property and remove the default `outline`, now that we have rounded corners.

```css
select:hover {
  border-color: #777;
}

select:focus {
  border-color: #999;
  box-shadow: 0 0 1px 2px #6db4ff;
  outline: none;
}
```

To finalize let's add custom styles for the `select` disabled state.

```css
select:disabled,
select[aria-disabled=true] {
  cursor: not-allowed;
  background-color: rgba(211, 211, 211, .75);
}

select:disabled:hover,
select[aria-disabled=true]:hover {
  border-color: #999;
}
```

## Final result

With custom styles applied for the `select` tag it will look consistent and more appealing across different browsers:

<div class="image-grid">
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/custom-select-tag-chrome.png" alt="Custom styled select tag on Chrome">
    <noscript>
      <img class="shadow" src="/images/resources/custom-select-tag-chrome.png" alt="Custom styled select tag on Chrome">
    </noscript>
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/custom-select-tag-firefox.png" alt="Custom styled select tag on Firefox">
    <noscript>
      <img class="shadow" src="/images/resources/custom-select-tag-firefox.png" alt="Custom styled select tag on Firefox">
    </noscript>
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/custom-select-tag-safari.png" alt="Custom styled select tag on Safari">
    <noscript>
      <img class="shadow" src="/images/resources/custom-select-tag-safari.png" alt="Custom styled select tag on Safari">
    </noscript>
    <figcaption>Safari</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/custom-select-tag-edge.png" alt="Custom styled select tag on Edge">
    <noscript>
      <img class="shadow" src="/images/resources/custom-select-tag-edge.png" alt="Custom styled select tag on Edge">
    </noscript>
    <figcaption>Edge</figcaption>
  </figure>
</div>

The final result with all the code is available on CodePen:

<p class="codepen" data-height="390" data-theme-id="dark" data-default-tab="css,result" data-user="nikitahl" data-slug-hash="GRZvPer" style="height: 295px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom styled select tag">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/GRZvPer">
  Custom styled select tag</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## The future of select tag styling

Currently, there’s an online initiative called [Open UI](https://open-ui.org/) to standardize UI components on the web such as the [`select` tag](https://open-ui.org/components/select). 

> The purpose of Open UI to the web platform is to allow web developers to style and extend built-in web UI controls, such as select dropdowns, checkboxes, radio buttons, and date/color pickers.

This means that this organization is working toward a unifying standard of styling `select` and other form tags and components for that matter (so no hacks and pain). [Stephanie Stimac](https://twitter.com/seaotta) talks about **[Standardizing select: What the future holds for HTML Controls](https://noti.st/seaotta/2UH3qv/standardizing-select-what-the-future-holds-for-html-controls)** in more detail at the [FrontCon 2020](https://2020.frontcon.com/) conference.

But as of the time this article is published the Open UI is in the infancy stage, as they call it. Hopefully in the near-future web developers will have the ability to give custom styles to all form elements with ease.