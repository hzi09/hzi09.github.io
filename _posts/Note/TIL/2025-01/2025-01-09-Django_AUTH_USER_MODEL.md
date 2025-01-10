---
title:  "[TIL] 내일배움캠프 44일차_[Django] AUTH_USER_MODEL" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Django
    - AUTH_USER_MODEL


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## Django User 모델을 참조하는 방법

- 일반적으로 3가지 방식이 존재

### User

- DJango 에서 제공하는 클래스 자체를 import 하여 사용하는 방식
- 기본으로 제공하는 `User` 의 기능은 정말로 간소
    - 나중에 커스텀마이징이 필요할 수 있음
    - 프로젝트 세팅을 기본 User로 한 후에 변경하게 되면 모든 코드를 수정해야할 수도 있기 때문에 가장 권장하지 않는 방법

```python
from django.contrib.auth.models import User

class SignupForm(UserCreationForm):
    class Meta:
        model= User
        fields = [
            'username',        
        ]
```

### get_user_model()

- 현재 활성화된 User 모델을 반환하며, 그렇지 않은 경우 User(default) 모델을 반환
- "**객체 인스턴스**"를 반환 ⇒ 클래스가 들어가야 하는 경우에 사용하면 됨
- 앱이 로드 되는 순간에 실행되므로 반드시 유효한 모델 객체를 반환한다는 보장이 없음(None이 리턴될수도 있음)

```python
from django.contirb.auth import get_user_model
 
 class SignupForm(UserCreationForm):
     class Meta:
         model= get_user_model()
         fields = [
             'username',        
         ]
```

### AUTH_USER_MODEL

- Django의 Settings 설정을 참고하여 사용하는 방식
- 외래키 모델을 전달할 때 문자열로 전달

```python
rom django.conf import settings

class SignupForm(UserCreationForm):
    class Meta:
        model= settings.AUTH_USER_MODEL
        fields = [
            'username',        
        ]
```

<br>

## 직접해보기

- `accounts/models.py`
    
    ```python
    from django.db import models
    from django.contrib.auth.models import AbstractUser
    
    # AbstractUser를 상속받아 Users 모델 구축
    class Users(AbstractUser) :
        pass # 추가하지 않았기 때문에 기본 auth.user
    ```
    
    - 기본적으로 제공하는 필드
        - id : PK
        - username
        - first_name
        - last_name
        - email
        - password
        - is_staff
        - is_activate
        - is_superuser
        - last_login
        - data_joined

- `settings.py`
    
    ```python
    AUTH_USER_MODEL = 'accounts.Users'
    ```
    
- `articles/models.py` 
    ```python
    from django.conf import settings
    from django.db import models
    
    # Post라는 데이터베이스-테이블 생성
    class Post(models.Model):
        # ForeignKey : settings.AUTH_USER_MODEL 참조
        author = models.ForeignKey(to=settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
        # CahrFied : 짧은 문자열 데이터 저장(18글자로 제한)
        title = models.CharField(max_length=18)
        # TextField : 긴 텍스트 데이터 저장
        message = models.TextField()
        # 객체가 처음 생성될 때 현재 시간을 자동으로 설정
        created_at = models.DateTimeField(auto_now_add=True)
        # 객체가 저장될 때마다 현재 시간으로 자동 업데이트
        updated_at = models.DateTimeField(auto_now=True)
    
        def __str__(self):
            return self.title
    ```

- admin 사이트에서 Users와 Post를 사용할 수 있도록 등록
  - `accounts/admin.py`
      
      ```python
      from django.contrib import admin
      from django.contrib.auth.admin import UserAdmin
      from .models import Users
      
      admin.site.register(Users, UserAdmin)
      ```
      
  - `articles/admin.py`
      
      ```python
      from django.contrib import admin
      from .models import Post
      
      admin.site.register(Post)
      ```

- 그러면 admin 사이트에서 user와 post를 등록할 수 있게 됨


    ![image](https://github.com/user-attachments/assets/288bcac2-75d2-43c5-bab5-742e12484ae3)

- user와 post를 등록한 후에 데이터베이스를 보면
    - users

        ![image](https://github.com/user-attachments/assets/edc7e7e1-1a91-497b-b65e-89119c39971a)

    - post

        ![image](https://github.com/user-attachments/assets/3bf4051b-b17b-486f-9ba9-aa9693219b9d)

    - users 테이블의 username과 id를 확인해보면 `user1 : 2`, `user2: 3`으로 설정되어 있음
    - 해당 유저가 작성한 post를 확인해보면 autho_id에 user1이 작성한 글은 2가 user2가 작성한 글은 3인 것을 확인 가능
    - 이를 통해 author_id는 users 테이블을 참조하는 것을 알 수 있음


<br>
<br>


# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 111-120
- [x]  SQL 코드카타 63
- [x]  백준 코딩테스트 1문제
- [x]  장고 강의 22강까지
- [x]  스탠다드반 과제
- [x]  TIL 작성

## 회고
&nbsp; 회고 누락시키고 push한거 실화인지..ㅎㅎ 저장도 안하고 냅다 올려버렸다. 항상 마음만 급한 나.. 이대로 괜찮은가.. 이마 탁.. 내일 TIL이랑 같이 커밋해야지...
&nbsp; 다들 알고리즘 코드카타가 100번 후반인거 같아서 조금 스피드를 올려야할 것 같다. 난 아직 120번인데 엉엉.. SQL도 너무 어려워서 이제 1개씩 푸는데.. 점점 내 실력이 보인다🥹 조금 더 공부가 필요할듯..