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
		<p>I'm a full time frontend developer at <a href="http://visualcomposer.com" target="_blank">Visual Composer</a>.</p>
		<p>Once I've started frontend development profession as a job but in a while it became my hobby.</p>
		<p>In this blog I'll post my observations and share experience related to frontend web development. Sometimes I write here as well <a href="https://visualcomposer.com/blog/author/nikitahlopov/" target="_blank">Visual Composer blog</a>.</p>
		<p>I do hope that this little blog of mine brings value and knowledge to developers out there.</p>
		<p>Find me on:</p>
		{% include svg-icons.html %}
	</div>
</div>

