---
layout: post
permalink: horizontal-rule-css
title: Horizontal rule CSS - Custom style hr tag
date: 2021-09-22T20:19:10.224Z
description: To give custom appearance to the horizontal rule with CSS, you need
  to modify either border property or background property.
tags:
  - css
---

By default, the `hr` tag is just a thin straight line. It doesn’t possess any special properties, but you can make it look more appealing with some custom CSS code.

The [`hr` HTML tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr) represents a break between paragraphs and looks like a straight line. It has a `display: block` property by default which means the element will span the full width of the container.

**NOTE: The `hr` tag doesn’t have any specific HTML attributes attached to it. However, there were some that are [currently deprecated](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr#attributes).**

That being said you’ll need to write custom CSS in order to change its appearance. The default styling for the `hr` tag is pretty much similar across different browsers and consist of CSS rules that style the border of the element.

```css
hr {
  border-style: inset;
  border-width: 1px;
}
```

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 10px;flex:1 0 47%}
hr.dashed{border:1px dashed cornflowerblue}
hr.dotted{border:1px dotted cornflowerblue}
hr.double{border:3px double cornflowerblue}
hr.gradient{border:none;height: 1px;background-image:linear-gradient(to right,rgba(0, 0, 0, 0),cornflowerblue,rgba(0, 0, 0, 0))}
hr.shadow{border:none;height:0;box-shadow:0 1px 4px 1px cornflowerblue}
hr.symbol{border:1px solid cornflowerblue;display:flex;justify-content:center;align-items:center}
hr.symbol::before{content:'A';position:absolute;padding:15px;font-size:20px;background:white;color:cornflowerblue}
main hr{margin:30px auto 50px}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/html-elements/hr-chrome.png" alt="Horizontal rule on Chrome" loading="lazy">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/hr-edge.png" alt="Horizontal rule on Edge" loading="lazy">
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/hr-firefox.png" alt="Horizontal rule on Firefox" loading="lazy">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/hr-safari.png" alt="Horizontal rule on Safari" loading="lazy">
    <figcaption>Safari</figcaption>
  </figure>
</div>

## Styling Horizontal rule using border

One of the ways you can modify the appearance of the horizontal rule element is to change the [`border`](https://developer.mozilla.org/en-US/docs/Web/CSS/border) CSS rule, which includes the `border-style`, `border-width`, `border-color` and `border-radius` properties.

You can do that in just one line of CSS:

```css
hr {
  border: 1px dashed cornflowerblue;
}
```

**Result**:

<hr class="dashed">

```css
hr {
  border: 1px dotted cornflowerblue;
}
```

**Result**:

<hr class="dotted">

```css
hr {
  border: 3px double cornflowerblue;
}
```

**Result**:

<hr class="double">

**NOTE: When using border properly, you control `hr` thickness with the `border-width` property.**

## Styling Horizontal rule using background

However, for more custom effects you can apply shadows and gradients styles. Thus you’ll need to disable the border property.

```css
hr {
  border: none;
  height: 1px;
  background-image: linear-gradient (to right, rgba(0, 0, 0, 0), cornflowerblue, rgba(0, 0, 0, 0));
}
```

**Result**:

<hr class="gradient">

```css
hr {
  border: none;
  height: 0px;
  box-shadow: 0 1px 4px 1px cornflowerblue;
}
```

**Result**:

<hr class="shadow">

**NOTE: When not using `border` property, you control `hr` thickness with `height` property.**

Horizontal rule with symbols:

```css
hr {
  border: 1px solid cornflowerblue;
  position: relative;
  display: flex;
  justify-content: center;
}

hr::before {
  content: 'A';
  position: absolute;
  height: 20px;
  width: 20px;
  font-size: 20px;
  background: white;
}
```

**Result**:

<hr class="symbol">