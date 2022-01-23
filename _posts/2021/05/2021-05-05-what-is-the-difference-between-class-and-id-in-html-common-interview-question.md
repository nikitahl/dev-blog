---
layout: post
permalink: difference-between-class-and-id
title: What is the difference between class and id in HTML, CSS and JavaScript
date: 2021-05-05T06:10:30.649Z
description: A complete guide explaining the difference between class and id
  attributes in HTML, CSS and JavaScript.
tags: [html, javascript, css]
---

What is the difference between class and id in HTML, CSS, and JavaScript? That kind of question is quite common in [technical interviews](https://www.zuaneducation.com/blog/front-end-developer-interview-questions-and-answers/) for Front-end developers, especially for beginners.

Both [class](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class) and [id](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id) are HTML attributes that can be assigned to any HTML tag. They can be used and manipulated in HTML, CSS, and JavaScript.

1. [class and id in HTML](#class-and-id-in-html)
2. [class and id in CSS](#class-and-id-in-css)
3. [class and id JavaScript](#class-and-id-in-javascript)

## class and id in HTML

Each HTML element can have an id and a class attribute, however, the differences are:

1. The id's value must be unique in the whole document. As for the class, the value can be the same for multiple elements.
2. The id's value must not contain [whitespace](https://developer.mozilla.org/en-US/docs/Glossary/Whitespace) (spaces, tabs, etc.), while the class attribute allows space-separated values

```html
<h1 id="main-heading" class="text heading-text"></h1>
<p class="text"></p>
```

**NOTE: both class and id can contain letters, numbers, dashes, and underscores, but the first character should always be a letter.**

## class and id in CSS

In CSS the minor difference between class and id is that they have special characters preceding the name. For id, it is pound "#" for class it is period "."

```css
#main-heading {
  font-size: 45px;
}

.text {
  color: #333;
}
```

The main difference between class and id in CSS is that they have different [selector specificity](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance#specificity). The id has a higher specificity than a class.

E.g. looking at the following code, the id selector will override the class selector styles, even if the class selector is [cascading](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance#the_cascade) after the id selector.

```css
#main-heading {
  color: #000;
}

.text {
  color: #333;
}
```

It is considered a good practice to use classes to style elements, not the ids. One of the reasons for this, that it is easier to override a class selector than an id.

## class and id in JavaScript

There's not much difference between id and class in JavaScript. These are how you are going to select DOM elements and how you're going to access attribute values.

In JavaScript, you can select elements by their class name or by id. There are different ways how you can utilize classes and id to select DOM elements.

To select the element by id you can use:

1. `document.getElementById('elementId')` method;
2. `document.querySelector('#elementId')` method;
3. `window.elementId or window['element-id']` if the id is using a dash.

To select the element by the class you can use:

1. `document.querySelector('.elementClass')` method;
2. `document.getElementsByClassName('elementClass')` method;

To access the id attribute value on the element you can use the following approaches:

1. `Element.id` - will output id string
2. `element.getAttribute('id')` - will output id string

To access the class value on the element you can use the following approaches:

1. `Element.classList` - will output class string
2. `element.className` - will output class string
3. `element.getAttribute('class')` - will output class string