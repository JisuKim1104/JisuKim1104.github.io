---
layout: page
title: work
description: Research and interactive systems in accessibility, human–AI interaction, and XR.
permalink: /work/
nav: true
nav_order: 2
display_categories: [research, research-engineering, undergraduate]
horizontal: false
---

<div class="projects">
{% for category in page.display_categories %}
  {% if category == 'research' %}
    <h2 class="category">Research</h2>
  {% elsif category == 'research-engineering' %}
    <h2 class="category">Research Engineering</h2>
  {% elsif category == 'undergraduate' %}
    <h2 class="category">Undergraduate Projects</h2>
  {% endif %}
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
{% endfor %}
</div>
