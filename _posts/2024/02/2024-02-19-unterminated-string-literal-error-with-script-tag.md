---
layout: post
permalink: unterminated-string-literal-error-with-script-tag
title: Unterminated string literal error with the script and style tags
date: 2024-02-19T20:42:19.102Z
description: I recently encountered an `Unterminated string literal` error, which turned out to be totally unexpected for me, as the string looked completely fine for me.
tags: [javascript]
---

I recently encountered an `Unterminated string literal` error, which turned out to be totally unexpected for me, as the string looked completely fine to me.

Usually, the [`Unterminated string literal`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unterminated_string_literal){:target="_blank"} error occurs when the string is not enclosed inside the single (`'`) or double (`"`) quotes.

In my case, the string looked as follows:

```javascript
var str = "<script></script>";
```

Immediately I was notified by the code editor that there was an issue with this string.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/errors/unterminated-string-literal-error-in-editor.webp" alt="Unterminated string literal error">
  <figcaption>Unterminated string literal error</figcaption>
</figure>

Since I've ensured that the string was closed by the double quote, I was confused a bit, to say the least.

I've tried both single and double quotes. But the error was still there, and the console was saying the same. However, Firefox was more precise.

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:30px 0}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 30px;flex:0 0 47%}
.vertical{width:60%}
</style>
<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/errors/unterminated-string-literal-error-in-chrome.webp" alt="Unterminated string literal error in Chrome">
    <figcaption>Chrome console error</figcaption>
  </figure>
    <figure>
    <img class="shadow" loading="lazy" src="/images/errors/unterminated-string-literal-error-in-firefox.webp" alt="Unterminated string literal error in Firefox">
    <figcaption>Firefox console error</figcaption>
  </figure>
</div>

But after some investigation, I've [found out](https://stackoverflow.com/questions/236073/why-split-the-script-tag-when-writing-it-with-document-write#answer-236106){:target="_blank"} that the `script` and `style` tags inside a string should be treated like HTML, hence the error.

There are a few ways to fix that.

1. **Escape the closing tag slash:**
```javascript
var str = "<script><\/script>";
```

2. **Split the string:**
```javascript
var str = "<script>" + "</script>";
```

3. **Use template literals:**
```javascript
var str = `<script></script>`;
```
