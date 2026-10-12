---
layout: about
title: About
permalink: /
subtitle: Gravitational-Wave Cosmologist · <a href='https://www.unipd.it/en/' target='_blank'>University Of Padova</a> · INFN Padova

profile:
  align: right
  image: picture_Nicola_2.jpg
  image_circular: false # crops the image to make it circular
  more_info: >

    <p style="text-align: center; margin-top: 0.5rem;">
      <button id="cat-easter-egg" type="button" title="Meow?" aria-label="A curious cat button"
        style="background: none; border: none; cursor: pointer; font-size: 1.4rem; padding: 0; line-height: 1;">🐈</button>
    </p>

selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page

announcements:
  enabled: false # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

<!-- The normal biography. To edit it, change the text inside the div below. -->

<div id="bio-human" markdown="1">
I am a cosmologist working at the interface between gravitational-wave astronomy and the large-scale structure of the Universe. My research focuses on what gravitational waves can teach us about the cosmos as a whole: the anisotropies of the astrophysical gravitational-wave background, primordial black holes as a dark matter candidate, and the cross-correlation of gravitational-wave sources with galaxy surveys.

<!-- PROXY: review and personalize this biography. -->

I am currently a researcher at the University of Padova and INFN, where I develop theoretical models and numerical tools — such as [CLASS_GWB](https://arxiv.org/abs/2110.15059) — that connect gravitational-wave observations with the standard toolkit of modern cosmology. I am also involved in forecasting the science reach of upcoming facilities, from pulsar timing arrays to the SKA Observatory and next-generation interferometers.

Before moving to Padova I was a postdoctoral fellow at the University of Texas at Austin, and I obtained my PhD at the Institute of Cosmos Sciences of the University of Barcelona.

</div>

<!-- The cat biography, revealed by the easter egg. Edit freely — it is supposed to be silly. -->

<div id="bio-cat" markdown="1" style="display: none;">
I am Ginza, Principal Investigator of this household and, frankly, of this website. My research focuses on the large-scale structure of the living room, the anisotropies of the afternoon sunbeam background, and the mysterious dark matter that is definitely hiding behind the refrigerator.

My main observational campaigns are carried out from the windowsill, where I monitor gravitationally bound systems of pigeons with unmatched angular resolution. My most cited work, _On The Optimal Occupation Of Freshly Printed Papers_, has been reproduced independently on every desk of the department.

The human who claims to run this page is, at best, a useful collaborator: he operates the can opener. All remaining errors on this website are entirely his.

</div>


<!-- Cat easter egg: clicking the cat button swaps the profile picture and the biography. -->

<script>
  document.addEventListener("DOMContentLoaded", function () {
    var button = document.getElementById("cat-easter-egg");
    var catMode = false;
    var savedPicture = null;
    var savedHeading = null;
    var savedDocumentTitle = document.title;

    function setCatMode(nextCatMode) {
      catMode = nextCatMode;
      var bioHuman = document.getElementById("bio-human");
      var bioCat = document.getElementById("bio-cat");
      if (bioHuman && bioCat) {
        bioHuman.style.display = catMode ? "none" : "";
        bioCat.style.display = catMode ? "" : "none";
      }
      var heading = document.querySelector(".post-title");
      if (heading) {
        if (catMode) {
          if (savedHeading === null) savedHeading = heading.innerHTML;
          heading.textContent = "Ginza";
        } else if (savedHeading !== null) {
          heading.innerHTML = savedHeading;
          savedHeading = null;
        }
      }
      document.title = catMode ? "Ginza" : savedDocumentTitle;
      var img = document.querySelector(".profile img");
      if (img) {
        var picture = img.closest("picture");
        if (catMode) {
          if (picture && savedPicture === null) {
            savedPicture = picture.innerHTML;
            picture.innerHTML = '<img src="{{ 'assets/img/ginzona.jpg' | relative_url }}" alt="Ginza the cat" class="' + img.className + '" width="100%">';
          } else if (!picture) {
            img.dataset.humanSrc = img.src;
            img.src = "{{ 'assets/img/ginzona.jpg' | relative_url }}";
          }
        } else {
          if (picture && savedPicture !== null) {
            picture.innerHTML = savedPicture;
            savedPicture = null;
          } else if (!picture && img.dataset.humanSrc) {
            img.src = img.dataset.humanSrc;
          }
        }
      }
      if (button) {
        button.textContent = catMode ? "🧑‍🔬" : "🐈";
        button.title = catMode ? "Bring the human back" : "Meow?";
      }
    }

    window.toggleGinzaMode = function () {
      setCatMode(!catMode);
    };

    if (button) {
      button.addEventListener("click", window.toggleGinzaMode);
    }

    var startInCatMode = window.location.hash === "#ginza";
    try {
      startInCatMode = startInCatMode || window.sessionStorage.getItem("ginzaMode") === "1";
      window.sessionStorage.removeItem("ginzaMode");
    } catch (error) {
      // Ignore private browsing or storage restrictions.
    }
    if (startInCatMode) {
      setCatMode(true);
    }
  });
</script>
