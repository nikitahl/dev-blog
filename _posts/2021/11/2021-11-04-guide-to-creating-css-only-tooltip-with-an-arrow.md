---
layout: post
permalink: css-only-tooltip
title: Guide to creating CSS only tooltip with an arrow
date: 2021-11-04T21:25:25.604Z
description: Tooltip is a nice way to display additional information when there
  isn’t much space for it. You can create beautiful tooltips using only CSS.
tags:
  - css
---

Tooltip is a nice way to display additional information when there isn’t much space for it. You can create beautiful tooltips using only CSS.

Usually, tooltips are shown on hover state. Below you can see tooltip examples from some of the most popular apps and websites:

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px;}
.image-grid figure{margin:0 10px 10px;flex:1 0 30%;}
.image-grid .head-figure{flex:1 0 100%;}
</style>

<div class="image-grid">
  <figure class="head-figure">
    <img class="shadow lozad" data-src="/images/html-elements/wikipedia-tooltip.png" alt="Wikipedia tooltip">
    <noscript>
      <img class="shadow" src="/images/html-elements/wikipedia-tooltip.png" alt="Wikipedia tooltip">
    </noscript>
    <figcaption>Wikipedia tooltip</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/youtube-tooltip.png" alt="YouTube tooltip">
    <noscript>
      <img class="shadow" src="/images/html-elements/youtube-tooltip.png" alt="YouTube tooltip">
    </noscript>
    <figcaption>YouTube tooltip</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/jira-tooltip.png" alt="Jira tooltip">
    <noscript>
      <img class="shadow" src="/images/html-elements/jira-tooltip.png" alt="Jira tooltip">
    </noscript>
    <figcaption>Jira tooltip</figcaption>
  </figure>
  <figure>
    <img class="shadow lozad" data-src="/images/html-elements/gmail-tooltip.png" alt="Gmail tooltip">
    <noscript>
      <img class="shadow" src="/images/html-elements/gmail-tooltip.png" alt="Gmail tooltip">
    </noscript>
    <figcaption>Gmail tooltip</figcaption>
  </figure>
</div>

**NOTE: By default, HTML provides a way to show native tooltip using the title attribute. The tooltip will appear with a slight delay when the user hovers over an element with the title attribute.**

<figure>
  <img class="shadow lozad" data-src="/images/html-elements/youtube-title-attribute.png" alt="YouTube title attribute">
  <noscript>
    <img class="shadow" src="/images/html-elements/youtube-title-attribute.png" alt="YouTube title attribute">
  </noscript>
  <figcaption>YouTube title attribute</figcaption>
</figure>

## Creating a tooltip

Say we have an `abbr` element and we want to display a nice looking tooltip for it, to let users know what it means:

```html
<abbr>HTML</abbr>
```

Before we move any further, we need to tweak the existing HTML a bit.

We’ll add a *tooltip* `class` to select it and apply styles via CSS and add the `data-tooltip` attribute that holds the actual tooltip value, so it looks as follows:

```html
<abbr class="tooltip" data-tooltip="HyperText Markup Language">HTML</abbr>
```

To create a tooltip with only CSS, we’ll need to use the [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements). The pseudo-element has a [`content` attribute](https://developer.mozilla.org/en-US/docs/Web/CSS/content) that can store its value. We can pass a text, that will be used to display tooltip info.

```css
content: "HyperText Markup Language";
```

To reuse the tooltip component for multiple elements, the pseudo-element `content` attribute can have an `attr()` value linked to the element’s HTML attribute.

```css
content: attr(data-tooltip);
```

## Styling the tooltip

First, we need to set the `position` rule for the *tooltip* `class`. That way we can properly position our tooltip later. Also, we can add a [dotted underline](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration) (`abbr` tag already has it by default in [some browsers](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/abbr#default_styling)) and a *help* `cursor`, to indicate that additional information is available.

```css
.tooltip {
  position: relative;
  text-decoration: underline dotted;
  cursor: help;
}
```

The pseudo-element will look as follows:

```css
.tooltip::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translate(-50%);
  margin-bottom: 15px;
  color: #fff;
  background: rgba(0,0,0, .7);
  border-radius: 5px;
  padding: 5px;
}
```

### Tooltip arrow

To create the tooltip arrow, we can use the [triangle shape](https://css-tricks.com/the-shapes-of-css/) made out of the second pseudo-element border.

```css
.tooltip::after {
  position: absolute;
  content: "";
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 7px solid rgba(0,0,0, .7);
}
```

## Animating the tooltip

For more appealing interaction we can animate the tooltip by adding a small transition. By adding a zero opacity and a transition property for both pseudo-elements, on hover, we can fade-in tooltip by setting opacity to 0.

```css
.tooltip::before,
.tooltip::after {
  opacity: 0;
  visibility: hidden;
  transition: opacity .3s ease-in-out;
}

.tooltip:hover::before,
.tooltip:hover::after {
  opacity: 1;
  visibility: visible;
}
```

## Positioning the tooltip

The provided example will create a tooltip above the element. However, that’s not always the case. You may want to display your tooltip below, left, or right of an element.

For that reason, we can create modification classes (using [BEM principle](http://getbem.com/introduction/)). So in total, we’ll have four additional classes to set tooltip position:

1. `tooltip--top`
2. `tooltip--bottom`
3. `tooltip--left`
4. `tooltip--right`

```css
.tooltip--top::before,
.tooltip--top::after {
  bottom: 100%;
  left: 50%;
  transform: translate(-50%);
  margin-bottom: 15px;
}

.tooltip--top::after {
  margin-bottom: 8px;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 7px solid rgba(0,0,0, .7);
}

.tooltip--bottom::before,
.tooltip--bottom::after {
  top: 100%;
  left: 50%;
  transform: translate(-50%);
  margin-top: 15px;
}

.tooltip--bottom::after {
  margin-top: 8px;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-bottom: 7px solid rgba(0,0,0, .7);
}

.tooltip--right::before,
.tooltip--right::after {
  top: 50%;
  left: 100%;
  transform: translate(0, -50%);
  margin-left: 15px;
}

.tooltip--right::after {
  margin-left: 8px;
  border-top: 5px solid transparent;
  border-right: 7px solid rgba(0,0,0, .7);
  border-bottom: 5px solid transparent;
}

.tooltip--left::before,
.tooltip--left::after {
  top: 50%;
  right: 100%;
  transform: translate(0, -50%);
  margin-right: 15px;
}

.tooltip--left::after {
  margin-right: 8px;
  border-top: 5px solid transparent;
  border-left: 7px solid rgba(0,0,0, .7);
  border-bottom: 5px solid transparent;
}
```

## End result

You will find the resulting tooltips and the complete code example on CodePen:

<p class="codepen" data-height="320" data-default-tab="result" data-slug-hash="QWMvwKx" data-user="tippingpointdev" style="height: 320px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/QWMvwKx">
  Untitled</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>