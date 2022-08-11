---
layout: post
permalink: using-svg-background-image-with-css-code-only
title: Using SVG background image with CSS code only
date: 2020-10-09T11:20:29.058Z
updated: 2022-08-11T16:37:13.025Z
description: A detailed guide with use cases to handle encoded SVG background
  image with CSS code only
tags:
  - svg
  - css
---
It is possible to set an SVG background image using only CSS. To do that you’ll need to convert SVG code to the Data URL string.

> Data URLs, URLs prefixed with the `data:` scheme, allow content creators to embed small files inline in documents.
>
> [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)

Browser support for Data URLs on CanIUse: <https://caniuse.com/#feat=mdn-http_data-url_css_files>

## Example

Say we have the initial SVG code:

```html
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" x="0px" y="0px" viewBox="0 0 426.667 426.667" style="enable-background:new 0 0 426.667 426.667;" xml:space="preserve">
  <g>
    <g>
      <g>
        <path d="M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333     S272.213,106.667,213.333,106.667z" fill="gold"/>
        <path d="M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333     S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667     S384,119.04,384,213.333S307.627,384,213.333,384z" fill="gold"/>
      </g>
    </g>
  </g>
</svg>
```

To convert it to Data URL string use the [URL-encoder for SVG](https://yoksel.github.io/url-encoder/) online tool. So the end code will look as follows.

Encoded SVG string:

```css
data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='gold'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E
```

Once SVG code is converted to an encoded string it then can be then set via `background` property in CSS.

HTML:

```html
<div class=”svg-background”></div>
```

CSS:

```css
.svg-background {
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='gold'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}
```

Result:

<p class="codepen" data-height="360" data-theme-id="dark" data-default-tab="css,result" data-user="nikitahl" data-slug-hash="bONXoZ" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="SVG as background image with hover">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/bONXoZ">
  SVG as background image with hover</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Use cases

This technique is quite useful when you don’t have access to markup (HTML) but you can edit CSS. This is a quite common case for **WordPress** sites.

### Lists

Say you have an existing list with bullets. And you need to set a custom symbol for [list items](/custom-bullet-points-css). You can use the `list-style-image` property which accepts the `url()` value where you can pass encoded SVG image.

HTML:

```html
<ul>
  <li>Banana</li>
  <li>Apple</li>
  <li>Kiwi</li>
</ul>
```

CSS:

```css
li {
  list-style-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='gold'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}
```

### Hover effects

Another great part of the SVG background image is that you can change the SVG properties on hover. For example change color to the part of the SVG image in our case `fill` property.

If we use the same list element then we can add a `:hover` pseudo-class with a slight change to the color. Newly encoded SVG will contain the code with an updated color (the inner circle is going to have a color of `tomato`).

```css
li:hover {
  list-style-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' version='1.1' x='0px' y='0px' viewBox='0 0 426.667 426.667' style='enable-background:new 0 0 426.667 426.667;' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cg%3E%3Cpath d='M213.333,106.667c-58.88,0-106.667,47.787-106.667,106.667S154.453,320,213.333,320S320,272.213,320,213.333 S272.213,106.667,213.333,106.667z' fill='tomato'/%3E%3Cpath d='M213.333,0C95.467,0,0,95.467,0,213.333s95.467,213.333,213.333,213.333S426.667,331.2,426.667,213.333 S331.2,0,213.333,0z M213.333,384c-94.293,0-170.667-76.373-170.667-170.667S119.04,42.667,213.333,42.667 S384,119.04,384,213.333S307.627,384,213.333,384z' fill='gold'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}
```

### Inputs and select element

You can also use this technique to show icons for [input](/search-icon-inside-input) and [select](/how-to-custom-style-select-tag-with-css-only) elements. For example, to add custom styling to a `select` tag, you can hide the native arrow and add a custom one using an encoded SVG image:

```css
select {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='292.4' height='292.4'%3E%3Cpath fill='%23333' d='M287 69.4a17.6 17.6 0 0 0-13-5.4H18.4c-5 0-9.3 1.8-12.9 5.4A17.6 17.6 0 0 0 0 82.2c0 5 1.8 9.3 5.4 12.9l128 127.9c3.6 3.6 7.8 5.4 12.8 5.4s9.2-1.8 12.8-5.4L287 95c3.5-3.5 5.4-7.8 5.4-12.8 0-5-1.9-9.2-5.5-12.8z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 8px center;
  background-size: 9px;
}
```