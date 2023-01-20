---
layout: post
permalink: remove-item-from-array-javascript
title: How to remove a specific item from an array in JavaScript
description: JavaScript doesn’t have a single explicit method to remove a specific item from an array. However, there are a few simple ways you can do that, depending on your needs.
tags: [javascript]
---

JavaScript doesn’t have a single explicit method to remove a specific item from an array. However, there are a few simple ways you can do that, depending on your needs.

1. [Remove by first and last](#remove-by-first-and-last)
2. [Remove by index](#remove-by-index)
3. [Remove by filtering out](#remove-by-filtering-out)
4. [Remove using Set object](#remove-using-set-object)
5. [Notes](#notes)

## Remove by first and last

To remove the [first or last](/javascript-array-push-pop-shift-unshift) item from an array, JavaScript offers the `shift()` and `pop()` methods.

The [shift() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift){:target="blank"} removes the first item in an array and returns that removed element.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

fruits.shift() // 'apple'

console.log(fruits) // ['banana', 'orange', 'mango']

```

The [pop() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop){:target="blank"} removes the last element from an array and returns that element.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

fruits.pop() // 'mango'

console.log(fruits) // ['apple', 'banana', 'orange']
```

## Remove by index

If you need to remove an item at a specific array index, you can use the [`splice()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice){:target="blank"}. This method can remove and replace specific items in a given array. 

It can accept multiple arguments, depending on whether you want to insert additional items or not. But the first argument is the starting index to begin modifying array and the second one is the number of items to remove.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

fruits.splice(2,1) // ['orange']

console.log(fruits) // ['apple', 'banana', mango]
```

## Remove by filtering out

To [find the item in an array](/how-to-find-an-item-in-a-javascript-array) you can use the `indexOf()` method. That way if you know the item’s index you wish to remove, pass it as the first argument into `splice()` method.

 ```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

const removeIndex = fruits.indexOf('orange')
fruits.splice(removeIndex,1) // ['orange']

console.log(fruits) // ['apple', 'banana', mango]
```

Finally you can remove the items from an array without even knowing the item index. That is by using the [`filter()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter){:target="blank"}. This method accepts a callback function that is executed on each item in an array and returns it if the condition is met.

<p class="note">💡 NOTE: the <code>filter()</code> method doesn’t mutate initial array, instead it creates a new modified array.</p>

 ```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

const filteredFruits = fruits.filter(item => item !== 'orange')

console.log(filteredFruits) // ['apple', 'banana', mango]
console.log(fruits) // ['apple', 'banana', 'orange', 'mango']
```
The use of `filter()` method comes in handy when you’re working with an array of objects. Because it may be hard to get the item’s index, and instead you can run each item through a condition and remove multiple at once, instead of removing them one by one. 

## Remove using Set object

The last one is an unconventional approach, but some might find it useful. The [`Set()` constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/Set){:target="blank"} lets you create a [`Set` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set){:target="blank"}, that can store unique values of any type.

<p class="note">💡 NOTE: when creating a new <code>Set</code> object, it will remove all duplicates from the array, leaving only unique values.</p>

The `Set` object can be converted to array with [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax){:target="blank"}. So you can store your array values in a `Set` object and convert them to array when needed.

The `Set` object possess multiple methods, one of which is [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/delete){:target="blank"}. So you can directly remove an item from Set object by passing its value to `delete` method.

```javascript
const fruitsSet = new Set(['apple', 'banana', 'orange', 'mango']);

console.log(fruitsSet) // Set(4) {'apple', 'banana', 'orange', 'mango'}
console.log([...fruitsSet]) // ['apple', 'banana', 'orange', 'mango']

fruitsSet.delete('orange')

console.log(fruitsSet) // Set(3) {'apple', 'banana', 'mango'}
console.log([...fruitsSet]) //['apple', 'banana', 'mango']
```

## Notes

<p class="note">💡 NOTE: using the <code>delete</code> operator on an array won’t delete the item from an array. Instead the value at a given index will be equal to undefined and the array length will remain the same.</p>

 ```javascript
const fruits = ['apple', 'banana', 'orange', 'mango']

delete fruits[2] // true

console.log(fruits) // ['apple', 'banana', empty, 'mango']
console.log(fruits[2]) // undefined
console.log(fruits.length) // 4
```
