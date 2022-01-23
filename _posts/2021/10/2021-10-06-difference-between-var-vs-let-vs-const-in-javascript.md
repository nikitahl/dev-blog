---
layout: post
permalink: var-vs-let-vs-const
title: Difference between var vs let vs const in JavaScript
date: 2021-10-06T13:43:26.837Z
description: In JavaScript you can declare a variable using one of three ways,
  var, let, or const. Understanding the difference will help you debug and write
  code more effectively.
tags:
  - javascript
---

In JavaScript you can declare a variable using one of three ways, var, let, or const. But how are they different and which one to use? Understanding the difference will help you debug and write code more effectively.

## Comparison Table

|                 | [var](#var) | [let](#let) | [const](#const) |
| --------------- | :---------: | :---------: | :-------------: |
| Redeclarable    | ✅           | ❌           | ❌               |
| Reassignable    | ✅           | ✅           | ❌               |
| Global property | ✅           | ❌           | ❌               |
| Block scope     | ❌           | ✅           | ✅               |
| Hoisted         | ✅           | ❌           | ❌               |

## Var

### Declaration

The `var` variables can be declared multiple times.

```javascript
var message = "Hello!"
var message = "Hello World!"

console.log(message)
// "Hello World!"
```

Once declared, it can also be reassigned a value:

```javascript
var message = "Hello!"
message = "Hello World!"

console.log(message)
// "Hello World!"
```

### Scope

The `var` variables have a global scope, which means that they can be accessed anywhere from the script.

```javascript
var i = 2
if (i < 0) {
  var message = "Hello"
}

console.log(message)
// "Hello"
```

However, they can be **scoped to a function block**. Now the `message` variable can only be accessed inside the `getMessage` function.

```javascript
// This will be global scope
var greeting = "Hello World"

// This will be function scope
function getMessage () {
  var message = "Hello!"
  return message
}

console.log(message)
// Uncaught ReferenceError: message is not defined
```

One particular trait of the `var` variable is that once declared in the global scope (e.g. at the very beginning of the script) it becomes available as a property in the global `window` object:

```javascript
var message = "Hello!"

console.log(window.message)
// "Hello!"
```

### Hoising

[Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) is a term in JavaScript used to describe the process of moving the declaration of a variable to the top of the script.

So in case of `var` it would look like follows:

```javascript
console.log (message)

var message = "Hello!"

// output will be undefined
```

This is due to the interpreter read this as follows:

```javascript
var message

console.log (message)

message = "Hello!"
```

## Let

### Declaration

The `let` variables can only be declared once. If declared more than once, a Syntax Error will be thrown to the console.

```javascript
let message = "Hello!"
let message = "Hello World!"

// Uncaught SyntaxError: Identifier 'message' has already been declared
```

Same as `var`, `let` variable can also be reassigned a value:

```javascript
let message = "Hello!"
message = "Hello World!"

console.log(message)
// "Hello World!"
```

**NOTE: when used in the global scope it won’t be available in the global window object.**

### Scope

Unlike the `var` variable, `let` is **block-scoped** variable. This means that it’s only accessible inside a single block, which is marked by a set of curly braces.

```javascript
let i = 2
if (i > 0) {
  let message = "Hello"
  console.log("message variable inside if block: ", message)
}

console.log("message variable outside if block: ", message)

// Output:
// "message variable inside if block:  Hello"
// Uncaught ReferenceError: message is not defined
```

### Hoising

`let` variables are also hoisted, but unlike for `var`, the variables are not initialized with a default value of `undefined`. A Reference Error is thrown instead.

```javascript
console.log (message)
let message = "Hello!"

// Uncaught ReferenceError: Cannot access 'message' before initialization
```

## Const

### Declaration

The `const` variables can only be declared once. If declared more than once, a Syntax Error will be thrown to the console.

```javascript
const message = "Hello!"
const message = "Hello World!"

// Uncaught SyntaxError: Identifier 'message' has already been declared
```

Unlike `var` and `let`, the `const` variable cannot  be reassigned a value:

```javascript
const message = "Hello!"
message = "Hello World!"

// Uncaught TypeError: Assignment to constant variable.
```

**NOTE: when used in the global scope it won’t be available in the global window object.**

### Scope

Just like the `let` variable, `const` is **block-scoped** variable. This means that it’s only accessible inside a single block, which is marked by a set of curly braces.

```javascript
const i = 2

if (i > 0) {
  const message = "Hello"
  console.log("message variable inside if block: ", message)
}

console.log("message variable outside if block: ", message)

// Output:

// "message variable inside if block:  Hello"
// Uncaught ReferenceError: message is not defined
```

### Hoising

`const` variables are also hoisted, but unlike for `var`, the variables are not initialized with a default value of `undefined`. A Reference Error is thrown instead.

```javascript
console.log (message)
const message = "Hello!"

// Uncaught ReferenceError: Cannot access 'message' before initialization
```

## Which one to use?

It is considered a good practice to use `let` and `const` most of the time and to avoid using `var`. The reason is since `let` and `const` are block-scoped, it is less likely to produce bugs. Additionally using `let` and `const` over var gives your code more meaning.

Use `const` for constant values. Some developers also use uppercase characters to indicate that this is indeed a const variable:

```javascript
const GREETING_MESSAGE = "Hello World!"
```

When skimming the code you’ll know for sure that this is a `const` variable.

Use `let` for changing values. Since `let` is block-scoped you can use the same name for a variable in multiple blocks.

**Browser Support:**

`var` - <https://caniuse.com/mdn-javascript_statements_var>

`let` - <https://caniuse.com/let>

`const` - <https://caniuse.com/const>