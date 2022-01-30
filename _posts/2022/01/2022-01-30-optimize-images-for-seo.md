---
layout: post
title: How to optimize images for SEO, Performance, and Accessibility
description: Developers guide on how to optimize images for SEO, Performance, and Accessibility
tags: [seo, performance, html]
---

Images are an essential part of any web page, as they provide additional information and supplement the content. In this guide, I’d like to share with you some tips on how you can optimize images on your website to improve SEO, Performance, and Accessibility.

## Image name (Affects SEO)
The image name can affect the way search engines parse/understand the content of the image  (Google in particular).

A descriptive image name is preferable over an unreadable (e.g. auto-generated) one:

```html
<!-- Good -->
<img src="my-new-black-kitten.jpg" />
<!-- Bad -->
<img src="IMG00023.JPG" />
```

> Likewise, the filename can give Google clues about the subject matter of the image. For example, my-new-black-kitten.jpg is better than IMG00023.JPG. If you localize your images, make sure you translate the filenames, too.
>
> &mdash;<cite><a href="https://developers.google.com/search/docs/advanced/guidelines/google-images#descriptive-titles-captions-filenames">Google</a></cite>

It comes in handy not only for the search engines to understand the context of the image but also to rank it higher in the images search results.

## Alt text (Affects SEO and Accessibility)
The proper image name is immediately followed by the alt text. Each image should have the [`alt` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#alternative_text) containing the image description. It helps people using assistive technologies like screen readers understand the content of the page.

Also if the image fails to load, users will still be able to understand what it is about, by reading the alt text that will be shown.

Search engines like Google take the `alt` attribute into account to understand the [subject matter of the image](https://developers.google.com/search/docs/advanced/guidelines/google-images#use-descriptive-alt-text). Thus it will help understand crawl bot what this image is about. So make sure to provide a meaningful description.

```html
<!-- Good -->
<img src="kitten.jpg" alt="Black kitten sitting on a couch" />
<!-- Bad -->
<img src="kitten.jpg" />
```

## Image file size (Affects Performance)

Jumping into the performance zone. Before you add an image to the page check image file size. The larger the file size the longer it will take to load, the more bandwidth it will use.

So image size can drastically affect your page load speed.

To optimize your image file size, you can:
- [Resize the image](https://gtmetrix.com/blog/how-to-properly-size-images/) (in the image editor), you don’t necessarily need a 2000x2000 px image inside a 600px container. So it’s a good idea to have proper image dimensions that can affect total file size. Of course, there might be cases when you need that 2000x2000px image on your page, but that’s a whole other story.
- Compress the image. Image compression can save you up to 60% of the total image size. There are even [online tools for image compression](https://tinypng.com/).

## Image format (Affects Performance)

The image format is closely related to image size from the previous point. [Choosing the right image format](https://developers.google.com/web/fundamentals/design-and-ux/responsive/images#choose_the_right_format) can impact the total image size.

Two of the most popular image formats used today are:
- JPEG
- PNG

However, there are [modern image formats](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/) that provide lossy and lossless compression, as well as animation and alpha transparency. This means that the same image with the new format will take up less size:
- AVIF ([check AVIF browser support](https://caniuse.com/avif))
- WebP ([check WebP browser support](https://caniuse.com/webp))

It is worth mentioning the SVG format for images. It is great for logos and line art, and because vector images are built on simple primitives they can be scaled without any loss in quality or change in file size. But the best part is that it can be inserted directly into HTML code. Thus it won’t take additional network requests to display the image.

## srcset attribute (Affects Performance)

With the help of [`srcset` attribute](https://html.com/attributes/img-srcset/) you can specify different images to be loaded on different devices (viewports), thus ensuring a [better user experience](https://developers.google.com/search/docs/advanced/guidelines/google-images#responsive-images).

For instance, it’s a good idea to show a high-resolution image on a device with a [retina display](https://en.wikipedia.org/wiki/Retina_display) and to show a standard image for a regular device. The same principle can be applied to a device viewport. Smaller images are displayed on smaller screens, larger images are displayed on wider screens.

```html
<img
 srcset="
  /img/snowy-mountain-320w.png 320w,
  /img/snowy-mountain-480w.png 480w,
  /img/snowy-mountain-640w.png 640w,
  /img/snowy-mountain-800w.png 800w
 "
 src="/img/snowy-mountain-800w.png"
>
```

## loading attribute (Affects Performance)

Page load speed is one of the [Google ranking factors](https://developers.google.com/search/blog/2010/04/using-site-speed-in-web-search-ranking). And images along with other media contribute to the overall page size and page load speed.

To ensure the page loads fast you can lazy load images by using the [`loading` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-loading) with a `lazy` value. The `loading="lazy"` attribute will tell the browser to load the image only when the user scrolls near it.

```html
<img loading="lazy" src="kitten.jpg" alt="Black kitten sitting on a couch" />
```

This is a native way to lazy load your images, however, it is [not yet supported by all browsers](https://caniuse.com/loading-lazy-attr). On the other hand, if you wish to support all browsers you can use a JavaScript library to [lazy load your images](/lazy-load-images).

