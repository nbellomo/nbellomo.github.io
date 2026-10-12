---
layout: page
permalink: /publications/
title: Publications
description:
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<div class="profile-links">
  <a href="https://ui.adsabs.harvard.edu/search/q=author%3A%22Bellomo%2C%20Nicola%22&sort=date%20desc%2C%20bibcode%20desc&p_=0" target="_blank" rel="noopener">NASA ADS</a>
  <a href="https://inspirehep.net/authors/1626904" target="_blank" rel="noopener">INSPIRE-HEP</a>
  <a href="https://orcid.org/0000-0002-4375-705X" target="_blank" rel="noopener">ORCID</a>
</div>

<style>
  .profile-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.6rem;
    margin: 1rem 0 1.5rem;
  }
  .profile-links a {
    padding: 0.45rem 0.9rem;
    border: 1px solid var(--global-theme-color);
    border-radius: 0.4rem;
    color: var(--global-theme-color);
    text-decoration: none;
  }
  .profile-links a:hover {
    background: var(--global-theme-color);
    color: var(--global-bg-color);
  }
</style>

<!-- ## All Papers

The list below is fetched live from [INSPIRE-HEP](https://inspirehep.net/authors/1626904) every time this page loads, so it never needs to be updated by hand. -->

<div id="inspire-publications">
  <p id="inspire-status">Loading the publication list from INSPIRE-HEP…</p>
</div>

<style>
  .inspire-paper {
    margin-bottom: 1.1rem;
    padding-left: 3.2rem;
    position: relative;
  }
  .inspire-paper .inspire-year {
    position: absolute;
    left: 0;
    top: 0.1rem;
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--global-text-color-light, #828282);
  }
  .inspire-paper .inspire-title {
    font-weight: 500;
  }
  .inspire-paper .inspire-meta {
    font-size: 0.85rem;
    color: var(--global-text-color-light, #828282);
  }
</style>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    var AUTHOR_QUERY = "a N.Bellomo.1"; // INSPIRE author identifier of Nicola Bellomo
    var container = document.getElementById("inspire-publications");
    var status = document.getElementById("inspire-status");
    var url =
      "https://inspirehep.net/api/literature?sort=mostrecent&size=200&q=" +
      encodeURIComponent(AUTHOR_QUERY) +
      "&fields=titles,arxiv_eprints,publication_info,earliest_date,citation_count,authors.full_name,dois";

    fetch(url)
      .then(function (response) {
        if (!response.ok) throw new Error("INSPIRE responded with status " + response.status);
        return response.json();
      })
      .then(function (data) {
        var hits = (data.hits && data.hits.hits) || [];
        if (hits.length === 0) throw new Error("No records returned");
        status.remove();
        hits.forEach(function (hit) {
          var m = hit.metadata;
          var title = m.titles && m.titles[0] ? m.titles[0].title : "Untitled";
          var year = (m.earliest_date || "").slice(0, 4);
          var arxivId = m.arxiv_eprints && m.arxiv_eprints[0] ? m.arxiv_eprints[0].value : null;
          var doi = m.dois && m.dois[0] ? m.dois[0].value : null;
          var link = arxivId
            ? "https://arxiv.org/abs/" + arxivId
            : doi
              ? "https://doi.org/" + doi
              : "https://inspirehep.net/literature/" + hit.id;
          var journal = "";
          if (m.publication_info && m.publication_info[0] && m.publication_info[0].journal_title) {
            var info = m.publication_info[0];
            journal = info.journal_title + (info.journal_volume ? " " + info.journal_volume : "");
          } else if (arxivId) {
            journal = "arXiv:" + arxivId;
          }
          var authors = (m.authors || []).map(function (a) {
            return a.full_name;
          });
          var shownAuthors = authors.slice(0, 5).join("; ");
          if (authors.length > 5) shownAuthors += " et al.";
          shownAuthors = shownAuthors.replace(/Bellomo, Nicola/g, "<u>Bellomo, Nicola</u>");
          var citations = m.citation_count || 0;

          var entry = document.createElement("div");
          entry.className = "inspire-paper";
          entry.innerHTML =
            '<span class="inspire-year">' + year + "</span>" +
            '<div class="inspire-title"><a href="' + link + '" target="_blank" rel="noopener">' + title + "</a></div>" +
            '<div class="inspire-meta">' + shownAuthors + "</div>" +
            '<div class="inspire-meta">' + journal + (citations ? " · " + citations + " citations" : "") + "</div>";
          container.appendChild(entry);
        });
      })
      .catch(function (error) {
        status.innerHTML =
          "The live list could not be loaded right now. You can always find the complete, up-to-date list on " +
          '<a href="https://inspirehep.net/authors/1626904" target="_blank" rel="noopener">INSPIRE-HEP</a> or ' +
          '<a href="https://arxiv.org/a/bellomo_n_1" target="_blank" rel="noopener">arXiv</a>.';
      });
  });
</script>
