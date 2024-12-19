---
title: "TIL"
layout: archive
permalink: /categories/til
author_profile: true
types: posts
---


{% assign posts = site.categories.TIL %}
{% for post in posts %}
 {% include archive-single2.html type=page.entries_layout %} 
{% endfor %}