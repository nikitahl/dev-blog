---
layout: post
permalink: join-arrays-in-javascript
title: How to join two arrays in JavaScript
date: 2021-07-28T06:18:27.830Z
description: There are few ways how you can join two arrays in JavaScript,
  spread syntax, .concat() method and push() method
tags:
  - js
---

There are a few ways how you can join two arrays in JavaScript, a spread syntax, a `concat()` method, and a `push()` method.

1. [Joining arrays with the Spread syntax](#joining-arrays-with-the-spread-syntax)
2. [Joining arrays with the `concat()` method](#joining-arrays-with-the-concat-method)
3. [Joining arrays with the `push()` method](#joining-arrays-with-the-push-method)
4. [Dealing with duplicates](#dealing-with-duplicates)

Often joining two arrays is called array merging.

Given you have two arrays:

```javascript
const fruits = ['banana', 'apple']
const veggies = ['corn', 'pumpkin']
```

## Joining arrays with the Spread syntax

The [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) (or spread operator) is used when items from and iterable need to be expanded, e.g. in the array.

So to join fruits and veggies arrays, we’ll create a new variable and assign it a new array:

```javascript
const foods = [...fruits, ...veggies]
foods // ['banana', 'apple', 'corn', 'pumpkin']
```

Using this approach you can actually join multiple arrays:

```javascript
const foods = [...fruits, ...veggies, ...dairy, ...grains]
```

**Browser support for the Spread syntax:** [supported in all major browsers](https://caniuse.com/mdn-javascript_operators_spread_spread_in_arrays) except IE.

## Joining arrays with the .concat() method

The [`concat()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) is used to merge two or more arrays.

You can use it the similar way as the above example, create a new variable and assign it a merged array:

```javascript
const foods = fruits.concat(veggies)
foods // ['banana', 'apple', 'corn', 'pumpkin']
```

**NOTE: The `concat()` method does not change the existing arrays but instead returns a new array.**

To join multiple arrays, just specify each array as an additional argument to the `concat()` method:

```javascript
// another way to use the concat method
const foods = [].concat(fruits, veggies, dairy, grains)
```

**Browser support for the `concat()` method**: [supported in all major browsers](https://caniuse.com/mdn-javascript_builtins_array_concat).

## Joining arrays with the .push() method

In case you want to join arrays and update the value of the initial array (mutate it) you can use the [`push()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push).

The `push()` method adds one or more elements to the end of an array. In order to push a whole array, you’ll need to use the Spread syntax:

```javascript
fruits.push(...veggies)
fruits // ['banana', 'apple', 'corn', 'pumpkin']
```

The `push()` methods accept multiple arguments, so you can join multiple arrays into one:

```javascript
fruits.push(...veggies, ...dairy, ...grains)
```

The `push()` method is a useful approach inside the loops when you need to update the existing array.

**Browser support for the `push()` method:** [supported in all major browsers](https://caniuse.com/mdn-javascript_builtins_array_push).

## Dealing with duplicates

In case the array items you’re joining are strings or numbers, there might be a case when you need to merge duplicate values. So that each item is unique and appears once in the array.

To deal with duplicates you can use the [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/Set) object and assign it to a new variable:

```javascript
const fruits = ['banana', 'apple', 'tomato']
const veggies = ['corn', 'pumpkin', 'tomato']

const foods = [...new Set([...fruits, ...veggies])]
foods // ['banana', 'apple', 'tomato', 'corn', 'pumpkin']
```

In case you’re joining arrays that hold objects or mixed type value items I recommend using the [lodash](https://lodash.com/docs/4.17.15#unionWith) library to check for duplicates and merge them.

Example from lodash using the `unionWith` method to join two arrays that has a duplicate item:

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }]

_.unionWith(objects, others, _.isEqual)

// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```