---
layout: post
permalink: css-select-previous-element
title: CSS Select previous element
date: 2021-07-08T07:55:24.562Z
description: To select previous element in CSS you'll have to implement a
  workaround as selector for such cases does not exist
tags:
  - css
---
There could be cases when you want to apply a certain styling for the previous element in CSS. But can that be achieved? I’ll try to break it down in this article.

The previous element selector or the previous sibling selector is not available in the CSS (see list of all [available selectors](https://www.w3.org/TR/selectors-3/#selectors)). However a possible workaround exists, and you can imitate such behavior using the flex property.

The most common example could be a `label` with an `input`. On `input` `:hover` or `:focus` state, we would like to highlight the `label` as well, which in this case is comes before the `input`. 

**HTML**:

```html
<div class="field">
  <label class="label" for="email">E-mail:</label>
  <input class="input" type="email" id="email">
</div>
```

To implement a workaround we’ll need to change HTML a bit. We’ll switch `input` and `label` places. That way we can target the `label` element via the sibling selector (`+`).

**HTML**:

```html
<div class="field">
  <input class="input" type="email" id="email">
  <label class="label" for="email">E-mail:</label>
</div>
```

As for styling, we can set the visual order of `label` and `input` with `flex-direction: row-reverse` rule.

**CSS**:

```css
.field {
  display: flex;
  flex-direction: row-reverse;
  justify-content: flex-end; /* to pull content to the left */
}

.input:focus + .label {
  color: #5a6cce;
}
```

**Result**:

<style>
.field {display: flex;flex-direction: row-reverse;justify-content:flex-end;align-items:center}
.label {margin-right:5px}
.input {border:1px solid #777;border-radius:3px;padding:5px 9px}
.input:focus + .label{color:#5a6cce}
.input:focus {outline-color:#5a6cce}
</style>

<div class="field"><input class="input" type="email" id="email"><label class="label" for="email">E-mail:</label>
</div>

In case there are more than two elements in the container you can set the order property to each one to visually allocate them one after another. In this case, don’t forget to remove the `flex-direction: reverse` on the container element. 

```css
.label {
  order: 1;
}

.input {
  order: 2
}
```

The last tip, if you’re operating with inputs and `:focus` state, you can utilize the [`:focus-within`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-within) pseudo-class to select the desired element. In this case, you can leave the HTML as is:

```html
<div class="field">
  <label class="label" for="email">E-mail:</label>
  <input class="input" type="email" id="email">
</div>
```

**CSS**:

```css
.field:focus-within .label {
  color: #5a6cce;
}
```

However, if you’re going beyond just `:hover` and/or `:focus` states the `flex-direction` and `order` properties are your main way to go to select the previous sibling element.