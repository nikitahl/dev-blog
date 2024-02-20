---
layout: post
permalink: copy-paste-to-clipboard
title: Exploring Subtle intricacies in Implementing Cut, Copy, and Paste to Clipboard using JavaScript
date: 2023-11-10T11:01:02.112Z
description: Dealing with clipboard operations in JavaScript can present certain challenges. In this guide, I'll clarify the process and walk you through the fundamental clipboard tasks and addressing related nuances.
tags: [javascript]
---

Dealing with clipboard operations in JavaScript can present certain challenges. In this guide, I'll clarify the process and walk you through the fundamental clipboard tasks and addressing related nuances.

**Contents:**

1. [How users can copy content to clipboard](#how-users-can-copy-content-to-clipboard)
2. [Native clipboard](#native-clipboard)
3. [Clipboard API in JavaScript](#clipboard-api-in-javascript)
4. [Security concerns](#security-concerns)
5. [Handling events](#handling-events-copy-and-paste)
6. [Conclusions](#conclusions)

## How users can copy content to clipboard

Before we get into details, it's important to understand that there are a couple of ways how users can perform clipboard commands, which can affect the work with the clipboard.

1. **Natively via keyboard/mouse.**
2. **By clicking on a designated "Copy" button.**

### 1. Natively via keyboard/mouse

To perform cut, copy, and paste operations, users have two native options at their disposal:

**Using Keyboard Shortcuts:**

- Cut: Press <kbd>Cmd</kbd> + <kbd>X</kbd> on a Mac or <kbd>Ctrl</kbd> + <kbd>X</kbd> on Windows.
- Copy: Press <kbd>Cmd</kbd> + <kbd>C</kbd> on a Mac or <kbd>Ctrl</kbd> + <kbd>C</kbd> on Windows.
- Paste: Press <kbd>Cmd</kbd> + <kbd>V</kbd> on a Mac or <kbd>Ctrl</kbd> + <kbd>V</kbd> on Windows.

**Mouse and HUD (if available):**

Alternatively, users can right-click with the mouse to access the context menu, offering the cut, copy, and paste options. If available, the Edit menu in the HUD (Head-Up Display) can also be utilized to perform these actions.

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 30px;flex:1 0 47%}
.vertical{width:60%}
</style>
<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/safari-context-menu.webp" alt="Safari context menu with cut, copy and paste">
    <figcaption>Safari context menu on right click</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/safari-hud-edit-menu.webp" alt="Safari HUD Edit menu dropdown with cut, copy and paste">
    <figcaption>Safari HUD Edit menu dropdown</figcaption>
  </figure>
</div>

<p class="note">💡 NOTE: By using native options the content get copied/pasted to the <a href="#native-clipboard">native clipboard</a> of the operating system.</p>

### 2. By clicking on a designated "Copy" button

Besides the native options users can click custom buttons on the webpage to copy/paste the content.

In this case, the contents get copied/pasted to the JavaScript's [Clipboard API](#clipboard-api-in-javascript).

<figure>
  <img class="shadow" loading="lazy" src="/images/misc/github-copy-button.webp" alt="GitHub's custom 'Copy' button">
  <figcaption>GitHub's custom "Copy" button</figcaption>
</figure>

## Native clipboard

When users choose to copy content using native methods like keyboard shortcuts, they interact with the clipboard provided by the operating system itself.

This native clipboard acts as a temporary storage location for the copied content and is designed to seamlessly work with the operating system's environment.

However, it's essential to understand that while the native clipboard is an integral part of the operating system, the web browser also introduces its own clipboard functionality.

When users copy content within a browser, it's placed in the browser's clipboard, enabling users to paste that content within the browser's web pages and applications.

But one important thing to remember is that browsers maintain separate clipboard buffers for native clipboard operations and JavaScript-accessible clipboard operations. This separation is intentional and helps maintain security and user privacy.

<p class="note">💡 NOTE: Native clipboard integration is typically handled by the operating system, and developers don't have direct control over it.</p>


## Clipboard API in JavaScript

On the other hand, you can access the browser clipboard through JavaScript using the [Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API){:target="_blank"} to allow users to copy/paste content using custom UI elements e.g. buttons.

To access clipboard data you can use the [`navigator.clipboard`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/clipboard){:target="_blank"} property which returns the Clipboard object.

To read the clipboard data you can use the `readText` method, e.g. you want to trigger a *custom paste* command.

```javascript
// Check if the Clipboard API is available
if (navigator.clipboard) {
  navigator.clipboard.readText().then((clipboardText) => {
    console.log('Clipboard content:', clipboardText)
  }).catch((error) => {
    console.error('Error reading clipboard:', error)
  })
} else {
  // Provide a fallback if Clipboard API not available, 
  console.error('Clipboard API not supported in this browser.')
}
```

To write the data to a clipboard you can use the `writeText` method, e.g. you want to trigger *custom copy*.

```javascript
if (navigator.clipboard) {
  navigator.clipboard.writeText(text);
}
```

**Clipboard API browser support:**
<p class="ciu_embed" data-feature="mdn-api__Clipboard" data-periods="future_1,current,past_2" data-accessible-colours="false">
Data on support for the mdn-api__Clipboard feature across the major browsers
</p>

<p class="note">💡 NOTE: For older browsers, you can use the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand" target="_blank"><code>Document.execCommand()</code></a> method to perform copy and paste actions.</p>


## Security concerns

When working with clipboard data, there can be many cases of how and where the user has copied or cut content.

You may also notice that you're not able to copy and paste content from one site to another when working with Clipboard API.

Access to the Clipboard API is generally subject to user consent. Browsers often [prompt users to grant permission](https://w3c.github.io/clipboard-apis/#privacy-events){:target="_blank"} before a web application can access the clipboard.

<figure>
  <img class="shadow" loading="lazy" src="/images/misc/browser-clipboard-permission-prompt.webp" alt="Browser's clipboard permission prompt">
  <figcaption>Browser asking for a permission to access clipboard</figcaption>
</figure>

You can check permission by using the [`query`](https://developer.mozilla.org/en-US/docs/Web/API/Permissions/query){:target="_blank"} method from the [Permissions API](https://developer.mozilla.org/en-US/docs/Web/API/Permissions_API){:target="_blank"}.

```javascript
navigator.permissions.query({name: 'clipboard-read'}).then((permission) => {
    if (permission.state === 'granted') {
      navigator.clipboard.readText().then((clipboardText) => {
        console.log('Clipboard content:', clipboardText)
      });
    } else {
      console.error('Error permission not granted:', permission.state)
    }
  }).catch((error) => {
    console.error('Error permission denied:', error)
  });
```

The restriction on Clipboard API for cross-origin operations is primarily a [security measure](https://www.codecademy.com/learn/becj-22-web-security-fundamentals/modules/wdcp-22-web-security-ab022919-3153-4aa9-aee4-e7b0e108e1d7/cheatsheet){:target="_blank"} implemented by web browsers.

One of the reasons is that clipboard data can contain sensitive information, such as login credentials, personal details, or proprietary content.

Allowing cross-origin access to the clipboard could enable malicious websites to read sensitive data copied by users from other sites, compromising user privacy.

So you have to keep that in mind when implementing copy and paste functionality for your project.

## Handling events (copy and paste)

However, you can still allow users to copy content using a custom button click and they can paste via native commands.

As shown [above](#clipboard-api-in-javascript), the custom `copy` is available using the `navigator.clipboard` property. You can access it for example on a button click. Alternatively, you can "hook" into the native `copy` event and modify the clipboard content.

```javascript
document.body.addEventListener('copy', (event) => {
  const selection = document.getSelection()
  event.clipboardData.setData('text/plain', selection.toString().toUpperCase())
  event.preventDefault()
})
```

When you use <kbd>cmd</kbd> + <kbd>v</kbd> to paste content, the browser checks its native clipboard buffer for the copied content. The content copied using <kbd>cmd</kbd> + <kbd>c</kbd> is still available for pasting, and this operation is not affected by JavaScript code interacting with the Clipboard API.

And you can intercept the clipboard content during the [`paste` event](https://developer.mozilla.org/en-US/docs/Web/API/Element/paste_event){:target="_blank"} to modify it.

```javascript
document.body.addEventListener('paste', (event) => {
  console.log('Clipboard content: ', event.clipboardData.getData('text/plain'))
})
```

That way you can kind of work around the cross-origin restriction. This means you can allow for a custom `copy` event on one domain, and then paste it natively on another.

<p class="note">💡 NOTE: You cannot trigger the <code>paste</code> event, due to security reasons explained <a href="#security-concerns">above</a>, unless the user has configured it to do so.</p>

## Conclusion

When you use `navigator.clipboard`, you're using a high-level interface that handles the differences between native clipboard functionality and the Clipboard API.

You don't need to worry about whether you're on a Windows or macOS system, what keyboard shortcuts to use, or the specific data formats supported. The browser abstracts these details and provides a common interface, making it easier for you to work with clipboard data in a cross-browser and user-friendly manner.

In summary, `navigator.clipboard` abstracts the differences between the native clipboard mechanisms of different operating systems and the Clipboard API, allowing developers to work with clipboard data in a consistent and browser-agnostic way.
