---
layout: post
permalink: listen-for-class-change-in-javascript
title: Listen for a class change in JavaScript
date: 2021-09-01T14:54:54.296Z
description: JavaScript possesses the ability to listen for a class change right
  out of the box. Without any additional libraries or hacky workarounds.
tags: [javascript]
---

JavaScript possesses the ability to listen for a class change right out of the box. Without any additional libraries or hacky workarounds. It can be done with the [`MutationObserver` interface](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver).

As a matter of fact, the `MutationObserver` allows listening to any change being made to the DOM tree, not only to the class name. `MutationObserver` is [supported in all major browsers](https://caniuse.com/mutationobserver).

For the sake of a demonstration let’s look at how it works with changing the class names.

Say we have a button:

```html
<button class="btn">Click me!</button>
```

And this button might have additional classes added to it like `btn--active`, `btn--disabled`, `btn--loading`, etc.

To listen to class change we need to instantiate the [`MutationObserver`](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver/MutationObserver) object, pass the callback function, and call the `observe()` method.

The `observe()` method accepts two arguments the target node and options object which should contain attributes property that is set to true.

```javascript
const btn = document.querySelector('.btn')
const options = {
  attributes: true
}

function callback(mutationList, observer) {
  mutationList.forEach(function(mutation) {
    if (mutation.type === 'attributes' && mutation.attributeName === 'class') {
      // handle class change
    }
  })
}

const observer = new MutationObserver(callback)
observer.observe(btn, options)
```

Now every time the class is changed on the button the callback function will run. From that point, you can handle the event as you need to.

Quite often the case of the class name change (or any other HTML attribute for that matter) could be outside the scope of your program (e.g. WordPress environment or 3rd party library). That’s where the `MutationObserver` comes into play and listens for such events.

<style>.video-container{position: relative;padding-top: 56.25%;margin: 0 0 30px;}.video{position: absolute;top: 0;left:0;width:100%;height: 100%;object-fit: cover;margin:0!important;}</style>

**Video of `MutationObserver` in action:**

<div class="video-container">
  <video class="video lozad" data-src="/videos/mutation-observer.mp4" controls />
</div>