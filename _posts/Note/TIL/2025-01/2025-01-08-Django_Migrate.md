---
title:  "[TIL] 내일배움캠프 43일차_[Django] 마이그레이션(Migration)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Django
    - Migration


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 용어정리

### Model

- 저장할 데이터에 대한 필드와 동작들을 포함한 데이터베이스 구조(layout)
- Django는 Model을 이용해서 데이터를 조작
- 일반적으로 하나의 Model은 하나의 데이터베이스 테이블을 의미


### 마이그레이션(Migration)

- Python으로 Model 코드는 작성하여도 데이터베이스에는 반영이 안됨
- Django는 마이그레이션(migration)을 만들고 이 단위로 데이터베이스에 변경사항을 반영

<br>

## 직접해보기
### 1. Model 생성
- models.py
  - `Article`이라는 테이블을 생성하고 그 안에 `title` 컬럼을 생성
    ```python
    from django.db import models

    class Article(models.Model):
        title = models.CharField(max_length=50)

    def __str__(self):
        return self.title
    ```

### 2. Magration 생성
- 현재 모델의 변경사항을 마이그레이션으로 생성
- 아래와 같이 `python manage.py makemigrations <앱이름>`을 써주면 독립적으로 저장
- 여러개의 모델을 만들면 실수를 할 수도 있기 때문에 독립적으로 저장하는 습관을 기르는 것이 좋음
    ```bash
    python manage.py makemigrations articles
    ```
- 생성 완료
  
    ![image](https://github.com/user-attachments/assets/5b88e032-7978-467f-b316-764210e1af3f){: width="40%" height="40%"}

### 3. Magration 적용
- 데이터베이스에 반영되지 않은 마이그레이션을 반영
- Magration을 생성할때와 마찬가지로 앱이름을 써서 반영
    ```bash
    python manage.py migrate articles
    ```
- 적용 완료

    ![image](https://github.com/user-attachments/assets/7a409579-435e-4f81-a197-cd4c1085bab2){: width="40%" height="40%"}

- 적용이 완료되고나면 `articles` 앱에 magrations 폴더 속에 파일이 생성됨

    ![image](https://github.com/user-attachments/assets/447c9d15-b66e-4048-bd9f-047c1d9245c4){: width="40%" height="40%"}

- SQL에도 `앱이름_클래스명`형태로 테이블이 생성됨

    ![image](https://github.com/user-attachments/assets/c1bbde45-eb95-47a7-900e-fbc6869759bc){: width="30%" height="30%"}

- 데이터를 넣고 확인해보면 아래와 같이 컬럼이 생성된 것을 확인 가능

    ![image](https://github.com/user-attachments/assets/f460fe0d-d02a-4893-9c37-f066a35a876b){: width="20%" height="20%"}

### 4. Magration 추가
- 새로운 컬럼을 추가해보자!
- `content`라는 컬럼을 추가하기 위한 코드
    ```python
    from django.db import models

    class Article(models.Model):
        title = models.CharField(max_length=50)
        content = models.TextField()
        
        def __str__(self):
            return self.title
    ```
- 아까와 동일하게 Migration을 생성하면 다음과 같이 기존에 생성한 데이터는 어떻게 할것이냐는 메세지가 뜸!
  - 일단 값 하나를 넣고 추후에 수정하면 되므로 1번을 선택하여 진행
    
    ![image](https://github.com/user-attachments/assets/f3bb3608-e4f6-44bd-8fc7-f44568cce370)

- 그다음 migrtion을 저장해주면 아래와 같이 migrations 파일에 새로운 파일이 생김

    ![image](https://github.com/user-attachments/assets/86b3ad1e-e360-4422-a77c-b33be2171724){: width="40%" height="40%"}

- SQL에 들어가서 테이블을 확인해보면 `content` 컬럼이 생긴 것을 확인 가능

    ![image](https://github.com/user-attachments/assets/3cd2684b-7da4-4827-a2e2-033642ce0a05){: width="40%" height="40%"}

<br>

### 5. Magration 삭제
- 아래와 같이 `created_at`과 `updated_at`을 생성하고 magration을 생성하고 적용했다고 가정해보자.
    ```python
    from django.db import models

    class Article(models.Model):
        title = models.CharField(max_length=50)
        content = models.TextField()
        created_at = models.DateTimeField(auto_now_add=True)
        updated_at = models.DateTimeField(auto_now=True)
        
        def __str__(self):
            return self.title
    ```
- SQL문을 보면 아래와 같이 4개의 컬럼이 있는 것이 확인 가능

    ![image](https://github.com/user-attachments/assets/c8b6140a-a336-4dfd-bc4c-6814e29b44d9){: width="40%" height="40%"}

- `created_at`과 `updated_at`이 필요없을 때는 어떻게 해야할까?🤔 : 마이그레이션을 이전으로 돌리면 됨
- 일단 마이그레이션 목록과 적용여부를 확인하기 위해 아래의 명령을 사용
    ```bash
    python manage.py showmigration
    ```

  - 아래와 같이 0001 ~ 0003의 마이그레이션이 생성되고 적용([x])되어 있는 것을 확인

    ![image](https://github.com/user-attachments/assets/91cf5307-5fe1-40a3-93d7-31a94b67f4e8){: width="40%" height="40%"}

  - 0003을 취소해야하므로 0002로 migrate 명령어를 사용
    ```bash
    python manage.py migrate articles 0002
    ```
    - 다시 목록을 확인해보면 적용이 취소된 것을 볼 수 있음

        ![image](https://github.com/user-attachments/assets/aee387b8-e604-43de-bb68-b938b63b82ec){: width="40%" height="40%"}

    - SQL 테이블에서도 해당 컬럼이 사라짐

        ![image](https://github.com/user-attachments/assets/3cd2684b-7da4-4827-a2e2-033642ce0a05){: width="40%" height="40%"}

<br>
<br>


# 💡Today I Thought
## 오늘의 체크리스트
- [x]  알고리즘 코드카타 101-110
- [x]  SQL 코드카타 62
- [x]  백준 코딩테스트 1문제
- [x]  장고 강의 20강까지
- [x]  스탠다드반 과제
- [x]  TIL 작성

## 회고
&nbsp; 어제 학습반에서 했던 내용을 복습겸 숙제 제출겸 작성! 강의도 빨리 들어야하는데, 진도가 여전히 안나가는.. 내일은 다 듣고 이번주에 제대로 복습해야겠다.