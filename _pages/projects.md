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

<!-- Header row: filter tabs + PDF button -->
<div class="pf-projects-topbar">
  <div class="project-filter-tabs">
    <button class="filter-tab active" data-filter="all">전체</button>
    <button class="filter-tab" data-filter="실무">실무</button>
    <button class="filter-tab" data-filter="개인">개인</button>
  </div>
  <button class="pf-btn pf-btn--ghost pf-print-btn" onclick="window.print()" title="PDF로 저장">
    <i class="fa-solid fa-file-pdf" aria-hidden="true"></i> PDF 저장
  </button>
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

    {% assign col_class = "row-cols-1 row-cols-md-2" %}

    <div class="row {{ col_class }}" data-category="{{ category }}">
      {% for project in sorted_projects %}
        {% include projects.liquid %}
      {% endfor %}
    </div>
  {% endfor %}

{% else %}
  {% assign sorted_projects = site.projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-2">
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

  // Print: always show all categories regardless of active filter
  window.addEventListener('beforeprint', function () {
    document.querySelectorAll('[data-category]').forEach(function (g) {
      g.setAttribute('data-print-hidden', g.style.display === 'none' ? '1' : '0');
      g.style.display = '';
    });
    document.querySelectorAll('a[id]').forEach(function (a) {
      a.setAttribute('data-print-hidden', a.style.display === 'none' ? '1' : '0');
      a.style.display = '';
    });
  });

  window.addEventListener('afterprint', function () {
    document.querySelectorAll('[data-category]').forEach(function (g) {
      if (g.getAttribute('data-print-hidden') === '1') g.style.display = 'none';
    });
    document.querySelectorAll('a[id]').forEach(function (a) {
      if (a.getAttribute('data-print-hidden') === '1') a.style.display = 'none';
    });
  });
})();
</script>
