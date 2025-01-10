---
title:  "[TIL] 내일배움캠프 45일차_[Django] Model Relationship" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Django
    - Model Relationship


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 1:1 관계 (One-to-One Relationship)

- 1:1 관계는 한 모델의 인스턴스가 다른 모델의 인스턴스와 정확히 하나의 관계를 맺는 경우
    - ex. 한 사람당 하나의 프로필을 가질 때
- `OneToOneField`를 사용하여 구현.

### 예시 : 마일스톤(Milestone)

- `account/models.py`
    
    ```python
    from django.db import models
    from django.contrib.auth.models import AbstractUser
    from articles.models import Post
    
    class Users(AbstractUser) :
        pass
    
    class UserMilestone(models.Model):
        user = models.OneToOneField('Users', on_delete=models.CASCADE, related_name='milestone')
        join_anniversary = models.DateField(auto_now_add=True)  # 가입한 날
    
        def write_posts_count(self):
            # Post 테이블에서 해당 사용자의 게시물 수를 계산
            return Post.objects.filter(author=self.user).count()
        
        # Admin 페이지에서 보여줄 컬럼 이름 설정
        write_posts_count.short_description = 'Post Count'
    ```
    
- `account/admin.py`
    
    ```python
    from django.contrib import admin
    from .models import *
    
    @admin.register(Users)
    class UsersAdmin(admin.ModelAdmin):
        list_display = ("username",)
    
    @admin.register(UserMilestone)
    class UserMilestoneAdmin(admin.ModelAdmin):
        list_display = ('user', 'write_posts_count', 'join_anniversary',)
    ```
    

- User의 고유 Milestone 생성
    
    ![image](https://github.com/user-attachments/assets/023edb42-d906-4b76-aa19-0d5eaf776052)
    

<br>


## 1:N 관계 (One-to-Many Relationship)

- 1:N 관계는 한 모델의 인스턴스가 다른 모델의 여러 인스턴스와 관계를 맺는 경우
    - ex. 하나의 게시글에 여러 개의 댓글이 달릴 때
- `ForeignKey`를 사용하여 구현

### 예시 : 카테고리

- `articles/models.py`
    
    ```python
    from django.db import models
    from django.conf import settings
    
    class Post(models.Model):
        author = models.ForeignKey(to=settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
        title = models.CharField(max_length=18)
        message = models.TextField()
        created_at = models.DateTimeField(auto_now_add=True)
        updated_at = models.DateTimeField(auto_now=True)
        category = models.ForeignKey('Category', related_name='posts', on_delete=models.CASCADE, null=True)
    
        def __str__(self):
            return self.title
        
    class Category(models.Model):
        name = models.CharField(max_length=100)
    
        def __str__(self):
            return self.name
    ```
    
- `articles/admin.py`
    
    ```python
    @admin.register(Post)
    class PostAdmin(admin.ModelAdmin):
        list_display = ("title", "author", "category")
    
    @admin.register(Category)
    class Category(admin.ModelAdmin) :
        list_display = ('name',)
    ```
    
- 카테고리가 적용된 Post 리스트
    
    ![image](https://github.com/user-attachments/assets/7385ba78-febb-4cb6-a6f5-15fa85ec5c83)
    

<br>

## N:M 관계 (Many-to-Many Relationship)

- N:M 관계는 여러 모델 인스턴스가 서로 다수의 관계를 맺는 경우(1:N, N:1 관계를 가짐)
    - ex. 여러명의 유저가 좋아요를 누르는 경우, 유저는 여러 글에 좋아요를 남길 수 있음
- `ForeignKey` 가 여러개 있는 구조!
- `ManyToManyField`를 사용하여 구현.

### 예시: 사용자의 관심사

- `account/models.py`
    
    ```python
    class Users(AbstractUser) :
        interests = models.ManyToManyField('UserInterest', related_name='users')
        
    class UserInterest(models.Model):
        name = models.CharField(max_length=100)
    
        def __str__(self):
            return self.name
    ```
    
- `account/admin.py`
    
    ```python
    @admin.register(Users)
    class UsersAdmin(admin.ModelAdmin):
        list_display = ('username', 'show_interest')
    
        def show_interest(self, obj):
            return ", ".join([interest.name for interest in obj.interests.all()])
            
    @admin.register(UserInterest) 
    class UserInterestAdmin(admin.ModelAdmin) :
        pass
    ```
    
- 사용자의 관심사
    
    ![image](https://github.com/user-attachments/assets/425bac05-23fa-4838-a039-b85d5d6e66a5)


<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 121-130
- [x]  SQL 코드카타 64
- [x]  백준 코딩테스트 1문제
- [ ]  장고 강의 ~~25강까지~~ 23강까지
- [x]  스탠다드반 과제
- [x]  TIL 작성

## 회고
&nbsp; 생각보다 스탠다드반 과제가 어려워서 강의를 많이 못들었다. 주말에 마저 들어야지.. 빨리 심화도 들어야하는데, 너무 진도가 안나간다.. 엉엉..🥹