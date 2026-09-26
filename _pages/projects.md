---
layout: page
title: projects
permalink: /projects/
# description: A growing collection of your cool projects.
nav: true
nav_order: 1
display_categories:
  - work
  # - fun # Re-enable this category when you have projects to add.
horizontal: false
---

<style>
  /* Keep the navbar title, but hide the duplicate Projects heading on this page. */
  .post-header {
    display: none;
  }

  /* Show smaller project cards in four columns on tablet and desktop screens. */
  @media (min-width: 768px) {
    .projects .row > .col {
      flex: 0 0 25%;
      max-width: 25%;
    }
  }

  /* Reduce titles shown on project thumbnail cards. */
  .projects .card .card-title {
    font-size: 1.1rem;
    line-height: 1.2;
  }
</style>

<!-- pages/projects.md -->
<div class="projects">
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
