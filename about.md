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
		<h2>Hello, I'm Nikita! 👋</h2>
		<p>I'm a full time frontend developer at <a href="http://visualcomposer.com" target="_blank" rel="noreferrer noopener">Visual Composer</a> and <a href="https://indystack.com/" target="_blank" rel="noreferrer noopener">Indystack</a>.</p>
		<p>In this blog I'll share my experience related to frontend web development.</p>
		<p>Sometimes I like to make small tools like these:</p>
		<ul>
			<li><a href="https://nikitahl.github.io/css-base/">CSS Base</a> - An online tool to prototype and generate a base CSS theme</li>
			<li><a href="https://nikitahl.github.io/svg-2-code/">SVG to Code</a> - Online tool to convert SVG to code and vice versa</li>
			<li><a href="https://nikitahl.github.io/bg-image/">Background Image CSS</a> - Prototype, modify and edit a background image position, size, etc. and get a ready to use CSS code for your project</li>
			<li><a href="https://nikitahl.github.io/disavow-link-manager/">Disavow link manager</a> - Synchronize and manage disavow links for Google Search Console.</li>
		</ul>
		<h2>Credits</h2>
		<p>This site was created using:</p>
		<ul>
			<li>
				<a href="https://jekyllrb.com/" target="_blank" rel=" noopener">Jekyll</a> static site generator;
			</li>
			<li>
				<a href="https://github.com/aweekj/kiko-now/" target="_blank" rel=" noopener">kiko-now</a> theme by <a href="https://github.com/aweekj/" target="_blank" rel=" noopener">aweekj</a>;
			</li>
			<li>
				<a href="https://pages.github.com/" target="_blank" rel=" noopener">GitHub Pages</a> hosting.
			</li>
		</ul>
		<h2>Find me on</h2>
		{% include svg-icons.html %}
	</div>
</div>

