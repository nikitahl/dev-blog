---
layout: post
permalink: number-value-from-input-javascript
title: How to get number value from input in JavaScript
description: Working with HTML inputs may require handling proper value types, like numbers. However, the value property of an input element will return a string-type value by default.
tags: [javascript]
---

Working with HTML inputs may require handling proper value types, like numbers. However, the `value` property of an input element will return a string-type value by default.

## Default value

Given the input with a `type` of `number` let's get its value.

```html
<input type="number" value="42">
```

By default, the `value` property of the input element will always return a `string` type, even if the input `type` is a `number`.

```javascript
const numberInput = document.querySelector("input[type=number]")

numberInput.value // "42"
```

<p class="note">💡 NOTE: the <code>type</code> attribute of the <code>input</code> element can be equal to a many different values, but its <code>value</code> property will always return a string-type value</p>

## Number value

To get the `number` type value from the input element you can use one of two approaches.

The first one is to convert the string value to a number value with either the [`parseInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt){:target="blank"} or [`parseFloat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat){:target="blank"} method (depending on your needs).

```javascript
const numberInput = document.querySelector("input[type=number]")

parseInt(numberInput.value) // 42
```

This approach is useful when working with input types like `text` or `search`, as the user may input a numeric value, and you may want to capture that.

If the input value is not a number the `parseInt` or `parseFloat` will return a `NaN` value.

`parseInt` and `parseFloat` methods works in all browsers.

The second approach is to use the [`valueAsNumber`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement#instance_properties){:target="blank"} property instead of the `value` property on an input element.

```javascript
const numberInput = document.querySelector("input[type=number]")

numberInput.valueAsNumber // 42
```

The `valueAsNumber` property will always work on input types like: `number`, `range`, `date`, `month`, `time`, and `week`. But if you use this property say on a `text` type input it will return a `NaN` value.

This is a more straightforward approach especially if you know the input `type` you’re working with. `valueAsNumber` property is [supported in all browsers](https://caniuse.com/mdn-api_htmlinputelement_valueasnumber){:target="blank"} as well.

