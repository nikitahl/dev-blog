---
layout: post
permalink: how-to-include-css-to-a-page
title: How to include CSS to a page (with Pros and Cons)
date: 2021-05-19T12:55:50.367Z
description: A complete guide on how to include a CSS to an HTML page with pros
  and cons of each approach.
tags:
  - html
  - css
---

When it comes to including CSS on a page, there are few ways to do that, each one with its own pros and cons.

3 ways to add CSS to a page:

1. [Include via external file (External CSS)](#external-file)
2. [Include via style tag on a page (Internal/Embedded CSS)](#the-style-tag-on-a-page)
3. [Include via inline styling (Inline CSS)](#inline-styling)

## External file

This is the most common way how CSS stylesheet gets added to an HTML document. A `link` tag has to be added to the `head` of the document with a `href` attribute containing the path to a CSS file.

```html
<link rel="stylesheet" href="path/to/style.css">
```

This way you don’t have any additional code inside your HTML document, which keeps it clean.

You can add as many external files as you need to the page.

**Pros**:

* All styles are stored in one separate file, thus easier to manage and maintain;
* Ability to include multiple different files if needed;
* The CSS file can be minified meaning decreased size in bytes.

**Cons**:

* Linking external files creates [render-blocking](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css) content which affects [page load speed](https://developer.chrome.com/docs/devtools/speed/get-started/);
* May contain styles that are not used on a particular page, thus loading unused code.

## The style tag on a page

As the name states, the CSS can be added to the page via the `style` tag. You have to specify the `style` tag with the appropriate CSS rules inside.

This approach is handy when you’re modifying parts of the page with JavaScript. You can select the `style` tag and update its value or [create a new element](/create-element-with-javascript) and add it to the page.

```html
<style>
  body {
    background-color: #efefef;
    color: #2e2e2e;
  }
</style>
```

This approach can be used to import and external stylesheet to a page. Inside the `style` tag you can use the `@import` rule to include an external CSS file.

```html
<style>
  @import url("path/to/style.css");
</style>
```

**Pros**:

* Useful for overriding default styling;
* Can be toggled on and off with JavaScript;
* Can be used to contain default minimum styling if the main stylesheet is being loaded asynchronously.

**Cons**:

* Not a very convenient way to apply styling for the whole page, especially if it’s large;
* Hard to manage and maintain.

## Inline styling

Lastly CSS can be added via the `style` attribute of the HTML element. This way CSS styles will be applied only to the element that has the `style` attribute.

```html
<p style="font-size: 17px; color: #787878;">A paragraph with text</p>
```

**Pros**:

* Useful for overriding default styling;
* Has a higher specificity than any CSS selector (but can also be a Con).

**Cons**:

* Not a very convenient way to apply styling for the whole page, especially if it’s large;
* Has a higher specificity than any CSS selector (but can also be a Pro);
* Hard to manage and maintain.

## Conclusion

As you can see the CSS can be included in various ways. But that doesn’t mean you should only use one approach. Instead many projects use all three as it gives more flexibility and control over the app.

However, keep in mind the CSS cascading and CSS selector specificity when working with all three approaches at once.