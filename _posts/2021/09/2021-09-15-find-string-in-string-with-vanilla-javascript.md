---
layout: post
permalink: javascript-find-string-in-string
title: Find string in string with Vanilla JavaScript
date: 2021-09-15T13:28:24.232Z
updated: 2022-12-14T8:48:21.122Z
description: A complete guide to find string in string with JavaScript using the native String methods
tags: [javascript]
---

Finding a substring in a string can be done in a variety of ways, depending on your needs.

JavaScript provides native methods to handle different cases. Let's look at them and try to understand how they work.

To find a string in a string you can use one of the native JavaScript String methods.

1. [`includes` method](#1-includes-method)
2. [`indexOf` method](#2-indexof-method)
3. [`search` method](#3-search-method)
4. [`match` method](#4-match-method)
5. [`matchAll` method](#5-matchall-method)
6. [`startsWith` method](#6-startswith-method)
7. [`endsWith` method](#7-endswith-method)

## 1. includes method

The [`includes` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes){:target="blank"} will perform a **case-sensitive** search on a target string and will determine whether it contains a string to search. It will return a boolean value.

```javascript
const text = 'The World Wide Web is commonly known as the web'

text.includes('world') // false

text.includes('World') // true
```

The `includes` method accepts two arguments `searchString` and `position`.

The `searchString` is a string value to search for.

The `position` is an optional argument that defines the start position within a string at which to begin searching (default value is 0).

**NOTE: The includes method just tells you whether string exists in a target string, it doesn’t tell you the position.**

**Browser support**: [`includes` method](https://caniuse.com/es6-string-includes){:target="blank"}.

## 2. indexOf method

The [`indexOf` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf){:target="blank"} checks for the first occurrence of the specified value in a string and returns its index as an integer. If not found it returns -1. **NOTE: this method is case-sensitive.**

```javascript
const text = 'The World Wide Web is commonly known as the web'

text.indexOf('world') // -1

text.indexOf('World') // 4
```

The `indexOf` method accepts two arguments `searchValue` and `fromIndex`.

The `searchValue` is a string value to search for.

The `fromIndex` is an optional argument that defines the start position within a string at which to begin searching (default value is 0).

**Browser support**: [indexOf method](https://caniuse.com/mdn-javascript_builtins_string_indexof){:target="blank"}.

## 3. search method

The [`search` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search){:target="blank"} performs a match between a regular expression and the target string. It returns its index as an integer. If not found it returns -1.

```javascript
const text = 'The World Wide Web is commonly known as the web'
const regExpSensitive = /world/g
const regExpInsensitive = /world/gi

text.search(regExpSensitive) // -1

text.search(regExpInsensitive) // 4
```

The `search` method accepts only one argument `regexp` which is a [regular expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions){:target="blank"}.

To compose and test regular expressions you can use the [regex101](https://regex101.com/){:target="blank"} tool.

**Browser support**: [search method](https://caniuse.com/mdn-javascript_builtins_string_search){:target="blank"}.

## 4. match method

The [`match` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match){:target="blank"} will check the string against a regular expression and will return an array of found strings based on the regular expression [flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match#return_value){:target="blank"}. If no string is found it will return null.

```javascript
const text = 'The World Wide Web is commonly known as the web'

text.match(/World/)
// [
//   0: "World",
//   groups: undefined,
//   index: 4,
//   input: "The World Wide Web is commonly known as the web"
// ]

text.match(/world/) // null
```

The `search` method accepts only one argument `regexp` which is a [regular expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions){:target="blank"}.

**Browser support**: [match method](https://caniuse.com/mdn-javascript_builtins_string_match){:target="blank"}. 

## 5. matchAll method

The [`matchAll` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll){:target="blank"} returns an [iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators){:target="blank"} of all the string occurrences that match the regular expression parameter.

```javascript
const text = 'The World Wide Web is commonly known as the web'

// use spread syntax to get the results as an array
// 1. Case sensitive
[...text.matchAll(/web/g)]
// [
//   ["web", groups: undefined,index: 44, input: "The World Wide Web is commonly known as the web"]
// ]

// 2. Case insensitive
[...text.matchAll(/web/gi)]
// [
//   ["Web", index: 15, input: "The World Wide Web is commonly known as the web", groups: undefined],
//   ["web", index: 44, input: "The World Wide Web is commonly known as the web", groups: undefined]
// ]
```

**Browser support**: [matchAll method](https://caniuse.com/mdn-javascript_builtins_string_matchall){:target="blank"}.

## 6. startsWith method

The [`startsWith()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith){:target="blank"} checks whether a string begins with a specified character. It returns `true` if the string begins with a character, otherwise it returns `false`.

```javascript
const text = 'The World Wide Web is commonly known as the web'

text.startsWith('The') // true
text.startsWith('The World') // true
text.startsWith('The World', 0) // true

text.startsWith('The', 1) // false
text.startsWith('the') // false
text.startsWith('World') // false
```

The `startsWith()` method accepts two arguments `searchString` and `position`.

The `searchString` is a charachter to be searched for.

The `position` is optional argument and it represents the index at which to start searching for. Default value is `0`.

**Browser support**: [startsWith method](https://caniuse.com/mdn-javascript_builtins_string_startswith){:target="blank"}.

## 7. endsWith method

The [`endsWith()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith){:target="blank"} checks whether a string ends with a specified character. It returns `true` if the string ends with a character, otherwise it returns `false`.

```javascript
const text = 'The World Wide Web is commonly known as the web'

text.endsWith('web') // true
text.endsWith('the web') // true
text.endsWith('the web', 47) // true

text.endsWith('web', 4) // false
text.endsWith('Web') // false
text.endsWith('World') // false
```

The `endsWith()` method accepts two arguments `searchString` and `position`.

The `searchString` is a charachter to be searched for.

The `position` is optional argument and it represents the index at which to start searching for. Default value is `str.length`.

**Browser support**: [endsWith method](https://caniuse.com/mdn-javascript_builtins_string_endswith){:target="blank"}.