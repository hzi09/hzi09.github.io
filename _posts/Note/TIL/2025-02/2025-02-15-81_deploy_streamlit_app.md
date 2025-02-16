---
title:  "[TIL] 내일배움캠프 81일차_[Streamlit] Streamlit 앱 배포 방법" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Streamlit


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## Streamlit 앱 배포하는 방법
Streamlit 애플리케이션을 배포하는 방법에는 여러 가지가 있지만, 가장 많이 사용되는 방법은 다음과 같음

- Streamlit Community Cloud (무료, 간편)
- Heroku (무료 티어 제공, 간단한 설정 필요)
- Railway, Render (무료 및 유료 플랜 제공)
- AWS, GCP, Azure (클라우드 서비스 활용, 확장 가능)
- Docker + VPS (EC2, DigitalOcean 등) (유연한 배포 가능)

<br>

## Streamlit Community Cloud
### ✅장점
- Streamlit 공식 배포 플랫폼으로 무료 사용 가능
- GitHub과 연동하여 쉽게 배포 가능
- 별도의 서버 설정 없이 자동 업데이트

### 📌배포 방법
1. GitHub 저장소 준비
   - Streamlit 애플리케이션 코드를 GitHub에 업로드

2. Streamlit Cloud에 로그인
   - [Streamlit Community Cloud](https://streamlit.io/cloud)에 접속
   - GitHub 계정으로 로그인
   - "New App" 버튼 클릭

3. 배포할 저장소 선택
   - GitHub 저장소를 선택
   - 배포할 브랜치(branch) 및 실행할 파일(app.py) 지정
   - "Deploy" 버튼 클릭

4. 배포 완료 및 접근
   - 배포가 완료되면 고유한 URL이 생성됨
   - 해당 URL을 통해 누구나 애플리케이션에 접근 가능

5. 업데이트 방법
   - GitHub의 코드를 수정 후 푸시하면 자동으로 업데이트


<br>

## Heroku를 이용한 배포

### ✅장점
- 무료 티어 제공 (월 550시간까지)
- 간단한 설정으로 Python 앱 배포 가능

### 📌배포 방법
1. [eroku CLI](https://devcenter.heroku.com/articles/heroku-cli) 설치

    ```bash
    brew tap heroku/brew && brew install heroku
    ```

2. Heroku 로그인 및 앱 생성

    ```bash
    heroku login
    heroku create my-streamlit-app
    ```

3. requirements.txt 파일 추가
   - Heroku에서 Streamlit을 실행하려면 `requirements.txt`가 필요

      ```bash
      pip freeze > requirements.txt
      ```

4. `Procfile` 파일 추가
   - Heroku에서는 실행 명령어를 `Procfile`에 지정해야 함

      ```plaintext
         web: streamlit run app.py --server.port=$PORT --server.headless=true
         ```

5. Heroku에 코드 배포

   ```bash
   git add .
   git commit -m "Deploy to Heroku"
   git push heroku main
   ```

6. 배포된 앱 확인

   ```bash
   heroku open
   ```

- 주의: Heroku 무료 플랜은 제한이 있으며, 일정 시간이 지나면 자동으로 슬립 모드에 들어감

<br>

## Docker와 VPS를 활용한 배포
### ✅장점
- 유연한 환경 설정 가능
- 서버 성능과 트래픽을 직접 관리할 수 있음

### 📌배포 방법
1. Dockerfile 생성

   ```dockerfile
   FROM python:3.9

   WORKDIR /app
   COPY requirements.txt ./requirements.txt

   RUN pip install --no-cache-dir -r requirements.txt

   COPY . .
   CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
   ```

2. Docker 빌드 및 실행

   ```bash
   docker build -t my-streamlit-app .
   docker run -p 8501:8501 my-streamlit-app
   ```

3. VPS(예: AWS EC2)에서 실행
   - EC2 인스턴스를 생성 (Ubuntu 20.04 추천)
   - SSH 접속 후 Docker 설치

      ```bash
      sudo apt update && sudo apt install docker.io -y
      ```
   - Streamlit 애플리케이션을 실행
    
      ```bash
      docker run -d -p 80:8501 my-streamlit-app
      ```
   - 이제 퍼블릭 IP 주소를 사용해 배포된 웹앱에 접근할 수 있음

<br>

## 정리

| 배포 방법           | 난이도          | 비용            | 장점                     | 단점                   |
|:-------------------:|:---------------:|:---------------:|:------------------------:|:----------------------:|
| **Streamlit Cloud** | 초보자-friendly | 무료            | 빠른 배포, 자동 업데이트 | 커스텀 설정 불가       |
| **Heroku**          | 보통            | 무료 (제한적)   | 간편한 배포              | 일정 시간 후 슬립 모드 |
| **Docker + VPS**    | 어려움          | 유료 (서버 비용)| 성능 최적화 가능         | 설정이 복잡함          |

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 330
- [x] SQL 코드카타 115
- [x] 팀회의(19:00~20:00)
- [x] TIL 작성

## 회고
&nbsp;오늘도 코드카타를 하고 오랜만에 두리 미용시키고 목욕도 시켰다. 요즘 공부한다고 강아지들한테 너무 신경 못써주는 것 같다🫠 누나가.. 열심히 해서 취업 성공하면 너네 맛있는거 많이 사줄게😢 오늘 팀 회의도 잘 진행되서 다행이다. 내일 Streamlit과 LLM 계속 만져봐야겠다!