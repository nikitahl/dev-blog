---
layout: post
permalink: how-to-copy-css-from-website
title: How to copy CSS from a website (without any tools)
date: 2023-02-09T14:30:24.232Z
description: As a developer, you might need to copy certain CSS rules from a website. There are a number of ways to do this, depending on your needs.
tags: [css]
---

As a developer, you might need to copy certain CSS rules from a website. There are a number of ways to do this, depending on your needs. In this article, I'll show you how to copy CSS from a website using four different approaches without the need for any additional tools or extensions.

1. [Download the Whole Page](#download-the-whole-page)
2. [Right-Click Copy Styles](#right-click-copy-styles)
3. [Inspect styles and copy from DevTools](#inspect-styles-and-copy-from-devtools)
4. [Copy from the Source File](#copy-from-the-source-file)

## Download the Whole Page

You can obtain the entire CSS of a page by downloading it. To do this, right-click anywhere on the page and select **"Save as..."** or **"Save Page As..."**, depending on your browser.

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size: 13px;color: #666;font-style:italic;text-align:center}

.image-grid .figure-centered{margin:0 10px 10px;flex: 1 0 40%}
</style>

<div class="image-grid">
  <figure class="figure-centered">
    <img class="shadow" src="/images/dev-tools/page-css/chrome-save-page-as.webp" loading="lazy" alt="Save page as in Chrome">
    <figcaption>"Save page as" in Chrome</figcaption>
  </figure>
  <figure class="figure-centered">
    <img class="shadow" src="/images/dev-tools/page-css/firefox-save-page-as.webp" loading="lazy" alt="Save page as in Chrome">
    <figcaption>"Save page as" in Firefox</figcaption>
  </figure>
</div>

After you've saved the file, you'll find a folder with the same name which contains all the page assets (e.g., images, scripts, and styles) in your downloads folder.

<figure class="figure-centered">
  <img class="shadow" src="/images/dev-tools/page-css/downloaded-web-page.webp" loading="lazy" alt="Downloaded web page">
  <figcaption>Downloaded web page</figcaption>
</figure>

This approach is useful when you need to copy both the page's HTML structure and CSS styles and dissect it piece by piece. However, many sites now use CSS frameworks such as *TailwindCSS*, so you'll need to be familiar with the current framework to understand how it works.

## Right-Click Copy Styles

If you only need to copy the CSS styles of a specific element (e.g., a button or link), you can do so using a built-in feature in the DevTools.

<p class="note">💡 NOTE: This feature is only available in <a href="https://alvarotrigo.com/blog/best-chromium-browsers/" target="_blank" rel="noreferrer noopener">Chromium-based browsers</a>.</p>

To use this feature, open the DevTools, find the element you're interested in using the Element inspector, and right-click on it. In the dropdown menu, select **"Copy"** > **"Copy styles."** The CSS styles of the element will be copied to your clipboard, which you can then paste wherever you need them.

<figure class="figure-centered">
  <img class="shadow" src="/images/dev-tools/page-css/copy-element-styles.webp" loading="lazy" alt="Copy element styles via DevTools">
  <figcaption>Copy element styles via DevTools</figcaption>
</figure>

<p class="note">💡 NOTE: This approach won't copy the element state (e.g., <code>:hover</code>, <code>:focus</code>, etc.).</p>

## Inspect styles and copy from DevTools

You can also copy specific element styles directly from the Element inspector in the DevTools. To do this, open the DevTools, find the element you're interested in, and look under the **Styles** tab. You'll see all the CSS rules that are applied to that element.

You can select and copy CSS rules one by one or in bulk.

<figure class="figure-centered">
  <img class="shadow" src="/images/dev-tools/page-css/selected-css-properties.webp" loading="lazy" alt="Selected CSS properties">
  <figcaption>Selected CSS properties in element inspectors</figcaption>
</figure>

However, if the site uses a CSS framework like *TailwindCSS*, all the styles will be separated by selector, so if you want to copy multiple styles, you'll have to copy them along with all their selectors.

Firefox and Safari allow you to select and copy computed styles, which is handy for copying exact styles with readable values, especially if the page uses a lot of CSS variables. However, Chromium-based browsers don't allow the selection of all computed styles.

<div class="image-grid">
  <figure class="figure-centered" style="flex:1 0 47%">
    <img class="shadow" src="/images/dev-tools/page-css/selected-computed-css-properties-firefox.webp" loading="lazy" alt="Computed CSS property selection in Firefox">
    <figcaption>Computed CSS property selection in Firefox</figcaption>
  </figure>
  <figure class="figure-centered">
    <img class="shadow" src="/images/dev-tools/page-css/selected-computed-css-properties-safari.webp" loading="lazy" alt="Computed CSS property selection in Safari">
    <figcaption>Computed CSS property selection in Safari</figcaption>
  </figure>
</div>

## Copy from the Source File

Finally, you can find and copy styles from specific selectors within the source files of the page.

To do this, you can either open the **Sources** tab in the DevTools and search for CSS files, or you can find the element in the Element inspector and click on the source file name next to the CSS selector. This will open the specific CSS file at the location of the rules.

The cool part is that you can search for additional styles which may include states, media queries, animations and more.

<div class="image-grid">
  <figure class="figure-centered" style="flex:1 0 17.7%">
    <img class="shadow" src="/images/dev-tools/page-css/inspect-element-css-properties.webp" loading="lazy" alt="Inspect element CSS source files">
    <figcaption>Inspect element CSS source files</figcaption>
  </figure>
  <figure class="figure-centered">
    <img class="shadow" src="/images/dev-tools/page-css/page-css-source-file.webp" loading="lazy" alt="Sources tab for page CSS files">
    <figcaption>Sources tab for page CSS files</figcaption>
  </figure>
</div>

<p class="note">💡 NOTE: The file may be minified, so you'll need to click the <strong>Format</strong> button - <kbd>{&nbsp;}</kbd>, to make the code readable.</p>



