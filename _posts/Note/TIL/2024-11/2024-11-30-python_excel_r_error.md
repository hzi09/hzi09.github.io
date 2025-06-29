---
title: "[TIL] 내일배움캠프 6일차_[Python] 엑셀파일(.xlsx) 읽기 에러"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - .xlsx

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

> 사용환경 : Pycharm <br>
> pandas : ver.2.2.3

## 문제

- 개인과제 문제를 풀려고 엑셀파일을 불러오기를 실행하였다.

  ```python
  import pandas as pd

  df_excel = pd.read_excel('관서별 5대범죄 발생 및 검거.xlsx')
  print(df_excel.head())
  ```

- 바로 에러가 떠버렸다.

  ```bash
  ImportError: Missing optional dependency 'openpyxl'. Use pip or conda to install openpyxl.
  ```

  - 처음에는 파일 위치를 잘못한줄 알고 확인했더니, 파일 위치는 맞는데 싶어서 맨 마지막 줄에 보니 ImportError!

<br>

## 해결 방법

- openpyxl이 없어서 생긴 문제이므로 터미널 창에서 conda 혹은 pip으로 깔아줌

  ```bash
  pip install openpyxl
  ```

  ![image](https://i.imgur.com/MxF5r73.png)

- 다시 불러오면 잘 된다.

  ![image](https://i.imgur.com/9Eu1455.png)

<br>

# 💡Today I Thought

&nbsp;에러가 많이 나는 것도 성장의 요소의 하나라고 했다..(아마두) 에러날때마다 기록해서 모아두면 나중에 또 쓸모가 있을 것 같아서 오늘의 TIL은 에러 해결로 결정했다.
