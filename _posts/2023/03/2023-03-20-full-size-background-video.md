---
layout: post
permalink: full-size-background-video
title: Create a full-size background video with pure CSS
date: 2023-03-20T21:15:12.133Z
description: You can create a full-size background video that scales for a given container on all devices from mobile to desktop using nothing but pure CSS.
tags: [css]
---

You can create a full-size background video that scales for a given container on all devices from mobile to desktop using nothing but pure CSS.

Having a background video on your site is a good way to highlight the feature of your product, services, or your brand in general. Quite often you can see a full-size background video as the first section of a website.

In this article, I’ll show you how to make any video scale the full size of any section’s background.

1. [Self-hosted video](#full-size-self-hosted-video)
2. [YouTube video](#full-size-youtube-background-video)
3. [Vimeo video](#full-size-vimeo-background-video)

For this example, let’s create a section with a title, subtitle, and a call to action button.

Also for the sake of this example let’s make this section span the full width and full height of the viewport (but you can make it [any size](/css-aspect-ratio) you want).

```html
<section>
  <h1>Hello World! 👋</h1>
  <p>A full-size background video section with pure CSS.</p>
  <button>Get it now</button>
<section>
```

```css
section {
  width: 100vw;
  height: 100vh;
}
```

## Full-size self-hosted video

For the self-hosted video, we’ll need to add a video element with a source that specifies the path of the video file. We’ll add it to our section:

```html
<section>
  <h1>Hello World! 👋</h1>
  <p>A full-size background video section with pure CSS.</p>
  <button>Get it now</button>
  <video class="video-background" poster="url/for/poster-image.webp" autoplay muted loop>
    <source src="/videos/runner.mp4" type="video/mp4">
  </video>
</section>
```

It’s a good practice to specify additional attributes for the video element. It’ll make the video more user-friendly and appealing.

We want the video to be without any sound - `muted`, to start playing immediately on page load - `autoplay`, and play it on a loop - `loop`.

Also, we’ll specify the `poster` attribute for a nice-looking preview, a nice way to handle the idle time while the video is being loaded.

Now to make it a full-size background:

```css
section {
  position: relative;
  overflow: hidden; /* prevent video from overflowing */
}

.video-background {
  position: absolute; /* make it relative to the section */
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%); /* center it */
  object-fit: cover; /* fill the element’s entire content box */
  height: 100%; /* make it 100% of the section */
  margin: 0; /* remove margins that could be added by the browser */
  z-index: -1; /* make it below the text */
}
```

## Full-size YouTube background video

For the YouTube background, we’ll need additional HTM that will help us position the video.

```html
<section>
  <div class="yt-container">
    <div class="yt-background">
      <svg class="yt-sizer" width="640" height="360"></svg>
      <iframe
        class="yt-video"
        src="https://www.youtube.com/embed/CVHj7Wxhvdo?controls=0&mute=1&autoplay=1&loop=1&playlist=CVHj7Wxhvdo"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen>
      </iframe>
    </div>
  </div>
</section>
```

Lets break it down.

First, we’ll need to create a container `div` (`yt-container`), which will take full size of the section.

Inside the container we’ll add a second `div` (`yt-background`) will stretch beyond the first one but no overflow it. And position it in the center.

Inside the second `div` we’ll place the transparent `svg` (`yt-sizer`) with `width` and `height` attributes, this will prevent our wrappers from collapsing.

Finally, the video itself will be inside the `iframe`, which you’ll have to copy from YouTube.

Additionaly, for the `iframe` URL you'll need to specify few parameters, each separeated by ampersand symbol `&`.

- `controls=0` - hide video controls
- `mute=1` - mute the video
- `autoplay=1` - make video autoplay
- `loop=1` - set it on a loop
- `playlist=idOfTheVideo` - a playlist parameter equal to the id of the video, in my example it is `CVHj7Wxhvdo`, otherwise the infinite loop won't work

A full list of [YouTube player paremeters](https://developers.google.com/youtube/player_parameters){:target="_blank"}.

Full CSS for the YouTube background video:

```css
.yt-container {
  position: absolute; /* Postion relative to section */ 
  /* Make it full size ↓ */
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  overflow: hidden; /* Prevent video overflow */
  pointer-events: none; /* Prevent user interaction */ 
  z-index: -2; /* Make YouTube container underneath section content */
}

.yt-background {
  position: absolute; /* Postion relative to .yt-container */
  /* center it ↓ */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* make it full height ↓ */
  height: 100%;
}

/* Make a hidden sizer SVG to take up full size of the .yt-background */
.yt-sizer {
  display: inline-block;
  width: auto;
  max-width: none;
  height: 100%;
  border: none;
  vertical-align: top;
}

.yt-video {
  position: absolute; /* Postion relative to .yt-background */
  /* Postion at the top and make it full size ↓ */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* cover image, if video is failed to load */
  background: url(url/to/a/cover-image.webp) no-repeat center; 
  background-size: cover;
}
```

## Full-size Vimeo background video

For the full-size Vimeo background we’ll need to do essentially the same as we did for YouTube video.

Create a additional HTML to position the Vimeo `iframe` embed.

```html
<section>
  <div class="vimeo-container">
    <div class="vimeo-background">
      <svg class="vimeo-sizer" width="640" height="360"></svg>
      <iframe
        class="vimeo-video"
        src="https://player.vimeo.com/video/27246366?h=75fabdf419&title=0&byline=0&portrait=0&muted=1&autoplay=1&autopause=0&controls=0&loop=1"
        width="640"
        height="360"
        frameborder="0"
        allow="autoplay; fullscreen; picture-in-picture"
        allowfullscreen>
      </iframe>
    </div>
  </div>
</section>
```

Additionaly, for the `iframe` URL you'll need to specify few parameters, each separeated by ampersand symbol `&`.

- `title=0` - hide video title
- `byline=0` - hide video author name
- `portrait=0` - hide video author portrait
- `muted=1` - mute the video
- `autoplay=1` - make video autoplay
- `autopause=1` - prevent video from pausing
- `controls=0` - hide video controls
- `loop=1` - set it on a loop

A full list of [Vimeo player paremeters](https://developer.vimeo.com/player/sdk/embed){:target="_blank"}.

The CSS code does similar thing, it positions containers relative to one another and aligns the video.

```css
.vimeo-container {
  position: absolute;  /* Postion relative to section */
  /* Make it full size ↓ */
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  overflow: hidden;  /* Prevent video overflow */
  pointer-events: none;  /* Prevent user interaction */
  z-index: -2;  /* Make Vimeo container underneath section content */
}

.vimeo-background {
  position: absolute; /* Postion relative to .vimeo-container */
  /* center it ↓ */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* make it full height ↓ */
  height: 100%;
}

/* Make a hidden sizer SVG to take up full size of the .vimeo-background */
.vimeo-sizer {
  border: none;
  max-width: none;
  height: 100%;
  width: auto;
  display: inline-block;
  vertical-align: top;
}

.vimeo-video {
  position: absolute; /* Postion relative to .vimeo-background */
  /* Postion at the top and make it full size ↓ */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* cover image, if video is failed to load */
  background: url(url/to/a/cover-image.webp) no-repeat center; 
  background-size: cover;
}
```

## Demo

You can find full demo with complete code examples on my CodePen:

- [Self-hosted video](https://codepen.io/nikitahl/pen/PoddXQR){:target="_blank"}
- [YouTube video](https://codepen.io/nikitahl/pen/mdGGaxq){:target="_blank"}
- [Vimeo video](https://codepen.io/nikitahl/pen/oNPPJdZ){:target="_blank"}
