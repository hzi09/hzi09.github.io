---
title: "Python 공부기록"
layout: archive
permalink: /categories/study
author_profile: true
types: posts
---


{% assign posts = site.categories['study'] %}
{% for post in posts %}
 {% include archive-single.html type=page.entries_layout %} 
{% endfor %}