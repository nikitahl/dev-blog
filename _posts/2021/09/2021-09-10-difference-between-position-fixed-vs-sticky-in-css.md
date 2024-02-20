---
layout: post
permalink: position-fixed-vs-sticky-css
title: Difference between position fixed vs sticky in CSS
date: 2021-09-10T08:30:20.439Z
description: The difference between position fixed vs sticky is that fixed
  always positions an element relative to the viewport, while sticky behaves
  like a regular element until it reaches the defined offset and then becomes
  fixed.
tags: [css]
---

It sometimes can be confusing to both beginners and even seasoned developers to understand the difference between position `fixed` vs `sticky`. Due to the fact that they behave similarly, yet each of those [properties](https://developer.mozilla.org/en-US/docs/Web/CSS/position#values) has its own purpose.

The difference between position `fixed` vs `sticky` is that `fixed` always positions an element relative to the viewport, while `sticky` behaves like a regular element until it reaches the defined offset and then becomes fixed.

<figure>
  <img class="shadow" src="/images/misc/fixed-vs-sticky.gif" alt="Fixed vs Sticky" loading="lazy">
  <figcaption>Fixed vs Sticky side by side</figcaption>
</figure>

## Position fixed

When the element position is set to `fixed` it is removed from the [normal document flow](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow), which means no space is created for this element. The element is then becomes positioned relative to the viewport.

Elements’ position is determined by the `top`, `right`, `bottom`, and `left` CSS properties. So if the values of `top`, `right`, `bottom`, and `left` properties become negative the element can actually go outside the boundaries of the viewport and become invisible.

```css
.fixed {
  position: fixed;
  top: 20px;
  left: 20px;
}
```

**NOTE: There could be cases when a fixed element can cover other elements on the page. So make sure to test your page well, especially on different viewports, as it may produce unwanted results.**

Use position `fixed` in case you always want to show the element. For example, it can be a site navbar or sidebar that is always visible.

## Position sticky

When the element position is set to `sticky` it remains in the normal document flow and is positioned relative to its closest ancestor element. But once the ancestor element is scrolled and reaches the offset defined for the `sticky` element it becomes fixed and stays that way until the ancestor is scrolled off the viewport.

```css
.fixed {
  position: sticky;
  top: 20px; /* the offset */
}
```

Use position `sticky` in case you want to show the element fixed to a certain position conditionally. An example could be a section in the sidebar with a call to action button.

### Issues with position sticky

Working with position sticky can sometimes be tricky, as it may not work for you as expected.

**NOTE: Certain conditions have to be met in order for the element to become sticky!**

When the element is not becoming sticky you need to check the following things:

1. Check [browser support](#browser-support)
2. Is offset specified (CSS `top` property)
3. Is there an `overflow` property set for the parent element
4. Is there a `height` property set for the parent element
5. Is a parent element is set to `display: flex`

Make sure to check Daniyal Hamid's article on [How to Fix Issues With CSS Position Sticky Not Working](https://www.designcise.com/web/tutorial/how-to-fix-issues-with-css-position-sticky-not-working#checking-if-an-ancestor-element-has-overflow-property-set) for a more thorough explanation.

## Browser support

Position `fixed` is [supported by all browsers](https://caniuse.com/css-fixed).

Position `sticky` is [supported by all modern browsers](https://caniuse.com/css-sticky).

## Position fixed vs sticky Demo

<p class="codepen" data-height="450" data-default-tab="result" data-slug-hash="rNwyPrN" data-user="tippingpointdev" style="height: 450px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
<span>See the Pen <a href="https://codepen.io/tippingpointdev/pen/rNwyPrN">
</a> by Tippingpoint Dev (<a href="https://codepen.io/tippingpointdev">@tippingpointdev</a>) on <a href="https://codepen.io">CodePen</a>.</span>
</p>
