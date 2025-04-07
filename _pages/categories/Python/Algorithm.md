---
title: "알고리즘"
layout: archive
permalink: /categories/python_algorithm
author_profile: true
types: posts
---

✍️ [이것이 취업을 위한 코딩 테스트다 with 파이썬](https://www.hanbit.co.kr/store/books/look.php?p_code=B8945183661)에서 스터디한 내용을 기록합니다.
{: .notice--info}

{% assign posts = site.categories.Python_Algorithm %}
{% for post in posts %}
 {% include archive-single.html type=page.entries_layout %} 
{% endfor %}