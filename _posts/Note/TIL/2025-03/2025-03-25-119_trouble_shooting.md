---
title:  "[TIL] 내일배움캠프 119일차_[트러블 슈팅] scikit-surprise 설치 오류" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 트러블 슈팅
    - scikit-surprise


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 이슈내용

- 어제까진 잘 되던 Docker compose build가 오늘 파일이 바뀐이후로 또 안됐다.
    
    ```
    7.10 Building wheels for collected packages: scikit-surprise
    67.10   Building wheel for scikit-surprise (pyproject.toml): started
    68.00   Building wheel for scikit-surprise (pyproject.toml): finished with status 'error'
    68.01   error: subprocess-exited-with-error
    68.01
    68.01   × Building wheel for scikit-surprise (pyproject.toml) did not run successfully.
    68.01   │ exit code: 1
    68.01   ╰─> [111 lines of output]
    68.01       /tmp/pip-build-env-4u_i5kzc/overlay/lib/python3.12/site-packages/setuptools/config/_apply_pyprojecttoml.py:82: SetuptoolsDeprecationWarning: `project.license` as a TOML table is deprecated
    68.01       !!
    
    ...
    
    68.01   ERROR: Failed building wheel for scikit-surprise
    68.02 Failed to build scikit-surprise
    68.05 ERROR: Failed to build installable wheels for some pyproject.toml based projects (scikit-surprise)
    ------
    failed to solve: process "/bin/sh -c pip install -r steamate/requirements.txt" did not complete successfully: exit code: 1
    ```
    

- scikit-surprise가 설치가 되지 않는다는 것..

- 처음에는 gcc가 없다고 해서 따로 추가했는데도 안되고, 그 다음에는 이것저것 다 설치했는데도.. 안되는..🥺
- 혹시나 싶어서, 아예 requirement.txt에서 빼서 따로 설치하니까 되는거 아니겠는가..😱
- 그래서 확인하게 된 이유는 가까운 곳에 있었음

## 해결방법

- 새로 생긴 Dockerfile이 wsgi와 asgi로 나뉘었는데 asgi에는 패키지가 없기 때문에 계속 오류가 생겼음

- 해결방법 1 : asgi에도 이걸 추가해준다
    
    ```docker
    RUN apt-get update && apt-get install -y netcat-openbsd \
        libpq-dev \
        postgresql-client \
        build-essential \
        python3-dev \
        libatlas-base-dev \
        gfortran \
        cmake \
        wget \
        && rm -rf /var/lib/apt/lists/*
    ```
    
- 해결방법 2 : 초기 방법처럼 두 파일을 합쳐 사용한다

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 1문제
- [x]  Pickmate 수정
    - [x]  사용자가 가지고 있는 게임 제외하는 함수 추가
    - [x]  게임 플레이 기록이 10개 이하인 유저에 대한 예외처리 추가
- [x]  FE 연결
- [x]  TIL 작성

## 회고
&nbsp;내일 유저테스트라서 부랴부랴 PickMate완성.. 엉엉.. 너무 힘든 하루였다.