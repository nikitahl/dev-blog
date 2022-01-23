---
layout: post
permalink: add-multiple-classes-in-javascript
title: Add and remove multiple classes in JavaScript for DOM element
date: 2021-04-12T07:20:40.572Z
description: There are different ways how to add and remove multiple classes in
  JavaScript. In this guide I'm showing three ways how you can achieve that.
tags:
  - js
---
Vanilla JavaScript allows you to add or remove multiple classes for the DOM element in 3 different ways. Depending on your needs you may choose one of the following:

1. [`classList` property](#1-classlist-property)
2. [`className` property](#2-classname-property)
3. [`setAttribute` method](#3-setattribute-method)
4. [Bonus toggle multiple classes in DevTools](#4-bonus-toggle-multiple-classes-in-devtools)

## 1. classList property

> The `Element.classList` is a read-only property that returns a live [`DOMTokenList`](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList) collection of the `class` attributes of the element
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

The `classList` property should be your primary way to work with classes in JavaScript. The `classList` property has `add()` and `remove()` methods that allow passing multiple classes as arguments.

Let's say we have a button with `id` value of `button`. To add multiple classes, you'll need to pass each class as a separate parameter to the `add` method. The same goes if you want to remove multiple classes.

```javascript
const button = document.getElementById('button')

button.classList.add('btn', 'btn-primary', 'btn-primary--footer')
button.classList.remove('btn', 'btn-primary', 'btn-primary--footer')
```

You can utilize the [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) if you're willing to store and manipulate your classes in an array. In my opinion, this approach is much cleaner, and arrays have a bunch of useful methods you can utilize to add or remove classes.

```javascript
const button = document.getElementById('button')
const classes = ['btn', 'btn-primary', 'btn-primary--footer']

button.classList.add(...classes)
button.classList.remove(...classes)
```

### Toggle classes

With the help of the `classList` property you can actually toggle classes with one method: [`toggle()`](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList/toggle). The `toggle()` method accepts two arguments: `token` and `force`. 

The `token` is a string and represents a class name. The `force` is optional, if included, based on the value will only add or remove a class. If it's `true` then it will only add, if `false` only remove.

**However please note that the `token` argument should be a single string without any spaces. So this means it can toggle one class name at a time!**

```javascript
const button = document.getElementById('button')

button.addEventListener('click', () => {
  button.classList.toggle('btn--active')
})
```

**[Browser support for `classList` property](https://caniuse.com/classlist)**.

## 2. className property

> The `className` property of the [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/Element) interface gets and sets the value of the [`class` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class) of the specified element.
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)

This `className` approach is convenient when you're decided to work with string type for the class value. To add or remove multiple classes, you'll have to add up or remove the class on the string.

```javascript
const button = document.getElementById('button')

button.className = 'btn btn-primary btn-primary--footer'
// to remove certain classes, you'll need to reassign 
// the value to the className property
button.className = 'btn'
```

**[Browser support for `className` property](https://caniuse.com/mdn-api_element_classname)**.

## 3. setAttribute method

> Sets the value of an attribute on the specified element. If the attribute already exists, the value is updated; otherwise a new attribute is added with the specified name and value.
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)

While the `setAttribute` method may not look as straightforward as `classList` still, it can be used to add multiple classes. Like in the method above, multiple classes can be specified in one string.

```javascript
const button = document.getElementById('button')

button.setAttribute('class', 'btn btn-primary btn-primary--footer')
// to remove certain classes, you'll need to update the 
// the value by calling this method again
button.setAttribute('class', 'btn')
```

This approach is quite useful when [creating a new element](/create-element-with-javascript), and you use a custom function to assign multiple different attributes to an element.

**[Browser support for `setAttribute` method](https://caniuse.com/mdn-api_element_setattribute)**.

## 4. Bonus toggle multiple classes in DevTools

You can easily add or remove multiple classes in your browser's DevTools. This works in Chrome and Firefox:

<figure>
  <img class="shadow lozad" data-src="/images/misc/toggle-classes.gif" alt="Toggle classes in Dev Tools">
  <noscript>
    <img class="shadow" src="/images/misc/toggle-classes.gif" alt="Toggle classes in Dev Tools">
  </noscript>
  <figcaption>Toggle classes in Dev Tools</figcaption>
</figure>