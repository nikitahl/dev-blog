---
layout: post
permalink: custom-styled-input-type-file
title: Custom styled input type file upload button with pure CSS
description: Learn how to create a custom styled input type file upload button with drop zone only with pure CSS and HTML
updated: 2023-07-04T20:45:15.123Z
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

  .drop-container:hover,
  .drop-container.drag-active {
    background: #eee;
    border-color: #111;
  }

  .drop-container:hover .drop-title,
  .drop-container.drag-active .drop-title {
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
  .image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
  .image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}

  .image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}
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

Input with type file default look differs on different browsers: 

<div class="image-grid">
  <figure>
    <img class="shadow" src="/images/html-elements/input-type-file-chrome.png" alt="Input type file on Chrome" loading="lazy">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/input-type-file-edge.png" alt="Input type file on Edge" loading="lazy">
    <figcaption>Edge</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/input-type-file-firefox.png" alt="Input type file on Firefox" loading="lazy">
    <figcaption>FireFox</figcaption>
  </figure>
  <figure>
    <img class="shadow" src="/images/html-elements/input-type-file-safari.png" alt="Input type file on Safari" loading="lazy">
    <figcaption>Safari</figcaption>
  </figure>
</div>


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
<label for="images" class="drop-container" id="dropcontainer">
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

## Handling drag and drop events

Additionally, you can handle cases when the user will try to drag the file over the drop area. CSS alone cannot handle such cases, so we can add a little bit of JavaScript.

There are two points to consider to improve UX for the drop field:

1. Indicate the drop area when the user is dragging a file over it
2. Make it possible to drop a file inside the drop area, and not just the `input` element

To indicate drop area when user is dragging a file over it, we'll need to use the `dragenter` and `dragleave` [events](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/drag_event){:target="_blank"}. Both on the `label` tag, since it represents the drop area. For each event we add or remove a CSS class accordingly.

Since user will be dropping to the `label` tag we also need to set the `input` value with the file. To do that we need to do 2 things:

1. Set `dragover` event for the `label` tag, set `e.preventDefault()` and pass `false` as the [third parameter](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#usecapture){:target="_blank"} for the `addEventListener` method
2. On `drop` event, we need to set the input's `files` property to the file via `fileInput.files = e.dataTransfer.files`

```javascript
  const dropContainer = document.getElementById("dropcontainer")
  const fileInput = document.getElementById("images")

  dropContainer.addEventListener("dragover", (e) => {
    // prevent default to allow drop
    e.preventDefault()
  }, false)

  dropContainer.addEventListener("dragenter", () => {
    dropContainer.classList.add("drag-active")
  })

  dropContainer.addEventListener("dragleave", () => {
    dropContainer.classList.remove("drag-active")
  })

  dropContainer.addEventListener("drop", (e) => {
    e.preventDefault()
    dropContainer.classList.remove("drag-active")
    fileInput.files = e.dataTransfer.files
  })
```

As for styles, we can use similar styles to `:hover` state, but this time with a designated class:

```css
.drop-container.drag-active {
  background: #eee;
  border-color: #111;
}

.drop-container.drag-active .drop-title {
  color: #222;
}
```

**Result:**

<label for="files" class="drop-container" id="dropcontainer">
  <span class="drop-title">Drop files here</span>
  or
  <input class="file file-block" type="file" id="files" accept="image/*" required>
</label>

## Demo

See the full example on CodePen:

<p class="codepen" data-height="360" data-default-tab="result" data-slug-hash="oNqYaaQ" data-user="nikitahl" style="height: 360px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/oNqYaaQ">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

<script>
  const dropContainer = document.getElementById("dropcontainer")
  const fileInput = document.getElementById("files")
  dropContainer.addEventListener("dragover", (e) => {e.preventDefault()}, false)
  dropContainer.addEventListener("dragenter", () => {dropContainer.classList.add("drag-active")})
  dropContainer.addEventListener("dragleave", () => {dropContainer.classList.remove("drag-active")})
  dropContainer.addEventListener("drop", (e) => {
    e.preventDefault()
    dropContainer.classList.remove("drag-active")
    fileInput.files = e.dataTransfer.files
  })
</script>