---
layout: post
title: TILs in June, July and August 2019
description: A summarized list of my web development related TILs in Summer of 2019
tags: [html, css, javascript, til]
comments: true
---

It has been three busy summer months. I bring you my list of the things I've learned over this period.

1. [Variable fonts](#variable-fonts)
2. [Native JavaScript methods to manipulate text nodes](#native-javascript-methods-to-manipulate-text-nodes)
3. [Capture the change of contenteditable element](#capture-the-change-of-contenteditable-element)
4. [The formation of element's inner border-radius](#the-formation-of-elements-inner-border-radius)
5. [SVG elements have an extra space below](#svg-elements-have-an-extra-space-below)
6. [Global variable of id attribute](#global-variable-of-id-attribute)
7. [New JavaScript feature - optional chaining](#new-javascript-feature---optional-chaining)
8. [Duplicate selector with CSS](#duplicate-selector-with-css)
9. [Javascript in operator](#javascript-in-operator)
10. [JavaScript native string method endsWidth](#javascript-native-string-method-endsWidth)

## Variable Fonts
It is a technology which allows an **Open Type variable font** to store multiple fonts within a single file. This technology was introduced by Microsoft, Google, Apple, and Adobe.

The cool thing about these fonts, that the way these fonts looks can be controlled with the help of CSS. A `font-variation-settings` property must be used in order to control the parameters of the font.

Usefull resources on variable fonts:
- [Variable Fonts](https://v-fonts.com/){:target="blank"}
- [MDN font-variation-settings](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variation-settings
){:target="blank"}
- [Google's Introduction to variable fonts on the web
](https://developers.google.com/web/fundamentals/design-and-ux/typography/variable-fonts/){:target="blank"}
- [Introducing OpenType Variable Fonts on Medium](https://medium.com/variable-fonts/https-medium-com-tiro-introducing-opentype-variable-fonts-12ba6cd2369){:target="blank"}

## Native JavaScript methods to manipulate text nodes
The [`normalize()` method](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize){:target="blank"} will merge element's text nodes into one node.

```javascript
const text = document.createElement("p")

text.appendChild(document.createTextNode("Hello "))
text.appendChild(document.createTextNode("World!"))

// text.childNodes.length === 2
// text.childNodes[0].textContent === "Hello "
// text.childNodes[1].textContent === "World"

text.normalize();

// text.childNodes.length === 1
// text.childNodes[0].textContent === "Hello World!"
```

The [`wholeText()` method](https://developer.mozilla.org/en-US/docs/Web/API/Text/wholeText){:target="blank"} on the other hand *"returns the full text of all Text nodes logically adjacent to the node"*.

```javascript
const text = document.createElement("p")

text.appendChild(document.createTextNode("Hello "))
text.appendChild(document.createTextNode("World!"))

text.childNodes[0].wholeText // "Hello World!"

// text.childNodes.length === 2
// text.childNodes[0].textContent === "Hello "
// text.childNodes[1].textContent === "World"
```

## Capture the change of contenteditable element
To do so an [`"input"` event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event){:target="blank"} is used on a `contenteditable` element.

```html
<p class="text" contenteditable>Hello World!</p>
```

```javascript
const text = document.querySelector('.text')

text.addEventListener('input', updateValue)

function updateValue(e) {
  console.log(e.target.value)
}
```

## The formation of element's inner border-radius
The element's inner border-radius is formed by the following formula:

> the outer border radius minus the corresponding border thickness

I actually wrote an article on [how to adjust element inner border radius](https://nikitahl.com/adjust-element-inner-border-radius/) thanks to that discovery.

## SVG elements have an extra space below
I was having an issue with SVG element inside a `<div>`. The [SVG had a small space below](https://stackoverflow.com/questions/24626908/how-to-get-rid-of-extra-space-below-svg-in-div-element
){:target="blank"} thus a `<div>` wasn't wrapping it tightly.

> This is because inline-block elements (like `<svg>` and `<img>`) sit on the text baseline. The extra space is the space left to accommodate character descenders (the tail on 'y', 'g' etc).

I've found a solution with a sprinkle of CSS.

```html
<div>
  <svg style="display: block;">
    ...
  </svg>
</div>
```

## Global variable of id attribute
Setting `id` on an html element creates a global variable. Might be useful for quick prototyping and access in the browser console.

> may also cause a bug and headache (name clash)

```html
<div id="helloWorld">Hello World!</div>
```

```javascript
window.helloWorld
// <div id="helloWorld">Hello World!</div>
```

## New JavaScript feature - optional chaining
<blockquote>
	Optional chaining allows developers to reference object properties which may or may not exist without trigger an error.
	<br />
	&mdash;<cite><a href="https://davidwalsh.name/optional-chaining" target="_blank">David Walsh</a></cite>
</blockquote>

So instead of using long conditionals with logical AND (`&&`) operator:

```javascript
const car = {
  name: "Audi",
  model: "A6",
  parts: {
    wheels: 4,
    doors: 2
  }
}

if (car && car.parts && car.parts.wheels) {
  // ...
}
```

You can go like so:

```javascript
const wheels = car?.parts?.wheels
```

## Duplicate selector with CSS
This is actually one of suggestions on MDN docs to avoid using `!important`:
<blockquote>
	duplicate simple selectors to increase specificity when you have nothing more to specify.
		<br />
	&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#The_!important_exception" target="_blank">MDN</a></cite>
</blockquote>

```css
#myId#myId span { color: yellow; }
.myClass.myClass span { color: orange; }
```

## Javascript in operator
A clear and simple way to check if the property exists in an object.
<blockquote>
	The <code>in</code> operator returns <code>true</code> if the specified property is in the specified object or its prototype chain.
	&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in" target="_blank">MDN</a></cite>
</blockquote>
So instead of using `hasOwnProperty()` method or chaining you can go:

```javascript
const car = {
  name: "Audi",
  model: "A6",
  parts: {
    wheels: 4,
    doors: 2
  }
}

console.log("parts" in car);
// true

if ("parts" in car) {
  // ...
}
```

## JavaScript native string method endsWidth
A cool native way to check if the given string is the last set of characters in the specified string.
<blockquote>
  determines whether a string ends with the characters of a specified string, returning <code>true</code> or <code>false</code> as appropriate.
  &mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith" target="_blank">MDN</a></cite>
</blockquote>

```javascript
const text = "Hello World"

console.log(text.endsWith("World"))
// true

const text2 = "Hello World!"

console.log(text2.endsWith("World"))
// false
```


