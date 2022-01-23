---
layout: post
permalink: html-meta-tags-for-social-media
title: HTML meta tags for social media cards
date: 2021-10-20T10:21:57.066Z
description: A complete guide to create beautiful cards using HTML meta tags for
  social media
tags:
  - html
---
Your website can have a social media card so that when you share it online it looks more appealing and provide additional information for people. To do so you’ll need to add HTML meta tags for social media.

## What is a social media card?

A social media card is a visual representation of the content of a specific web page on a social media platform that it is being shared on. You most probably have already seen these on Twitter, Facebook, and LinkedIn.

<figure>
  <img class="shadow lozad" data-src="/images/misc/facebook-card.png" alt="Facebook social media card">
  <noscript>
    <img class="shadow" src="/images/misc/facebook-card.png" alt="Facebook social media card">
  </noscript>
  <figcaption>Facebook social media card</figcaption>
</figure>

<figure>
  <img class="shadow lozad" data-src="/images/misc/twitter-card.png" alt="Twitter social media card">
  <noscript>
    <img class="shadow" src="/images/misc/twitter-card.png" alt="Twitter social media card">
  </noscript>
  <figcaption>Twitter social media card</figcaption>
</figure>

<figure>
  <img class="shadow lozad" data-src="/images/misc/linkedin-card.png" alt="LinkedIn social media card">
  <noscript>
    <img class="shadow" src="/images/misc/linkedin-card.png" alt="LinkedIn social media card">
  </noscript>
  <figcaption>LinkedIn social media card</figcaption>
</figure>

A social media card acts as a teaser to a webpage, by providing users with some information on what kind of content it has. Like page title, description, and an image.

When a link is shared on a social media platform it scans the page for specific meta tags, and then it takes the data from these meta tags and displays it in a form of a card.

If no social media meta tags are specified then the shared webpage will be represented as a regular link.

## Open Graph meta tags (Facebook, LinkedIn)

The [Open Graph](https://ogp.me/) meta tags are used by most of the social media platforms, most known are Facebook and LinkedIn.

These meta tags have a property attribute that contains a value with the `og:` prefix and the content attribute.

There are quite a few properties you can use for the Open Graph meta tags, but the four required ones are:

* `og:title` - represents the web page title
* `og:description` - the description of your web page
* `og:image` - an image URL
* `og:url` - the URL of your web page

**NOTE: Recommended [image size](https://developers.facebook.com/docs/sharing/best-practices#images) for the Facebook card is 1080 pixels in width and the minimum is 600px in width.**

## Twitter meta tags

Unlike other social media platforms, Twitter has its [own unique meta tags](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started) for displaying cards. It is called a Twitter Card and it looks very similar to the Open Graph cards.

Just like the Open Graph, the Twitter meta tags have a property attribute with the `twitter:` prefix.

* `twitter:title` - represents the web page title
* `twitter:description` - the description of your web page
* `twitter:image` - an image URL

**NOTE: [Images](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/summary-card-with-large-image) for Twitter Card support an aspect ratio of 2:1 with minimum dimensions of 300x157 or a maximum of 4096x4096 pixels.**

When the Twitter card processor looks for tags on a page, it first checks for the Twitter-specific property, and if not present, falls back to the supported Open Graph property. This allows for both to be defined on the page independently and minimizes the amount of duplicate markup required to describe content and experience.

**NOTE: all meta tags should be placed at the `head` of your web page.**

## Ready to use code snippet

```html
<head>

<meta property="og:title" content="Frontend Dev Blog" />
<meta property="og:description" content="A blog about frontend web development - tips, tricks, use cases, how-tos, examples, stories." />
<meta property="og:url" content="https://nikitahl.com/" />
<meta property="og:image" content="https://nikitahl.com/images/icons/twitter-image.png" />

<meta name="twitter:title" content="Frontend Dev Blog">
<meta name="twitter:description" content="A blog about frontend web development - tips, tricks, use cases, how-tos, examples, stories.">
<meta name="twitter:image" content="https://nikitahl.com/images/icons/twitter-image.png">
<meta name="twitter:card" content="summary_large_image">

</head>
```

## Useful Resources

* [Twitter card validator](https://cards-dev.twitter.com/validator)
* [Twitter Summary card with large image](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/summary-card-with-large-image)
* [Facebook guide to sharing](https://developers.facebook.com/docs/sharing/webmasters)
* [LinkedIn card inspector](https://www.linkedin.com/post-inspector/inspect/)
* [Pinterest URL debugger](https://developers.pinterest.com/tools/url-debugger/)