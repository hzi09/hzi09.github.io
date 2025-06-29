---
title: "[TIL] 내일배움캠프 1일차_[Python] 가상환경설정(conda)"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - 가상환경
  - conda

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## conda?

- 파이썬 패키지 관리 및 가상환경 관리를 돕는 도구
- 여러 프로젝트에서 서로 다른 패키지 버전을 사용해야 할때 유용!

### 가상환경 만들기

- 가상환경(이름 : pandas_course) 생성

  ```bash
  conda create --name pandas_course
  ```

- 가상환경 활성화 시키기

  - 활성화 시키면 왼쪽에 괄호'(가상환경명)'가 생김!

  ```bash
  conda activate pandas_course
  ```

  ![image](https://i.imgur.com/x2tjen7.png)

- 참고) 가상환경 비활성화 시키기

  ```bash
  conda deactivate
  ```

<br>

## Jupyter notebook에서 가상환경 사용하기

### ipykernel 설치

- 가상환경을 Jupyter Notebook에서 사용하려면 ipykernel 설치가 필요

  ```bash
  pip install ipykernel
  ```

### 가상환경을 Jupyter Notebook에 추가

- 이 명령어를 실행하면 Jupyter Notebook에서 pandas_course라는 이름의 가상환경 선택 가능

  ```bash
  python -m ipykernel install --user --name pandas_course --display-name "pandas_course"
  ```

- Jupyter Notebook에서 새로운 노트북을 열 때, kernel을 pandas_course로 선택

  ![image](https://i.imgur.com/dNBtfhD.png)

<br>
<br>

# 💡Today I Thought

&nbsp; 오늘 애증의 pandas를 다시 만났다. 주피터 노트북에서 많이 사용했었는데, 가상환경을 만들어서 사용하는 것은 처음이라 세팅이 조금 어려웠다. 그래도 해결 완!
