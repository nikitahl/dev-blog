---
layout: post
title: How to get the length of an object with Vanilla JavaScript in 3 ways
description: I'll show you how to get the length of an object with Vanilla JavaScript in 3 easy ways using native methods
tags: [javascript]
comments: true
---

In this article, I'll show you how to get the length of an object with Vanilla JavaScript in 3 ways.

In JavaScript, there's no direct way to call the `length` property on an object.

```javascript
const planet = {
  name: 'Earth',
  order: 3,
  hasJavaScript: true
}

// Calling length property on planet object will result in undefined
planet.length // undefined
```

This is due to the object itself does not possess such property.

```javascript
planet.hasOwnProperty('length') // false
```

You can, however, convert an object to an array and then use the `length` property on it. The JavaScript has three native ways to do so:

1. [Object.keys() method](#1-objectkeys-method)
2. [Object.values() method](#2-objectvalues-method)
3. [Object.entries() method](#3-objectentries-method)

## 1. Object.keys() method

This method returns an array of a given object's own enumerable property names.

```javascript
const planet = {
  name: 'Earth',
  order: 3,
  hasJavaScript: true
}

Object.keys(planet) // ['name', 'order', 'hasJavaScript']
Object.keys(planet).length // 3
```

This approach is **fully cross-browser**, read full docs on [Object.keys() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys){:target="blank"}.

## 2. Object.values() method

This method returns an array of a given object's own enumerable property values.

```javascript
const planet = {
  name: 'Earth',
  order: 3,
  hasJavaScript: true
}

Object.values(planet) // ['Earth', 3, true]
Object.values(planet).length // 3
```

This method is **not supported by Internet Explorer** browser. Find out more about [Object.values() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values){:target="blank"}.

## 3. Object.entries() method

This method returns an array of a given object's own enumerable string-keyed property [key, value] pairs.

```javascript
const planet = {
  name: 'Earth',
  order: 3,
  hasJavaScript: true
}

Object.entries(planet) // [['name', 'Earth'], ['order', 3], ['hasJavaScript', true]]
Object.entries(planet).length // 3
```

This method is **not supported by Internet Explorer** browser. Find out more about [Object.entries() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries){:target="blank"}.

