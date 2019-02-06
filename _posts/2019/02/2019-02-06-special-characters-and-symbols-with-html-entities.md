---
layout: post
title: Special characters and symbols with HTML entities
description: Use icons, special characters and symbols without any library with HTML entities
tags: [html]
comments: true
---

HTML entities are a set of special encoded characters reserved for use in the HTML.

Entities can represent arrows, currency, letters, mathematical operators, numbers, punctuation, symbols, shapes and more. Some of the most familiar are a copyright character - &copy; or a heart symbol - &hearts;.

Entities are also useful when you need to insert a reserved character inside HTML tag like &lt; or &gt; signs.
These signs are used by HTML, but you can use `&lt;` or `&gt;` entities to display them.

Another useful enity is `&nbsp;` which is non breakable space. The name says it all. If you want to add several spaces to your HTML you'll need to use several `&nbsp;` entities, each one will represent one space. Otherwise if you enter multiple <kbd>space</kbd>s on a keyboard HTML will trim them to one sinle space.

Each entity starts with an ampersand `&` and ends with a semicolon `;`.
The middle part can be:

* entity name;
* decimal code;
* hexadecimal code.

## Examples

Below just a few examples of some of the entities.

| Character  | Entity name | Decimal code | Hexadecimal code |
| :--------: | :---------: | :-----------:| :--------------: |
| &copy;     | `&copy;`    | `&#169;`     | `&#x000A9;`      |
| &lt;       | `&lt;`      | `&#60;`      | `&#x0003C;`      |
| &gt;       | `&gt;`      | `&#60;`      | `&#x0003C;`      |
| &#33;      | `&excl;`    | `&#33;`      | `&#x00021;`      |
| &pound;    | `&pound;`   | `&#163;`     | `&#x000A3;`      |
| &euro;     | `&euro;`    | `&#8364;`    | `&#x020AC;`      |
| &#36;      | `&dollar;`  | `&#36;`      | `&#x00024;`      |
| &#8470;    | `&numero;`  | `&#8470;`    | `&#x02116;`      |


The best part about entities is that you might not need an icon library, complex CSS or SVG to display a special character or a symbol.

And since entities are strings, you can apply different implementations like HTML, CSS and JavaScript.

**You just add the necessary entity code to your HTML and that's it.**
**The example below uses entity name.**

HTML:
```html
<p>&copy; Copyright</p>
```
**Example with non breakable space**

HTML:
```html
<p>A&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Z</p>
```

**You can access the `data` attribute of an HTML tag containing the entity code in CSS.**
**The example below uses hexadecimal code.**

HTML:
```html
<p class="price" data-entity="&#x020AC;">19.95</p>
```
CSS:
```css
.price::before {
  content: attr(data-entity);
}
```

**Lastly, you can insert an entity code with JavaScript.**
**The example below uses decimal code.**

HTML:
```html
<p id="entity">Like</p>
```
JavaScript:
```javascript
const entity = document.getElementById('entity')
entity.innerHTML += '&#9829;'
```

The results will look like this:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html,result" data-user="nikitahl" data-slug-hash="rPYOZb" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="rPYOZb">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/rPYOZb/">
  rPYOZb</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Resources

There are hundreds of various entities available. The following links contains a vast list of entities with visual and encoded representations with a name/decimal/hexadecimal values.

[https://dev.w3.org/html5/html-author/charref](https://dev.w3.org/html5/html-author/charref){:target="blank"} - Official W3C entity reference
[https://www.toptal.com/designers/htmlarrows/symbols](https://www.toptal.com/designers/htmlarrows/symbols){:target="blank"} - Designers collection of entities with categories, search and view

---



