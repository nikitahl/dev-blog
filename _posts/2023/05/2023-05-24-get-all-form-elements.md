---
layout: post
permalink: get-all-form-elements
title: Get all form's elements in JavaScript
date: 2023-05-24T14:24:12.131Z
updated: 2023-11-17T08:24:45.111Z
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
    <button type="submit">Subscribe</button>
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

To [convert HTMLCollection](/convert-array-like-collections-to-array) to an Array you can use `Array.from()` method.

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

## Get only specific fields

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

While your form may only contain input fields, that's not always the case. Besides the `input` fields, it can be `select` and `textarea` elements.

Also, there can be some form elements that you don't want to get, like `fieldset` or `button` elements.

So it's a good idea to give each form element a `name` attribute. One of the reasons is the `input` element's value won't be submitted with the form if the [`name` attribute is not specified](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#name){:target="_blank"}.

That way your form will contain fields (elements) that might have a user-generated value.

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
    <label for="topic">Topic: </label>
    <select name="topic" id="topic">
      <option value="html">HTML</option>
      <option value="CSS">CSS</option>
      <option value="javascript">JavaScript</option>
    </select>
  </fieldset>
  <fieldset>
    <button type="submit">Subscribe</button>
  </fieldset>
</form>
```

Now you can get all form elements as previously, and use the `filter` method to get the ones with the `name` attribute.

```javascript
const formElements = Array.from(formElements).filter(element => element.name)

formElements // (4) [input#name, input#email, input#newsletter, select#topic]
```


## Conclusion

Use `elements` property when you need to get each form element. The HTMLCollection offers a way to access items via their name. However, if you want to iterate over it, you’ll need to convert it to an Array.

On the other hand, you can always use the `for` loop to iterate over HTMLCollection, and then use the `name` property.

To get a set of specific form elements you can use the `querySelectorAll()` method and specify the elements you wish to get. This approach would make sense to get specific form elements, for example, certain inputs that are confined within a fieldset element.



