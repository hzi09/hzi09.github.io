---
title:  "[TIL] 내일배움캠프 53일차_[Python] any(), all() 함수" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Python


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## any()와 all() 함수
- any()와 all() 함수는 Python에서 제공하는 내장 함수
- 주로 조건을 만족하는지를 확인하거나 데이터를 간단히 검사하는 데 사용
- 이 두 함수는 iterable(반복 가능한 객체)을 입력으로 받아, 조건을 만족하는지 여부를 각각 확인


### any() 함수

1. 정의
- `any()` 함수는 iterable의 
  - 요소 중 하나라도 참(True)인 값이 있으면 `True`를 반환
  - 모두 거짓(False)일 경우 `False`를 반환

1. 사용법
    ```python
    any(iterable)
    ```
- iterable: 리스트, 튜플, 문자열 등 반복 가능한 객체.

1. 동작 원리
- iterable의 각 요소를 순회하며, 값이 True로 평가되는 요소를 찾음
- 첫 번째 True를 만나면 즉시 True를 반환
- iterable에 모든 요소가 False이면 False를 반환

1. 예제
    ```python
    # 리스트에서 하나라도 참인 값이 있는 경우
    print(any([False, False, True]))  # 출력: True

    # 모두 거짓인 경우
    print(any([False, 0, ""]))       # 출력: False

    # 빈 iterable의 경우
    print(any([]))                   # 출력: False

    # 조건에 따른 사용 예
    numbers = [0, 1, 2, 3, 4]
    print(any(num > 3 for num in numbers))  # 출력: True
    ```

### all() 함수

1. 정의
- all() 함수는 iterable의 
  - 모든 요소가 참(True)일 경우에만 `True`를 반환
  - 하나라도 거짓(False)인 값이 있으면 `False`를 반환

1. 사용법
    ```python
    all(iterable)
    ```
- iterable: 리스트, 튜플, 문자열 등 반복 가능한 객체.

1. 동작 원리
- iterable의 각 요소를 순회하며, 값이 False로 평가되는 요소를 찾음
- 첫 번째 False를 만나면 즉시 False를 반환
- iterable에 모든 요소가 True이면 True를 반환

1. 예제
    ```python
    # 리스트에서 모든 값이 참인 경우
    print(all([True, 1, "hello"]))   # 출력: True

    # 하나라도 거짓인 경우
    print(all([True, 0, "hello"]))   # 출력: False

    # 빈 iterable의 경우
    print(all([]))                   # 출력: True

    # 조건에 따른 사용 예
    numbers = [2, 4, 6, 8]
    print(all(num % 2 == 0 for num in numbers))  # 출력: True
    ```

## any()와 all() 비교
- any()와 all() 비교표

    | 함수        | 동작                        | 반환값                       |
    | :---------: | :-------------------------: | :--------------------------: |
    | `any()`     | 하나라도 참이면 `True` 반환 | 모든 요소가 거짓이면 `False` |
    | `all()`     | 모두 참이어야 `True` 반환   | 하나라도 거짓이면 `False`    |



- 예제 비교
    ```python
    values = [0, 1, 2]

    print(any(values))  # 출력: True (1, 2는 참이므로)
    print(all(values))  # 출력: False (0이 거짓이므로)
    ```

<br>

## 사용법
### 1. 조건 확인
- 데이터 중 특정 조건을 만족하는 값이 있는지 확인할 때 `any()`를 사용
- 모든 값이 조건을 만족하는지 확인할 때 `all()`을 사용

### 2. 입력 검증
```python
user_inputs = ["name", "email", ""]

if any(input == "" for input in user_inputs):
    print("모든 입력값을 채워주세요.")

if all(input.isalpha() for input in user_inputs if input):
    print("모든 입력값이 유효합니다.")
```

### 3. 중단 로직
- `any()`와 `all()`은 단축 평가(short-circuit evaluation)를 지원하므로, 불필요한 계산을 줄일 수 있음

    ```python
    conditions = [True, False, True]

    if any(conditions):
        print("하나 이상의 조건이 참입니다.")

    if all(conditions):
        print("모든 조건이 참입니다.")
    else:
        print("하나 이상의 조건이 거짓입니다.")
    ```

<br>

## 요약
- `any()`: 하나라도 참이면 True
- `all()`: 모두 참이어야 True
- 두 함수 모두 iterable을 순회하며, 간단한 조건 확인과 검증에 유용
- `any()`와 `all()`은 단순하지만 강력한 도구로, 다양한 상황에서 활용할 수 있음

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 201-210
- [x] SQL 코드카타 76
- [x] 백준 코딩테스트 1문제
- [x] TIL 작성

## 회고
&nbsp; 코딩테스트 하면서 처음 알게된 any와 all함수 잘 쓰면 코테에서 많이 사용할 수 있을 것 같다👀 오늘 공부 야무지게 하려고 했는데, 체력 이슈로 완벽하게 늦잠자고 강아지들이랑 놀다보니 하루가 다 가버렸다. 내일은 좀 공부에 몰입헤야지🥲🥲