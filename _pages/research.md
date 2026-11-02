---
layout: page
title: Research
permalink: /research/
description: #What I Work On, And Why It Is Exciting
nav: true
nav_order: 1
horizontal: false
---

<!-- The ten-line research description. Edit the text below to update it. PROXY: review and personalize. -->

The core of my research sits at the crossroads of Gravitational Wave Astronomy and Cosmology. I became very interested in gravitational waves since they opened a genuinely new window into our Universe. In particular, I investigate how the anisotropic distribution of gravitational waves can provide a view of the structure of the Universe that is complementary to that of more traditional astrophysical objects, such as galaxies. In the near future, thanks to an accurate modeling of gravitational wave anisotropies, it will be possible to test not only the physics of compact objects but also how our Universe evolved from its first instants to the present day.

However, over the course of my career, I have worked on numerous topics, for instance dark matter, dark energy, and inflationary physics. All these topics still represent open questions in modern day Cosmology, and my research mainly aims to provide a way of testing the intrinsic nature of the Early and Late Universe. Below you can find the main topics I am currently working on; click on any card to read more.

<!-- Research highlight cards, generated from the files in the `_projects` folder. -->

<div class="projects">
  {% assign sorted_projects = site.projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
</div>
