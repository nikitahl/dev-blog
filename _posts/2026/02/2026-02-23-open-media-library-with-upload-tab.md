---
layout: post
permalink: open-media-library-with-upload-tab
title: How to open the WordPress Media Library with an Upload files tab by default
date: 2026-02-25
description: A short guide explaining how to open the Media Library in WordPress, with the Upload files tab by default, using JavaScript.
tags: [javascript, wordpress]
---

By default, the Media Library in WordPress opens up with a list of media files to select from. However, you can set the default tab to Upload files with a single property.

<p class="note">
💡 NOTE: First, make sure the global <code>wp.media</code> object is available in your <code>window</code> scope.
</p>

If `wp.media` is not available, ensure the Media Library scripts are enqueued in PHP via:

```php
 wp_enqueue_media();
```

Full reference is available in the [WordPress codex](https://codex.wordpress.org/Javascript_Reference/wp.media#Enqueue_Required_Media_Script){:target="_blank"}.

In JavaScript, create a frame.

```javascript
const myFrame = wp.media({
        title: 'Add images',
        library: {
          type: 'image'
        }
      });
```

Use the `open` method to open the actual Media Library:

```javascript
myFrame.open()
```

The config above will open Media Library with the *"Add media"* tab by default, where all the media files are listed.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-media-library-media-list.png" alt="Default WordPress Media Library panel">
  <figcaption>Default WordPress Media Library panel</figcaption>
</figure>

To open the Media Library with the Upload files tab by default, you’ll need to specify an additional property in your frame's [`Library` object](https://atimmer.github.io/wordpress-jsdoc/wp.media.controller.Library.html){:target="_blank"}.

That is the `contentUserSetting` property, which should be set to `false`; by default, it is set to `true`.

If you're using a single frame without any states, you can just add this snippet to your code. Which will set the `contentUserSetting` property's value.

```javascript
wp.media.controller.Library.prototype.defaults.contentUserSetting = false;
```

Then, on the next Media Library frame open, you should see the Upload files tab active by default.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-media-library-upload-files.png" alt="WordPress Media Library panel with active Upload tab">
  <figcaption>WordPress Media Library panel with active Upload tab</figcaption>
</figure>

Similarly, if you use states with your frame, then for the upload state, set the `contentUserSetting` property.

```javascript
const myFrame = wp.media({
  state: 'select', // Default state of the frame
  title: 'Select images',
  library: {
    type: 'image'
  },
  states: [
    new wp.media.controller.Library({
      id: 'upload',
      title: 'Upload image',
      contentUserSetting: false // Make an upload file tab open by default
    }),
    new wp.media.controller.Library({
      id: 'select',
      title: 'Select images'
    })
  ]
});
```

Then, after you change the state, the Upload tab will be active on the next opening of the frame.

```javascript
myFrame.setState('upload');
myFrame.open();
```

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/wordpress/wordpress-media-library-states.png" alt="WordPress Media Library panel with different states toolbar">
  <figcaption>WordPress Media Library panel with different states toolbar</figcaption>
</figure>
