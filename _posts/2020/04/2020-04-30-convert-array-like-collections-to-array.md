---
layout: post
title: 3 ways how to convert NodeList or HTMLCollection to an array with JavaScript
description: A breakdown of 3 ways how and why to convert a NodeList or HTMLCollection of elements to an Array with Vanilla JavaScript API
tags: [javascript]
comments: true
---

There are 3 native ways in JavaScript API to convert `NodeList` or `HTMLCollection` to an `Array`.

## What are a `NodeList` and `HTMLCollection`?

When selecting element on the page, with `.querySelectorAll()`:

```javascript
const paragraphs = document.querySelectorAll('p')
```

it will return all paragraph elements on the page as a `NodeList`.

[The `NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) is a collection of [DOM nodes](https://developer.mozilla.org/en-US/docs/Glossary/Node/DOM) 
 that has similar to an `Array` appearance and structure.

You can, however, select element via other ways like `document.forms`:

```javascript
document.forms
```
This property will return all form elements on the page and the result will be an [`HTMLCollection`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection). The `HTMLCollection` returns a collection of HTML elements it also has an array-like structure.

**So what's the problem?**

Both `NodeList` and `HTMLCollection` are collections and they might look like an `Array` and even possess some properties and methods inherent to arrays, they're still not actual arrays.

This means if you're willing to use [`Array` methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) on your `NodeList`s and `HTMLCollection`s then you'll need to convert them into an actual Array.

## 1. Array.from()

[Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from) method will create a new `Array` instance from an array-like or iterable object. So it can be used both on `NodeList` and `HTMLCollection`.

```javascript
const paragraphs = document.querySelectorAll('p') // NodeList
const paragraphsArray = Array.from(paragraphs)

paragraphsArray // Will output an Array

const documentForms = document.forms // HTMLCollection
const documentFormsArray = Array.from(documentForms)

documentFormsArray // Will output an Array
```

This is a clear and straightforward method to create an `Array`, and not only from `NodeList` or `HTMLCollection`.

**[Browser Support](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from#Browser_compatibility):** All major browsers except IE.

## 2. Spread syntax

<blockquote>
<strong>Spread syntax</strong> allows an iterable such as an array expression or string to be expanded
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax" target="_blank">MDN</a></cite>
</blockquote>

In the case of `NodeList` or `HTMLCollection`, the Spread syntax has to be used inside square brackets to spread iterable into a new `Array`.

```javascript
const paragraphs = document.querySelectorAll('p') // NodeList
const paragraphsArray = [...paragraphs]

paragraphsArray // Will output an Array

const documentForms = document.forms // HTMLCollection
const documentFormsArray = [...documentForms]

documentFormsArray // Will output an Array
```

This approach is useful when joining arrays.

**[Browser Support](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Browser_compatibility):** All major browsers except IE.

## 3. Array.prototype.slice.call()

This is the old school method, due to it's fully cross-browser.

What this piece of code does is it takes the [`.slice()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) from `Array` prototype and then invokes this method by binding it to the object (in our case `NodeList` or `HTMLCollection`) via [`.call()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call).

The `.slice()` method will:

<blockquote>
return a shallow copy of a portion of an array into a new array object selected from <code>begin</code> to <code>end</code>
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice" target="_blank">MDN</a></cite>
</blockquote>


But since no arguments passed it will return the full array.

```javascript
const paragraphs = document.querySelectorAll('p') // NodeList
const paragraphsArray = Array.prototype.slice.call(paragraphs)

paragraphsArray // Will output an Array

const documentForms = document.forms // HTMLCollection
const documentFormsArray = Array.prototype.slice.call(documentForms)

documentFormsArray // Will output an Array
```

Also just to shorten up a bit you can use the `[].slice.call()` syntax instead.

**[Browser Support](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice#Array-like_objects):** All major browsers.