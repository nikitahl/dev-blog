---
layout: post
permalink: detect-mouse-right-click-with-javascript
title: Detect mouse right-click with JavaScript
date: 2021-06-30T14:22:18.160Z
description: There are simple ways to detect mouse right-click with JavaScript,
  to handle custom cases for your web app
tags:
  - js
---

JavaScript API allows developers to detect mouse right-click. It can be useful if you want to handle specific cases when a user clicks certain buttons on the mouse.

To start off, a typical computer mouse has 3 buttons:

1. **Primary** button (usually on the left, can be changed for left-handed users)
2. **Secondary** button (usually on the right, to invoke contextual menu);
3. **Scroll wheel** button (in the middle);

However, some have 5 buttons and more, like advanced or gaming mice. Additional buttons provide extra functionality, like **Back** and **Forward** in the browser.

You can detect which button has been clicked by checking the [`MouseEvent.button`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/button) property.

This property will be available on mouse clicking events like: `mousedown`, `mouseup`, `click`, `dblclick`, `contextmenu`.

```javascript
window.addEventListener('click', (event) => {
  console.log(event.button)
})
```

The `MouseEvent.button` is a read-only property that returns a number. Each number represents a button on the mouse:

* **0** - Main button
* **1** - Wheel button (middle button if present)
* **2** - Secondary button 
* **3** - Fourth button (Back button)
* **4** - Fifth button (Forward button)

**Browser support for the `MouseEvent.button` property**: <https://caniuse.com/mdn-api_mouseevent_button>

To specifically capture the mouse right-click, JavaScript has a special event for that - [`contextmenu`](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event).

Depending on the situation, instead of identifying which button has been clicked, you can specify the `contextmenu` event.

```javascript
window.addEventListener('contextmenu', (event) => {
  console.log(event.button)
})
```

This event still has the `button` property, with the number value of the, clicked button. But now for example, if you need to prevent further action, you can specify the `e.preventDefault()` without checking against a button property.

**Disable the right-click on a page**:

```javascript
window.addEventListener('contextmenu', (event) => {
  event.preventDefault()
})
```

**Browser support for the `contextmenu` event**: <https://caniuse.com/mdn-api_element_contextmenu_event>

## Conclusion

Use `MouseEvent.button` to detect which button has been clicked on a mouse. Useful if you need to intercept certain cases like Back and Forward actions in an iframe.
To react on mouse right-click specifically use a designated `contextmenu` event.