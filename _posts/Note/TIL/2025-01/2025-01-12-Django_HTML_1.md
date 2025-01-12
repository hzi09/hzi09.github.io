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
- Django 템플릿에서 데이터를 HTML에 삽입하려면 아래와 같은 문법을 사용

    ![image](https://github.com/user-attachments/assets/f532be20-a0db-4b82-8f1c-7a3f22685e23)


<br>

## 2. 조건문
- 조건문은 아래와 같이 사용

    ![image](https://github.com/user-attachments/assets/d872352f-9528-4452-a3ba-e5be187e17a5)

- 예시
    
    ![image](https://github.com/user-attachments/assets/26ffd144-2b60-4ab8-bbe4-67bdba517c0f)

<br>

## 3. 반복문

- 반복문은 아래와 같이 사용

    ![image](https://github.com/user-attachments/assets/0067cca5-30e4-4c1f-9be6-d6c70f59c9ed)

- 예시

    ![image](https://github.com/user-attachments/assets/4285069f-ad7b-4636-85e0-a869a243c16a)

<br>

## 4. 필터 사용
- Django 템플릿에서는 변수를 출력할 때 필터를 사용할 수 있음
- 필터는 `|`를 사용해 적용

    ![image](https://github.com/user-attachments/assets/358b44ef-ed0a-43c1-9eab-182c304840f7)

- 예시

    ![image](https://github.com/user-attachments/assets/6f7a99b7-e28e-4951-9918-eef957a809b3)

- 주요 필터
  - upper: 문자열을 대문자로 변환
  - lower: 문자열을 소문자로 변환
  - date: 날짜 형식 지정
  - length: 리스트 또는 문자열의 길이 반환

<br>

## 5. 주석
- Django 템플릿에서 주석은 `{# #}`를 사용
- 브라우저에 표시되지 않음

    ![image](https://github.com/user-attachments/assets/a5166b99-9f4f-4e43-aade-050ab9c9226d)

<br>

## 6. include 태그
- HTML 파일을 분리하여 재사용할 때 include 태그를 사용

    ![image](https://github.com/user-attachments/assets/de7cbfbd-6eeb-4d02-92ec-26529d0f9cec)

- 예시

    ![image](https://github.com/user-attachments/assets/cee18faf-3411-4cfa-b183-545133da8d12)

<br>

## 7. url 태그
- Django URL의 이름을 사용해 링크를 생성할 때 **url** 태그를 사용

    ![image](https://github.com/user-attachments/assets/3b93f410-7447-4596-ba0d-1d93fa4e079a)

- 예시

    ![image](https://github.com/user-attachments/assets/73f6532f-3b1b-4e8a-9f83-d9baa881b1ce)

<br>

## 8. 정적 파일 사용
- CSS, JavaScript, 이미지 등 정적 파일을 사용할 때 `static` 태그를 사용

    ![image](https://github.com/user-attachments/assets/472f9ca7-411a-46fb-b670-915691951f8a)

- 정적 파일을 사용하려면 템플릿 상단에 `load static`를 추가해야 함

    ![image](https://github.com/user-attachments/assets/5797b3e6-d569-46a9-bae6-a4aaf86fb077)

<br>

## 9. csrf_token
- Django에서 폼을 제출할 때 보안을 위해 CSRF 토큰을 추가해야 함

    ![image](https://github.com/user-attachments/assets/584fe4fb-cab3-41a4-9d54-8be1e80d3fa3)

## 10. 커스텀 태그와 필터
- Django는 기본 제공 기능 외에도 커스텀 태그와 필터를 작성할 수 있음
- 커스텀 태그를 사용하려면 템플릿에서 로드해야 함

    ![image](https://github.com/user-attachments/assets/7eb5d08d-6ec4-4ad6-97e5-7d6d12f98b78)

- 예시

    ![image](https://github.com/user-attachments/assets/c11eb07a-dda9-4d6b-9bda-2ba0d8bf9015)



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
&nbsp; 장고 문법이 백틱안으로 안들어가져서 코드를 다 이미지로 대체했다.. 이게 무슨일이람.. 이건 방법을 좀 찾아봐야 할것 같다.