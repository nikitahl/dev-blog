---
layout: post
title: Parse URL strings with native JavaScript API
description: How to parse URL strings with native JavaScript API
tags: [javascript]
comments: true
---

There's an easy native way to parse URL strings with JavaScript API.

To do that you'll need to use the `URL` interface:

<blockquote>
The <code>URL</code> interface is used to parse, construct, normalize, and encode URLs.
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/API/URL" target="_blank">MDN</a></cite>
</blockquote>

To use this API you'll need to create a new object via `new URL()`. This object will hold multiple URL properties and methods which will allow you to later manipulate parts of URL.

```javascript
const url = 'http://localhost:8888/wp-one/wp-admin/post-new.php?post_type=page&vcv-action=frontend'
const urlData = new URL(url)
```
The `urlData` object will look like this:

```javascript
{
href: "http://localhost:8888/wp-one/wp-admin/post-new.php?post_type=page&vcv-action=frontend"
origin: "http://localhost:8888"
protocol: "http:"
username: ""
password: ""
host: "localhost:8888"
hostname: "localhost"
port: "8888"
pathname: "/wp-one/wp-admin/post-new.php"
search: "?post_type=page&vcv-action=frontend"
searchParams: URLSearchParams {}
hash: ""
  __proto__: URL
  href: (...)
  origin: (...)
  protocol: (...)
  username: (...)
  password: (...)
  host: (...)
  hostname: (...)
  port: (...)
  pathname: (...)
  search: (...)
  searchParams: (...)
  hash: (...)
  toJSON: ƒ toJSON()
  toString: ƒ toString()
}
```
The initial URL string is torn apart and each part is accessible via corresponding property that holds a `string` value. E.g. the protocol can be accessed via `protocol` property:

```javascript
urlData.protocol // 'http:'
```

The cool thing about it, is that now you can manipulate the search query of the URL via `searchParams` property which return the `URLSearchParams` interface.

<blockquote>
The <code>URLSearchParams</code> interface can be used to build and manipulate the URL query string.
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams" target="_blank">MDN</a></cite>
</blockquote>

Let's use the existing data to get the part of the search query:

```javascript
url // 'http://localhost:8888/wp-one/wp-admin/post-new.php?post_type=page&vcv-action=frontend'

url.searchParams.get('post_type') // 'page'
```
This interface allows also to delete, set, sort, iterate and [more](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams#Methods){:target="blank"}!

**The URL interface is availabe in all modern browsers:**

<p class="ciu_embed" data-feature="url" data-periods="future_1,current,past_1" data-accessible-colours="false">
<a href="https://caniuse.com/#feat=url">Can I Use URL API?</a> Data on support for the URL API feature across the major browsers from caniuse.com.
</p>

<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/caniuse-embed.min.js"></script>


