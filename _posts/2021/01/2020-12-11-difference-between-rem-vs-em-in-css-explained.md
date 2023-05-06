---
layout: post
permalink: rem-vs-em
title: "The difference between Rem vs Em in CSS explained"
date: 2021-01-06T07:38:25.506Z
updated: 2022-07-19T16:22:19.407Z
description: A complete guide explaining the difference between rem vs em units
  in CSS with examples and use cases
tags: [css]
---

It can be confusing and frustrating when trying to understand units in CSS. Especially [relative units](https://developer.mozilla.org/en-US/docs/Web/CSS/length#Relative_length_units) like `em` and `rem`.

In this guide, I'll explain what they are and how are they different. As well as provide additional information like, examples, use cases and pitfalls so you better understand the topic.

**Contents:**

1. [Em units](#em-units)
2. [Rem units](#rem-units)
3. [Examples](#examples)
4. [Use cases](#use-cases)
5. [Pitfalls](#pitfalls)
6. [Accessibility](#accessibility)
7. [Tools](#accessibility)
8. [Final thoughts](#final-thoughts)

**Rem vs em difference in essence**:

* `em` units are relative to the current element `font-size` value;
* `rem` units are relative to the root element (`html`) `font-size` value.

<style>
  #main .container {font-size:16px;color:#444;margin-bottom:20px}
  .nested {font-size:1.5em}
  .image-grid{display: flex;justify-content: space-evenly;margin: 0 0 30px}
  .image-grid figcaption{font-size: 13px; color: #666; font-style:italic; text-align:center}
  .image-grid figure{margin: 0 10px 10px;flex: 1 0 47%}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/misc/em-unit-relation.png" alt="Em unit relation" loading="lazy">
    <figcaption>Em unit relation</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/misc/rem-unit-relation.png" alt="Rem unit relation" loading="lazy">
    <figcaption>Rem unit relation</figcaption>
  </figure>
</div>

## EM units

The `em` unit is **relative** to the `font-size` of the **current element or the next parent element** in case no `font-size` property is set to the current element. 

The formula to calculate the value of `em` unit is **em unit × element font size = value.** So if the `font-size` is set to `14px` then `1em` will be equivalent to the `14px` *(1 × 14 = 14)*.

> The name *em* was originally a reference to the width of the capital *M* in the typeface and size being used.
>
> \- [Wikipedia](https://en.wikipedia.org/wiki/Em_(typography))

`em` units can be used on a variety of CSS properties like `padding`, `margin`, etc, not only `font-size`.

**Example 1:**

```css
p {
  font-size: 14px;
  margin-bottom: 1em; /* computed value of margin-bottom will be 14px */
}
```

**Example 2:**

```css
p {
  font-size: 14px;
}

p span {
  font-size: 1.2em; /* computed value will be 16.8px (1.2 × 14 = 16.8) */
}
```

To check the resulted size in pixels you can use the **Computed** tab under **Element Inspector** in DevTools (same in all browsers DevTools).

<figure>
  <img class="shadow" src="/images/dev-tools/computed-styles-tab.png" alt="Element Inspector Computed Tab" loading="lazy">
  <figcaption>Element Inspector Computed Tab</figcaption>
</figure>

## REM units

`rem` stands for Root EM. The root is being the `html` element. So the `rem` unit is relative to the `font-size` of the `html` element.

It uses the same formula to calculate the value **rem unit × html element font size = value**.

**Example:**

```css
html {
  font-size: 14px;
}

p {
  font-size: 1.1rem; /* computed value will be 15.4px (1.1 × 14 = 15.4) */
}
```

## Examples

Following pen serves as a visual aid to show the difference between `rem` and `em` units. Change the `font-size` of `html` and `.container` elements to see how it affects headings and paragraphs:

<p class="codepen" data-height="418" data-theme-id="dark" data-default-tab="result" data-user="nikitahl" data-slug-hash="BaLYZoz" style="height: 418px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS rem vs em visualized example">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/BaLYZoz">
  CSS rem vs em visualized example</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Use cases

Unlike pixels `em` and `rem` are relative units. Thus is easier to control and scale different CSS properties of an element since relative units can be applied not only for `font-size`. That's why they come in handy for **styling responsive/adaptive interfaces**.

One of the simplest examples is setting the `font-size` on the `html` element and use `rem` units to set the `font-size` for typography elements (`h1`, `h2`, `p`...). As an addition `em` units can be used to set the `margin` for the same elements.

With this approach, you'll need to change only one property at a given breakpoint. Consider the code below:

```css
html {
  font-size: 16px;
  line-height: 1.5;
}

body {
  margin: 10px;
}

h1 {
  font-size: 3.2rem;
  margin: .3em 0;
}

h2 {
  font-size: 2.2rem;
  margin: .5em 0;
}

h3 {
  font-size: 1.4rem;
  margin: .4em 0;
}

p {
  font-size: 1.2rem;
}

@media screen and (max-width: 768px) {
  html {
    font-size: 14px;
  }
}
```

**Result:**

<p class="codepen" data-height="390" data-theme-id="dark" data-default-tab="result" data-user="nikitahl" data-slug-hash="BaLxYYv" style="height: 355px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Font scaling with rem units">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/BaLxYYv">
  Font scaling with rem units</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Pitfalls

While `em` and `rem` units are great, there are some pitfalls that aren't necesserily bad but you have to be aware of.

### Nested inheritance

Setting `em` units for the same child elements that can be nested multiple levels down the tree may cause a negative effect. Since `em` units calculate value based on parent element `font-size` *(in case current element font-size is missing)* nested element's `font-size` value will increase with each nesting level.

**HTML:**

```html
<div class="container">
  Container text
  <div class="nested">
    Nested element text
    <div class="nested">
      Nested element text
      <div class="nested">
        Nested element text
      </div>
    </div>
  </div>
</div>
```

**CSS:**

```css
.container {
  font-size: 16px;
}

.nested {
  font-size: 1.5em;
}
```

**Result:**

<div class="container">
  Container text
  <div class="nested">
    Nested element level 1 
    <div class="nested">
      Nested element level 2
      <div class="nested">
        Nested element level 3
      </div>
    </div>
  </div>
</div>

### Browser font size settings

A user can define font size inside the browser settings. This means that elements that don't have an explicit `font-size` property set will scale to the user-selected font size. Elements that have an absolute `font-size` value set like `px` will remain the same size. Elements with relative units like `em` or `rem` will scale accordingly.

<figure>
  <img class="shadow" src="/images/tools/chrome-font-size.png" alt="Chrome browser font size settings" loading="lazy">
  <figcaption>Chrome browser font size settings</figcaption>
</figure>

### Complexity

The use of relative units can bring complexity to a codebase and maintenance especially if all font sizes use `em` units. It will be harder to trace and debug an issue since all values will be dependant. Issues like nested inheritance mentioned above may arise.

## Accessibility

In terms of accessibility relative units `em` and `rem` are more preferable. Relative units can scale which makes UX more pleasant and UI more readable thus more accessible. I highly recommend this definitive guide on [Pixels vs. Relative Units in CSS: why it’s still a big deal](https://www.24a11y.com/2019/pixels-vs-relative-units-in-css-why-its-still-a-big-deal/) to better understand the implication of relative units and how it affects different groups of users.

## Tools

It's easy to calculate the value of `em` and `rem` units to pixels if you know the formula (**relative unit × element font size = value**). Also, you can always check the browsers' Element Inspector for the computed values.

But if you feel lazy or want to quickly fiddle around with values here are some nice online tools to convert values.

* <http://pxtoem.com/>
* <https://nekocalc.com/px-to-rem-converter>
* <https://www.w3schools.com/TAGS/ref_pxtoemconversion.asp>

## Final thoughts

I've tried to cover all the basics in this article to make it clear for you about the difference between `em` vs `rem`.

Relative units are great and can make your UI more appealing and accessible. Just remember to use caution when working with `em` and `rem` units.

In the end my tips for you are:

1. don't go to extremes;
2. use relative units sparingly;
3. test well before publishing;
4. consult with other people if possible.