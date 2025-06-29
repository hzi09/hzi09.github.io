---
title: "[TIL] 내일배움캠프 3일차_[Python] input() / sys.stdin.readline()"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - input()
  - sys.stdin.readline()

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## input()

- 사용자의 입력을 문자열로 받아오는 파이썬 내장함수

  ```python
  a = input() # 안녕하세요.
  print("입력한 값을 받기 : ", a)
  ```

  - 실행 결과

    ```
    안녕하세요.
    입력한 값을 받기 : 안녕하세요.
    ```

<br>

## sys.stdin.readline()

```python
import sys

a = sys.stdin.readline()
print("입력한 값을 받기 : ", a)
```

- 실행 결과

  ```
  안녕하세요.
  입력한 값을 받기 : 안녕하세요.
  ```

<br>

## 왜 sys.stdin.readline()가 더 빠를까?

- 내부적으로 C라이브러리를 사용
  - `sys.stdin.readline()`은 내부적으로 C라이브러리를 사용하여 입력을 읽어옴
  - 인터프리터 언어인 python 보다는 컴파일 언어인 C가 메모리를 접근하는데 있어 더 빠름!
- 개행 문자 처리
  - `sys.stdin.readline()` 은 입력 라인의 끝에 있는 개행 문자(’\n’)을 포함해서 읽어옴
  - 필요하다면 개행 문자를 직접 제거해야함 `rstrip()`
- 개행 문자를 처리하지 않는다는 점에서 더 빠름!
  - `input()`은 개행 문자를 제거하는 과정이 포함되어 있음
  - 입력이 많지 않으면 굳이 `sys.stdin.readline()`를 사용하지 않는 것이 좋음

### 문제 풀어보기

[[백준][Python] 15552. 빠른 A+B](https://hzi09.github.io/python_boj/python_15552/)

```python
import sys

t = int(input())

for i in range(t) :
    a, b = map(int, sys.stdin.readline().split())
    print(a + b)
```

<br>

# 💡Today I Thought

&nbsp; 백준 숏코드를 한번씩 보면 이 문법이 있어서 뭔가 했더니, 빠르게 하려고 사용한다니..! 이런게 있는지도 모르게 시간 초과나면 엉엉 울면서 조금 더 빠르게 돌려보려고 노력했던 과거들이 스쳐지나간다.

&nbsp;오늘은 라이브러리 강의도 드디어 다 들었다! 조금 복습을 하고 실제 데이터로 실습도 해봐야지. 그래도 배웠으니 예전에 회사에서 썼던 코드도 분석해봐야겠다🧐
