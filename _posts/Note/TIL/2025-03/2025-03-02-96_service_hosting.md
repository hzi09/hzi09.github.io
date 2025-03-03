---
title:  "[TIL] 내일배움캠프 96일차_[Django] Django 서비스 호스팅" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Django
    - 서비스 호스팅


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
- 나중에 서비스 호스팅을 위해 서버 환경을 어떻게 구성할지 고민해봤다🤔(사실 숙제기도 함ㅎㅎ)

## 서비스 호스팅 : AWS vs 로컬 호스팅
### AWS 호스팅
- 장점
  - 확장성(Scalability): 트래픽 증가 시 손쉽게 인프라를 확장 가능
  - 고가용성(High Availability): 여러 가용 영역을 활용하여 안정적인 서비스 제공
  - 관리 편의성: 자동 백업, 로깅, 모니터링 등의 기능 제공
  - 보안 강화: IAM, VPC, 보안 그룹 등을 통한 강력한 보안 설정 가능

- 단점:
  - 비용 부담: EC2, RDS, S3 등 다양한 서비스를 사용할수록 비용 증가
  - 학습 곡선: AWS 서비스 및 설정을 익히는 데 시간이 필요함

### 로컬 호스팅
- 집에 남는 컴퓨터를 활용하는 방법

- 장점
  - 비용 절감: AWS와 비교하여 초기 비용이 거의 없음
  - 직접 컨트롤 가능: 서버 설정을 자유롭게 변경 가능
  - 연습 및 학습용으로 적합

- 단점
  - 접근성 제한: 외부에서 접속하려면 포트포워딩, 도메인 설정 등이 필요
  - 유지보수 부담: 하드웨어 장애, 네트워크 장애 시 직접 해결해야 함
  - 확장성 부족: 트래픽 증가 시 즉각적인 스케일업이 어려움

### 정리
- 실제 운영 서비스: AWS를 활용하는 것이 안정성과 확장성을 고려했을 때 적합
- 개발 및 테스트 환경: 로컬 호스팅으로 충분

<br>

## 서비스 실행 : Nginx & Gunicorn 활용
- Django는 기본적으로 `runserver` 명령어를 사용하여 개발 서버를 실행하지만, 운영 환경에서는 적합하지 않음
- Gunicorn + Nginx 조합을 사용하여 안정적인 서비스 운영이 가능

### Gunicorn: Django WSGI 서버
- **Gunicorn(Green Unicorn)**은 WSGI(Web Server Gateway Interface) 서버로, Django 애플리케이션을 실행하는 역할을 함
- 설치 및 실행

  ```bash
  pip install gunicorn
  gunicorn --workers 3 myproject.wsgi:application
  ```

- 장점
  - 멀티 프로세스를 지원하여 성능 개선
  - 간단한 설정으로 빠르게 실행 가능
- 단점
  - 직접적인 요청을 처리할 수 없고, 리버스 프록시(예: Nginx)와 함께 사용해야 함

### Nginx: 리버스 프록시 서버
- Nginx는 Gunicorn 앞단에서 클라이언트 요청을 받아 적절히 라우팅해주는 역할을 함
- 설정 예시(/etc/nginx/sites-available/myproject)

  ```
  server {
      listen 80;
      server_name example.com;

      location / {
          proxy_pass http://127.0.0.1:8000;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
      }
  }
  ```

- 장점
  - 정적 파일(Static files) 제공 최적화
  - 로드 밸런싱 가능
  - 보안 및 성능 개선 가능

### 결론
- Gunicorn + Nginx 조합을 사용하면 Django 서비스를 안전하고 효율적으로 배포할 수 있음


<br>

## 서버 환경 통일 및 관리: Docker 활용
### Docker를 사용하는 이유
- 환경 일관성 유지: 팀원별 로컬 환경 차이를 없앰
- 배포 용이성: 서버와 동일한 환경을 로컬에서도 실행 가능
- 확장성: 컨테이너 기반으로 확장 및 배포 용이

### Docker로 Django 애플리케이션 실행하기
1) Dockerfile 작성

  ```Dockerfile
  FROM python:3.9
  WORKDIR /app
  COPY requirements.txt .
  RUN pip install -r requirements.txt
  COPY . .
  CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
  ```

2) docker-compose.yml 작성

  ```yml
  version: '3'
  services:
    web:
      build: .
      ports:
        - "8000:8000"
      volumes:
        - .:/app
  ```

3) 실행 명령어

  ```
  docker-compose up --build
  ```

### 결론
- Docker를 활용하면 개발 환경과 배포 환경을 통일할 수 있어 유지보수가 용이


## 요약

### AWS vs 로컬 호스팅 비교

| 항목   | AWS | 로컬 호스팅 |
|--------|-----|-------------|
| 비용   | 유료 | 무료        |
| 확장성 | 높음 | 낮음        |
| 유지보수 | 쉬움 | 어려움     |
| 보안   | 강함 | 약함        |

### 서버 기술 비교

| 기술      | 역할 |
|-----------|-------------------------------|
| Gunicorn  | Django 애플리케이션 실행       |
| Nginx     | 리버스 프록시 및 정적 파일 서빙 |
| Docker    | 환경 통일 및 배포 자동화       |

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 1문제
- [x] SQL 코드카타 1문제
- [x] ML 공부
- [x] TIL 작성

## 회고
&nbsp;오늘은 쉬어가는 날..☕