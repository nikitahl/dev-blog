---
layout: post
permalink: pure-css-truncate-text
title: How to handle long text overflow with pure CSS (truncate/ellipsis, wrap)
date: 2021-05-11T20:14:20.122Z
updated: 2022-03-21T18:16:21.123Z
description: A complete guide explaining how to utilize pure CSS properties to truncate and wrap long overflowing text
tags: [css]
---

When working on a website or a web app texts are often overlooked, that’s when issues like overflowing text occur. To solve that, you can use some solutions like truncating or *ellipsizing* a text (add three dots) or wrapping the text.

Page contents:

1. [Wrapping text](#1-wrapping-text);
2. [Truncating text](#2-truncating-text).

Overflowing text content quite often happens in the following cases:

* For long words;
* For long URL’s;
* On mobile devices;
* For narrow container elements;
* For table cells;
* For button elements.

Depending on the CSS styles you have, the text overflow will usually look either like a horizontal scroll or like a cut-off content.

Consider the following issue. There’s a fixed-width container on a page with a link containing and pointing to a long URL. The link text will overflow the container and will look messy, as well as it can produce an unwanted horizontal scroll on smaller screen sizes.

## 1. Wrapping text

### 1.2 The word-break property

One way to handle long text in CSS is to wrap it to the next line. This approach is handy when you don't have to worry about text spanning multiline. When using [`word-break`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break) property you have two options how to wrap it:

* `break-all` - this will break text once the characters don’t fit inside the container
* `break-word` - this will break text once the characters don’t fit inside the container but it will preserve the word sequence. **NOTE: this is a deprecated API and it is not recommended to use.**

```css
.container a {
  word-break: break-all;
}
```

**Browser support for `word-break` property:** <https://caniuse.com/word-break>

### 1.2 The overflow-wrap property

Another option to wrap text is to use the [`overflow-wrap`](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap) property. This property also has two options for wrapping:

* `anywhere` - will break text at any given point if it doesn’t fit;
* `break-word` - same as `anywhere` except it will break long words at arbitrary points.

```css
.container a {
  overflow-wrap: break-word;
}
```

**Browser support for `overflow-wrap` property:** <https://caniuse.com/wordwrap>

## 2. Truncating text

### 2.1 The text-overflow property

The [`text-overflow`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow) property will add an ellipsis (will add three dots) to a text if it doesn't fit inside the container. This approach is handy if you want to keep text in a single line. However, with some additional modifications, it can be made for multiline text as well.

The `text-overflow` property with a value of `ellipsis` must be set on a parent element, relative to the text. Two additional properties must be specified `overflow` and `white-space`.

**NOTE: Learn how to handle [text overflow for select tag](/text-overflow-ellipsis-on-select-tag).**

#### Single line

```css
.container {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

#### Multiline

For the multiline solution the `white-space` property must be removed, this way the text will be truncated on the last available line.

```css
.container {
  overflow: hidden;
  text-overflow: ellipsis;
}
```

**Browser support for `text-overflow` property:** <https://caniuse.com/text-overflow>

### 2.2 The line-clamp property

A more modern approach is the [`line-clamp`](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-line-clamp) property which will limit the container text to a specified number of lines. As well as add the three dots at the end. This property will only work with a `-webkit-` vendor prefix and a `display` property set to `-webkit-box` or `-webkit-inline-box`.

Unline the `text-overflow` solution, this approach is straightforward and more understandable, when it comes to truncating multiline text. The `line-clamp` property must be set to the element that is overflowing and the value should be equal to the number of lines to span.

```css
.container a {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
}
```

**Browser support for the line-clamp property:** <https://caniuse.com/css-line-clamp>

A full demo is available on [CodePen](https://codepen.io/tippingpointdev/pen/RwKOpoz):

<p class="codepen" data-height="435" data-theme-id="dark" data-default-tab="result" data-user="tippingpointdev" data-slug-hash="RwKOpoz" style="height: 435px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Long text truncate and wrap with CSS">
<span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/RwKOpoz">
Long text truncate and wrap with CSS</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>

<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>