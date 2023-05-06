---
layout: post
permalink: loop-through-an-object-in-javascript
title: A Complete Guide How to Loop Through Object in JavaScript (+ performance tests)
date: 2020-11-05T11:11:22.105Z
description: There are different ways how to loop through object in JavaScript.
  It includes a built-in approach and a few workarounds that involves working
  with Arrays.
tags: [javascript]
---
There are multiple different ways how to loop through object in JavaScript. But ...

**NOTE: in JavaScript, there's only one built-in way to loop through an object (for...in), all other ways are custom approaches utilizing Arrays.**

That said, looping (iterating) through an object can be divided into two main approaches:

1. [`for..in` statement](#1-forin-statement)
2. [Convert the object to an Array](#2-convert-the-object-to-an-array) and use different methods/loops on it

   1. [`forEach` method](#21-foreach-method)
   2. [`for...of` statement](#22-forof-statement)
   3. [`for` statement](#23-for-statement)
   4. [`while` statement](#24-while-loop)

But before we move on, there's an important detail to understand. All of the below approaches will iterate only over `enumerable` object properties.

> Enumerable properties are those properties whose internal enumerable flag is set to true, which is the default for properties created via simple assignment or via a property initializer
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)

This means that if the object's property `enumerable` flag is set to `false`, then the loop will not iterate over this property.

To check an object's property `enumerable` flag you can use the [`getOwnPropertyDescriptor`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor) method.

Example object.

```javascript
const car = {
  name: "Audi",
  model: "A6",
  year: 2012,
  isUsed: true,
  transmission: "manual"
}

Object.getOwnPropertyDescriptor(car, 'name')
// Output:
// {
//   configurable: true
//   enumerable: true
//   value: "Audi"
//   writable: true
// }
```

## 1. for...in statement

Let's start with the built-in approach. JavaScript offers a nice way to loop over an object. It is [`for..in` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in). We'll use the `car` object shown above.

```javascript
for (let property in car) {
 console.log(`${property}: ${car[property]}`)
}

// Output:
// "name: Audi"
// "model: A6"
// "year: 2012"
// "isUsed: true"
// "transmission: manual"
```

As you can see you have a clear and simple construction inside which you have access to both property name and property value.

One of the drawbacks of this method that it will loop over all properties. This means that you cannot break the loop, and have to wait when it finishes.

**Browser support:** [Supported in all browsers](https://caniuse.com/mdn-javascript_statements_for_in)

## 2. Convert the object to an Array

The second approach is quite custom and can be divided into a few separate ways. But first, to convert the object to an Array, you can use one of three methods:

1. [`Object.keys()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) - *returns an array of a given object's own enumerable property names* ([supported in all browsers](https://caniuse.com/mdn-javascript_builtins_object_keys))*;*
2. [`Object.values()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values) - *returns an array of a given object's own enumerable property values* ([some older browsers lacking support](https://caniuse.com/object-values))*;*
3. [`Object.entries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) - *returns an array of a given object's own enumerable string-keyed property `[key, value]` pairs* ([some older browsers lacking support](https://caniuse.com/object-entries)).

Now, you can use one of the below ways to iterate over a received Array:

```javascript
const carKeys = Object.keys(car)

// carKeys value:
// ["name", "model", "year", "isUsed", "transmission"]
```

### 2.1. forEach method

The first approach is to use is `forEach`, one of the available [Array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Instance_methods).

> forEach calls a provided `callback` function once for each element in an array in ascending order
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

For the above `carKeys` Array:

```javascript
carKeys.forEach((carKey, index) => {
  console.log(`${index}. ${carKey}: ${car[carKey]}`)
});

// Output:
// "0. name: Audi"
// "1. model: A6"
// "2. year: 2012"
// "3. isUsed: true"
// "4. transmission: manual"
```

With `forEach`, you are also able to get both object property name and property value for each Array entry. In addition, the callback function accepts up to four arguments: `currentValue`, `index`, `array`, `thisArg`. These arguments sometimes might be quite handy, like the `index` to set a flag or place an `if` statement.

**Browser support:** [Supported in all browsers](https://caniuse.com/mdn-javascript_builtins_array_foreach)

### 2.2. for...of statement

The [`for...of` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) will iterate over [iterable objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol), like an Array. So with the `carKeys` Array it will look like this:

```javascript
for (let carKey of carKeys) {
  console.log(`${carKey}: ${car[carKey]}`)
}

// Output:
// "name: Audi"
// "model: A6"
// "year: 2012"
// "isUsed: true"
// "transmission: manual"
```

This is very similar to the `for...in` statement. The only difference is what they iterate over. And unlike the `forEach` method the `for...in` statement executes a code once per Array entry without any additional arguments.

**Browser support:** [Some older browsers lacking support](https://caniuse.com/mdn-javascript_statements_for_of)

### 2.3. for statement

The basic `for` statement that you're probably already familiar with. If not,

> The **for statement** creates a loop that consists of three optional expressions, enclosed in parentheses and separated by semicolons, followed by a statement (usually a [block statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)) to be executed in the loop.
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)

It can be used to iterate over just about anything (except the object, like the initial `car`). We can use it to loop over the `carKeys` Array.

```javascript
for (let i = 0; i < carKeys.length; i++) {
  console.log(`${i}. ${carKeys[i]}: ${car[carKeys[i]]}`)
}

// Output:
// "0. name: Audi"
// "1. model: A6"
// "2. year: 2012"
// "3. isUsed: true"
// "4. transmission: manual"
```

With this approach, you also have the access to the property name, property value, and index all in one block. Another good thing about it is that you can break the loop when needed by using `break` statement.

**Browser support:** [Supported in all browsers](https://caniuse.com/mdn-javascript_statements_for)

### 2.4. while loop

The last approach is to use the `while` statement.

> The **while statement** creates a loop that executes a specified statement as long as the test condition evaluates to true. The condition is evaluated before executing the statement.
>
> \- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)

It can be used as follows:

```javascript
let i = 0
while (i < carKeys.length) {
  console.log(`${i}. ${carKeys[i]}: ${car[carKeys[i]]}`)
  i++
}

// Output:
// "0. name: Audi"
// "1. model: A6"
// "2. year: 2012"
// "3. isUsed: true"
// "4. transmission: manual"
```

It is quite similar to `for` statement. You have access to all the properties and values. As well as you are able to break the loop at any given point by using the `break` statement.

The thing that differs it from other loops, is that you can write custom condition for the next evaluation.

**Browser support:** [Supported in all browsers](https://caniuse.com/mdn-javascript_statements_while)

## Performance tests

For performance comparison, all of the above approaches have been run with a benchmark test at [jsbench.me](https://jsbench.me/) playground.

A benchmark test takes an object with a hundred entries and runs it for each case.

The fastest approach is the `forEach` method. Performance test results can be viewed and tested at [jsbench.me](https://jsbench.me/a3kh4jp5ot).

<figure>
  <img class="shadow" src="/images/misc/object-iterate-performance.png" alt="Object Iterate Performance Test Results" loading="lazy">
  <figcaption>Object Iterate Performance Test Results</figcaption>
</figure>