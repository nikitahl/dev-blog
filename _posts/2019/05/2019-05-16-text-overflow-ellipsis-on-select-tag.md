---
layout: post
title: Text overflow ellipsis on select tag
description: Applying a CSS text-overflow property on select tag for an ellipsis effect
updated: 2023-04-14T11:16:21.123Z
tags: [html, css]
comments: true
---

For a better UI and appeal a CSS `text-overflow` property is used on a long piece of text. I'm going to show how to apply that to a `select` tag.

By default `select` tag will handle overflowing text pretty decently, depending on the browser. 

<style>
.image-grid {display: flex;justify-content: space-evenly;flex-wrap: wrap;margin: 0 0 30px;}
.image-grid figcaption {font-size: 13px; color: #666; font-style:italic; text-align:center}
.image-grid figure{margin: 0 10px 10px;flex: 1 0 47%;}
</style>

<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/select-tag-long-text-chrome.webp" alt="Select tag on Chrome">
    <figcaption>Chrome</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/select-tag-long-text-firefox.webp" alt="Select tag on Firefox">
    <figcaption>Firefox</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/select-tag-long-text-safari.webp" alt="Select tag on Safari">
    <figcaption>Safari</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/html-elements/select-tag-long-text-edge.webp" alt="Select tag on Edge">
    <figcaption>Edge</figcaption>
  </figure>
</div>


However, instead of just cutting out a text in the middle and have some consistency across browsers, lets give it custom styling by truncating the text.

## Definitions

Before we move on it's important to establish the starting ground in order to understand the issue and a solution to it.

As for the `select` tag, the HTML specs says:

<blockquote>
The <code>select</code> element represents a control for selecting amongst a set of options.
<br />
&mdash;<cite><a href="https://html.spec.whatwg.org/multipage/form-elements.html#the-select-element" target="_blank">html specs</a></cite>
</blockquote>

The MDN on styling the `select` element:

<blockquote>
The <code>select</code> element is notoriously difficult to style productively with CSS.
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select#Styling_with_CSS" target="_blank">MDN</a></cite>
</blockquote>

Also MDN on the `text-overflow` property itself:

<blockquote>
The <code>text-overflow</code> CSS property sets how hidden overflow content is signaled to users. It can be clipped, display an ellipsis ('…'), or display a custom string.
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow" target="_blank">MDN</a></cite>
</blockquote>

<p class="note">
💡 NOTE: The <code>text-overflow</code> property applies to block container elements.
</p>

So we have a unique form element that is hard to style and the question is - how does one apply the `text-overflow` property to a `select` tag and [handle text overflow](/pure-css-truncate-text)? The answer is with a little bit of HTML and a sprinkle of JavaScript.

The main idea is to get the value of the `select` tag and store it in the `data` attribute of the container element. Then display it with the help of CSS.

## Markup

First things first, to display the ellipsized text we're going to need a container element. This element will wrap the `select` element and display the current value that the `select` element has. To do so, the `data` attribute must be declared.

Also, I'm going to set one of the `option` tags with a long value, to make sure it overlaps the `select` tag.

The end HTML code will look as follows:
```html
<div class="select-container" data-content="">
  <select class="select" id="words">
    <option value="lorem ipsum dolor sit amet">Lorem ipsum dolor sit amet</option>
    <option value="lorem">Lorem</option>
    <option value="ipsum">Ipsum</option>
    <option value="dolor">Dolor</option>
    <option value="sit">Sit</option>
    <option value="amet">Amet</option>
  </select>
</div>
```

## Styles

Next, we're going to add some styles. Since the `.select-container` element is going to display the value we need to hide the actual `select` tag content and some of the original appearance.

Then we'll add a custom arrow as a background and set padding.

```css
.select {
  color: transparent;
  appearance: none;
  padding: 5px;
  background: transparent url("https://cdn4.iconfinder.com/data/icons/ionicons/512/icon-arrow-down-b-128.png") no-repeat calc(~"100% - 5px") 7px;
  background-size: 10px 10px;
}
```

For the wrapper element, we'll set the `position` and `display` property. The main trick is the `::before` pseudo element which will have the `content` property equals to a `data` attribute. This way the content of the pseudo element will always be equal to whatever value the `data` stores.

Since the pseudo element is going to store and display the value, we're going to set the necessary CSS properties to ellipsize text `white-space`, `text-overflow` and `overflow`.

```css
.select-container {
  position: relative;
  display: inline-block;
}

.select-container::before {
    content: attr(data-content);
    pointer-events: none;
    position: absolute;
    top: 0;
    right: 10px;
    bottom: 0;
    left: 0;
    padding: 7px;
    font: 11px Arial, sans-serif;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    text-transform: capitalize;
  }
```

To give your select tag a unique and consistent look across all browsers check out my article where I explain in detail [how to style select tag](/how-to-custom-style-select-tag-with-css-only) with pure css. 

## Script

Finally, we'll need a few lines of JavaScript to respond to `select` element value change and setting the value to a container element `data` attribute.

Define two variables containing the `select` element and its container. Set initial values to the `select` element and container's `data` attribute. And lastly, add an event listener to a `select` element.


```javascript
const selectContainer = document.querySelector(".select-container");
const select = selectContainer.querySelector(".select");

select.value = "lorem ipsum dolor sit amet";
selectContainer.dataset.content = select.value;

function handleChange(e) {
  selectContainer.dataset.content = e.currentTarget.value;
}

select.addEventListener("change", handleChange);
```

## Demo

You can find the end result I've made on [Codepen](https://codepen.io/nikitahl/pen/vyZbwR
){:target="blank"}:

<p class="codepen" data-height="320" data-theme-id="0" data-default-tab="html,result" data-user="nikitahl" data-slug-hash="vyZbwR" style="height: 378px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Text-overflow ellipsis on Select tag hack">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/vyZbwR/">
  Text-overflow ellipsis on Select tag hack</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>