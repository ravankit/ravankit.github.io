---
layout: page
permalink: /publications/
title: Publications
description: For complete list of papers I have published, checkout my  <a href="https://scholar.google.co.jp/citations?user=DOiXntEAAAAJ&hl=en" target="_blank">Google Scholar</a> page.
sections:
  - bibquery: "@article"
    text: "Journal articles"
    id: "journals"  # Add this to match the navigation link
  - bibquery: "@inproceedings"
    text: "Conference and workshop papers"
    id: "conferences"  # Add this to match the navigation link
  - bibquery: "@misc|@phdthesis|@mastersthesis"
    text: "Thesis"
    id: "preprints"  # Add this to match the navigation link
years: [2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014, 2013, 2012, 2011]
social: true
nav: true
nav_order: 4
---
<!-- Horizontal navigation -->
<p>
  <a href="#journals">Journals</a> |
  <a href="#conferences">Conferences/Proceedings</a> |
  <a href="#preprints">Thesis</a>
</p>
<div class="publications">

{%- for section in page.sections %}
  <a id="{{section.id}}"></a>
  <p class="bibtitle">{{section.text}}</p>
  {%- for y in page.years %}

    {%- comment -%}  Count bibliography in actual section and year {%- endcomment -%}
    {%- capture citecount -%}
    {%- bibliography_count -f {{site.scholar.bibliography}} -q {{section.bibquery}}[year={{y}}] -%}
    {%- endcapture -%}

    {%- comment -%} If exist bibliography in actual section and year, print {%- endcomment -%}
    {%- if citecount !="0" %}

      <h2 class="year">{{y}}</h2>
      {% bibliography -f {{site.scholar.bibliography}} -q {{section.bibquery}}[year={{y}}] %}

    {%- endif -%}

  {%- endfor %}

{%- endfor %}

</div>