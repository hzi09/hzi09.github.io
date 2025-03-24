---
title:  "[TIL] 내일배움캠프 118차_[ML] scikit surprise install 에러" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝
    - scikit surprise


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## windows
### 에러코드
    ```
        building 'surprise.similarities' extension
        error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
        [end of output]

    note: This error originates from a subprocess, and is likely not a problem with pip.
    ERROR: Failed building wheel for scikit-surprise
    Failed to build scikit-surprise
    ERROR: Failed to build installable wheels for some pyproject.toml based projects (scikit-surprise)
    ```

### 해결방법
- [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/ko/visual-cpp-build-tools/)에서 "Download Build Tools"를 클릭하여 설치
- 설치할 때, "Desktop development with C++" 항목을 선택하고 설치
- 설치가 완료된 후, 컴퓨터를 재부팅한 뒤 다시 scikit-surprise를 설치

- 이렇게 하면 보통 해결된다는데,, 안되서 나는 docker환경에서 점검했다.

<br>


## docker환경
- docker에서 surprise를 사용하여 추천시스템을 구현하기 위해서는 dockerfile에서 필요한 라이브러리가 설치되어야함

    ```dockerfile
    FROM python:3.12.9-slim

    # 필수 빌드 도구 및 라이브러리 설치 (scikit-surprise를 빌드하는 데 필요)
    RUN apt-get update && apt-get install -y \
        netcat-openbsd \
        libpq-dev \
        postgresql-client \
        build-essential \
        python3-dev \
        libatlas-base-dev \
        gfortran \
        cmake \
        wget \
        && rm -rf /var/lib/apt/lists/*

    COPY requirements.txt /tmp/
    RUN pip install --no-cache-dir -r /tmp/requirements.txt

    COPY . /app/
    WORKDIR /app

    ENV PYTHONPATH=/steamate 

    CMD ["sh", "-c", "python manage.py migrate && python manage.py runserver 0.0.0.0:8000"]

    ```

- 아주 잘 학습한다.

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 1문제
- [x]  콘텐츠 기반 추천시스템 DRF 구현
- [ ]  FE 연결
- [x]  vectorDB appid 기반으로 데이터 수집(트레일러, 백그라운드 이미지, 상세페이지)
- [ ]  ~~url관련(트레일러, 백그라운드 이미지, 상세페이지) DB 추가~~
- [x]  TIL 작성

## 회고
&nbsp;프론트 연결은 조금 더 코드를 손 보고 나서 진행해야지. 오늘 못할줄 알았는데, 그래도 일단 대강 구현은 됐다. 이제 내일의 내가 해결해줄거야...🥺