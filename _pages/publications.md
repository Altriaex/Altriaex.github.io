---
layout: page
permalink: /publications/
title: Publications
description:
journal_years: [2022]
conference_years: [2022, 2018, 2017]
preprints_years: [2021]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">
<h2>Journal Papers</h2>
{%- for y in page.journal_years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @article[year={{y}}]%}
{% endfor %}</div>


<div class="publications">
<h2>Conference Papers</h2>
{%- for y in page.conference_years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @inproceedings[year={{y}}]%}
{% endfor %}

<div class="publications">
<h2>Preprints</h2>
{%- for y in page.preprints_years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @misc[year={{y}}]%}
{% endfor %}
</div>
