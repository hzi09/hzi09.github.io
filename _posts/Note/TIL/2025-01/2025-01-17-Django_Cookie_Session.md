---
title:  "[TIL] 내일배움캠프 00일차_[Django] 쿠키(Cookie)와 세션(Session)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## HTTP의 특징

- HTTP는 상태를 유지하지 않는(stateless) 프로토콜
- 따라서, 사용자가 로그인 시 입력한 아이디와 비밀번호 정보는 HTTP 통신 중 POST 방식으로 서버에 전달되지만, 이 정보는 저장되지 않음
- 이를 해결하기 위해 로그인 유지 기능이 필요하며, 이를 구현하는 방법으로 **쿠키(Cookie)**와 **세션(Session)**을 사용

<br>

## 🍪쿠키(Cookie)
### 쿠키란?
- 쿠키는 클라이언트(웹 브라우저) 로컬에 저장되는 키-값 쌍으로 이루어진 작은 데이터 파일
- 이를 통해 서버와 클라이언트 간 상태 정보를 유지할 수 있음

### 쿠키의 특징
- 만료 시점
   - 쿠키에는 유효기간을 설정할 수 있음
   - 브라우저가 종료되더라도 유효기간이 남아 있으면 쿠키는 유지

- 구성 요소
   - **이름**: 각 쿠키를 식별하는 고유 이름
   - **값**: 쿠키와 관련된 데이터
   - **유효시간**: 쿠키의 유지 시간
   - **도메인**: 쿠키를 전송할 도메인
   - **경로**: 쿠키를 전송할 경로

- 용량 제한
   - 하나의 쿠키는 최대 4KB
   - 한 도메인당 최대 20개
   - 전체 브라우저에서 최대 300개

- 동작 방식
   1. 클라이언트가 페이지 요청
   2. 서버가 쿠키 생성
   3. HTTP 응답 헤더에 쿠키 포함
   4. 브라우저가 쿠키를 저장
   5. 같은 요청 시 HTTP 헤더에 쿠키 포함
   6. 서버는 쿠키를 읽어 상태를 업데이트

### 쿠기의 활용 예시
- 로그인 시 "아이디와 비밀번호 저장" 여부
- 로그인하지 않은 상태에서 장바구니에 담긴 품목 유지

<br>

## 세션(Session)
### 세션이란?
- 세션은 일정 시간 동안 같은 사용자로부터 들어오는 일련의 요청을 하나의 상태로 보고, 그 상태를 유지하는 기술
- 서버에서 정보를 관리하며, 클라이언트를 식별하기 위해 세션 ID를 사용

### 세션의 특징
- 만료 시점
   - 브라우저가 종료되거나 세션 유효시간이 끝날 때

- 장단점
   - 장점 : 클라이언트 정보가 서버에 저장되어 보안에 강함
   - 단점 : 사용자가 많아지면 서버 메모리 사용량이 증가하여 성능 저하 발생 가능

- 동작 방식
  1. 클라이언트가 서버에 접속 시 세션 ID 발급
  2. 클라이언트는 세션 ID를 쿠키에 저장
  3. 이후 요청 시 세션 ID를 서버로 전달

<br>

## 쿠키와 세션의 비교

| **항목**       | **쿠키**                  | **세션**                   |
|:--------------:|:-------------------------:|:--------------------------:|
| **저장 위치**  | 클라이언트                | 서버                       |
| **보안**       | 상대적으로 낮음           | 상대적으로 높음            |
| **속도**       | 빠름                      | 느림                       |
| **유효 시간**  | 설정된 만료 시간까지 유지 | 브라우저 종료 시 삭제 가능 |


<br>


## 활용 : 로그인 유지 기능 구현
### 쿠키 생성
- `set_cookie(name, value, max_age=None)`
- 인수
  - `name`: 쿠키 이름(필수)
  - `value`: 저장할 값(필수)
  - `max_age`: 쿠키 유효시간(초, 선택)

### 쿠키 읽기
- `request.COOKIES[name]`
- 쿠키는 딕셔너리와 비슷한 속성을 가지며, 쿠키 데이터를 문자열로 반환

### Django 예제 코드

<h4>로그인</h4>

```python
def login(request):
    # 이미 로그인 쿠키가 있는 경우 처리
    if request.COOKIES.get('username') is not None:
        username = request.COOKIES.get('username')  # 쿠키에서 저장된 사용자 이름을 가져옴
        password = request.COOKIES.get('password')  # 쿠키에서 저장된 비밀번호를 가져옴
        # 사용자 인증
        user = auth.authenticate(request, username=username, password=password)
        if user is not None:  # 인증 성공 시
            auth.login(request, user)  # 사용자 세션 생성 및 로그인
            return redirect("account:home")  # 홈 페이지로 리다이렉트

    # POST 요청 처리: 로그인 폼 제출 시
    elif request.method == 'POST':
        username = request.POST['username']  # 입력받은 사용자 이름
        password = request.POST['password']  # 입력받은 비밀번호
        # 사용자 인증
        user = auth.authenticate(request, username=username, password=password)
        if user is not None:  # 인증 성공 시
            auth.login(request, user)  # 사용자 세션 생성 및 로그인
            response = redirect("account:home")  # 홈 페이지로 리다이렉트

            # 로그인 유지 체크박스가 선택된 경우 쿠키 설정
            if request.POST.get('keep_login') == 'TRUE':
                response.set_cookie('username', username)  # 쿠키에 사용자 이름 저장
                response.set_cookie('password', password)  # 쿠키에 비밀번호 저장
            return response
        else:  # 인증 실패 시
            return render(request, 'account/login.html', {'error': 'Invalid credentials'})

    # 기본 로그인 페이지 렌더링
    return render(request, 'account/login.html')
```

<h4>로그아웃</h4>

```python
def logout(request):
    # 홈 페이지 렌더링
    response = render(request, 'account/home.html')
    # 쿠키 삭제
    response.delete_cookie('username')  # 사용자 이름 쿠키 삭제
    response.delete_cookie('password')  # 비밀번호 쿠키 삭제
    # 사용자 로그아웃
    auth.logout(request)
    return response  # 홈 페이지 응답 반환
```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 191-200
- [x]  SQL 코드카타 82-83
- [x]  백준 코딩테스트 1문제
- [x]  장고 심화 강의 13-14강
- [x]  TIL 작성
- [x]  WIL 작성

## 회고
&nbsp; 오늘은 동생 생일이었다. 영국에 가는 중이라고...🥹 부러워.. 나는 12시간 앉아서 공부하고 있는데.. 나도 언능 취뽀해서 해외여행 다녀야지😁!! 이번주도 마무리!! 내일은 조금 쉬엄쉬엄 공부해야지😭 이번주는 유독 컨디션도 안좋고 잠도 잘 못깨는 일주일이었다. 다시 영양제 잘 챙겨야지..💊