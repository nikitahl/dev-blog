---
layout: post
permalink: add-element-with-javascript
title: A complete list of methods to add an element to DOM with JavaScript
date: 2021-02-10T12:00:32.858Z
description: A definitive guide to help you understand and decide how to add an
  element to DOM with Vanilla JavaScript.
tags: [javascript]
---

JavaScript API allows developers to add (append) an element to the DOM in several different ways. I'll explain each one of them in detail.

Once you've selected, cloned, or [created a new element](/create-element-with-javascript), you have several options to add it to the DOM:

1. [append](#1-append-method)
2. [prepend](#2-prepend-method)
3. [appendChild](#3-appendchild-method)
4. [after](#4-after-method)
5. [before](#5-before-method)
6. [insertBefore](#6-insertbefore-method)
7. [insertAdjacentElement](#7-insertadjacentelement-method)

Each of these methods allows you to perform a specific action depending on your needs.

Initial HTML markup as an example:

```html
<div class="hero-section">
  <h1 class="hero-heading">Hello World! 👋</h1>
</div>
```

## 1. append() method

The [`ParentNode.append()`](https://developer.mozilla.org/en-us/docs/Web/API/ParentNode/append) method appends a set of [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node) or [DOMString](https://developer.mozilla.org/en-US/docs/Web/API/DOMString) objects after the last child of the `ParentNode`. This means that you can append not only HTML elements but also text.

For this example, we'll create a new paragraph element and use the `append()` method to add it as a last child to the `.hero-section` element.

```javascript
const section = document.querySelector('.hero-section')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

section.append(newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <h1 class="hero-heading">Hello World! 👋</h1>
  <p>Nice to meet you.</p>
</div>
```

To append multiple Nodes `append()` method accepts a set of Node objects as an argument, use [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) to pass arguments:

```javascript
ParentNode.append(...nodesOrDOMStrings)
```

**Browser support:** The `append()` method is [supported](https://caniuse.com/mdn-api_headers_append) in all browsers except Internet Explorer ([polyfill is available](https://developer.mozilla.org/en-us/docs/Web/API/ParentNode/append#polyfill)). 

## 2. prepend() method

The [`ParentNode.prepend()`](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/prepend) method does essentially the same thing as `append()`, but instead, it inserts a set of Nodes before the first child the `ParentNode`.

```javascript
const section = document.querySelector('.hero-section')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

section.prepend(newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <p>Nice to meet you.</p>
  <h1 class="hero-heading">Hello World! 👋</h1>
</div>
```

Just like `append()`, the `prepend()` method accepts a set of Node as an argument, with a spread syntax to pass arguments:

```javascript
ParentNode.prepend(...nodesOrDOMStrings)
```

**Browser support:** The `prepend()` method is [supported](https://caniuse.com/mdn-api_parentnode_prepend) in all browsers except Internet Explorer ([polyfill is available](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/prepend#polyfill)).

## 3. appendChild() method

As the method name states [`Node.appendChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild) adds an element to the end of the node list of a parent element.

Unlike `append()` method `appendChild()` accepts only Node objects, so you're not able to add strings, also you cannot pass more than one node as an argument.

```javascript
const section = document.querySelector('.hero-section')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

section.appendChild(newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <h1 class="hero-heading">Hello World! 👋</h1>
  <p>Nice to meet you.</p>
</div>
```

**Browser support:** The `appendChild()` method is [supported](https://caniuse.com/mdn-api_node_appendchild) in all browsers.

## 4. after() method

The [`ChildNode.after()`](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/after) method inserts a set of Node or DOMString objects after this `ChildNode`.

```javascript
const heading = document.querySelector('.hero-heading')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

heading.after(newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <h1 class="hero-heading">Hello World! 👋</h1>
  <p>Nice to meet you.</p>
</div>
```

To add multiple Node or DOMString objects pass them as an argument, with a spread syntax:

```javascript
ChildNode.after(...nodesOrDOMStrings)
```

**Browser support:** The `after()` method is [supported](https://caniuse.com/mdn-api_childnode_after) in all browsers except Internet Explorer ([polyfill is available](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/after#polyfill)).

## 5. before() method

The [`ChildNode.before()`](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/before) method is the opposite of the above method. It inserts a set of Node or DOMString objects before this `ChildNode`.

```javascript
const heading = document.querySelector('.hero-heading')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

heading.before(newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <p>Nice to meet you.</p>
  <h1 class="hero-heading">Hello World! 👋</h1>
</div>
```

To add multiple Node or DOMString objects pass them as an argument, with a spread syntax:

```javascript
ChildNode.before(...nodesOrDOMStrings)
```

**Browser support:** The `before()` method is [supported](https://caniuse.com/mdn-api_childnode_before) in all browsers except Internet Explorer ([polyfill is available](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/before#polyfill)).

## 6. insertBefore() method

The [`Node.insertBefore()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore) method inserts a node before a reference node as a child of a specified parent node.

This method accepts two arguments a new Node and a reference Node.

```javascript
const section = document.querySelector('.hero-section')
const heading = document.querySelector('.hero-heading')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

section.insertBefore(heading, newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <p>Nice to meet you.</p>
  <h1 class="hero-heading">Hello World! 👋</h1>
</div>
```

**Browser support:** The `insertBefore()` method is [supported](https://caniuse.com/mdn-api_node_insertbefore) in all browsers.

## 7. insertAdjacentElement() method

The [`Element.insertAdjacentElement()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement) method inserts a given element node at a given position relative to the element it is invoked upon.

This method accepts two arguments position and the inserted element. Possible positions are:

* `'beforebegin'`: Before the `targetElement` itself.
* `'afterbegin'`: Just inside the `targetElement`, before its first child.
* `'beforeend'`: Just inside the `targetElement`, after its last child.
* `'afterend'`: After the `targetElement` itself.

```javascript
const section = document.querySelector('.hero-section')
const newParagraph = document.createElement('p')
newParagraph.textContent = 'Nice to meet you.'

section.insertAdjacentElement('afterend', newParagraph)
```

**Result:**

```html
<div class="hero-section">
  <h1 class="hero-heading">Hello World! 👋</h1>
</div>
<p>Nice to meet you.</p>
```

**Browser support:** The `insertAdjacentElement()` method is [supported](https://caniuse.com/insert-adjacent) in all browsers.