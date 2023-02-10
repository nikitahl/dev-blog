---
layout: post
title: 5 reasons of why Semantic HTML is important
description: A short list of reasons of why it is important to write Semantic HTML as a web developer
updated: 2023-02-10T09:45:10.124Z
tags: [html, seo]
comments: true
---

I’ll go through a list of 5 reasons of why semantic HTML is important and why web developers should pay more attention to it.

1. [Understandable code](#1-understandable-code)
2. [Screen readers](#2-screen-readers)
3. [Search engines (SEO)](#3-search-engines-seo)
4. [Usability (UX)](#4-usability-ux)
5. [Default styling](#5-default-styling)


What does MDN say about Semantic HTML:
> In programming, Semantics refers to the meaning of a piece of code — for example ... "what purpose or role does that HTML element have" (rather than "what does it look like?".)

So the number one reason is:

## 1. Understandable code

By giving a meaning to your HTML code, you make it more understandable, for yourself and other developers. From a human perspective semantic code is more readable, understandable and easier to maintain. Imagine looking at the code like this:

```html
<div id=”brown-fox”>
  <div>A story of quick brown fox</div>
  <div>The quick brown fox jumps over the lazy dog.</div>
  <div>Fox properties:</div>
  <div>- quick</div>
  <div>- brown</div>
  <div>- jumpy</div>
<div>
```

The same structure but with meaningful tags:
```html
<section id=”brown-fox”>
  <h2>A story of quick brown fox</h2>
  <p>The quick brown fox jumps over the lazy dog.</p>
  <h3>Fox properties:</h3>
  <ul>
    <li>quick</li>
    <li>brown</li>
    <li>jumpy</li>
  </ul>
<section>
```
You can immediately spot the difference. Straight off the bat, you can tell what each line of the code represents and what is its meaning.

## 2. Screen readers
Not only humans (programmers) have the need to understand the meaning of the page structure, so do the machines, one of them are screen readers.

<blockquote>
  A screen reader is a form of assistive technology which is essential to people who are blind, as well as useful to people who are visually impaired, illiterate, or have a learning disability.	<br />
	&mdash;<cite><a href="https://en.wikipedia.org/wiki/Screen_reader" target="_blank" rel="noreferrer noopener">Wikipedia</a></cite>
</blockquote>

A screen reader analyzes the contents of the web page and outputs the results via speech. This means whatever a screen reader sees, it will read.

So it’s quite important to structurize your web page with a meaning. However modern screen readers are quite *“smart”* and handle web pages very well.

Both MAC and Windows have built in screen readers. For MAC it is [VoiceOver](https://www.apple.com/accessibility/mac/vision/){:target="blank"}, for Windows it is [Narrator](https://support.microsoft.com/en-us/help/22798/windows-10-complete-guide-to-narrator){:target="blank"}.

## 3. Search engines (SEO)
Moving on from one machine type to another. The structure of your web page can affect SEO (Search Engine Optimization) results.

<blockquote>
  SEO stands for ‘Search Engine Optimization’. It’s the practice of optimizing your web pages to make them reach a high position in the search results of Google or other search engines.
	&mdash;<cite><a href="https://yoast.com/what-is-seo/" target="_blank">YOAST</a></cite>
</blockquote>

However semantic HTML is not the primary factor that affect the SEO of the page, but it helps page [crawlers](https://www.google.com/search/howsearchworks/crawling-indexing/){:target="blank"} understand the structure of this page. A page with proper semantic HTML will have a chance to [rank higher in the search results](https://www.inboundnow.com/html5-semantic-elements-mean-seo/){:target="blank"}.

## 4. Usability (UX)

By implementing semantic HTML not only you are aiding the machines, but you can also help people and make their lives better. The use of proper semantic HTML can boost up your website usability and accessibility. I think you all will agree with me, that you like resources that are intuitive and easy to use.

Sometimes small adjustments or fine tuning can make a huge difference for users. For instance adding a `label` element next to `input`, or adding a proper attribute to the same `input` element.

Some of the widgets you can create with pure semantic HTML:
- [Accordion](/native-html-accordion)
- [Autocomplete input](/html-autocomplete)
- [Modal/dialog window](/html-dialog-element)
- [Clickable email and phone links](/clickable-email-and-phone-links)

## 5. Default styling

The good thing about semantic HTML is that semantic elements comes with default styling. Even without additional CSS the page that is built with proper semantic HTML will look good, be accessible and is going to provide the meaning and outline the structure.

Even though the default styling can vary from browser to browser, the main look of the page will remain.

Default styling comes to the rescue when something goes wrong and your CSS fails.

Below I’ll share a list of resources I have found useful when I was learning about semantic HTML and Semantic Web in particular.


Blogs:
* [https://codepen.io/mi-lee/post/an-overview-of-html5-semantics](https://codepen.io/mi-lee/post/an-overview-of-html5-semantics){:target="blank"}
* [https://internetingishard.com/html-and-css/forms/](https://internetingishard.com/html-and-css/forms/){:target="blank"}
* [http://html5doctor.com/lets-talk-about-semantics/](){:target="blank"}
* [https://stackoverflow.com/questions/17272019/why-to-use-html5-semantic-tag-instead-of-div](https://stackoverflow.com/questions/17272019/why-to-use-html5-semantic-tag-instead-of-div){:target="blank"}
* [https://webflow.com/blog/html5-semantic-elements-and-webflow-the-essential-guide](https://webflow.com/blog/html5-semantic-elements-and-webflow-the-essential-guide){:target="blank"}
* [https://www.dallasseogeek.com/uncategorized/understanding-semantic-html-and-its-applications-for-2015-and-beyond/#.WdRs79MjFTY](https://www.dallasseogeek.com/uncategorized/understanding-semantic-html-and-its-applications-for-2015-and-beyond/#.WdRs79MjFTY){:target="blank"}
* [https://www.smashingmagazine.com/2011/11/our-pointless-pursuit-of-semantic-value/](https://www.smashingmagazine.com/2011/11/our-pointless-pursuit-of-semantic-value/){:target="blank"}
* [http://html5doctor.com/microformats/](http://html5doctor.com/microformats/){:target="blank"}
* [http://html5doctor.com/microdata/](http://html5doctor.com/microdata/){:target="blank"}
* [https://www.lifewire.com/why-use-semantic-html-3468271](https://www.lifewire.com/why-use-semantic-html-3468271){:target="blank"}

Docs:
* [https://en.wikipedia.org/wiki/Semantic_Web](https://en.wikipedia.org/wiki/Semantic_Web){:target="blank"}
* [https://developers.google.com/web/fundamentals/native-hardware/click-to-call/](https://developers.google.com/web/fundamentals/native-hardware/click-to-call/){:target="blank"}
* [https://developers.google.com/web/fundamentals/accessibility/semantics-builtin/](https://developers.google.com/web/fundamentals/accessibility/semantics-builtin/){:target="blank"}
* [http://microformats.org/wiki/html5](http://microformats.org/wiki/html5){:target="blank"}
* [https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time){:target="blank"}
* [https://www.w3.org/RDF/FAQ](https://www.w3.org/RDF/FAQ){:target="blank"}
* [https://www.w3.org/2006/Talks/0718-aaai-tbl/Overview.html#(1)](https://www.w3.org/2006/Talks/0718-aaai-tbl/Overview.html#(1)){:target="blank"}
* [https://medium.com/virtuoso-blog/a-semantic-web-artificial-intelligence-ea480b8f4507](https://medium.com/virtuoso-blog/a-semantic-web-artificial-intelligence-ea480b8f4507){:target="blank"}
* [https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA){:target="blank"}
* [https://www.w3.org/TR/rdfa-primer/](https://www.w3.org/TR/rdfa-primer/){:target="blank"}
* [http://schema.org/docs/about.html](http://schema.org/docs/about.html){:target="blank"}
* [http://rdfa.info/](http://rdfa.info/){:target="blank"}
* [https://developer.mozilla.org/en-US/docs/Glossary/Semantics#Semantics_in_HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#Semantics_in_HTML){:target="blank"}

Videos:
* [https://www.youtube.com/watch?v=qvONd7Z8vec](https://www.youtube.com/watch?v=qvONd7Z8vec){:target="blank"}
* [https://www.youtube.com/watch?v=z9_rdtdA2BQ](https://www.youtube.com/watch?v=z9_rdtdA2BQ){:target="blank"}
* [https://www.youtube.com/watch?v=OGg8A2zfWKg](https://www.youtube.com/watch?v=OGg8A2zfWKg){:target="blank"}











