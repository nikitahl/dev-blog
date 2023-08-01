---
layout: post
permalink: get-gutenberg-block-data-javascript
title: How to get Gutenberg blocks data in WordPress with JavaScript
date: 2023-08-01T13:50:02.112Z
description: In this article I'm going to explain how to get Gutenberg blocks data in WordPress with JavaScript.
tags: [javascript, wordpress]
---

In this article I'm going to explain how to get Gutenberg blocks data in WordPress with JavaScript.

To get the Gutenberg blocks data you can use one of a few approaches, depending on your needs.

1. [Get all registered blocks](#get-all-registered-blocks)
2. [Get blocks added to the post](#get-blocks-added-to-the-post)

## Get all registered blocks

One way is to use the Blocks package. A WordPress is using multiple [JavaScript packages](https://developer.wordpress.org/block-editor/reference-guides/packages/){:target="_blank"} in order to handle specific functionality.

 The [Block package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-blocks/){:target="_blank"} which contains methods to manage Gutenberg blocks is available under the `wp.blocks` global object.

```javascript
window.wp.blocks
```
**Result:**

<figure>
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-blocks-module-object.webp" alt="WordPress Blocks module object">
  <figcaption>WordPress Blocks module object</figcaption>
</figure>

To get the data of all of the available Gutenberg blocks you'll have to use the [`getBlockTypes()`](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-blocks/#getblocktypes){:target="_blank"} method. It returns the array of objects, and it is available in the global scope inside the Gutenberg editor.

```javascript
window.wp.blocks.getBlockTypes()
```
**Result:**

<figure>
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-get-block-types-object.webp" alt="Blocks module getBlockTypes() method">
  <figcaption>Blocks module's getBlockTypes() method</figcaption>
</figure>

<p class="note">💡 NOTE: While the Blocks module is available as a global property inside the Gutenberg editor, you can install it independently via <code>npm</code> for your project.</p>

## Get blocks added to the post

You can also get the data of the blocks that are added to the post. For this appoach we'll be using the [Data module](https://developer.wordpress.org/block-editor/reference-guides/data/){:target="_blank"}, which is available in the [Data package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-data/){:target="_blank"}.

The Data module is used to manage the state of the Gutenberg editor and it is available via global `wp.data` property.

```javascript
window.wp.data
```
**Result:**

<figure>
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-data-module-object.webp" alt="WordPress Data module object">
  <figcaption>WordPress Data module object</figcaption>
</figure>

The way to get the added elements data is to use the [`select`](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-data/#select) method of the Data module with a [`core/block-editor` namespace](https://developer.wordpress.org/block-editor/reference-guides/data/data-core-block-editor/){:target="_blank"} as the argument.

This will return the object of the store's selectors.

```javascript
window.wp.data.select('core/block-editor')
```

**Result:**

<figure>
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-core-editor-blocks-object.webp" alt="WordPress core/block-editor object">
  <figcaption>WordPress core/block-editor object</figcaption>
</figure>

Finally you can use the desired method to get the data, in our case the [`getBlocks()`](https://developer.wordpress.org/block-editor/reference-guides/data/data-core-block-editor/#getblocks){:target="_blank"} method.

```javascript
window.wp.data.select('core/block-editor').getBlocks()
```

**Result:**

<figure>
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-get-blocks-object.webp" alt="WordPress getBlocks() object">
  <figcaption>WordPress getBlocks() object</figcaption>
</figure>

<p class="note">💡 NOTE: If you don't have any elements added to the post, the <code>getBlocks()</code> method will return an empty array.</p>
