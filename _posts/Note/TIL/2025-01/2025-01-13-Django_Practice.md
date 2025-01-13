---
title:  "[TIL] 내일배움캠프 48일차_[Django] 프로젝트 생성 연습" 

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
## accounts 앱 설정하기

- accounts/models.py
    
    ```python
    from django.conf import settings
    from django.contrib.auth.models import AbstractUser
    from django.db import models
    
    # Django 기본 User 모델을 확장하여 bio 필드 추가
    class User(AbstractUser):
        bio = models.TextField()
    
    class Profile(models.Model):
    		# 1:1 관계를 설정하는 OneToOneField를 사용하여 User와 연결
    		# 한명의 유저는 한개의 프로필을 가짐
        user = models.OneToOneField(to=settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
        # 주소는 50자까지 입력 가능
        address = models.CharField(max_length=50)
        # 우편번호는 6자까지 입력 가능
        zipcode = models.CharField(max_length=6)
        
        def __str__(self):
            return self.address
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

<br>

## Blog 앱 설정하기

- blog/models.py
    
    ```python
    from django.db import models
    from django.conf import settings
    
    # 게시글 모델
    class Post(models.Model):
        # 작성자 정보를 나타내는 ForeignKey 필드, User 모델과 연결
        # 작성자가 삭제되면 관련 게시글도 삭제
        author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
        # 게시글의 내용
        message = models.TextField()
        # 게시글 생성 시 자동으로 현재 시간 저장
        created_at = models.DateTimeField(auto_now_add=True)
        # 게시글 수정 시 자동으로 현재 시간 업데이트
        updated_at = models.DateTimeField(auto_now=True)
        # Tag와의 N:M 관계를 나타내는 ManyToManyField
        # 태그는 선택적으로 설정 가능
        tag_set = models.ManyToManyField('Tag', blank=True)
    
        def __str__(self):
            return self.message
    
    # 태그 모델
    class Tag(models.Model):
    		# 태그 이름은 최대 44자
        name = models.CharField(max_length=44)
    
        def __str__(self):
            return self.name
    ```
    
- blog/urls.py
    - 만약 /blog/에서 보여주고 싶다면?
        - route 인자를 `''` 로 설정하면 됨!!
    
    ```python
    from django.urls import path
    
    from blog import views
    
    urlpatterns = [
    		# 위치인자(route='', view=views.post_list)
        path('', views.post_list, name='post_list'),
        path('post_new/', views.post_new,),
    ]
    ```
    
- blog/views.py
    1. view func : 요청 처리 로직
    2. 데이터 처리 : 데이터베이스 핸들링(읽고, 쓰고, 쓰고, 수정, 삭제 등등)
    3. 응답반환(랜더링) 템플릿
    
    ```python
    from django.shortcuts import render, redirect
    from blog.forms import PostForm
    from blog.models import Post
    
    # 게시글 목록을 보여주는 뷰
    def post_list(request):
    		# 모든 Post 객체를 가져옴
        posts = Post.objects.all()
        # render 함수로 템플릿을 렌더링
    		# request와 template_name은 필수인자!
    		# context : DB에서 데이터 들고와서 템플릿에 던져주기 
        return render(request=request, template_name='blog/post_list.html', context={'posts': posts})
    
    # 새로운 게시글을 작성하는 뷰
    def post_new(request):
    		# POST 요청일 경우
        if request.method == 'POST':
    		    # 받은 데이터로 PostForm 인스턴스 생성
            form = PostForm(request.POST)
            
            # 다른 사용자가 수정을 하지 못하도록 하기
            # form 데이터가 유효한 경우 처리
            if form.is_valid():
    		        # DB 저장 전에 Post 객체 생성
                post = form.save(commit=False)
                # 현재 로그인한 사용자를 작성자로 설정
                post.author = request.user
                # DB에 저장
                post.save()
                # 게시글 목록 페이지로 보내기
                return redirect('post_list')
        else:
    		    # POST 요청이 아니면 빈 Form을 보여줌
            form = PostForm()
        return render(request=request, template_name='blog/post_new.html', context={'form': form})
    ```
    
    - HTTP Method
        - GET: 리소스를 조회하는 데 사용 서버에 전달하고 싶은 데이터는 query(parameter, query string)을 통해 전
        - POST: 데이터를 추가하거나 등록하는 데 사용
        - PUT: 리소스를 대체하거나 수정하는 데 사용합니다. 해당 리소스가 없으면 새롭게 생성
        - DELETE: 리소스를 삭제하는 데 사용
        - PATCH: 리소스의 부분을 변경하거나 수정하는 데 사용
- blog/forms.py
    1. HTML 폼을 자동 생성
    2. 사용자가 입력한 데이터를 검증 → 데이터베이스 상호작용
    
    ```python
    from django import forms
    from blog.models import Post
    
    # Post 작성을 위한 Form 정의
    class PostForm(forms.ModelForm):
        class Meta:
    		    # Form과 연결된 모델 지정
            model = Post
            # Form에 포함될 필드
            fields = ['message', 'tag_set']
    ```
    
- post_list.html

<div style="margin-left: 2em;">
{% highlight html %}
{% raw %}
<!-- 전체 페이지 제목 -->
<h1>Post_list</h1>

<!-- 게시글 목록을 보여주는 리스트 -->
<ui>
        <!-- posts 리스트를 반복하여 각 게시글의 내용을 출력 -->
    {% for post in posts %}
            <!-- 게시글의 message 필드 출력 -->
        <p>{{ post.message }}</p>
    {% endfor %}
</ui>
{% endraw %}
{% endhighlight %}
</div>


- post_new.html

<div style="margin-left: 2em;">
{% highlight html %}
{% raw %}
<!-- 페이지 제목 -->
<h1>post_new</h1>

<!-- 게시글 작성 폼 -->
<form method="post">
    {% csrf_token %}
    <!-- Form 객체를 <p> 태그 형식으로 렌더링 -->
    {{ form.as_p }}
    <!-- 제출 버튼 -->
    <button type="submit">Submit</button>
</form>
{% endraw %}
{% endhighlight %}
</div>

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 151-160
- [x]  SQL 코드카타 69
- [x]  백준 코딩테스트 1문제
- [x]  장고 심화 강의 5강까지
- [x]  스탠다드반 과제
- [x]  TIL 작성

## 회고
&nbsp; 저번주 금요일에 학습반에서 진행했던 내용을 바탕으로 내용을 조금 추가하고, 주석을 달면서 어떤식으로 작성하는지 익혔다. 수요일까지 메인과제 끝내봐야지..! 내일까지 DRF 강의 다 듣고 빨리 과제 시작해야겠다.


&nbsp; 그리고.. 장고문법도 해결했다. 어휴, 왜 저렇게 나오는지.. 그래도 내가 선택한 테마니까 꾸역꾸역 참아야지..ㅎㅎ