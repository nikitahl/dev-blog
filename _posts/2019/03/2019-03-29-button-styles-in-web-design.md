---
layout: post
title: Modern button styles in web design
description: An interesting observation of button styles used in web design today.
tags: [html, css]
comments: true
---

The modern world of web design and UI is dominated by Material and Flat design trends. 

This statement also applies to button elements on a webpage. And I'm talking about buttons, not menu items, various controls, links, icons, etc.

Keeping this in mind, if you think about it, there are 6 main style types of buttons in web design. You can split them into 2 categories: *filled* and *outlined*. Each category have 3 basic shapes: *square*, *rounded* and *round*.

<style type="text/css">
	.btn-container {
	  flex: 0 0 100%;
	  display: flex;
	  justify-content: space-between;
	  align-items: center;
	  flex-wrap: wrap;
    margin: 30px auto 0;
    width: 80%;
	}

	.btn {
	  font-size: 16px;
	  padding: 13px 40px;
	  background-color: transparent;
	  background-image: none;
	  border: none;
	  cursor: pointer;
	  display: inline-block;
	  margin: 0;
	  max-width: 100%;
	  position: relative;
	  text-align: center;
	  text-decoration: none;
	  vertical-align: middle;
	  white-space: normal;
	  touch-action: manipulation;
	  user-select: none;
	  line-height: 22px;
	  border-radius: 0;
	  transition: all 0.2s ease-in-out;
	  -webkit-appearance: none;
	  outline: none;
	}

	.btn-filled {
	  background: #2196f3;
	  color: #fff;
	}
	.btn-filled:hover {
	  background: #0a6ebd;
	}

	.btn-outlined {
	  border: 2px solid #2196f3;
	  color: #2196f3;
	}
	.btn-outlined:hover {
	  border-color: #0a6ebd;
	  color: #0a6ebd;
	}

	.btn-square {
	  border-radius: 0;
	}

	.btn-rounded {
	  border-radius: 5px;
	}

	.btn-round {
	  border-radius: 4em;
	}

	figure {
		margin-bottom: 40px;
	}

	@media screen and (max-width: 600px) {
		.btn-container {
		  flex-direction: column;
		  margin: 20px auto 0;
		}

		.btn {
		  margin: 0 0 30px;
		}
	}
</style>

## Filled buttons
<div class="btn-container">
  <button class="btn btn-filled btn-square">Sign in</button>
  <button class="btn btn-filled btn-rounded">Sign in</button>
  <button class="btn btn-filled btn-round">Sign in</button>
</div>

## Outlined buttons
<div class="btn-container">
  <button class="btn btn-outlined btn-square">Sign in</button>
  <button class="btn btn-outlined btn-rounded">Sign in</button>
  <button class="btn btn-outlined btn-round">Sign in</button>
</div>

Of course there are exceptions and you may find some bizarre and fancy buttons out there. Also there may be countless modifications to the original ones with all the effects and transitions CSS has to offer these days. But at the end of the day all of these fancy styled buttons are based on these 6 main button style types.

Below are some of the most famous services and resources putting these principles into practice.

<figure>
  <img class="shadow" src="/images/button-styles/awwwards-buttons.png" alt="Awwwards buttons" loading="lazy">
  <figcaption>Awwwards buttons</figcaption>
</figure>

<figure>
  <img class="shadow" src="/images/button-styles/gmail-buttons.png" alt="Gmail buttons" loading="lazy">
  <figcaption>Gmail buttons</figcaption>
</figure>

<figure>
  <img class="shadow" src="/images/button-styles/instagram-buttons.png" alt="Instagram buttons" loading="lazy">
  <figcaption>Instagram buttons</figcaption>
</figure>

<figure>
  <img class="shadow" src="/images/button-styles/medium-buttons.png" alt="Medium buttons" loading="lazy">
  <figcaption>Medium buttons</figcaption>
</figure>

<figure>
  <img class="shadow" src="/images/button-styles/reddit-buttons.png" alt="Reddit buttons" loading="lazy">
  <figcaption>Reddit buttons</figcaption>
</figure>

<figure>
  <img class="shadow" src="/images/button-styles/twitter-buttons.png" alt="Twitter buttons" loading="lazy">
  <figcaption>Twitter buttons</figcaption>
</figure>

Check out these awesome [buttons on Codepen](https://codepen.io/search/pens?q=buttons&page=1&order=popularity&depth=everything){:target="blank"} and notice that most of them uses the same kind of design princilpes.

This article on Medium describes the [7 rules for button design](https://uxplanet.org/7-basic-rules-for-button-design-63dcdf5676b4){:target="blank"}. And even there you can find the pattern in advices given.

To conclude, there is no actual point in this article, just an observation I've noticed and found it interesting, so I decided to share it with you.

