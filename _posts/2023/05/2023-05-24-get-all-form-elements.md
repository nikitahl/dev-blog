---
layout: post
permalink: get-all-form-elements
title: Get all form's elements in JavaScript
date: 2023-05-24T14:24:12.131Z
description: When working with forms, there are cases when you need to get all of the form elemens in a nice and structured way.
tags: [javascript]
---

When working with forms, there are cases when you need to get all of the form elements in a nice and structured way. JavaScript offers a native way to get all of the form's elements.

## Get all element

Consider the following HTML form:

```html
<form class="newsletter-form">
  <fieldset>
    <label for="name">Name: </label>
    <input type="text" name="name" id="name" required>
  </fieldset>
  <fieldset>
    <label for="email">Email: </label>
    <input type="email" name="email" id="email" required>
  </fieldset>
  <fieldset>
    <label for="newsletter">I'd like to receive newsletter: </label>
    <input type="checkbox" name="newsletter" id="newsletter">
  </fieldset>
  <fieldset>
    <button type="submit" name="submit">Subscribe</button>
  </fieldset>
</form>
```

To get all form elements use the [`elements` property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements){:target="_blank"} on a `form` tag.

```javascript
const form = document.querySelector('.newsletter-form')

form.elements // HTMLFormControlsCollection(8) [fieldset, input#name, fieldset, input#email, fieldset, input#newsletter, fieldset, button, name: input#name, email: input#email, newsletter: input#newsletter, submit: button]
```

In the console it will look as follows:

<figure>
  <img class="shadow" src="/images/dev-tools/form-elements.webp" alt="All form's elements with JavaScript" loading="lazy">
  <figcaption>All form's elements</figcaption>
</figure>

As you can see `elements` property will return an HTMLCollection. 

To access items you can use it as an Array to access by index or as an Object to access via `name` property which corresponds to the HTML `name` attribute.

The elements that are returned via the `elements` property will contain the following elements:

* `button`
* `fieldset`
* `input`
* `object`
* `output`
* `select`
* `textarea`

To [convert](/convert-array-like-collections-to-array) HTMLCollection to an Array you can use `Array.from()` method.

Now you can use `forEach` to iterate over this Array and [find specific items](/how-to-find-an-item-in-a-javascript-array).

Other benefit of having an Array instead of HTMLCollection is that you can use [Array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array){:target="_blank"} like `.map()`, `.filter()`, `.sort()`, etc.

```javascript
const form = document.querySelector('.newsletter-form')

Array.from(form.elements) // (8) [fieldset, input#name, fieldset, input#email, fieldset, input#newsletter, fieldset, button]
```

<figure>
  <img class="shadow" src="/images/dev-tools/form-elements-as-an-array.webp" alt="All form's elements as an Array with JavaScript" loading="lazy">
  <figcaption>All form's elements as an Array</figcaption>
</figure>

## Get only inputs

If you want to get only `input` elements then you can use the `querySelectorAll()` method.

```javascript
const formElements = document.querySelectorAll('.newsletter-form input')

formElements // NodeList(3) [input#name, input#email, input#newsletter]
```

<figure>
  <img class="shadow" src="/images/dev-tools/form-input-elements.webp" alt="Form's input elements" loading="lazy">
  <figcaption>All form's input elements</figcaption>
</figure>

In this case, you'll get a NodeList of input elements. Similar to HTMLCollection, it is not an Array, so you won't be able to use Array methods until you convert it to an Array.

```javascript
const formElements = document.querySelectorAll('.newsletter-form input')

Array.from(formElements) // (3) [input#name, input#email, input#newsletter]
```

## Conclusion

Use `elements` property when you need to get each form element. The HTMLCollection offers a way to access items via their name. However, if you want to iterate over it, you’ll need to convert it to an Array.

On the other hand, you can always use the `for` loop to iterate over HTMLCollection, and then use the `name` property.

To get a set of specific form elements you can use the `querySelectorAll()` method and specify the elements you wish to get. This approach would make sense to get specific form elements, for example, certain inputs that are confined within a fieldset element.



