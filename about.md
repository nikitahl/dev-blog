---
layout: page
title: About
description: Who I am and what I do. 
permalink: /about/
---

<style type="text/css">
	.about-container {
		display: flex
	}
	.about-image-container {
		flex: 0 0 200px;
		height: 200px;
		overflow: hidden;
		border-radius: 50%;
		margin: 0 30px 0 0
	}
	@media screen and (max-width: 768px) {
		.about-image-container {
			height: 130px;
			flex: 0 0 130px;
		}
	}
	@media screen and (max-width: 641px) {
		.about-container {
			flex-direction: column
		}
		.about-image-container {
			width: 200px;
			height: 200px;
			flex: 0 0 200px;
		}
	}
</style>
<div class="about-container">
	<div class="about-image-container">
		<img src="../../../images/me.png" alt="Nikita Hlopov profile picture">
	</div>
	<div class="about-content-container">
		<p>Hello, my name is Nikita!</p>
		<p>I'm a full time frontend developer at <a href="http://visualcomposer.com" target="_blank" rel="noreferrer noopener">Visual Composer</a>.</p>
		<p>Once I've started frontend development profession as a job but in a while it became my hobby.</p>
		<p>Sometimes I like to make small projects like these:</p>
		<ul>
			<li><a href="https://nikitahl.github.io/css-base/">CSS Base</a> - An online tool to prototype and generate a base CSS theme</li>
			<li><a href="https://nikitahl.github.io/svg-2-code/">SVG to Code</a> - Online tool to convert SVG to code and vice versa</li>
			<li><a href="https://nikitahl.github.io/bg-image/">Background Image CSS</a> - Prototype, modify and edit a background image position, size, etc. and get a ready to use CSS code for your project</li>
		</ul>
		<p>In this blog I'll post my observations and share experience related to frontend web development.</p>
		<p>I do hope that this little blog of mine brings value, knowledge and help to developers out there. It is my contribution to the dev community around the world.</p>
		<p>Find me on:</p>
		{% include svg-icons.html %}
	</div>
</div>

