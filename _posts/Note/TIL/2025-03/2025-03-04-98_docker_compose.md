---
title:  "[TIL] 내일배움캠프 98일차_[Docker] Docker Compose" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Docker
    - Docker Compose


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## Docker Compose란?

![Image](https://github.com/user-attachments/assets/295d927c-f225-4194-9fb5-b35d3a18c658){: .align-center style="width:50%;"}

- Docker Compose는 다중 컨테이너 애플리케이션을 정의하고 관리할 수 있도록 도와주는 도구
- 복잡한 서비스 구성을 YAML 파일(docker-compose.yml)로 정의하여 손쉽게 실행하고 관리할 수 있음

<br>

## 주요 기능
- 여러 컨테이너를 한 번에 실행: 웹 서버, 데이터베이스, 캐시 서버 등을 한 번에 실행 가능
- YAML 파일을 통한 설정 관리: docker-compose.yml 파일을 이용하여 환경을 정의
- 서비스 간 네트워킹 자동 설정: 서로 다른 컨테이너 간 통신을 쉽게 할 수 있음
- 로컬 개발 환경 구성 용이: 개발 및 테스트 환경을 쉽게 셋업 가능

<br>

## 설치하기

- Docker Compose는 Docker가 설치되어 있으면 기본적으로 포함되어 있음
- 확인하려면 다음 명령어를 실행하면 됨!
    
    ```bash
    docker-compose --version
    ```

- 만약 설치되지 않았다면, [공식 문서](https://docs.docker.com/compose/install/)를 참고하여 설치할 수 있음

<br>

## 예제
- Django + PostgreSQL을 실행하는 `docker-compose.yml` 파일 예제

    ```yml
    version: '3.8'

    services:
    web:
        image: python:3.9
        container_name: django_app
        working_dir: /app
        volumes:
        - .:/app
        ports:
        - "8000:8000"
        depends_on:
        - db
        command: >
        sh -c "pip install -r requirements.txt && python manage.py runserver 0.0.0.0:8000"

    db:
        image: postgres:15
        container_name: postgres_db
        environment:
        POSTGRES_USER: myuser
        POSTGRES_PASSWORD: mypassword
        POSTGRES_DB: mydatabase
        ports:
        - "5432:5432"
        volumes:
        - pg_data:/var/lib/postgresql/data

    volumes:
    pg_data:
    ```

- 설명
  - web 서비스 : Django 애플리케이션을 실행
  - db 서비스 : PostgreSQL 데이터베이스 실행
  - volumes : 데이터베이스 데이터를 지속적으로 유지

<br>

## 명령어
### 실행
- docker-compose.yml 파일이 있는 디렉토리에서 다음 명령어를 실행하면 모든 서비스가 시작됨

    ```bash
    docker-compose up -d
    ```

### 실행 확인
- 실행 중인 컨테이너를 확인

    ```bash
    docker-compose ps
    ```

### 컨테이너 로그 확인

```bash
docker-compose logs -f web
```

### 모든 서비스 중지 및 삭제

```bash
docker-compose down
```

<br>

## 환경변수 파일 사용하기
- 환경 변수를 .env 파일에서 정의할 수도 있음

### .env 파일 예제
```python
POSTGRES_USER=myuser
POSTGRES_PASSWORD=mypassword
POSTGRES_DB=mydatabase
```

### docker-compose.yml에서 사용
```yml
environment:
  POSTGRES_USER: ${POSTGRES_USER}
  POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
  POSTGRES_DB: ${POSTGRES_DB}
```

<br>

## 장점과 단점
### 장점
- 복잡한 다중 컨테이너 애플리케이션을 쉽게 관리
- 로컬 개발 환경을 빠르게 구축 가능
- 재사용 가능한 설정 (docker-compose.override.yml 지원)
- 네트워크 및 볼륨 관리를 자동화

### 단점
- 프로덕션 환경에서는 Kubernetes 같은 대체 솔루션이 더 적합할 수 있음
- 기본적으로 단일 호스트에서 실행됨 (멀티 노드 배포는 제한적)

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 1문제
- [x]  SA 문서 초안 완성
- [ ]  ~~개발 환경 구성~~ : 공부가 필요한 부분이라 내일 하기로 함!
- [x]  TIL 작성

## 회고
&nbsp;오늘은 SA문서 초안을 완성했다(ML 파트 제외). 아무래도 TIL 쓰고 ML파트 다 채워 놓고 오늘 공부 마무리 해야할 것 같다. 개발환경 구성까지 해서 내일은 개발 시작해야지 했는데, Docker 초보들에게는 너무 가혹한 일정이었던 걸로.. 일단 이미지 굽고 실행하는 것까지는 해놓고 협업 부분은 튜터님의 도움을 받던지 해서 진행하는 것이 좋지 않을까 생각한다🫠 휴,, 그래도 아직 우리가 정해놓은 일정대로 진행되고 있으니까 그나마 안심이다.