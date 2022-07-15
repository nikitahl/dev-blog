---
layout: post
permalink: custom-styled-input-type-file
title: Custom styled input type file upload button with pure CSS
description: Learn how to create a custom styled input type file upload button with drop zone only with pure CSS and HTML
tags: [css]
---

In this guide I'll show you how to create a stylish and user friendly file upload button with pure CSS and HTML.

<style>
  .drop-container {
    position: relative;
    display: flex;
    gap: 10px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 200px;
    padding: 20px;
    border-radius: 10px;
    border: 2px dashed #555;
    color: #444;
    cursor: pointer;
    transition: background .2s ease-in-out, border .2s ease-in-out;
  }

  .drop-container:hover {
    background: #eee;
    border-color: #111;
  }

  .drop-container:hover .drop-title {
    color: #222;
  }

  .drop-title {
    color: #444;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    transition: color .2s ease-in-out;
  }
  .file-block {
    width: 350px;
    max-width: 100%;
    color: #444;
    padding: 5px;
    background: #fff;
    border-radius: 10px;
    border: 1px solid #555;
  }
  .file::file-selector-button {
    margin-right: 20px;
    border: none;
    background: #084cdf;
    padding: 10px 20px;
    border-radius: 10px;
    color: #fff;
    cursor: pointer;
    transition: background .2s ease-in-out;
  }
  .file::file-selector-button:hover {
    background: #0d45a5;
  }
</style>


## Markup

To upload files you'll need to use the `input` tag with [`type="file"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file) attribute. Additionally you can specify which file types you're allowing to upload via [`accept`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/accept) attribute.

**HTML:**

```html
<input type="file" accept="image/*">
```

This markup produces a button with a *Choose file* title followed by a text which indicates the file name when selected. By default it is *No file chosen*.

**Result:**

<input type="file" accept="image/*">

## Styling

The upload file widget structure consists of a block that displays a button and a file name. A user can click anywhere inside the block or drag a file from the desktop and it will open up the upload window.

### Styling the upload file block

If you apply styles for the `input[type=file]` selector it will set them for the whole widget block, that is the button and text.

**CSS:**

```css
input[type=file] {
  width: 350px;
  max-width: 100%;
  color: #444;
  padding: 5px;
  background: #fff;
  border-radius: 10px;
  border: 1px solid #555;
}
```

The result already looks much better as it indicates the zone where user is able to click or drag the file.

**Result:**

<input class="file-block" type="file" accept="image/*">

### Styling the upload file button

By default, the *Choose file* button has a plain user-agent style. To style the button with CSS you should use the [`::file-selector-button`](https://developer.mozilla.org/en-US/docs/Web/CSS/::file-selector-button) pseudo-element to select it. It is supported in [all modern browsers](https://caniuse.com/mdn-css_selectors_file-selector-button).

**CSS:**

```css
input[type=file]::file-selector-button {
  margin-right: 20px;
  border: none;
  background: #084cdf;
  padding: 10px 20px;
  border-radius: 10px;
  color: #fff;
  cursor: pointer;
  transition: background .2s ease-in-out;
}

input[type=file]::file-selector-button:hover {
  background: #0d45a5;
}
```

**Result**

<input class="file file-block" type="file" accept="image/*">

### Styling the the click/drop zone

If you wich to go a bit further, you can create a large zone where user can click and drag files. This large zone will make it easier for people to use the widget, as it don't require to be that precise when dragging a file, especially on smaller screens.

To implement a large drop zone, you'll need to wrap your file upload `input` into a `label` tag and specify a description text that will let users know how to use the widget.

**HTML**

```html
<label for="images" class="drop-container">
  <span class="drop-title">Drop files here</span>
  or
  <input type="file" id="images" accept="image/*" required>
</label>
```

For the layout, we need to set `display` to `flex` with flex related properties for positioning. The `height` and `padding` properties for proportion. And finally add some fancy styles like border and hover effects to highlight the file upload zone and you're ready to go.

**CSS:**

```css
.drop-container {
  position: relative;
  display: flex;
  gap: 10px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 200px;
  padding: 20px;
  border-radius: 10px;
  border: 2px dashed #555;
  color: #444;
  cursor: pointer;
  transition: background .2s ease-in-out, border .2s ease-in-out;
}

.drop-container:hover {
  background: #eee;
  border-color: #111;
}

.drop-container:hover .drop-title {
  color: #222;
}

.drop-title {
  color: #444;
  font-size: 20px;
  font-weight: bold;
  text-align: center;
  transition: color .2s ease-in-out;
}
```

**Result:**

<label for="images" class="drop-container">
  <span class="drop-title">Drop files here</span>
  or
  <input class="file file-block" type="file" id="images" accept="image/*" required>
</label>


## Demo

See the full example on CodePen:

<p class="codepen" data-height="360" data-default-tab="html,result" data-slug-hash="oNqYaaQ" data-user="nikitahl" style="height: 360px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/oNqYaaQ">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>