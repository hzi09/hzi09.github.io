---
title: "BLOG"
layout: archive
permalink: /categories/blog
author_profile: true
types: posts
---


{% assign posts = site.categories.BLOG %}
{% for post in posts %}
 {% include archive-single.html type=page.entries_layout %} 
{% endfor %}