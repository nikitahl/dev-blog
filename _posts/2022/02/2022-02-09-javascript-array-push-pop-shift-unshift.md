---
layout: post
title: Add and remove items in JavaScript array with push, pop, shift, unshift
description: Developers guide on how to add and remove items in JavaScript with array push, pop, shift, unshift methods
tags: [javascript]
---

JavaScript have native methods to add and remove items at the beginning and the end of array.

1. [Add item at the end push()](#add-item-at-the-end-push)
2. [Add item at the beginning unshift()](#add-item-at-the-beginning-unshift)
3. [Remove last item pop()](#remove-last-item-pop)
4. [Remove first item shift()](#remove-first-item-shift)

## Add item at the end push()

The [`push()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) adds one or more elements to the end of an array and returns the new length of the array.

```javascript
const fruits = ['apple', 'banana', 'orange']

fruits.push('mango') // 4

console.log(fruits) // ['apple', 'banana', 'orange', 'mango']
```

## Add item at the beginning unshift()

The [`unshift()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) adds one or more elements to the beginning of an array and returns the new length of the array.

```javascript
const fruits = ['apple', 'banana', 'orange']

fruits.unshift('mango') // 4

console.log(fruits) // ['mango', 'apple', 'banana', 'orange']
```

## Remove last item pop()

The [`pop()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) removes the last element from an array and returns that element.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

fruits.pop() // 'mango'

console.log(fruits) // ['apple', 'banana', 'orange']
```

## Remove first item shift()

The [`shift()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) removes the first element from an array and returns that removed element.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

fruits.shift() // 'apple'

console.log(fruits) // ['banana', 'orange', 'mango']
```