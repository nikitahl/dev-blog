---
layout: post
permalink: link-underline-with-css
title: Styling link underline with CSS 101
date: 2022-12-23T11:32:24.232Z
description: There are different ways how to add an underline to a link in CSS, in this guide I'll highlight all the ways you can achieve that
tags: [css]
---

Default HTML links have a distinct style that lets the user know it’s clickable text. Usually, links have a blue color and an underline, upon hover a pointer cursor is shown.

However, other elements besides text can be a link (image, button, etc). But in this guide, I’ll cover approaches to custom-style text links to show an underline. There are three ways to do so, by using:

- [Text decoration](#text-decoration)
- [Border](#border)
- [Box shadow](#box-shadow)

## Text decoration
The first and most obvious way is to use the `text-decoration` property to give your links a distinct style. The [`text-decoration`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration){:target="blank"} property is a shorthand that *“sets the appearance of decorative lines on text"*.

This property will set `text-decoration-line`, `text-decoration-color`, `text-decoration-style`. However, it can take from one to three parameters.

```css
a {
  text-decoration: underline;
}
```

You can add more unique styles by throwing in the color and style properties:

```
a {
  text-decoration: underline dotted #da28e0;
}
```
**Result:**

<a href="#" style="text-decoration: underline dotted #da28e0">Click here</a>

Available underline styles are:

- solid;
- double;
- dotted;
- dashed;
- wavy.

To specify the space between the underline and text use the [`text-underline-offset`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-underline-offset){:target="blank"} property.

```css
a {
  text-underline-offset: 5px;
}
```
**Result:**
<a href="#" style="text-underline-offset: 5px;">Click here</a>

The `text-decoration` also allows you to set the width/thickness of the underline via the [`text-decoration-thickness`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration-thickness){:target="blank"}

```css
a {
  text-decoration-line: underline;
  text-decoration-thickness: 5px;
}
```
**Result:**
<a href="#" style="text-decoration-line: underline;text-decoration-thickness: 5px;">Click here</a>

Finally, the `text-decoration` property can be animated. For example, you can hide an underline on hover with a transition.

 ```css
a {
    text-decoration: underline solid currentColor;
    transition: text-decoration-color .2s ease-in-out;
}

a:hover {
  text-decoration-color: transparent;
}
```
<style>
  .underline-hover {transition: text-decoration-color .2s ease-in-out;}
  .entry .underline-hover:hover {text-decoration-color: transparent;}
</style>
**Result:**
<a class="underline-hover" href="#">Click here</a>

## Border
You can also use the `border-bottom` property to make the link’s underline style even fancier. But you have to set the `text-decoration` to `none`, to avoid duplicate underline.

```css
a {
  text-decoration: none;
  border-bottom: 1px dashed #da28e0;
}
```
**Result:**
<a href="#" style="text-decoration: none;border-bottom: 1px dashed #da28e0;">Click here</a>

Same as with the `text-decoration` you can control the underline's width, color, and styles that are specific only to the border property like:

- dotted;
- dashed;
- solid;
- double;
- groove;
- ridge;
- inset;
- outset.

To control the space between the text and the underline you can add a `padding` property.

```css
a {
  text-decoration: none;
  border-bottom: 1px dashed #da28e0;
  padding-bottom: 5px; 
}
```

**Result:**
<a href="#" style="text-decoration: none;border-bottom: 1px dashed #da28e0;padding-bottom: 5px;">Click here</a>

To make your underlines unique and fancy, you can apply gradient colors. The [border can have gradient](/gradient-border-css) colors, to set it you can use the `border-image` property.

```css
a {
  text-decoration: none;
  border-bottom: 3px solid;
  border-image: linear-gradient(45deg, purple, orange) 1;
}
```
**Result:**
<a href="#" style="text-decoration: none;border-bottom: 3px solid;border-image: linear-gradient(45deg, purple, orange) 1;">Click here</a>

## Box shadow

The last one is the `box-shadow` property. Same as the border it will allow you to control the width of the underline and space between the text as well. The `text-decoration` has to be set to `none`.

```css
a {
  text-decoration: none;
  box-shadow: 0 2px #da28e0;
  padding-bottom: 3px;
}
```
**Result:**
<a href="#" style="text-decoration: none;box-shadow: 0 2px #da28e0;padding-bottom: 3px;">Click here</a>

Along with other properties like blur and spread which can create some funky glowing effects.

```css
a {
  text-decoration: none;
  box-shadow: 0 5px 4px -3px #047cea;
}
```
**Result:**
<a href="#" style="text-decoration: none;box-shadow: 0 5px 4px -3px #047cea">Click here</a>
## Remove the underline

To remove the underline from a link you’ll need to set the corresponding CSS property to `none`. In some cases, you’ll need to unset all the above rules to `none`.

This is especially true for 3rd party environments like WordPress, as themes and plugins developers may use one of the above approaches. So to make sure you’ve removed the underline for good you can set all three rules to `none`:

```css
a {
  text-decoration: none;
  border: none;
  box-shadow: none;
}
```

## Conclusion

To conclude, if you want something more than a default underline styling use `border` or `box-shadow` properties. These properties also allow using transitions on them so you can get creative with hover effects. 😉

I've put together a collection of possible link underline styles on CodePen, check 'em out.

<p class="codepen" data-height="390" data-default-tab="result" data-slug-hash="jvaPrp" data-user="nikitahl" style="height: 390px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/jvaPrp">
  Link hover effect collection</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
