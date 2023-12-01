---
layout: post
permalink: how-to-change-2fa-app-in-github
title: How to change 2FA authentication app (TOTP) in GitHub
date: 2023-12-01T12:40:02.112Z
description: I was a bit stuck and confused initially when I had to change the authenticator app on my phone and enable it on GitHub, luckily it was pretty easy.
tags: [tools, tips]
---

I was a bit stuck and confused initially when I had to change the authenticator app on my phone and enable it on GitHub, luckily it was pretty easy.

Recently I changed the 2FA app on my phone, so I had to also enable it in the GitHub settings.

At first, I thought there would be a separate option to change the authenticator app. And I was looking for such an option under **Two-factor authentication** in **Settings**, but couldn't find such.

Then I used the **Edit** option on the existing **Two-factor method** section under the **Password and authentication**.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/github-2fa-methods.webp" alt="GitHub settings 2fa methods">
  <figcaption>GitHub settings 2fa methods</figcaption>
</figure>

Which prompted me to authenticate with my existing app.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/github-authenticate-dialog.webp" alt="GitHub authenticate dialog">
  <figcaption>Authenticate dialog in GitHub </figcaption>
</figure>

After I authenticated, I was able to generate a new QR code, and this time used my new authenticator app.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/github-authenticate-app.webp" alt="GitHub authenticate new app">
  <figcaption>Authenticate new app in GitHub</figcaption>
</figure>

Now I can use a new app that I've installed on my phone to authenticate into GitHub.
