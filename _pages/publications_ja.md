---
layout: page
permalink: /ja/publications/
title: 論文
description:
lang: ja
ref: publications
sections:
  - bibquery: "@article"
    text: "学術雑誌"
    id: "journals"
  - bibquery: "@inproceedings"
    text: "国際会議・ワークショップ"
    id: "conferences"
years: [2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014, 2013, 2012, 2011]
social: true
nav: true
nav_order: 4
dropdown: true
children:
  - title: 論文一覧
    permalink: /ja/publications/
  - title: divider
  - title: 学術雑誌
    permalink: /ja/publications/#journals
  - title: 国際会議
    permalink: /ja/publications/#conferences
---
<div class="publications-intro">
  <p>
    学術雑誌論文および国際会議論文を掲載しています。
    最新かつ完全な一覧は
    <a href="https://scholar.google.co.jp/citations?user=DOiXntEAAAAJ&hl=ja" target="_blank">Google Scholar</a>
    をご覧ください。
  </p>
</div>

<nav class="pub-nav" aria-label="Publications sections">
  <a href="#journals">学術雑誌</a>
  <a href="#conferences">国際会議</a>
</nav>

<div class="publications">

{%- for section in page.sections %}
  <section id="{{section.id}}" class="publication-section">
  <p class="bibtitle">{{section.text}}</p>
  {%- for y in page.years %}

    {%- capture citecount -%}
    {%- bibliography_count -f {{site.scholar.bibliography}} -q {{section.bibquery}}[year={{y}}] -%}
    {%- endcapture -%}

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
