---
title: "Publications"
permalink: /publications/
layout: single
classes: wide
author_profile: false
toc: true
toc_sticky: true
toc_label: "Contents"
read_time: false
share: false
---

[Google Scholar](https://scholar.google.com/citations?user=3RqGjxwAAAAJ&hl=en) carries the most current list and citation counts.

## Journal articles

{% assign journals = site.data.publications | where: "type", "journal" %}
{% include pub-list.html entries=journals %}

## Conference papers

{% assign conferences = site.data.publications | where: "type", "conference" %}
{% include pub-list.html entries=conferences %}

## Preprints and technical reports

{% assign reports = site.data.publications | where: "type", "report" %}
{% include pub-list.html entries=reports %}

## Talks

### Conference presentations

- **Graph-based domain decomposition for scalable cardiovascular flow super-resolution**<br>
  <span class="talks__venue">APS Division of Fluid Dynamics Meeting, Houston, TX — November 2025</span>
- **Adaptive local domain decomposition for learning large-scale multi-physics numerical simulations**<br>
  <span class="talks__venue">APS Division of Fluid Dynamics Meeting, Salt Lake City, UT — November 2024</span>
- **Taylor series error correction network for super-resolution of discretized fluid solutions**<br>
  <span class="talks__venue">APS Division of Fluid Dynamics Meeting, Washington, DC — November 2023</span>
- **MegaFlow2D: a parametric dataset for machine learning super-resolution in CFD simulations**<br>
  <span class="talks__venue">CPS-IoT Week, San Antonio, TX — May 2023</span>
{: .talks}

### Invited talks

- **Machine learning for large-scale multi-physics engineering simulations**<br>
  <span class="talks__venue">CMU Mechanical Engineering Ph.D. Research Symposium — March 2025</span>
- **Machine learning in large-scale engineering simulations**<br>
  <span class="talks__venue">Autodesk Research, San Francisco, CA — November 2024</span>
{: .talks}
