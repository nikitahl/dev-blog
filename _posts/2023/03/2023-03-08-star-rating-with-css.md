---
layout: post
permalink: star-rating-with-css
title: Simple star rating with pure CSS
date: 2023-03-08T20:00:24.232Z
description: You can implement a simple star rating using only CSS, without additional assets like images, fonts, or SVGs.
tags: [css]
---

A star rating is a great way to highlight user satisfaction with a product or a service. You can implement a simple star rating using only CSS, without additional assets like images, fonts, or SVGs.

In this guide, we’ll create a:
1. [star rating widget](#star-rating-widget) for users to leave a review
2. [star rating](#displaying-average-rating) to display the average rating

<p class="note">💡 NOTE: In this guide, we’ll focus only on the visual appearance of the star rating.</p>

We will use special Unicode symbols a.k.a. [html entities](/special-characters-and-symbols-with-html-entities) to keep it as simple and native as possible.

One of the benefits of using Unicode symbols is that they are treated as a font, which means you can apply font-related CSS properties like `font-size` and `color`.

## Star rating widget

We will use a form with a set of checkboxes to allow users to leave ratings without using any JavaScript or 3rd party library. It will act as a widget with which users can interact.

```html
<form class="star-rating">
  <input class="radio-input" type="radio" id="star5" name="star-input" value="5" />
  <label class="radio-label" class for="star5" title="5 stars">5 stars</label>

  <input class="radio-input" type="radio" id="star4" name="star-input" value="4" />
  <label class="radio-label" for="star4" title="4 stars">4 stars</label>

  <input class="radio-input" type="radio" id="star3" name="star-input" value="3" />
  <label class="radio-label" for="star3" title="3 stars">3 stars</label>

  <input class="radio-input" type="radio" id="star2" name="star-input" value="2" />
  <label class="radio-label" for="star2" title="2 stars">2 stars</label>

  <input class="radio-input" type="radio" id="star1" name="star-input" value="1" />
  <label class="radio-label" for="star1" title="1 star">1 star</label>
</form>
```

As you can see the order of labels and checkboxes is reversed. This is done to implement the hover effect so that all starts up until the one that is hovered is selected.

Since you cannot [select previous elements in CSS](/css-select-previous-element) we’ll use the `flex-direction` property to reverse the order of labels and checkboxes.

```css
.star-rating {
  display: flex;
  flex-direction: row-reversed;
  justify-content: flex-end;
}
```
Now that labels and checkboxes are displayed in the correct order, we’ll create our stars.

To do that we’ll hide checkboxes and set a pseudo-element with a content property equal to a star symbol (★).

```css
.radio-input {
  position: fixed;
  opacity: 0;
  pointer-events: none;
}

.radio-label {
  cursor: pointer;
  font-size: 0;
  color: rgba(0,0,0,0.2);
  transition: color 0.1s ease-in-out;
}

.radio-label:before {
  content: "★";
  display: inline-block;
  font-size: 32px;
}
```
Finally, let’s add some fancy effects so that the user can see the total number of stars on hover.

```css
.radio-input:checked ~ .radio-label {
  color: #ffc700;
  color: gold;
}

.radio-label:hover,
.radio-label:hover ~ .radio-label {
  color: goldenrod;
}

.radio-input:checked + .radio-label:hover,
.radio-input:checked + .radio-label:hover ~ .radio-label,
.radio-input:checked ~ .radio-label:hover,
.radio-input:checked ~ .radio-label:hover ~ .radio-label,
.radio-label:hover ~ .radio-input:checked ~ .radio-label {
  color: darkgoldenrod;
}
```

## Displaying average rating

To display the total average rating we’ll use the `meter` tag. As the [HTML Specs](https://html.spec.whatwg.org/multipage/form-elements.html#the-meter-element){:target="_blank"} says:

> The meter element represents a scalar measurement within a known range, or a fractional value

This tag comes with a set of attributes that determines the semantics of its gauge. In our case, it’s the `min` (minimum value), `max` (maximum value), and `value` (the current value).

```html
<meter min="0" max="5" value="4.3"></meter>
``` 
As the spec suggests:

> Authors are encouraged to include a textual representation of the gauge's state in the element's contents, for users of user agents that do not support the meter element.

So in our case to make it more [semantic](/why-it-is-important-to-write-semantic-html) and user-friendly we’ll include a short label:

```html
Product rating: <meter class="average-rating" min="0" max="5" value="4.3" title="4.3 out of 5 stars">4.3 out of 5</meter>
``` 

Now that we’re done with HTML, let’s apply some styling to make the `meter` tag look like stars.

First, we’ll need to visually hide the meter tag.

```css
.average-rating {
  position: relative;
  appearance: none;
  color: transparent;
  width: auto;
  display: inline-block;
  vertical-align: baseline;
}
```

Next to display stars we’ll use a pseudo-element with a `content` property equal to the 5 star symbols.

To highlight the star percentage we’ll use the text background gradient hack. That is setting the `linear-gradient` property, combined with the `background-clip` and `text-fill-color` properties.

To calculate the fill area percentage we need to use the following formula:

*rating ÷ max rating × 100%*.

```css
.average-rating::before {
  --percent: calc(4.3/5*100%);
  content: '★★★★★';
  position: absolute;
  top: 0;
  left: 0;
  color: rgba(0,0,0,0.2);
  background:
    linear-gradient(90deg, gold var(--percent), rgba(0,0,0,0.2) var(--percent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

## Demo

The end result with complete code can be viewed on CodePen:

<p class="codepen" data-height="345" data-default-tab="result" data-slug-hash="LYJyzyM" data-user="nikitahl" style="height: 345px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/LYJyzyM">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
