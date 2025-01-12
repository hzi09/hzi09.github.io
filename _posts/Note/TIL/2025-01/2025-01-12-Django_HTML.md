---
title:  "[TIL] 내일배움캠프 47일차_[Django] Django에서 사용되는 HTML 문법" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프


toc: true
toc_sticky: true
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

- Django는 강력한 템플릿 엔진을 제공하여 서버에서 데이터를 처리하고 HTML 파일로 전달하는 기능을 지원
- Django 템플릿에서 자주 사용하는 HTML 문법과 관련 태그를 정리
- 추가적인 문법은 [Django 공식 문서](https://docs.djangoproject.com/en/stable/topics/templates/) 참고!


## 1. 변수 출력
- Django 템플릿에서 데이터를 HTML에 삽입하려면 `{{ }}` 문법을 사용

    ```html
    <p>{{ 변수이름 }}</p>
    ```

- 예시

    ```html
    <p>{{ username }}</p> <!-- username 변수의 값 출력 -->
    ```

<br>

## 2. 조건문
- 조건문은 `{% if %}`와 `{% endif %}` 사이에 작성

    ```html
    {% if True %}
        <p>조건이 참일 때 출력됩니다.</p>
    {% else %}
        <p>조건이 거짓일 때 출력됩니다.</p>
    {% endif %}
    ```

- 예시
    
    ```html
    {% if is_authenticated %}
        <p>환영합니다, {{ username }}님!</p>
    {% else %}
        <p>로그인이 필요합니다.</p>
    {% endif %}
    ```

<br>

## 3. 반복문

- 반복문은 `{% for %}`와 `{% endfor %}`로 작성

    ```html
    {% for item in 리스트 %}
        <p>{{ item }}</p>
    {% endfor %}
    ```

- 예시

    ```html
    <ul>
        {% for product in products %}
            <li>{{ product.name }} - {{ product.price }}</li>
        {% endfor %}
    </ul>
    ```

<br>

## 4. 필터 사용
- Django 템플릿에서는 변수를 출력할 때 필터를 사용할 수 있음
- 필터는 `|`를 사용해 적용

    ```html
    {{ 변수|필터이름 }}
    ```

- 예시

    ```html
    <p>{{ name|upper }}</p> <!-- 대문자로 출력 -->
    <p>{{ date|date:"Y-m-d" }}</p> <!-- 날짜 형식 지정 -->
    ```

- 주요 필터
  - upper: 문자열을 대문자로 변환
  - lower: 문자열을 소문자로 변환
  - date: 날짜 형식 지정
  - length: 리스트 또는 문자열의 길이 반환

<br>

## 5. 주석
- Django 템플릿에서 주석은 `{# #}`를 사용
- 브라우저에 표시되지 않음

    ```html
    {# 이 부분은 주석입니다. #}
    ```

<br>

## 6. include 태그
- HTML 파일을 분리하여 재사용할 때 include 태그를 사용

    ```html
    {% include "파일경로.html" %}
    ```

- 예시

    ```html
    {% include "partials/header.html" %}
    ```

<br>

## 7. url 태그
- Django URL의 이름을 사용해 링크를 생성할 때 `url` 태그를 사용

    ```html
    <a href="{% url 'url_name' %}">링크</a>
    ```

- 예시

    ```html
    <a href="{% url 'home' %}">홈으로 이동</a>
    <a href="{% url 'article_detail' article.id %}">자세히 보기</a>
    ```

<br>

## 8. 정적 파일 사용
- CSS, JavaScript, 이미지 등 정적 파일을 사용할 때 `{% static %}` 태그를 사용

    ```html
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
    <img src="{% static 'images/logo.png' %}" alt="로고">
    ```

- 정적 파일을 사용하려면 템플릿 상단에 `{% load static %}`를 추가해야 함

    ```html
    {% load static %}
    ```

<br>

## 9. csrf_token
- Django에서 폼을 제출할 때 보안을 위해 CSRF 토큰을 추가해야 함

    ```html
    <form method="post">
        {% csrf_token %}
        <input type="text" name="name">
        <button type="submit">제출</button>
    </form>
    ```

## 10. 커스텀 태그와 필터
- Django는 기본 제공 기능 외에도 커스텀 태그와 필터를 작성할 수 있음
- 커스텀 태그를 사용하려면 템플릿에서 로드해야 함

    ```html
    {% load custom_tags %}
    ```

- 예시

    ```html
    <p>{{ text|custom_filter }}</p>
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] Django 기초 강의 완강
- [x] Django 심화 강의 2강까지
- [x] 알고리즘 코드카타 131-140
- [x] SQL 코드카타 67, 68, 77, 78
- [x] LeetHub 연동하고 테스트
- [x] 백준 코딩테스트 1문제
- [x] TIL 작성

## 회고
&nbsp; 오늘은 장고 기초 강의를 드디어 끝냈다. 스탠다드반 과제도 하려고 했는데, LeetHub 연동에 애를 먹어서 시간이 지체되어버렸다. 내일 과제발제 끝나면 호록 끝내야지. 심화강의도 이번주까지 다 듣는 걸 목표로 해야겠다. 과제를 해야하는데 강의를 다 못들어서 어쩌나 싶기도 하구..🥹
