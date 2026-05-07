---
layout: page
title: projects
permalink: /projects/
description: 실무·개인 프로젝트 모음
nav: true
nav_order: 2
display_categories: [실무, 일반, 게임]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">

<!-- Filter tabs -->
<div class="project-filter-tabs mb-4">
  <button class="filter-tab active" data-filter="all">전체</button>
  <button class="filter-tab" data-filter="실무">실무</button>
  <button class="filter-tab" data-filter="일반">일반</button>
  <button class="filter-tab" data-filter="게임">게임</button>
</div>

{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2" data-category="{{ category }}">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3" data-category="{{ category }}">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>

<script>
(function () {
  var tabs = document.querySelectorAll('.filter-tab');
  tabs.forEach(function (tab) {
    tab.addEventListener('click', function () {
      tabs.forEach(function (t) { t.classList.remove('active'); });
      tab.classList.add('active');
      var filter = tab.dataset.filter;
      var categories = document.querySelectorAll('[data-category]');
      var categoryHeadings = document.querySelectorAll('h2.category');
      if (filter === 'all') {
        categories.forEach(function (c) { c.closest('.container, .row').style.display = ''; });
        categoryHeadings.forEach(function (h) { h.parentElement.style.display = ''; });
      } else {
        categories.forEach(function (c) {
          var show = c.dataset.category === filter;
          c.style.display = show ? '' : 'none';
        });
        categoryHeadings.forEach(function (h) {
          var anchor = h.parentElement;
          var id = anchor.id;
          anchor.style.display = id === filter ? '' : 'none';
        });
      }
    });
  });
})();
</script>
