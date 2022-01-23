---
layout: post
permalink: advanced-console-log-javascript
title: Advanced console log and other console tools in JavaScript
date: 2021-09-29T21:18:25.765Z
description: Tricks and tips to make your JavaScript console log more productive
  and efficient.
tags: [javascript]
---
Logging to the console is an essential part of debugging in JavaScript. In this article, I’d like to show you some tricks and tips to make your JavaScript console log more productive and efficient.

Contents of the article:

1. [console.log](#consolelog)
2. [console.table](#consoletable)
3. [console.trace](#consoletrace)
4. [console.count](#consolecount)

## console.log

### Arguments

Most know about the `console.log()` method, it outputs passed argument to the browser console.

```javascript
console.log('Test')
// Test
```

But you can pass multiple arguments to this method:

```javascript
console.log('Test', '. Hello ', 'World!')
// Test. Hello World!
```

Argument types can be different, that’s quite handy when you need to specify what you’re logging:

```javascript
const userName = 'Jon Doe'

console.log('userName: ', userName)
// userName: Jon Doe
```

This way you’ll know the variable name you’re logging.

You can also log a variable as an object property by wrapping it into curly braces:

```javascript
const userName = 'Jon Doe'

console.log({ userName })
// { userName: 'Jon Doe' }
```

This approach is useful when you need to log multiple variables or items to the console.

If you don’t have a variable name defined but the object instead, and you want to log a specific property like in the example above you can define the property inside the object you’re logging:

```javascript
const user = {
  name: 'Jon Doe'
}

console.log({ userName: user.name })
// { userName: 'Jon Doe' }
```

Also, you can use the spread operator to log the contents of the array on one line:

```javascript
const user = {
  name: 'Jon Doe'
}

const userData = [user, 'foo', 'bar']

console.log(...userData)
// {name: 'Jon Doe'} 'foo' 'bar'
```

**NOTE: To log objects and arrays you can use the `console.table` method listed below.**

### Formatting

The `console.log()` method also allows you to add some styling to your messages. To do that you need to add a `%c` specifier to your message and pass CSS styling as an additional parameter to the `log()` method.

```javascript
console.log('%c console.log is awesome', 'color: green; font-size: 16px');
```

<figure>
  <img class="shadow lozad" data-src="/images/misc/styled-console-log.png" alt="Styled console log">
  <noscript>
    <img class="shadow" src="/images/misc/styled-console-log.png" alt="Styled console log">
  </noscript>
  <figcaption>Styled console log</figcaption>
</figure>

## console.table

Use `console.table()` to display object or array data as a table.

```javascript
const user = {
  name: 'Jon Doe',
  age: 42
}
const fruits = ['banana', 'apple', 'kiwi']

console.table(user)
console.table(fruits)
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/console-table.png" alt="Console table">
  <noscript>
    <img class="shadow" src="/images/dev-tools/console-table.png" alt="Console table">
  </noscript>
  <figcaption>Console table</figcaption>
</figure>

## console.trace

A handy method to log to console the stack trace. It will show you the function call path up until your `console.trace()` call. Quite useful during the debug process to instantly show which functions gets called.

```javascript
function toggleClass(el, className) {
  el.classList.toggle(className);
  console.trace('toggleCLass')
}

function handleClick(e){
  toggleClass(e.currentTarget, 'active')
}

const heading = document.getElementById('main-heading')

heading.addEventListener('click', handleClick)
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/console-trace.png" alt="Console trace">
  <noscript>
    <img class="shadow" src="/images/dev-tools/console-trace.png" alt="Console trace">
  </noscript>
  <figcaption>Console trace</figcaption>
</figure>

## console.count

A method acts as a counter and is used to output the number of times the particular `count()` method has been called.

You can pass a string (label) as an argument and it will output like a regular `console.log` with a number next to it. If no argument is specified then the default label will be shown.

```javascript
function handleClick(){
  console.count('click count')
}

const heading = document.getElementById('main-heading')

heading.addEventListener('click', handleClick)
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/console-count.png" alt="Console count">
  <noscript>
    <img class="shadow" src="/images/dev-tools/console-count.png" alt="Console count">
  </noscript>
  <figcaption>Console count</figcaption>
</figure>

This method is useful when checking the number of times a certain function gets called, like the event handler.