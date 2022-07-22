---
layout: post
permalink: numbered-headings-with-css-counter
title: Numbered headings made with CSS counter
description: Numbered headings will emphasize page structure and provide additional cues for users who are navigating your web page.
tags: [css]
---

Adding numbers to headings will emphasize page structure and provide additional cues for users while navigating your web page.

You can add numbers to your headings with pure CSS. It won't require any additional markup or JavaScript.

It can be done by implementing a [CSS counters](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Counter_Styles/Using_CSS_counters) concept.

Say you have a following headings structure:

**HTML:**

```html
<h1>Article Title</h1>
<h2>Introduction</h2>
<h2>Main part</h2>
<h3>Details</h3>
<h3>More details</h3>
<h2>Conclusion</h2>
```

You can make it look like this:

<figure>
  <img class="shadow" loading="lazy" src="/images/misc/numbered-headings.png" width="50%" alt="Numbered headings">
  <figcaption>Numbered headings</figcaption>
</figure>

## Adding CSS counters for headings

In CSS you'll need to specify the [`counter-reset`](https://developer.mozilla.org/en-US/docs/Web/CSS/counter-reset) property on the `body` tag to start a new counter for the whole page. The value of this property is a variable that should be unique to be used by the specific heading level e.g. `h2` headings.

```css
body {
  counter-reset: headings2;
}
```

To display the numeric value next to a heading, a `::before` pseudo-element is used. Its `content` property should be equal to the [`counter()`](https://developer.mozilla.org/en-US/docs/Web/CSS/counter) function, which accepts the same variable we used for the `counter-reset` property.

You can add a dot to a number, to separate it from heading text. To do so add a dot with a space as a string `". "` next to `counter()` function.

Finally lets add a `counter-increment` property and set its value to the same heading variable. As the name states it will increment counter value for the next heading.

```css
h2::before {
  content: counter(headings2) ". ";
  counter-increment: headings2;
}
```

## Adding counters for nested headings

Same logic can be applied for the next level of headings `h3` and so on, up to `h6`.

First we need to reset the counter on the parent heading, in this case `h2`.

```css
h2 {
  counter-reset: headings3;
}
```

For the pseudo-element we need to set the `content` equal to `heading2` counter + `heading3` counter with a dot separator. This structure will indicate the belonging to the parent heading section.

```css
h3:before {
  content: counter(headings2) "." counter(headings3) ". ";
  counter-increment: headings3;
}
```

## Prevent counters for specific headings

To prevent a number on a heading we can stop counters by setting a `none` value for `content` and `counter-increment` properties of a headings' pseudo-element.

Add a class name for those headings you wish to prevent numbers. And in CSS add following:

```css
.non-numbered:before {
  content: none;
  counter-increment: none;
}
```

This is useful when you want to show regular headings after ending a list of numbered sections.

## Final result

See the live example and a complete code on CodePen:

<p class="codepen" data-height="500" data-default-tab="html,result" data-slug-hash="OJvpEJE" data-user="nikitahl" style="height: 500px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/OJvpEJE">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>