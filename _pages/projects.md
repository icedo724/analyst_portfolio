---
layout: page
title: projects
permalink: /projects/
description: 실무·개인 프로젝트 모음
nav: true
nav_order: 2
display_categories: [실무, 개인]
horizontal: false
---

<div class="projects">

<!-- Filter tabs -->
<div class="project-filter-tabs mb-4">
  <button class="filter-tab active" data-filter="all">전체</button>
  <button class="filter-tab" data-filter="실무">실무</button>
  <button class="filter-tab" data-filter="개인">개인</button>
</div>

{% if site.enable_project_categories and page.display_categories %}
  {% for category in page.display_categories %}
    {% assign categorized_projects = site.projects | where: "category", category %}
    {% assign sorted_projects = categorized_projects | sort: "importance" %}
    {% assign proj_count = sorted_projects | size %}
    {% if proj_count == 0 %}{% continue %}{% endif %}

    <a id="{{ category }}" href=".#{{ category }}">
      <h2 class="category">{{ category }}</h2>
    </a>

    {% if proj_count <= 2 %}
      {% assign col_class = "row-cols-1 row-cols-md-2" %}
    {% else %}
      {% assign col_class = "row-cols-1 row-cols-md-3" %}
    {% endif %}

    <div class="row {{ col_class }}" data-category="{{ category }}">
      {% for project in sorted_projects %}
        {% include projects.liquid %}
      {% endfor %}
    </div>
  {% endfor %}

{% else %}
  {% assign sorted_projects = site.projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
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
      var categoryGroups = document.querySelectorAll('[data-category]');
      var categoryAnchors = document.querySelectorAll('a[id]');
      if (filter === 'all') {
        categoryGroups.forEach(function (g) { g.style.display = ''; });
        categoryAnchors.forEach(function (a) { a.style.display = ''; });
      } else {
        categoryGroups.forEach(function (g) {
          g.style.display = g.dataset.category === filter ? '' : 'none';
        });
        categoryAnchors.forEach(function (a) {
          a.style.display = a.id === filter ? '' : 'none';
        });
      }
    });
  });
})();
</script>
