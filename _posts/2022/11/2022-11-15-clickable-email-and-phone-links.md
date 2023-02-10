---
layout: post
permalink: clickable-email-and-phone-links
title: How to make clickable contact links in HTML (email, phone, etc)
description: To make your page more accessible and user-friendly you can create clickable links for specific texts.
updated: 2023-02-10T09:45:10.124Z
tags: [html]
---

To make your page more accessible and user-friendly you can create clickable links for specific texts. It can be phone number, email, sms, and more.

In this article, I’d like to show you how you can improve the accessability of a page by implementing just [semantic HTML](/why-it-is-important-to-write-semantic-html) changes (additionally to indicate the link purpose you can add a [specific styles](/link-underline-with-css) to it).

To create links with specific actions you should use an anchor tag with a `href` attribute that contains certain parameters (following the [URI syntax](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Syntax){:target="blank"}).

## Clickable email link

Inside the `href` attribute specify `mailto` parameter and the email that is separated by a colon

```html
<a href="mailto:email@example.com">email@example.com</a>
```

Clicking on this link will open an email client on a user’s device with a specified email address to send it to.

You can specify more than one email, just separate them with a comma:

```html
<a href="mailto:email@example.com, secondemail@example.com">Send us an email</a>
```

You can use other parameters for sending emails like [cc and bcc](https://blog.udemy.com/cc-vs-bcc/){:target="blank"}.

* mailto: recipient’s email address
* cc: the email address that will receive the carbon copy of the mail (optional)
* bcc: the email address that will receive the blind carbon copy of the mail (optional)
* subject: the subject of the email (optional)
* body: the content of the email (optional)
* ?: the first parameter delimiter (optional).
* &: the other parameter delimiter (optional).

The full set of these parameters might look like this:

```html
<a href="mailto:email@example.com?cc=secondemail@example.com, thirdemail@example.com, &bcc=lastemail@example.com&subject=Mail from my site&body=Hello!">Send us an email</a>
```

## Clickable phone link

Having a click action on a phone number is as important as the previous one. Clicking on a phone number will instantly make a phone call.

You'll need to specify the `tel` parameter separated by colon from a phone number:

```html
<a href="tel:+012345678910">0-123-45678910</a>
```

A click on such a link will trigger a phone call.

## Clickable sms link

To send an SMS message use the following syntax.

```html
<a href="sms:+012345678910">Send us a message</a>
```

You can add a body parameter to set the initial text of the message:

```html
<a href="sms:+012345678910?body=Hello!%20How%20are%20you%3F">Send us a message</a>
```

The body attribute should contain a [URL-encoded](https://meyerweb.com/eric/tools/dencoder/){:target="blank"} value.

## Clickable Geolocation link

For Android OS devices you can specify geolocation via the [geo URI Scheme](https://en.m.wikipedia.org/wiki/Geo_URI_scheme){:target="blank"} `"geo:latitude,longitude"` specified by [RFC 5870](https://www.rfc-editor.org/rfc/rfc5870){:target="blank"}.

Clicking on such a link will open a map application with given coordinates.

```html
<a href='geo:47.26769008051434, 11.407943002524679'>Our location</a>
```

<p class="note">💡 TIP: Make sure that these links are easily clickable on mobile devices. To do so, you can increase spacingbetween links by adding margin and increase tappable area by adding padding.</p>
