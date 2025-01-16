---
title:  "[TIL] 내일배움캠프 51일차_[Django] Model Field" 

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

- Django의 모델 필드는 데이터베이스 테이블의 열(column)을 정의하는 데 사용되며 다양한 데이터 타입에 맞는 필드 클래스가 제공
- 공식문서 : [🔗Model field reference](https://docs.djangoproject.com/en/4.2/ref/models/fields/#module-django.db.models.fields)


## 1. 문자열 관련 필드
### CharField
- 고정 길이의 문자열 데이터를 저장할 때 사용
- 주요 옵션
  - `max_length`: 문자열의 최대 길이를 지정 (필수)
- 예시
    ```python
    from django.db import models

    class Product(models.Model):
        name = models.CharField(max_length=100)  # 최대 100자의 문자열 저장
    ```

### TextField
- 긴 텍스트 데이터를 저장할 때 사용함
- 길이 제한이 없으나 데이터베이스 성능상 너무 긴 데이터를 저장하는 것은 권장하지 않음
- 예시
    ```python
    class BlogPost(models.Model):
        content = models.TextField()  # 긴 텍스트 저장
    ```

<h3>차이점</h3>

- `CharField`: 필수적으로 max_length를 지정해야 하며, 길이 제한이 있음.
- `TextField`: 길이 제한이 없으나, 일반적으로 더 큰 데이터를 저장하는 데 적합

<br>

## 2. 숫자 관련 필드

### IntegerField
- 정수를 저장할 때 사용
- 예시
    ```python
    class Order(models.Model):
        quantity = models.IntegerField()  # 정수 저장
    ```

### FloatField
- 부동 소수점 숫자를 저장할 때 사용함
- 예시
    ```python
    class Product(models.Model):
        price = models.FloatField()  # 소수점 포함 숫자 저장
    ```

### DecimalField
- 정확한 소수점 연산이 필요한 경우 사용
- 소수점 이하 자리수와 전체 자리수를 지정할 수 있음
- 주요 옵션
  - `max_digits`: 전체 자리수 지정
  - `decimal_places`: 소수점 이하 자리수 지정
- 예시
    ```python
    class Invoice(models.Model):
        amount = models.DecimalField(max_digits=10, decimal_places=2)  # 최대 10자리, 소수점 이하 2자리
    ```

<h3>차이점</h3>

- `FloatField`: 근사치를 저장하므로, 금융 계산에는 적합하지 않음
- `DecimalField`: 금융 및 정밀한 계산이 필요한 경우 적합

<br>

## 3.날짜/시간 관련 필드
### DateField
- 날짜를 저장할 때 사용함
- 주요 옵션
  - `auto_now`: 객체가 저장될 때 현재 날짜로 자동 갱신
  - `auto_now_add`: 객체가 처음 생성될 때 현재 날짜로 설정
- 예시
    ```python
    class Event(models.Model):
        event_date = models.DateField()  # 날짜 저장
    ```

### DateTimeField
- 날짜와 시간을 저장할 때 사용
- `DateField`와 옵션 동일
- 예시
    ```python
    class Log(models.Model):
        created_at = models.DateTimeField(auto_now_add=True)  # 생성 시점 저장
    ```

<h3>차이점</h3>

- `DateField`: 날짜만 저장
- `DateTimeField`: 날짜와 시간을 함께 저장

<br>

## 4. Boolean 관련 필드
### BooleanField
- True 또는 False 값을 저장
- 예시
    ```python
    class Task(models.Model):
        is_completed = models.BooleanField(default=False)  # 기본값은 False
    ```

<br>

## 5.관계형 필드
### ForeignKey
- 다른 모델과의 1:N 관계를 정의할 때 사용
- 주요 옵션
  - `on_delete`: 참조된 객체가 삭제될 때의 동작 지정 (CASCADE, SET_NULL 등)
    - `CASCADE` : 참조된 객체가 삭제되면, 해당 객체를 참조하는 모든 객체도 함께 삭제
    - `SET_NULL` : 참조된 객체가 삭제되면, 참조하는 객체의 필드를 NULL로 설정 하며, 사용하기 위해서는 `null=True` 옵션도 추가해야함
- 예시
    ```python
    class Author(models.Model):
        name = models.CharField(max_length=100)

    class Book(models.Model):
        author = models.ForeignKey(Author, on_delete=models.CASCADE)  # 1:N 관계 정의
    ```

### OneToOneField
- 다른 모델과의 1:1 관계를 정의할 때 사용
- 예시
    ```python
    class UserProfile(models.Model):
        user = models.OneToOneField(User, on_delete=models.CASCADE)  # 1:1 관계 정의
    ```

### ManyToManyField
- 다른 모델과의 N:N 관계를 정의할 때 사용
- 예시
    ```python
    class Student(models.Model):
        name = models.CharField(max_length=100)

    class Course(models.Model):
        enrolled_students = models.ManyToManyField(Student)  # N:N 관계 정의
    ```

<br>

## 6. 기타 필드
### EmailField
- 이메일 주소를 저장하며, 형식 검증을 제공
- 예시
    ```python
    class Contact(models.Model):
        email = models.EmailField()  # 이메일 형식 검증 포함
    ```

### URLField
- URL을 저장하며, 형식 검증을 제공
- 예시
    ```python
    class Bookmark(models.Model):
        url = models.URLField()  # URL 형식 검증 포함
    ```

### FileField
- 파일 경로를 저장하며 파일 업로드를 지원
- 예시
    ```python
    class Document(models.Model):
        file = models.FileField(upload_to='documents/')  # 파일 업로드 경로 지정
    ```

### ImageField
- 이미지 파일을 저장하며, FileField를 상속받아 이미지 검증 기능이 추가
- 예시
    ```python
    class Profile(models.Model):
        avatar = models.ImageField(upload_to='avatars/')  # 이미지 업로드 경로 지정
    ```

<br>
<br>


# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타181-190
- [x]  SQL 코드카타 81
- [x]  백준 코딩테스트 1문제
- [x]  장고 심화 강의 11-12강
- [x]  TIL 작성

## 회고
&nbsp; 모델 만들때마다 필드를 찾으러 다녀서 좀 자주 쓰는 것들을 추려서 정리했다. 이제 여기서 필요한거 찾아야지! 오늘은 공부가 잘 안되는 하루였던 것 같다. 코딩테스트도 10시 반이면 다 끝났는데 오늘은 계속 딴 짓하면서 했더니.. 11시 넘어서 끝났다ㅠㅠ 강의도 너무 오래걸렸다.. 내일은 더 열심히 해야지...