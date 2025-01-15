---
title:  "[TIL] 내일배움캠프 50일차_[Django] GET과 POST 요청 메서드" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Django


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## GET과 POST 요청 메서드
- 웹 개발에서 HTTP 요청 메서드는 클라이언트와 서버 간의 데이터를 주고받을 때 중요한 역할을 함
- 특히, 장고(Django)와 같은 웹 프레임워크에서 자주 사용되는 두 가지 요청 메서드가 바로 `GET`과 `POST`
- 이 두 메서드는 각각의 목적과 사용 방식에 차이가 있으며, 어떤 상황에서 어떤 메서드를 사용해야 할지 이해하는 것이 중요

### 1. GET 요청이란?
- `GET`은 웹에서 데이터를 가져오는 데 사용되는 HTTP 요청 메서드
- 주로 조회나 검색 작업을 할 때 사용되며, 요청 URL에 데이터를 포함하여 서버로 전달
- 브라우저에서 URL을 통해 요청을 보내면 서버는 해당 요청에 맞는 데이터를 응답으로 반환

<h4>특징</h4>

- 데이터 조회용으로 주로 사용됨
- 데이터는 쿼리스트링(query string)으로 URL에 포함되어 전송됨 
  - 예: http://example.com/search?query=django
- URL에 데이터가 노출되기 때문에 민감한 정보는 포함하지 않아야 함
- URL에 포함된 데이터는 길이가 제한적(서버나 브라우저에 따라 제한이 있을 수 있음)


<h4>장고에서 GET 요청 처리하기</h4>

- 장고에서는 `request.GET`을 사용하여 `GET` 요청으로 전달된 데이터를 처리할 수 있음
  - 예를 들어, 사용자가 검색어를 입력하면 그 값을 URL을 통해 받아올 수 있음
- 예시
    ```python
    from django.http import HttpResponse
    from django.shortcuts import render

    def search_view(request):
        query = request.GET.get('query', '')  # 'query' 파라미터 가져오기
        return HttpResponse(f'Search results for: {query}')
    ```
    - 위의 코드에서 `GET` 방식으로 전달된 query 파라미터를 가져와서 검색 결과를 보여주고 있음

<br>

### 2. POST 요청이란?
- `POST`는 서버로 데이터를 전송하는 데 사용되는 HTTP 요청 메서드
- 주로 폼 제출, 데이터 저장, 서버 변경 작업을 할 때 사용 
- `POST` 요청은 URL에 데이터를 포함시키지 않고, 요청 본문(body)에 데이터를 포함시켜 전송하기 때문에 더 안전하게 데이터를 전달할 수 있음

<h4>특징</h4>

- 데이터 제출 및 변경 용도로 사용
- 데이터는 요청 본문에 포함되어 서버로 전달
- 데이터 크기에 제한이 없으므로, 대용량 데이터를 전송할 수 있음
- 민감한 정보도 URL에 노출되지 않기 때문에 보안적으로 더 안전

<h4>장고에서 POST 요청 처리하기</h4>

- 장고에서는 `request.POST`를 사용하여 `POST` 요청으로 전달된 데이터를 처리할 수 있음 
  - 예를 들어, 사용자가 로그인 폼을 제출하면 그 값을 POST 방식으로 받아올 수 있음
- 예시
    ```python
    from django.http import HttpResponse
    from django.shortcuts import render

    def login_view(request):
        if request.method == 'POST':
            username = request.POST.get('username')
            password = request.POST.get('password')

            # 로그인 로직 처리
            return HttpResponse(f'Hello, {username}')
        
        return render(request, 'login_form.html')
    ```
    - 위의 코드에서 `POST` 방식으로 제출된 `username`과 `password`를 받아 로그인 처리를 진행


### 3. GET과 POST 요청의 차이점

- `GET`과 `POST` 요청은 각각 다르게 동작하며, 사용하는 목적에 따라 선택해야 함 
- 주요 차이점은 다음과 같음

    | **특징**             | **GET**                         | **POST**                        |
    |----------------------|---------------------------------|---------------------------------|
    | **목적**             | 데이터 조회                     | 데이터 제출 및 변경             |
    | **데이터 전송 위치** | URL의 쿼리스트링에 포함         | 요청 본문에 포함                |
    | **데이터 양**        | 전송할 수 있는 데이터 양 제한   | 데이터 양에 제한 없음           |
    | **보안**             | 민감한 정보 전송에 부적합       | 보안성이 높음                   |
    | **사용 예시**        | 검색, 필터링, 페이지 조회       | 회원가입, 로그인, 폼 제출       |

<h4>GET 요청 예시: 검색 기능</h4>

- 검색 페이지에서 사용자가 입력한 검색어를 GET 방식으로 서버에 전송하여 결과를 반환하는 예시
- 서버에서는 `GET` 방식으로 전달된 query 파라미터를 읽어 검색 결과를 처리

<div style="margin-left: 2em;">
{% highlight html %}
{% raw %}

<form method="get" action="/search/">
    <input type="text" name="query" placeholder="검색어 입력">
    <button type="submit">검색</button>
</form>


{% endraw %}
{% endhighlight %}
</div>


<h4>POST 요청 예시: 로그인 폼</h4>

- 로그인 페이지에서 사용자가 아이디와 비밀번호를 `POST` 방식으로 서버에 전송하는 예시
- 서버에서는 `POST` 방식으로 제출된 데이터를 읽어 사용자 인증을 진행

<div style="margin-left: 2em;">
{% highlight html %}
{% raw %}

<form method="post" action="/login/">
    {% csrf_token %}
    <input type="text" name="username" placeholder="아이디">
    <input type="password" name="password" placeholder="비밀번호">
    <button type="submit">로그인</button>
</form>


{% endraw %}
{% endhighlight %}
</div>

<br>

### 4. GET과 POST 선택 요령
- `GET`은 데이터를 조회하거나, URL에 포함된 데이터를 기반으로 결과를 반환할 때 사용 
  - 예를 들어, 검색, 필터링, 페이지네이션 등의 작업에 적합
- `POST`는 데이터를 제출하거나, 서버에서 데이터를 변경하는 작업에 사용 
  - 예를 들어, 로그인, 회원가입, 폼 제출, 데이터 저장 등에서는 POST를 사용



# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 171-180
- [x]  SQL 코드카타 70
- [x]  백준 코딩테스트 1문제
- [x]  장고 메인과제
- [x]  TIL 작성

## 회고
&nbsp; 과제하면서 잘 안되는 부분이 있어서 튜터님한테 물으러 갔다가.. 나의 부족함을 또 깨달아버린.. 코드는 문제가 없었지만, 내가 GET과 POST에 대한 지식이 부족했다. 코드에 대한 이해도도 부족하고 그냥 외워서 작성을 하고있었던 것.. 그래서 GET과 POST에 대해 공부했다ㅠㅠ 매일매일 공부해도 매일매일 모르는게 생기다니..