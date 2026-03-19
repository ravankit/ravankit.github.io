---
layout: page
permalink: /publications/
title: Publications
description:
sections:
  - bibquery: "@article"
    text: "Journal articles"
    id: "journals"
  - bibquery: "@inproceedings"
    text: "Conference and workshop papers"
    id: "conferences"
  - bibquery: "@misc|@phdthesis|@mastersthesis"
    text: "Thesis"
    id: "thesis"
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
  - title: Thesis
    permalink: /publications/#thesis
---
<div class="publications-intro">
  <p>
    A curated archive of journal articles, conference papers, and thesis work.
    For a complete and updated list, visit
    <a href="https://scholar.google.co.jp/citations?user=DOiXntEAAAAJ&hl=en" target="_blank">Google Scholar</a>.
  </p>
</div>

<nav class="pub-nav" aria-label="Publications sections">
  <a href="#journals">Journals</a>
  <a href="#conferences">Conferences</a>
  <a href="#thesis">Thesis</a>
</nav>

<div class="publications">

{%- for section in page.sections %}
  <section id="{{section.id}}" class="publication-section">
  <p class="bibtitle">{{section.text}}</p>
  {%- for y in page.years %}

    {%- comment -%}  Count bibliography in actual section and year {%- endcomment -%}
    {%- capture citecount -%}
    {%- bibliography_count -f {{site.scholar.bibliography}} -q {{section.bibquery}}[year={{y}}] -%}
    {%- endcapture -%}

    {%- comment -%} If exist bibliography in actual section and year, print {%- endcomment -%}
    {%- if citecount !="0" %}

      <h2 class="year">{{y}}</h2>
      {% bibliography --group_by none -f {{site.scholar.bibliography}} -q {{section.bibquery}}[year={{y}}] %}

    {%- endif -%}

  {%- endfor %}
  </section>

{%- endfor %}

</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  ['journals', 'conferences'].forEach(function (sectionId) {
    var section = document.getElementById(sectionId);
    if (!section) return;

    var items = section.querySelectorAll('ol.bibliography > li');
    items.forEach(function (li, index) {
      var titleDiv = li.querySelector('.title');
      if (!titleDiv || titleDiv.querySelector('.pub-number')) return;

      var numSpan = document.createElement('span');
      numSpan.className = 'pub-number';
      numSpan.textContent = (index + 1) + '. ';
      titleDiv.insertBefore(numSpan, titleDiv.firstChild);
    });
  });
});
</script>
