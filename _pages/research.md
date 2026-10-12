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

My research sits at the crossroads of gravitational-wave astronomy and cosmology. Gravitational waves opened a genuinely new window on the Universe: they let us count and characterize populations of compact objects, probe epochs and environments that are invisible to light, and test gravity in regimes far beyond the reach of laboratory experiments.

I am particularly interested in treating gravitational-wave observables the way cosmologists treat galaxies: as tracers of the underlying large-scale structure. The astrophysical gravitational-wave background — the superposition of countless unresolved mergers — carries anisotropies that encode both the astrophysics of its sources and the cosmology of the spacetime the signal travels through. Modeling these anisotropies accurately, and extracting them from data, is one of the central threads of my work.

The other main thread concerns primordial black holes: could some of the black holes we observe have formed in the early Universe, and could they make up part of the dark matter? Answering this question requires connecting early-Universe physics to present-day observables, from merger rates to the primordial curvature power spectrum.

Below are the main topics I currently work on. Click on any card to read more.

<!-- Research highlight cards, generated from the files in the `_projects` folder. -->

<div class="projects">
  {% assign sorted_projects = site.projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
</div>
