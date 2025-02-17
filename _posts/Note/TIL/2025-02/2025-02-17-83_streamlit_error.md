---
title:  "[TIL] 내일배움캠프 83일차_[Streamlit] ModuleNotFoundError / KeyError 해결과정" 

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
## Today...
- 어제 팀프로젝트용 Streamlit을 만지작거려서 틀 만든 것을 정리된 구조에 넣었더니 에러 발생..
  - 새로 정리된 구조

    ```
    📂 my_project/             # 프로젝트 루트 폴더
    │── main.py                # 앱의 진입점 (메인 페이지)
    │── 📂 pages/              # 여러 개의 페이지를 관리하는 폴더
    │   │── home.py            # 기본 정보를 제공, 앱의 목적 안내 ex) 사용법
    │   │── chat.py            # 챗봇 페이지
    │   └── history.py         # 대화 기록 조회 페이지
    │── 📂 backend/            # 백엔드 로직 (DB, API 등)
    │   │── database.py        # DB 연결 및 관리
    │   │── chatbot.py         # 챗봇 관련 로직
    │   └── utils.py           # 유틸리티 함수
    │── 📂 .streamlit/         # Streamlit 설정 파일
    │   └── secrets.toml       # 환경 변수 (DB, API Key)
    │── requirements.txt       # 설치할 라이브러리 목록
    │── venv                   # 가상환경
    │── .gitignore             # Git 관리 파일
    └── README.md              # 프로젝트 설명
    ```
- 오늘 생긴 오류는 아래의 두 오류 ➡️ 두 개 다 해결 완료!
  - `ModuleNotFoundError: No module named 'backend'`
  - `KeyError: 'st.secrets has no key "OPENAI_API_KEY"'`

<br>

## ModuleNotFoundError
- `backend/chatbot.py`에 챗봇을 사용할 수 있는 함수를 구현하여 `pages/chat.py`에 import하여 사용하려고 하였는데 아래와 같은 에러가 뜸 

    ```bash
    ModuleNotFoundError: No module named 'backend'
    ```

- Module로 아예 인식을 못한다는 뜻 같아서 이리저리 방법을 찾아봄

### 방법1: __init__.py 추가
- `backend`를 패키지로 인식하게 하기 위해서 `backend/__init__.py` 파일을 빈 상태로 추가

    ```
    📂 my_project/             # 프로젝트 루트 폴더
    │── 📂 backend/            # 백엔드 로직 (DB, API 등)
    │   │── __init__.py        
    │   │── database.py        # DB 연결 및 관리
    │   │── chatbot.py         # 챗봇 관련 로직
    │   └── utils.py           # 유틸리티 함수
    ```

- 위와 같은 형태로 만들어줬지만 인식하지 못함

### 방법2: sys.path를 활용
- `sys.path`를 사용하여 `backend` 폴더를 파이썬 모듈 경로에 추가

  ```python
  import streamlit as st
  import sys
  import os

  # backend 폴더 경로를 sys.path에 추가
  sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), "..", "backend")))

  # 이제 backend.chatbot 모듈을 불러올 수 있음
  from chatbot import get_chat_response  # 변경된 import 경로
  ```

- 이 방법도 계속 똑같이 인식하지 못함

### ✅방법3: psycopg2-binary
- 방법을 찾지 못해 시간이 너무 많이 쓰여서 민준튜터님께 도움을 요청하였음
- 그리고 빠르게 해결됨🤣

  ```bash
  pip install psycopg2-binary
  ```

- `psycopg2-binary` 라이브러리를 설치하니까 해결이 되었음
  - 윈도우에서 한번씩 생기는 오류라고는 하는데, chatgpt는 가상환경이 재설정되면서 해결됐을 수도 있다고 함

<br>

## KeyError
- 두번째 에러는 갑자기 잘 불러오던 `OPENAI_API_KEY`를 못 불러오고 있다는 것

  ```bash
  KeyError: 'st.secrets has no key "OPENAI_API_KEY"'
  ```

### ✅방법1: 네임스페이스 설정
- 이 에러는 내가 `toml`에 대한 지식이 없어서 생긴 오류였음
- 처음에는 여기저기 알아보다가 `toml` 코드를 쳐다보다보니 의문이 생김

  ```toml
  [openai]
  OPENAI_API_KEY = "secret_key"
  ```

  - 여기서 저 대괄호(`[]`)에 들어가는건 도대체 뭘까?
    - 검색해보니까 네임스페이스라고 하며 여러개가 충돌할 수도 있기 때문에 관리가 쉽도록 분리해놓는 용도라고 함
- 그래서 지워봄

    ```toml
    OPENAI_API_KEY = "secret_key"
    ```

    - 이렇게 하니까 잘 실행됨
    - 그럼 내가 네임스페이스를 쓰는 방법을 모르는구나..! 싶어서 검색을 했음 

- 찾아보니 네임스페이스도 같이 불러줘야 하는 형태..!
  
  ```python
  # before
  client = OpenAI(api_key=st.secrets["OPENAI_API_KEY"])

  # after
  client = OpenAI(api_key=st.secrets["openai"]["OPENAI_API_KEY"])
  ```

- before의 코드에 `["openai"]` 즉, 네임스페이스를 추가해주니 해결


<br>
<br>


# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 325
- [x]  SQL 코드카타 117
- [x]  Streamlit UI 구현 및 에러 해결
- [x]  TIL 작성

## 회고
&nbsp;오늘은 에러때문에 하루를 다 보냈다🫠 그래도 오늘 안에 다 해결해서 다행...! 내일은 조금 스피드 내서 UI를 만들고 로그인과 회원가입도 구현해야할 것 같다. 첫 팀프로젝트라서 협업하는 github도 어려워서 계속 찾아보면서 진행하고 그래서 조금 더 더딘거 같다. 최종 프로젝트 준비를 빡세게 하는 기분이다🤭