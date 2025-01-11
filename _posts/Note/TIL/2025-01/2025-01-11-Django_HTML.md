---
title:  "[TIL] 내일배움캠프 46일차_[HTML] HTML 기초 문법 정리" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - HTML


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 1. HTML
- HTML은 웹페이지의 구조를 정의하는 마크업 언어
- 모든 HTML 문서는 태그(tag)를 사용하여 콘텐츠를 구조화
- 태그는 보통 `<`와 `>`로 감싸여 있으며, 열고 닫는 형태로 사용됨

<br>

### HTML 문서의 기본 구조
- HTML 문서는 아래와 같은 기본 구조를 가짐
    ```html
    <!DOCTYPE html> <!-- HTML5 문서임을 선언 -->
    <html lang="ko"> <!-- 언어 설정 -->
    <head>
        <meta charset="UTF-8"> <!-- 문서의 문자 인코딩 설정 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- 반응형 웹 설정 -->
        <title>문서 제목</title> <!-- 브라우저 탭에 표시될 제목 -->
    </head>
    <body>
        <!-- 본문 내용 -->
        <h1>HTML 기초 문법</h1>
        <p>HTML은 HyperText Markup Language의 약자입니다.</p>
    </body>
    </html>   
    ```

<br>

## 2. 주요 태그

### 제목 태그
- 제목을 표시할 때 사용
- `<h1>`은 가장 큰 제목, `<h6>`은 가장 작은 제목
    ```html
    <h1>제목 1</h1>
    <h2>제목 2</h2>
    <h3>제목 3</h3>
    ```

<h1>제목 1</h1>
<h2>제목 2</h2>
<h3>제목 3</h3>
<hr>

### 문단 태그
- 문단을 작성할 때 사용
    ```html
    <p>이것은 문단입니다.</p>
    <p>HTML은 간단한 마크업 언어입니다.</p>
    ```

<p>이것은 문단입니다.</p>
<p>HTML은 간단한 마크업 언어입니다.</p>   
<hr> 

### 리스트 태그
- 순서 없는 리스트 : `<ul>`과 `<li>`사용
    ```html
    <ul>
        <li>사과</li>
        <li>바나나</li>
        <li>체리</li>
    </ul>
    ```


<ul>
    <li>사과</li>
    <li>바나나</li>
    <li>체리</li>
</ul>
<hr> 

- 순서 있는 리스트 : `<ol>`과 `<li>` 사용
    ```html
    <ol>
        <li>첫 번째</li>
        <li>두 번째</li>
        <li>세 번째</li>
    </ol>
    ```


<ol>
    <li>첫 번째</li>
    <li>두 번째</li>
    <li>세 번째</li>
</ol>
<hr> 


### 링크 태그
- 링크를 생성할 때 `<a>` 태그를 사용
  - `href`: 링크 주소
  - `target="_blank"`: 새 탭에서 열기
```html
<a href="https://www.google.com" target="_blank">구글로 이동</a>
```

<a href="https://www.google.com" target="_blank">구글로 이동</a>

<hr>


### 이미지 태그
- 이미지를 삽입할 때 <img> 태그를 사용
  - src: 이미지 경로
  - alt: 이미지가 로드되지 않을 때 표시할 텍스트
  - width/height: 이미지 크기 조절
```html
<img src="image.jpg" alt="이미지 설명" width="300">
```

<hr>


### 강조 태그
- 텍스트를 강조하거나 스타일을 추가할 때 사용

```html
<strong>굵게 표시</strong>
<em>기울임 표시</em>
<u>밑줄 표시</u>
```

<strong>굵게 표시</strong>
<em>기울임 표시</em>
<u>밑줄 표시</u>
<hr>

<br>

## 3. HTML 속성 (Attributes)
- HTML 태그에는 속성을 추가하여 태그의 동작이나 스타일을 정의할 수 있음
- 속성은 `속성이름="값"` 형식으로 작성
```html
<a href="https://www.example.com" target="_blank">링크</a>
<img src="logo.png" alt="로고 이미지">
```

<br>

## 4. 주석
- HTML에서 주석은 `<!--`와 `-->` 사이에 작성
- 브라우저에 표시되지 않음
```html
<!-- 이 부분은 주석입니다 -->
```

<br>

## 5. 폼 태그
- 사용자로부터 데이터를 입력받을 때 사용
  - action: 데이터를 보낼 URL
  - method: 데이터 전송 방식 (GET 또는 POST)

```html
<form action="/submit" method="post">
    <label for="name">이름:</label>
    <input type="text" id="name" name="name">
    <button type="submit">제출</button>
</form>
```

<br>

## 6. 표(Table) 태그
- 데이터를 표로 정리할 때 사용
  - `<table>`: 표 생성
  - `<tr>`: 행(Row)
  - `<th>`: 제목 셀
  - `<td>`: 데이터 셀

```html
<table border="1">
    <tr>
        <th>이름</th>
        <th>나이</th>
        <th>직업</th>
    </tr>
    <tr>
        <td>홍길동</td>
        <td>25</td>
        <td>개발자</td>
    </tr>
</table>
```

<table border="1">
    <tr>
        <th>이름</th>
        <th>나이</th>
        <th>직업</th>
    </tr>
    <tr>
        <td>홍길동</td>
        <td>25</td>
        <td>개발자</td>
    </tr>
</table>

<hr>
<br>

## 7. HTML5 추가 요소

- 시맨틱 태그: 문서 구조를 명확히 함
  - `<header>`: 머리말
  - `<nav>`: 내비게이션
  - `<section>`: 섹션
  - `<article>`: 독립적인 콘텐츠
  - `<footer>`: 바닥글
- 미디어 태그:
  - `<audio>`: 오디오 삽입
  - `<video>`: 비디오 삽입

<br>

더 필요한 내용은 [HTML 공식 문서](https://developer.mozilla.org/ko/docs/Web/HTML) 참고!

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 121-130
- [x]  SQL 코드카타 64
- [x]  백준 코딩테스트 1문제
- [x]  TIL 작성

## 회고
&nbsp; 장고를 하면서 HTML 문법을 잘 모르겠어서 정리! 두고두고 보면서 웹페이지 잘 만들어봐야지!