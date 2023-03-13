---
layout: post
permalink: increase-selector-specificity
title: How to increase selector specificity
date: 2023-03-13T19:50:14.133Z
description: Sometimes you need to override existing styles but you can't change HTML. There are a few ways how you can increase selector specificity by only modyfying CSS.
tags: [css]
---

Sometimes you need to override existing styles but you can't change HTML. There are a few ways how you can increase selector specificity by only modifying CSS.

This is especially true when working in an environment such as WordPress, where different themes and plugins produce CSS code, which you need to override.

1. [Make use of cascading](#1-make-use-of-cascading)
2. [Use selector with more weight](#2-use-selector-with-more-weight)
3. [Use compound selector](#3-use-compound-selector)
4. [Use duplicating selectors](#4-use-duplicating-selectors)
5. [Use attribute selector](#5-use-attribute-selector)
6. [Use pseudo-classes](#6-use-pseudo-classes)
7. [Use !important as the last resort](#7-use-important-as-the-last-resort)

## 1. Make use of cascading

You don't always have to create a stronger selector in CSS. You can use [cascading](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade){:target="_blank"} to override the existing styles.

To do this, simply create a new selector that has the same level of specificity as the existing one and place it after the existing selector.

```css
.main-heading {
  font-size: 32px;
}

.main-heading {
  font-size: 42px;
}
```

## 2. Use selector with more weight

If possible use a [descendant combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_combinator){:target="_blank"} selector with more weight to increase specificity and override existing selector.

For the type selector add class selector, for class selector add the id selector.

```css
p {
  font-size: 16px;
}

.container p {
  font-size: 18px;
}
```

```css
.paragraph {
  font-size: 16px;
}

#page .paragraph {
  font-size: 18px;
}
```

## 3. Use compound selector

Combine a type selector with a class selector to create a [compound selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors#compound_selector){:target="_blank"}.

```css
h1 {
  font-size: 32px;
}

h1.heading {
  font-size: 42px;
}
```

It works well with a descendant combinator.

```css
.container h1 {
  font-size: 32px;
}

.container h1.heading {
  font-size: 42px;
}
```

## 4. Use duplicating selectors

Another way to utilize a single class or id selector for increasing specificity is to duplicate it.

```css
.heading {
  font-size: 32px;
}

.heading.heading {
  font-size: 42px;
}
```

```css
#heading {
  font-size: 32px;
}

#heading#heading {
  font-size: 42px;
}
```

## 5. Use attribute selector

[Attribute selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors){:target="_blank"} have the same weight as class selectors. To use the attribute selector, specify the attribute name inside square brackets e.g. `[title]` or `[href]`.

It works great if you don't have any class selectors.

```css
a {
  font-size: 16px;
}

a[href] {
  font-size: 18px;
}
```
Or if you have a class on the element.
```css
.container {
  width: 600px;
}

.container[class] {
  width: 700px;
}
```

## 6. Use pseudo-classes

Just like the attribute selector, the [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes){:target="_blank"} has the same weight as the class selector.

They come in handy when you need to increase specificity conditionally. Some of the selectors are `:is`, `:has`, `:not` and `:where`.

In the following example the `:has` selector will select only those `h1` tags which have `a` tags inside them.

```css
h1 {
  color: black;
}

h1:has(a) {
  color: blue;
}
```
 
## 7. Use !important as the last resort

Finally if none of the above solves your issue, you can always use `!important`. Although using `!important` is [frowned upon](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#the_!important_exception){:target="_blank"}, sometimes it's the only way.

If you decide to go with `!important` make sure to leave a comment in the code explaining why you decided to add it.

<p class="note">💡 NOTE: To calculate CSS selector specificity I recommend <a href="https://specificity.keegan.st/" target="_blank">Specificity Calculator</a> tool.</p>