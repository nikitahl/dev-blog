---
layout: post
permalink: create-element-with-javascript
title: How to create a new element with class name in JavaScript
date: 2021-02-02T14:06:55.871Z
updated: 2022-09-02T22:17:50.114Z
description: A complete guide to create a new element with class name in
  JavaScript. Native solution explained plus a tip on creating a custom function
tags: [javascript]
---

JavaScript provides a native way to create new elements. A single [`createElement()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) method is available inside the document object which is [supported by all browsers](https://caniuse.com/mdn-api_document_createelement). But it's not enough to create a new element with a class name or any other attributes for that matter. 

## Creating an element

The `createElement()` method accepts two arguments, first one is being the HTML tag of the new element.

```javascript
const anchorElement = document.createElement('a')
```

It is relatively easy to use. However, **this method creates an empty element** (without any content) and without any attributes. So additional steps must be taken if you wish to create a more meaningful element.

## Adding content to the new element

To add content to your element you can choose one of four ways, depending on your needs. It can be:

1. [`innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) - to set HTML to the element;
2. [`innerText`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText) - to set the text of the element;
3. [`textContent`](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) - to set text node to the element;
4. [`appendChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild) - to append HTML elements or Nodes to the element.

In our case let's use `innerText` property for the sake of example:

```javascript
anchorElement.innerText = 'Apply Now'
```

## Adding custom class name and attributes

So when the content is added let's add missing attributes with [`setAttribute()`](https://developer.mozilla.org/en-us/docs/Web/API/Element/setAttribute) method:

```javascript
anchorElement.setAttribute('href', 'https://example.com/apply-now')
```

To add a class name to your element you can use the `classList` property with the `add` method:

```javascript
anchorElement.classList.add('apply-now-link')
```

Finally to [add created element](/add-element-with-javascript) to the DOM, use the `appendChild()` method:

```javascript
document.body.appendChild(anchorElement)
```

The final code snippet looks as follows:

```javascript
const anchorElement = document.createElement('a')
anchorElement.innerText = 'Apply Now'
anchorElement.setAttribute('href', 'https://example.com/apply-now')
anchorElement.classList.add('apply-now-link')
document.body.appendChild(anchorElement)
```

## Creating custom function

The example given above is quite simple. But imagine creating multiple different elements dynamically that could contain different attributes.

For that, you can create your own custom helper function that will create a new element and set attributes.

```javascript
function createCustomElement (tag, content, attributes) {
  const element = document.createElement(tag)
  element.innerHTML = content
  for (const name in attributes) {
    element.setAttribute(name, attributes[name])
  }
  return element
}
```

Let's break it down. The function accepts three arguments.

First, it creates a new element from the `tag` argument which should be a string.

Next, it sets the `content` via `innerHTML` property for more versatility (you can pass both text and HTML strings).

Then, it iterates over the `attributes` argument (should be an object), and sets corresponding HTML attributes with values.

Finally, the function returns a new element.

Compose necessary arguments and then use the function as follows:

```javascript
const tag = 'a'
const content = 'Apply Now'
const elementAttributes = {
  href: 'https://example.com',
  class: 'link',
  target: '_blank',
  rel: 'noopener noreferrer'
}

const newAnchor = createCustomElement(tag, content, elementAttributes)
document.body.appendChild(newAnchor)
```

Now you can re-use this function in different places to create your own ready-to-go elements with content and attributes.

End result: 

```javascript
function createCustomElement (tag, content, attributes) {
  const element = document.createElement(tag)
  element.innerHTML = content
  for (const name in attributes) {
    element.setAttribute(name, attributes[name])
  }
  return element
}

const tag = 'a'
const content = 'Apply Now'
const elementAttributes = {
  href: 'https://example.com',
  class: 'link',
  target: '_blank',
  rel: 'noopener noreferrer'
}

const newAnchor = createCustomElement(tag, content, elementAttributes)
document.body.appendChild(newAnchor)
```

## Update

As noted by [@Jhey](https://twitter.com/jh3yy), you can [create a new element](https://twitter.com/jh3yy/status/1564926775620243456) with all the attributes using the [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) method.

This approach is much cleaner:

```javascript
const newAnchor = Object.assign(
  document.createElement('a'),
  {
    innerText: 'Apply Now',
    href: 'https://example.com',
    className: 'link',
    target: '_blank',
    rel: 'noopener noreferrer'
  }
)

document.body.appendChild(newAnchor)
```
