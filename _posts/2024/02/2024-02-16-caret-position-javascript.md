---
layout: post
permalink: cursor-at-the-end-of-text-field
title: How to place cursor at the end of the text field with JavaScript
date: 2024-02-16T08:40:17.102Z
description: It’s a good idea to place the cursor at the end of the text field when it gains focus, especially if the field already contains a value.
tags: [javascript]
---

It’s a good idea to place the cursor at the end of the text field when it gains focus, especially if the field already contains a value.

I’m referring to both `input` elements (which can hold text values) and `textarea` elements.

However, the `focus()` method alone doesn’t achieve this. Since there are no native solutions to set the cursor position, we can employ a small JavaScript trick.

Let's assume we have the following search `input` element, which already contains a value:

```html
<input id="search-field" type="search" value="How to">
```

Next we'll need to use the [`setSelectionRange`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/setSelectionRange){:target="_blank"} method to set the cursor position.

The `setSelectionRange` method accepts two parameters:

* `selectionStart` - a zero-based index of the first selected character
* `selectionEnd` - a zero-based index of the character after the last selected character

Although this method is intended for text selection, we can use it to set the cursor position by specifying the same start and end position of the selection. Which both will be equal to the last character index.

```javascript
const searchInput =  document.getElementById('search-field')

// start and end position of the cursor
const pos = searchInput.value.length

searchInput.setSelectionRange(pos, pos)
searchInput.focus()
```
<p class="note">💡 NOTE: The <code>setSelectionRange</code> method will work the same for the <code>input</code> and <code>textarea</code> elements.</p>

<figure class="figure-centered">
  <a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/setSelectionRange#browser_compatibility" target="_blank" rel="noopener">
    <img class="shadow" loading="lazy" src="/images/browser-support/setselectionrange-browser-support.webp" alt="setSelectionRange Browser compatibility">
  </a>
  <figcaption>Browser compatibility</figcaption>
</figure>
