---
layout: post
permalink: responsive-table-with-css
title: Make a good looking responsive table with pure CSS
description: A table is a nice way to display large and complex data in a structured way. But often tables on websites are large and don't look good on smaller screens (mobile, tablet).
tags: [css]
---

A table is a nice way to display large and complex data in a structured way. But often tables on websites are large and don't look good on smaller screens (mobile, tablet).

Luckily there are a few ways how you can improve your table's appearance and make them responsive with just CSS code.

**Table of contents:**
1. [Text wrap](#text-wrap)
2. [Horizontal scroll](#horizontal-scroll)
3. [Responsive table without scrollbar](#responsive-table-without-scrollbar)
4. [Tips to make tables look better on mobile devices](#tips-to-make-tables-look-better-on-mobile-devices)
5. [Demo](#demo)

## Text wrap

The easiest way to make a table responsive and fit it into a mobile screen is to make [text wrap](/pure-css-truncate-text) to the next line.

That way longer words won't stick out of the viewport on smaller devices.

It works best if you have a relatively small table with minimum content in it. All you need is to add a `word-break` property to your table:

```css
table {
  word-break: break-all;
}
```

See a [demo](#demo).

## Horizontal scroll

The next approach is to make your table scroll horizontally. It is especially useful if you have a table with many columns.

You'll need to wrap your table in a container and set its `overflow` property to `auto`. This will give container a scroll if its contents won't fit inside.

```html
<div class="scroll-container">
  <table>
  </table>
</div>
```

```css
.scroll-container {
  overflow: auto;
}
```

Of course it depends on the structure of your table. But for the sake of example you can make the first column sticky, and let the rest of the columns scroll horizontally.

```css
.scroll td:first-of-type {
  position: sticky;
  left: 0;
  border-left: none;
  background: #f4f4f4;
  color: #212121;
  font-weight: bold;
}
```

See a [demo](#demo).

## Responsive table without scrollbar

Finally, you can make a fully responsive table that will adjust its layout depending on the viewport and will look appealing on mobile devices.

You'll need to specify a head for each column with a title. And for each cell, set a `data-label` attribute that corresponding to the column title.

```html
<table class="responsive">
  <thead>
    <tr>
      <td>Rank</td>
      <td>Title</td>
      <td>Genre</td>
      <td>Year</td>
      <td>Director</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-label="Rank">1.</td>
      <td data-label="Title">The Shawshank Redemption</td>
      <td data-label="Genre">Drama</td>
      <td data-label="Year">1994</td>
      <td data-label="Director">Frank Darabont</td>
    </tr>
    <tr>
      <td data-label="Rank">2.</td>
      <td data-label="Title">The Godfather</td>
      <td data-label="Genre">Crime, Drama</td>
      <td data-label="Year">1972</td>
      <td data-label="Director">Francis Ford Coppola</td>
    </tr>
    <!-- and so on for each row of the column -->
  </tbody>
</table>
```

For the given breakpoint you'll need to hide the `thead` tag with column titles. Slightly separate table rows from each other with a margin. And to show a label of the cell we'll use a `::before` pseudo-element that takes its `content` value from a `data-label` attribute.

```css
@media screen and (max-width: 600px) {  
  .responsive thead {
    visibility: hidden;
    height: 0;
    position: absolute;
  }
  
  .responsive tr {
    display: block;
    margin-bottom: .625em;
  }
  
  .responsive td {
    border: 1px solid;
    border-bottom: none;
    display: block;
    font-size: .8em;
    text-align: right;
  }
  
  .responsive td::before {
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
  }
  
  .responsive td:last-child {
    border-bottom: 1px solid;
  }
}
```

See a [demo](#demo).

## Tips to make tables look better on mobile devices

Creating responsive tables that looks good both on desktop and mobile devices can be tricky.

There's an in depth article by UXmatters on [mobile tables](https://www.uxmatters.com/mt/archives/2020/07/designing-mobile-tables.php){:target="blank"}. It covers in fine details the ways and guidelines on how to design appealing and good looking tables.

To give you a general understanding of the topic here are just some of the tips by UXmatters on how to design responsive tables.

- Showing Only What Users Really Need
- Leave Out Useless Data
- Abbreviate and Add Icons
- Eliminate Repetition
- Emphasize the Important
- Stack and Wrap Columns

## Demo

You can check final result for all of these approaches via CodePen:

<p class="codepen" data-height="500" data-default-tab="html,result" data-slug-hash="LYdQBZo" data-user="nikitahl" style="height: 500px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/LYdQBZo">
  Untitled</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
