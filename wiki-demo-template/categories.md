---
layout: page
title: Categories
permalink: /categories/
---

<div class="categories-page">
{% assign wiki_by_category = site.wiki | group_by: "category" %}
{% for category_group in wiki_by_category %}
  <h2 id="{{ category_group.name | slugify }}">{{ category_group.name }}</h2>
  <ul class="category-article-list">
    {% assign sorted_pages = category_group.items | sort: "order" %}
    {% for wiki_page in sorted_pages %}
    <li>
      <a href="{{ site.baseurl }}{{ wiki_page.url }}">{{ wiki_page.title }}</a>
      {% if wiki_page.description %}
      <span class="article-meta-small">{{ wiki_page.description }}</span>
      {% endif %}
    </li>
    {% endfor %}
  </ul>
{% endfor %}
</div>
