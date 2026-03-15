---
layout: page
permalink: /publications/
title: Publications
description:
sections:
  - bibquery: "@article"
    text: "Journal articles"
    id: "journals"  # Add this to match the navigation link
  - bibquery: "@inproceedings[note!=domestic && note!=intl_other]"
    text: "Conference and workshop papers"
    id: "conferences"  # Add this to match the navigation link
  - bibquery: "@inproceedings[note=intl_other]"
    text: "Other International Conferences"
    id: "intl_other"
  - bibquery: "@inproceedings[note=domestic]"
    text: "Domestic Conferences (国内会議)"
    id: "domestic"
  - bibquery: "@misc|@phdthesis|@mastersthesis"
    text: "Thesis"
    id: "preprints"  # Add this to match the navigation link
years: [2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014, 2013, 2012, 2011]
social: true
nav: true
nav_order: 4
dropdown: true
children:
  - title: All Publications
    permalink: /publications/
  - title: divider
  - title: Journals
    permalink: /publications/#journals
  - title: Conferences
    permalink: /publications/#conferences
  - title: Other International
    permalink: /publications/#intl_other
  - title: Domestic Conferences
    permalink: /publications/#domestic
  - title: Thesis
    permalink: /publications/#preprints
---
<p>
  For a complete and updated list of all publications, check out my profile on 
  <a href="https://scholar.google.co.jp/citations?user=DOiXntEAAAAJ&hl=en" target="_blank">Google Scholar</a>.
</p>
<!-- Horizontal navigation -->
<p>
  <a href="#journals">Journals</a> |
  <a href="#conferences">Conferences</a> |
  <a href="#intl_other">Other International</a> |
  <a href="#domestic">Domestic (国内会議)</a> |
  <a href="#preprints">Thesis</a>
</p>
<div class="publications">

{%- for section in page.sections %}
  <div id="{{section.id}}">
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
  </div>

{%- endfor %}

</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  ['journals', 'conferences', 'intl_other', 'domestic'].forEach(function (sectionId) {
    var section = document.getElementById(sectionId);
    if (!section) return;
    var items = section.querySelectorAll('ol.bibliography li');
    var total = items.length;
    items.forEach(function (li, index) {
      var titleDiv = li.querySelector('.title');
      if (titleDiv) {
        var numSpan = document.createElement('span');
        numSpan.className = 'pub-number';
        numSpan.textContent = (total - index) + '. ';
        titleDiv.insertBefore(numSpan, titleDiv.firstChild);
      }
    });
  });
});
</script>