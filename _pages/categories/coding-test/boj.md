---
title: "백준 코딩테스트"
layout: archive
permalink: /categories/boj
author_profile: true
types: posts
---


{% capture notice-2 %}
&nbsp;&nbsp;[![Solved.ac프로필](http://mazassumnida.wtf/api/mini/generate_badge?boj=hzi09)](https://solved.ac/hzi09)

&nbsp;&nbsp;✍️[Baekjoon Online Judge(백준)](https://www.acmicpc.net/) 사이트에서 코딩테스트를 진행하여 풀이법을 기록합니다.

{% endcapture %}

<div class="notice--info">{{ notice-2 | markdownify }}</div>


{% assign posts = site.categories['boj'] %}
{% for post in posts %}
 {% include archive-single.html type=page.entries_layout %} 
{% endfor %}