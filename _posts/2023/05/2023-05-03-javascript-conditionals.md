---
layout: post
permalink: javascript-conditionals
title: Write better JavaScript conditionals
date: 2023-05-03T20:25:12.133Z
description: You can make your code more concise and readable by writing better conditionals in JavaScript.
tags: [javascript]
---

You can make your code more concise and readable by writing better conditionals in JavaScript.

Of course it depends on the situation, but in this article, I want to show you different ways how you can optimize your condition statements to make your code more [clean and readable](https://www.freecodecamp.org/news/the-junior-developers-guide-to-writing-super-clean-and-readable-code-cd2568e08aae/){:target="_blank"}.

## if statement

One of the first things you'll learn as a developer is `if...else` conditional statement.

`if...else` will execute a block of code inside curly braces depending on a condition.

```javascript
const age = 18
let status = ""

if (age < 18) {
  status = "minor"
} else {
  status = "adult"
}

console.log(status) // adult
```

This approach is good to use when you have multiple actions to perform inside the condition. For example, you need to update class names for DOM elements, update or manipulate an object or an array, call a function, etc.

That way you can clearly see what code gets executed inside a block. Also, you can add more `else if` blocks to handle multiple and more complex conditions that may include AND and OR logical operators.

## switch statement

If you need to check multiple conditions you can use the `switch` statement. It will execute different blocks of code based on the value of a single variable.

```javascript
const dayOfWeek = 4
let dayName = ""

switch (dayOfWeek) {
  case 0:
    dayName = "Sunday"
    break
  case 1:
    dayName = "Monday"
    break
  case 2:
    dayName = "Tuesday"
    break
  case 3:
    dayName = "Wednesday"
    break
  case 4:
    dayName = "Thursday"
    break
  case 5:
    dayName = "Friday"
    break
  case 6:
    dayName = "Saturday"
    break
  default:
    dayName = "Invalid day of week"
    break
}

console.log(`Today is ${dayName}`)
// Today is Thursday
```

When compared to the `if...else` statement, the `switch` statement can be more efficient when checking the value of a single variable against multiple cases, especially if there are many cases.

It can also be more readable and easier to understand when there are many cases and simple actions, like a function call or assigning a variable value.

## Operators

You can make conditional decisions utilizing different operators instead of `if...else` or `switch` statements.

[Logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#logical_operators){:target="_blank"} are great when you need to set a variable value conditionally. Or even use them inside `if...else` statements.

### OR operator

The OR operator in JavaScript is represented by the `||` symbol. It will return `true` if at least one of the operands evaluates to a truthy value in a boolean context.

When setting a variable value, using the OR operator can make the code more concise and readable, especially when dealing with values that might be undefined or empty.

```javascript
const greeting1 = "Hello" || "" // Hello
const greeting2 = "Hello" || "World" // Hello
const greeting3 = "" || "World" // World
const greeting4 = "" || false // false
const greeting5 = false || "" // ""
``` 

As you can see we can set the variable value in just one line as compared to `if...else` or `switch` statements.

### AND operator

Similarly, you can use the AND operator, which is represented by the `&&` symbol.

When evaluating an expression with the AND operator, if the first operand is falsy (i.e., evaluates to `false` in a boolean context), then the entire expression is falsy without evaluating the second operand. This also means that the second operand will be ignored.

However if both operands are truthy (i.e., evaluate to `true` in a boolean context), then the AND operator will return the value of the second operand.

```javascript
const greeting1 = "Hello" && "" // ""
const greeting2 = "Hello" && "World" // World
const greeting3 = true && "Hello" // Hello
const greeting4 = "Hello" && true // true
const greeting5 = false && "Hello" // false
```

Once again we can set the variable value in just one line as compared to `if...else` or `switch` statements.

You can also use the AND operator to invoke functions conditionally.

```javascript
const isActive = true

function getActiveUser (name) {
  return `User name is ${name}`
}

isActive && getActiveUser("Leo") // User name is Leo
```

<p class="note">
💡 NOTE: Using OR (<code>||</code>) and AND (<code>&&</code>) operators for more than just simple boolean comparisons is called the <em>Short-circuit</em> evaluation.
</p>

### Optional chaining

You can check object property existence with the [optional chaining operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining){:target="_blank"} `?.`.

It greatly simplifies the code when checking long object property chain. Instead of using AND operator you can use optional chaining operator.

```javascript
const car = {
  brand: "Audi",
  features: {
    type: "Sedan",
    year: 2012
  }
}

console.log(car?.features?.type) // Sedan
console.log(car?.features?.color) // undefined
```

### Comparison operators

To enhance your conditions and cover more complex cases you can also use [comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators){:target="_blank"}.

```javascript
const score = 75

score === 75 // true
score !== 75 // false
score < 75 // false
score > 75 // false
score >= 75 // true
score <= 75 // true
```

You can even combine comparison operators with logical operators for more complex evaluation.

```javascript
const score = 75
const time = 10000

score > 70 || time < 9000 // true
score > 80 || time < 9000 // false
score > 70 && time < 11000 // true
score > 80 && time < 9000 // false
```

### Ternary operator

Finally, there's a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#conditional_ternary_operator){:target="_blank"}.

The ternary operator is like an `if...else` statement written in one line. It checks a condition, and if it's true, the value after `?` is assigned. If the condition is false, the value after `:` is assigned.

```javascript
const age = 18
const status = age < 18 ? "minor" : "adult"

console.log(status) // adult
```

The ternary operator comes in handy for small conditions and variable assignment.

Similarly as before you can combine comparison operators with logical operators and use them as a condition inside the ternary operator.

```javascript
const score = 100
const time = 10000

const rank = score === 100 && time < 11000 ? "Winner" : "Try again"

console.log(rank) // Winner
```