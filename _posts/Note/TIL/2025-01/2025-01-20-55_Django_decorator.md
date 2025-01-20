---
title:  "[TIL] 내일배움캠프 55일차_[Django] 데코레이터" 

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
## Django에서의 데코레이터
- Django에서 데코레이터를 활용하여 View 함수의 기능을 확장하거나 특정 조건을 쉽게 적용할 수 있음
- Django의 데코레이터는 간단한 코드로도 강력한 기능을 제공
- `@login_required`와 `@require_http_methods`를 함께 사용하면 인증 및 요청 검증 로직을 간결하게 처리할 수 있음
- 각 데코레이터는 특정 상황에서 유용하지만, 남용하면 디버깅이 어려워질 수 있으니 적절히 조합해야 함

### 1. @login_required
- 인증된 사용자만 View에 접근할 수 있도록 제한
- 비로그인 사용자가 접근하지 못하도록 보호해야 하는 페이지에 사용
- 예시

    ```python
    from django.contrib.auth.decorators import login_required

    @login_required
    def dashboard_view(request):
        return HttpResponse("Welcome to your dashboard!")
    ```
  - 비로그인 사용자가 접근하면 `LOGIN_URL`로 리다이렉트
  - 기본 리다이렉트 URL은 `/accounts/login/`, 하지만 `settings.py`에서 `LOGIN_URL`로 변경 가능

    ```python
    LOGIN_URL = '/custom-login/'
    ```


### 2. @require_http_methods(["GET", "POST"])
- HTTP 메서드를 제한하여 특정 요청만 처리.
- View 함수가 의도치 않은 메서드 호출을 처리하지 않도록 보호.
- 예시
    
    ```python
    from django.views.decorators.http import require_http_methods

    @require_http_methods(["GET", "POST"])
    def contact_view(request):
        if request.method == "POST":
            # 폼 데이터를 처리
            return HttpResponse("Form submitted successfully!")
        return render(request, "contact_form.html")
    ```
  - 허용되지 않은 메서드로 요청 시 `405 Method Not Allowed` 에러가 반환
  - 예를 들어, `DELETE` 메서드를 사용하면 에러 발생

### 3. @permission_required
- 특정 권한이 있는 사용자만 View에 접근 가능
- 세분화된 권한 관리가 필요한 경우
- 예시

    ```python
    from django.contrib.auth.decorators import permission_required

    @permission_required('app_name.can_edit', login_url='/no-permission/')
    def edit_view(request):
        return HttpResponse("You have permission to edit.")
    ```
  - 권한 이름은 `app_label.permission_codename` 형식
  - 권한이 없는 사용자는 `login_url`로 리다이렉트되거나 403 에러 발생


### 4. @csrf_exempt
- CSRF 보호를 비활성화
- CSRF 토큰이 필요 없는 API나 특정 View에서 사용 (주의 필요)
- 보안상 위험할 수 있으므로 꼭 필요한 경우에만 사용
- 예시

    ```python
    from django.views.decorators.csrf import csrf_exempt

    @csrf_exempt
    def webhook_view(request):
        return HttpResponse("CSRF token is not required here.")
    ```

### 5. @cache_page
- View의 응답 결과를 캐싱
- 동일한 요청에 대해 서버 부하를 줄이기 위해 캐싱 적용
- 예시

    ```python
    from django.views.decorators.cache import cache_page

    @cache_page(60 * 15)  # 15분 동안 캐싱
    def cached_view(request):
        return HttpResponse(f"Current timestamp: {time.time()}")
    ```
  - 설정한 시간 동안 캐시된 응답이 반환된다

## 데코레이터를 조합한 예시
- 인증된 사용자만 접근할 수 있으며, GET과 POST 요청만 허용하는 View
    ```python
    from django.contrib.auth.decorators import login_required
    from django.views.decorators.http import require_http_methods
    from django.http import HttpResponse
    from django.shortcuts import render

    # 로그인한 사용자만 접근할 수 있도록 제한
    @login_required
    # GET과 POST 요청만 허용
    @require_http_methods(["GET", "POST"])
    def profile_view(request):
        """
        사용자 프로필을 표시하거나 업데이트하는 View.
        - GET 요청: 프로필 페이지를 렌더링.
        - POST 요청: 프로필 업데이트를 처리.
        """
        if request.method == "POST":
            # POST 요청 처리 로직
            # 예: 사용자가 제출한 프로필 데이터를 저장
            return HttpResponse("Profile updated!")  # 업데이트 성공 메시지 반환
        
        # GET 요청 처리: 프로필 페이지 렌더링
        return render(request, "profile.html")  # HTML 템플릿을 렌더링하여 반환
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 221-230
- [x]  SQL 코드카타 73
- [x]  백준 코딩테스트 1문제
- [ ]  장고 도전과제 : 좋아요 구현
- [x]  TIL 작성

## 회고
&nbsp; 감기에 걸려버렸다..🤒 난방텐트 하루 열고 잤다고 감기에 걸려버린 운족부족의 몸..🥲 운동 좀 해야겠다.. 오늘은 공부도 조금해서 너무 아쉬운 하루.. 내일도 아프면 병원 빨리 다녀와야겠다ㅠㅠ 이번 감기 독하다던데 벌써 무서워🥹