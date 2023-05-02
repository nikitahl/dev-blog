---
layout: post
permalink: custom-mouse-cursor
title: Custom mouse cursor with CSS
date: 2023-04-17T20:09:12.133Z
description: In case you didn't know you can create a totally custom mouse cursor for your web page using only CSS.
tags: [css]
---

In case you didn't know you can create a totally custom mouse cursor for your web page using only CSS.

To set a mouse cursor styles in CSS you need to use the `cursor` rule and a value to show the appropriate cursor.

For example, if a user has to wait for some action to complete you can use the `progress` cursor. Or if you want to prevent the user from interacting with an element you can indicate that it is disabled with `not-allowed`.

```css
.loading {
  cursor: progress;
}

.disabled {
  cursor: not-allowed;
}
```

**Result:**
<style>.entry button{padding: 6px 20px}</style>

<button style="cursor: progress;">Loading</button>

<button style="cursor: not-allowed;">Disabled</button>

There are over [30 different values](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor#values){:target="_blank"}(keywords) that can be assigned to the `cursor` rule. Each one of them corresponds to a specific action or state, to help the user understand the behavior.

Although the values of these cursors are the same, they may look different based on the operating system you're using (Windows, MAC, Linux).

However, you can set a completely custom cursor appearance that will look exactly the same despite the operating system.

This is quite useful if you're building a game or a super custom website, and want to make it look special.

Custom cursors are essentially image files. And to set a custom mouse cursor you'll need to specify the file url and the fallback keyword.

```css
.custom {
  cursor: url("mouse-pointer.png"), auto;
}
```

**Result:**

<button style="cursor: url('/images/misc/mouse-pointer.png'), auto;">Custom cursor</button>

You are allowed to use several [image formats](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor#supported_image_file_formats){:target="_blank"} including PNG and SVG. Desktop browsers also support the `.cur` file format.
