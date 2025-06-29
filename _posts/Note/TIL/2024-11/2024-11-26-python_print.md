---
title: "[TIL] 내일배움캠프 2일차_[Python] print()"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - print()

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## print()

- `print()` 함수는 기본적으로 문자열을 출력하고 줄 바꿈을 함

  ```python
  print("Hello")
  print("World")
  ```

  - 실행 결과

    ```
    Hello
    World
    ```

<br>

## 줄 바꿈 없이 print() 출력

- `print(string)`은 string 문자열을 화면 출력하고, 줄바꿈을 함
- `print(string, end = "")`를 입력하면, 문자열만 출력하고 줄바꿈을 하지 않음
- end가 문자열의 마지막에 추가되는 문자열이며, 입력하지 않으면 기본적으로 `end = “\\n”`

  ```python
  print("Hello", end="")
  print("World")
  ```

  - 실행 결과

    ```
    HelloWorld
    ```

<br>

## 줄 바꿈 대신 다른 문자 출력

- `print()`에 줄 바꿈 문자 대신에 다른 문자를 출력할 수도 있음

  ```python
  print("Hello", end=",")
  print("World", end="!")
  ```

  - 실행 결과

    ```
    Hello,World!
    ```

<br>

## 문자열 중간에 있는 줄 바꿈 문자 제거

- 문자열 중간에 줄바꿈 문자인 \n가 포함될 수 있음
- 이런 경우 replace()를 이용하여 줄 바꿈 문자를 제거 가능

  ```python
  ## 줄바꿈 문자가 포함된 문자열 출력
  str = "Hello \n World!"
  print("first:", str)

  ## 줄바꿈 문자가 제거된 문자열 출력
  str = str.replace("\n", "")
  print("second:", str)
  ```

  - 실행 결과

    ```
    first: Hello
    World!
    second: Hello  World!
    ```

<br>
<br>

# 💡Today I Thought

&nbsp; 오늘 코딩테스트를 하다가 갑자기 print() 함수에서 딱 막혀버렸다. 그냥 print를 사용하기만 했었지, 원하는 형태로 출력하려니까 쉽지 않았다. 그래서 추가 공부를 하며 익혀봤다. 이제 헷갈리지 말자!
