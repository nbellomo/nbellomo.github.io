---
layout: post
title: What Is The Gravitational-Wave Background?
date: 2026-06-20 10:00:00+0200
description: An Outreach Introduction To The Faint Hum Of The Universe # PROXY: example post, replace with real content
tags: outreach
categories: []
related_posts: false
thumbnail: assets/img/9.jpg
---

<!-- PROXY: this is an example post showing how to write outreach articles with images and equations. -->
<!-- To create a new post, copy this file, rename it as YYYY-MM-DD-your-title.md, and edit the text. -->

Imagine standing in the middle of a stadium during a match. You cannot make out any single conversation, but you clearly hear the crowd: a continuous, unmistakable hum. The gravitational-wave background is exactly that — the combined "sound" of countless black hole and neutron star mergers, too faint and too numerous to be heard one by one.

## Adding An Image

Adding a picture to a post takes one line. Put the image file in the `assets/img/` folder and include it like this:

{% include figure.liquid loading="eager" path="assets/img/9.jpg" title="An example image" class="img-fluid rounded z-depth-1" %}

<div class="caption">
    Captions like this one are added with a simple "caption" block. PROXY: replace with a real figure.
</div>

## Adding Equations

Equations work out of the box, written in standard LaTeX. Inline math like $$h_c \sim 10^{-25}$$ flows with the text, while displayed equations get their own line:

$$
\Omega_{\rm GW}(f) = \frac{1}{\rho_c} \frac{d\rho_{\rm GW}}{d\ln f}
$$

This quantity — the energy density of gravitational waves per logarithmic frequency interval — is the main character of the field: measuring how it depends on frequency $$f$$ and on the direction in the sky tells us where the hum comes from.

## Why It Matters

The background carries information no single merger can provide: it knows about _all_ the sources, including those far too distant to detect individually, and about the structure of the Universe the signal traveled through. Listening to the crowd, not just the loudest fans, is how we will learn the demographics of black holes across cosmic history.
