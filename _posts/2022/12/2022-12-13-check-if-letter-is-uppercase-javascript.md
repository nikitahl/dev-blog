---
layout: post
permalink: check-if-letter-is-uppercase-javascript
title: Check if the letter is uppercase in JavaScript
date: 2022-12-13T14:26:48
description: To check if the letter is uppercase in JavaScript you can use the toUpperCase() method or check against a regular expression
tags: [javascript]
---

While working with strings, especially when validating forms, you may want to check whether the letter is uppercase.

By applying a few methods you can check almost any character's case.

## String.toUpperCase() and String.toLowerCase() method

The [`String.toUpperCase()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase){:target="blank"} will convert a string to uppercase, after that you can compare it to your test letter.

```javascript
const charA = "W"
const charB = "b"

console.log(charA.toUpperCase()) // W
console.log(charA.toUpperCase() === charA) // true

console.log(charB.toUpperCase()) // B
console.log(charB.toUpperCase() === charB) // false
```

However there’s a downside to this approach. If the character happens to be a number, punctuation or special character then it would not work.

The `toUpperCase()` method would just return a given value (number or punctuation), so the condition would be `true` in these cases.

```javascript
const charA = "3"
const charB = ";"

console.log(charA.toUpperCase()) // "3"
console.log(charA.toUpperCase() === charA) // true

console.log(charB.toUpperCase()) // ";"
console.log(charB.toUpperCase() === charB) // true
```
To handle this issue we need to extend the condition and check whether the character has an uppercase and lowercase variant by using the `toLowerCase` method.

```javascript
const charA = "3"
const charB = ";"

console.log(charA.toUpperCase() === charA && charA.toLowerCase() !== charA) // false
console.log(charB.toUpperCase() === charB && charB.toLowerCase() !== charB) // false
```

This condition will work for almost any letter in any language. You can wrap it into a function and pass a character as a parameter:

```javascript
const isUpperCase = (character) => {
  return character.toUpperCase() === character && character.toLowerCase() !== character
}

isUpperCase("W") // true
isUpperCase("b") // false
isUpperCase("3") // false
isUpperCase(";") // false
isUpperCase("ç") // false
isUpperCase("Ç") // true
isUpperCase("г") // false
isUpperCase("Г") // true
```

## Checking against a regular expression
Another approach would be to match a string against a regular expression. You can use `test()` or `match()` methods to check if the letter is uppercase.

The regular expression must include all capital letters of the alphabet within a character set, so in our case it will be `/[A-Z]/`.

To get the boolean value you can use the [`test()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test){:target="blank"}, it will test a string against a regular expression and will return `true` if at least one character is uppercase, otherwise it will return `false`.

```javascript
const regExp = /[A-Z]/

console.log(regExp.test("a")) // false
console.log(regExp.test("A")) // true
console.log(regExp.test("3")) // false
console.log(regExp.test(";")) // false
console.log(regExp.test("abCdefg1234?!,.;")) // true
console.log(regExp.test("abcdefg1234?!,.;")) // false
```

The [`match` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match){:target="blank"} will return an array if character is matched against a regular expression, otherwise it will return `null`. 

```javascript
const regExp = /[A-Z]/

console.log("a".match(regExp)) // null
console.log("3".match(regExp)) // null
console.log(";".match(regExp)) // null
console.log("A".match(regExp)) // ['A', index: 0, input: 'A', groups: undefined]
```

To handle letters from languages other than English for both `test` and `match` methods, you’ll need to extend your regular expression by specifying the first and the last letter of each alphabet you’re going to check.

```javascript
const regExp = /[A-ZÀ-ÖА-Я]/
```
