---
layout: post
permalink: clickable-email-and-phone-links
title: Creating Accessible Clickable Contact Links in HTML
description: To make your page more accessible and user-friendly you can create clickable links for specific texts.
updated: 2023-10-16T20:15:10.124Z
tags: [html]
---

To make your page more accessible and user-friendly you can create clickable links for specific texts. It can be phone number, email, SMS, and more.

In this article, I’d like to show you how you can improve the accessibility of a page by implementing just [semantic HTML](/why-it-is-important-to-write-semantic-html) changes (additionally to indicate the link purpose you can add a [specific style](/link-underline-with-css) to it).

1. [Clickable email link](#clickable-email-link)
2. [Clickable phone link](#clickable-phone-link)
3. [Clickable SMS link](#clickable-sms-link)
4. [Clickable Geolocation link](#clickable-geolocation-link)
5. [Tips to increase accessibility](#tips-to-increase-accessibility)

<br />

To create links with specific actions you should use an anchor tag with a `href` attribute that contains certain parameters (following the [URI syntax](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Syntax){:target="blank"}).

<style>
.image-grid{display:flex;justify-content:space-evenly;flex-wrap:wrap;margin:0 0 30px}
.image-grid figcaption{font-size:13px;color:#666;font-style:italic;text-align:center}
.image-grid figure{margin:0 10px 30px;flex:0 0 85%}
.vertical{width:60%}
</style>
<div class="image-grid">
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/tesla-contact-page.webp" alt="Tesla contact page">
    <figcaption>Example of a clickable email link on a Tesla website</figcaption>
  </figure>
  <figure>
    <img class="shadow" loading="lazy" src="/images/misc/tele2-contact-page.webp" alt="Tele2 contact page">
    <figcaption>Example of a clickable phone link on a Tele2 website</figcaption>
  </figure>
</div>

## Clickable email link

Inside the `href` attribute specify the `mailto` parameter and the email that is separated by a colon as follows:

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

You'll need to specify the `tel` parameter separated by a colon from a phone number:

```html
<a href="tel:+012345678910">0-123-45678910</a>
```

A click on such a link will trigger a phone call.

## Clickable SMS link

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

<p class="note">💡 TIP: Make sure that these links are easily clickable on mobile devices. To do so, you can increase spacing between links by adding margin and increase tapable area by adding padding.</p>

## Tips to increase accessibility

By adding the `title` and `aria-label` attributes, you improve the accessibility of the link for users with disabilities.

* `title`: This attribute provides a [tooltip](/css-only-tooltip) or title for the link, which is displayed when users hover over it.
* `aria-label`: This attribute provides an accessible label for the link, which is useful for screen readers and assistive technologies.

Here's a more detailed example with additional attributes:

```html
<a href="tel:+1234567890" title="Call our support team" aria-label="Call Us">
  Call Us
</a>
```

## Conclusion

By implementing clickable contact links with semantic HTML, you can enhance the accessibility and user-friendliness of your webpages. These links offer a seamless way for users to contact you, making their experience more convenient and engaging.