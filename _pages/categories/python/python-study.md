---
title: "📝Python 공부기록"
layout: archive
permalink: /python/study
author_profile: true
types: posts
---


{% assign posts = site.python['study'] %}
{% for post in posts %}
 {% include archive-single.html type=page.entries_layout %} 
{% endfor %}