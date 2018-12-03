---
layout: post
title: How to insert an element after an element with JavaScript
description: Simple native crossbrowser safe method to insert an element after an element with JavaScript
tags: [javascript]
comments: true
---

There is a simple and crossbrowser safe way to insert an element after another element with native Javascript.

There are actually a couple of ways you can acheive this.

1. [`insertAdjacentElement()`](#insertadjacentelement)
2. [`insertAdjacentHTML()`](#insertadjacenthtml)

## insertAdjacentElement()

> The insertAdjacentElement() method inserts a given element node at a given position relative to the element it is invoked upon.
>
> &mdash;<cite>MDN</cite>

**Example:**	

HTML
```html
<div>
  <h1 id="title">Hello World</h1>
  <p>This is it.</p>
</div>
```

JavaScript
```javascript
const title = document.getElementById('title')
const subTitle = document.createElement('p')
subTitle.innerText = 'How are you doing?'
title.insertAdjacentElement('afterend', subTitle)
```

**Result:**

HTML
```html
<div>
  <h1 id="title">Hello World</h1>
  <p>How are you doing?</p>
  <p>This is it.</p>
</div>
```

This method takes two arguments:
* **position**

	The position relative to the target element (in the example `title` variable). This is a *string* type argument and can take several values:

	* `'beforebegin'`: before the target element itself.
	* `'afterbegin'`: just inside the target element, before its first child.
	* `'beforeend'`: just inside the target element, after its last child.
	* `'afterend'`: after the target element itself.


* **element**

	The element to be inserted (in the example `subTitle` variable). 

So, in fact, you can insert an element at any position you want for a given target.

The best part is that this **method is supported by all browsers**, even Internet Explorer! Check out the full documentation on [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement){:target="blank"}.

[Browser support](https://caniuse.com/#search=insertAdjacentElement()){:target="blank"} for `insertAdjacentElement()`.

## insertAdjacentHTML()
Another way to insert element after another element is to use `insertAdjacentHTML()` method.
It does initially the same as `insertAdjacentElement()`, but instead of element it inserts a parsed HTML at a given position.

> The insertAdjacentHTML() method parses the specified text as HTML or XML and inserts the resulting nodes into the DOM tree at a specified position.
>
> &mdash;<cite>MDN</cite>

**Example:**	

HTML
```html
<div>
  <h1 id="title">Hello World</h1>
  <p>This is it.</p>
</div>
```

JavaScript
```javascript
const title = document.getElementById('title')
const subTitle = '<p>How are you doing?</p>'
title.insertAdjacentHTML('afterend', subTitle)
```

**Result:**

HTML
```html
<div>
  <h1 id="title">Hello World</h1>
  <p>How are you doing?</p>
  <p>This is it.</p>
</div>
```

As you can see `insertAdjacentHTML()` method also takes two arguments:
* **position**

	The position relative to the target element (in the example `title` variable). This is a *string* type argument and can take several values:

	* `'beforebegin'`: before the target element itself.
	* `'afterbegin'`: just inside the target element, before its first child.
	* `'beforeend'`: just inside the target element, after its last child.
	* `'afterend'`: after the target element itself.

* **text**
	The string to be parsed as HTML or XML (in the example `subTitle` variable).

Full documentation on [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML){:target="blank"}. And just like with the previous method it is supported by all browsers.

[Browser support](https://caniuse.com/#search=insertAdjacentHTML()){:target="blank"} for `insertAdjacentHTML()`.

---

