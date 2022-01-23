---
layout: post
permalink: margin-vs-padding-css-explained
title: Understand the difference between Margin vs Padding in CSS? [+Demo]
date: 2020-11-25T08:31:32.905Z
description: A definitive guide explaining you the difference between CSS margin
  and padding properties, as well as highlighting features and use cases.
tags:
  - css
---
Beginner developers often get confused between `margin` vs `padding` properties in CSS. They both create the space around the element. But how are they different? What are the use cases? This guide will answer those questions for you.

The difference explained in short:

**The padding is the space inside the element, that separates the content from the border.**

**The margin is the space outside the element, that separates it from other elements.**

<figure>
  <img class="shadow lozad" data-src="/images/misc/margin-vs-padding.gif" alt="Margin and Padding">
  <noscript>
    <img class="shadow" src="/images/misc/margin-vs-padding.gif" alt="Margin and Padding">
  </noscript>
  <figcaption>Margin and Padding side by side</figcaption>
</figure>

The image above highlights the button's padding area in green and the margin area in orange.

Try out an interactive [demo](#margin-vs-padding-demo) to see how `margin` vs `padding` works.

<style>

.post ul > li > p,.post ul > li > ul{margin:0}

.toc-toggle{color:#888;cursor:pointer}

.toc-toggle:hover{text-decoration:underline}

.table-of-contents{display:none}

.visible{display:initial}

</style>

<b>Page contents</b> [<span class="toc-toggle">show</span>]:

<div class="table-of-contents">

<ul>
<li>
<p><a href="#css-box-model">CSS Box model</a></p>
</li>
<li>
<p><a href="#margin">Margin</a></p>
<ul>
<li>
<p><a href="#margin-features">Margin features</a></p>
<ul>
<li><a href="#can-be-auto">Can be auto</a></li>
<li><a href="#collapsible-margins">Collapsible margins</a></li>
<li><a href="#can-be-negative">Can be negative</a></li>
<li><a href="#cannot-alter-element-size">Cannot alter element size</a></li>
</ul>
</li>
<li>
<p><a href="#when-to-use-margin">When to use margin</a></p>
</li>
</ul>
</li>
<li>
<p><a href="#padding">Padding</a></p>
<ul>
<li>
<p><a href="#padding-features">Padding features</a></p>
<ul>
<li><a href="#cannot-be-auto-or-negative">Cannot be auto or negative</a></li>
<li><a href="#not-collapsible">Not collapsible</a></li>
<li><a href="#can-alter-element-size">Can alter element size</a></li>
</ul>
</li>
<li>
<p><a href="#when-to-use-padding">When to use padding</a></p>
</li>
</ul>
</li>
<li>
<p><a href="#margin-and-padding-shorthand-syntax">Shorthand syntax</a></p>
</li>
<li>
<p><a href="#margin-vs-padding-demo">Margin vs Padding Demo</a></p>
</li>
</ul>
</div>

<script>
  var tocToggle = document.querySelector('.toc-toggle');
  var toc = document.querySelector('.table-of-contents');
  tocToggle.addEventListener('click', function(){
  toc.classList.toggle('visible')
});
</script>

## CSS Box model

To understand the difference between `margin` and `padding`, you need to understand the **[box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)** concept first.

The point is that each HTML element is rendered in a browser as a box, that consists of four parts:

1. Content area;
2. Padding;
3. Border;
4. Margin.

Each part is bound by the respective edge:

1. *content area edge*
2. *padding edge*
3. *border edge*
4. *margin edge*.

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/box-model.png" alt="CSS Box Model">
  <noscript>
    <img class="shadow" src="/images/dev-tools/box-model.png" alt="CSS Box Model">
  </noscript>
  <figcaption>CSS Box Model</figcaption>
</figure>

Thus the box model makes padding and margin both a part of the element. And they both directly affect the appearance of one.

Margin and padding have several features that make them different. Knowing these features will help you better understand their behavior and proper usage.

The following sections will break down each feature of both margin and padding.

## Margin

> The **margin area**, bounded by the margin edge, extends the border area to include an empty area used to separate the element from its neighbors.
>
> \- MDN

The margin is a transparent space outside the element that separates it from other elements. Basically, it pushes the element away from other elements.

### Margin features

The features listed below are only inherent to the margin.

#### Can be auto

Margin value can be set to `auto`. This means that the browser will automatically define the `margin` value. Margin's values will be split evenly, so they can be used to center an element.

```css
p {
  width: 50%;
  margin: auto; /* this will center paragraph horizontally */
}
```

**Result**:

<figure>
  <img class="shadow lozad" data-src="/images/misc/margin-auto.png" alt="Margin auto">
  <noscript>
    <img class="shadow" src="/images/misc/margin-auto.png" alt="Margin auto">
  </noscript>
  <figcaption>Margin auto</figcaption>
</figure>

#### Collapsible margins

In some cases, [margins may collapse](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing) into a single margin (one of the largest values or one of them if they're equal).

So when two elements placed side by side or one after another, the margins will collapse. However not always. In some cases, both margins will be applied e.g. *floats* or *absolutely positioned* elements.

I highly recommend checking this great article on [margin collapse](https://www.joshwcomeau.com/css/rules-of-margin-collapse/) by [Josh W. Comeau](https://twitter.com/JoshWComeau).

In the example below, the space between `h1` and `p` will be `30px`. Margins collapsed and the greater value is applied.

```html
<h1>Hello World!</h1>
<p>How are you?</p>
```

```css
h1 {
  margin-bottom: 30px; 
}

p {
  margin-top: 10px;
}
```

**Result**:

<figure>
  <img class="shadow lozad" data-src="/images/misc/h1-p-margins.gif" alt="Margin collapse">
  <noscript>
    <img class="shadow" src="/images/misc/h1-p-margins.gif" alt="Margin collapse">
  </noscript>
  <figcaption>Margin collapse</figcaption>
</figure>

#### Can be negative

Margins may have negative values. It works sort of like positioning. The negative value will shift the element in an opposite direction.

In the example below the paragraph will be moved to the left by `60px.`

```css
p {
  margin: 0 0 0 -60px;
}
```

**Result**:

<figure>
  <img class="shadow lozad" data-src="/images/misc/negative-margin.png" alt="Negative margin">
  <noscript>
    <img class="shadow" src="/images/misc/negative-margin.png" alt="Negative margin">
  </noscript>
  <figcaption>Negative margin</figcaption>
</figure>

#### Cannot alter element size

Unlike `padding`, the `margin` cannot alter element size. If you recall the box model, the margin is *"used to separate the element from its neighbors"*. So no matter what value you set element size will remain intact.

### When to use margin

Margins are generally used to set the space between elements (a "gap") or to position elements. These powers come from the ability to set `auto` and negative values.

**NOTE: The margin area is not clickable! Due to the fact that this is the empty area outside the element.**

## Padding

> The **padding area**, bounded by the padding edge, extends the content area to include the element's padding.
>
> \- MDN

The `padding` is the space between the actual content and the `border` of the element. It will have any `background-color` or `backgorund-image` property that has been applied to an element.

### Padding features

The features listed below are only inherent to the `padding`.

#### Cannot be auto or negative

Unlike `margin`, the `padding` cannot have auto or negative values. If you set `auto` or a negative value to `padding` it will not change the appearance of the element, however, in **Element Inspector** it will be shown as an *Invalid property value*.

#### Not collapsible

Since the `padding` is the space inside the element it cannot collapse.

#### Can alter element size

Paddings directly affect element size. Visually it can be seen well, especially if the `background-color` or `border` property is applied. But if you're trying to get element size with JavaScript it depends on the CSS `box-sizing` property and the method you're using. 

You can check my article explaining [how to get element size with JavaScript](/4-ways-to-get-the-width-and-height-of-an-element-with-vanilla-javascript) to avoid possible troubles.

### When to use padding

Use it to give your elements a visually appealing appearance. Also, additional paddings increase element size, which is quite useful from the **UX** and **Accessibility** perspective. E.g. on mobile devices, it is easier to tap a button or an input field that has some paddings. They make elements bigger in size, thus easier to tap.

With the help of padding, you can give your element an [aspect ratio](/css-aspect-ratio). It is called the *"padding hack"* and is used to maintain the proportions of the element throughout the viewports.

## Margin and Padding shorthand syntax

Both `padding` and `margin` properties have a [shorthand syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties). There are four ways you can set these properties.

**single value** - sets top, right, bottom, and left margins:

```css
p {
  margin: 10px;
}
```

**two values** - the first one sets vertical (top and bottom), second sets horizontal (right and left) margins:

```css
p {
  margin: 10px 20px;
}
```

**three values** - first and third sets top and bottom accordingly, the second one sets right and left margins.

```css
p {
  margin: 10px 20px 15px;
}
```

**four values** - each margin side is set separately in the following order top, right, bottom, left.

```css
p {
  margin: 10px 20px 15px 0;
}
```

## Margin vs Padding Demo

Change input values to see how margin and padding properties change for the set of buttons.

<style>
.button {
  border: 2px solid rgb(2, 189, 126);
  background: white;
  padding: 15px 40px;
  margin: 20px;
  font-size: 18px;
  cursor: pointer;
}

.log-in {
  background: rgb(2, 189, 126);
  color: white;
}

.sign-up {
  color: rgb(2, 189, 126);
}

.demo-input {
  display: inline-block;
  width: 60px;
  padding: 3px 5px;
  margin: 0 0 20px;
}
</style>

<form id="demo-form"><label for="margin-input" class="demo-label">Margin value (px): </label><input id="margin-input" class="demo-input" type="number" name="margin" value="5"><br><label for="padding-input" class="demo-label">Padding value (px): </label><input id="padding-input" class="demo-input" type="number" name="padding" value="18"></form><button class="log-in button">Log In</button><button class="sign-up button">Sign Up</button><br><button class="log-in button">Log In</button><button class="sign-up button">Sign Up</button>

<script>
  const demoForm = document.getElementById('demo-form');
  const formElements = Array.from(demoForm.elements);
  const buttons = Array.from(document.querySelectorAll('.button'));

  function handleFormChange () {
    buttons.forEach((button) => {
      formElements.forEach((element) => {
        button.style[element.name] = `${element.value}px`
      })
    });
  }

  demoForm.addEventListener('change', handleFormChange);
  handleFormChange();
</script>