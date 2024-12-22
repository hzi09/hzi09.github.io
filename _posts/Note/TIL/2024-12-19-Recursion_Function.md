---
title:  "[TIL] 내일배움캠프 25일차_[Python] 재귀함수(Recursion Function)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 내배캠
    - 스파르타내일배움캠프
    - Python
    - 재귀함수

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 0. 재귀호출🤔

- 함수 안에서 함수 자기자신을 호출하는 방식을 재귀호출(recursive call)이라고 함
- 일반적인 상황에서는 잘 사용하지 않지만, 알고리즘을 구현할 때 매우 유용하게 사용 됨!
- 보통 알고리즘에 따라서 반복문으로 구현한 코드보다 재귀호출로 구현한 코드가 좀 더 직관적이고 이해하기 쉬운 경우도 있음

<br>

## 1. 재귀호출 사용

```python
def hello():
    print('Hello, world!')
    hello()
 
hello()
```

- 이렇게 사용하게 되면 문자열이 무한 출력되다가 에러 발생!
- 파이썬에서 최대 재귀 깊이(maximum recursion depth)가 1,000으로 정해져 있기 때문!
- 최대 재귀 깊이를 초과하면 RecursionError가 발생

### 재귀호출에 종료조건 만들어주기

- 재귀호출을 사용하려면 반드시 종료조건이 필요!
    
    ```python
    def hello(count):
        if count == 0:  # 종료 조건을 만듦. count가 0이면 다시 hello 함수를 호출하지 않고 끝냄
            return
    
        print('Hello, world!', count)
    
        count -= 1  # count를 1 감소시킨 뒤
        hello(count)  # 다시 hello에 넣음
    
    hello(5)  # hello 함수 호출
    ```
- 결과값
    ```
    Hello, world! 5
    Hello, world! 4
    Hello, world! 3
    Hello, world! 2
    Hello, world! 1
    ```

<br> 

## 2. 재귀함수 사용해보기

### 팩토리얼

- 먼저 factorial 함수를 만들 때 매개변수 n을 지정해줌
- 팩토리얼은 1~n까지의 곱을 구하는 문제이지만, n부터 역순으로 1씩 감소하면서 재귀호출을 하고 n이 1이 되었을 때 재귀호출 중단
    
    ```python
    def factorial(n):
        if n == 1:      # n이 1일 때
            return 1    # 1을 반환하고 재귀호출을 끝냄
    ```
    
- factorial 함수의 핵심은 반환값(return)!
    - 계산 결과가 즉시 구해주는 것이 아니고 재귀호출로 n-1을 계속 전달하다가 n이 1이 되면 1을 반환하면서 n과 곱하고 다시 결과값을 반환
    - 그 뒤 n과 반환된 결과값을 곱하여 다시 반환하는 과정을 반복

```python
return n * factorial(n - 1)    # n과 factorial 함수에 n - 1을 넣어서 반환된 값을 곱함
```

- 이런식으로 진행된다.
    
    ![image](https://github.com/user-attachments/assets/625d6bc2-3c8c-4baa-bb4a-3cd11b6269c9)
    

### 회문 판별

: 다음 소스 코드를 완성하여 문자열이 회문인지 판별하고 결과를 True, False로 출력되게 만드세요. 여기서는 재귀호출을 사용해야 합니다.

- 문자열이 회문인지 판단할 때에는 종료 조건이 2개!
    - `word`가 한 글자라면 `True` 반환
    - `word`의 첫 글자와 마지막 글자가 다르면 `False` 반환
    - 맨 앞글자와 맨 뒷글자를 지우면서 반환되다가 word가 2미만이 되면 True를 리턴한다.

    ```python
    def palindrome(word):
        if len(word) < 2 :
            return True
        if word[0] != word[-1] :
            return False
        return palindrome(word[1:-1])
    ```

<br>
<br>


### ✍️스탠다드반 과제로 풀어본 재귀함수 문제

#### 91. 1부터 n까지의 합을 계산하는 재귀함수

```python
def sum_number(n):
    if n <= 1:
        return n
    return n + sum_number(n-1)
```

#### 92.숫자 리스트를 받아 재귀적으로 요소의 합을 계산하는 함수

```python
def sum_numbers(numbers):
        if not numbers :
                return 0
        return numbers[0] + sum_numbers(numbers[1:])
```

#### 93. 숫자 리스트를 받아 재귀적으로 최대 값을 찾는 함수

```python
def number_max(numbers):
    if len(numbers) == 1 :
        return numbers[0]
    return max(numbers[0], number_max(numbers[1:]))
```

#### 94. 숫자를 입력 받아 재귀적으로 정렬하는 함수

```python
def number_sort(number):
    n_list = [int(num) for num in str(number)]

    if len(n_list) <= 1 :
        return n_list

    min_num = min(n_list)
    n_list.remove(min_num)

    return [nim_num] + number_sort(int(''.join(map(str, n_list))))
```
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 23 ~ 25번
- [x]  SQL 코드카타 35 ~ 36번
- [x]  스탠다드반 과제
- [x]  프로그래머스 Day 21
- [x]  백준 코딩테스트 1문제
- [x]  TIL 작성

## 회고
&nbsp; 오늘은 특강이 하나도 없는 날이라서 할 일을 제시간에 다 끝냈다! 오예! 정처기 공부도 해야하지만,, 오늘은 대체로 코딩테스트도 막힘없이 풀렸고(코드가 더러워서 조금 손을 봐야하긴 하겠지만), 집중도 엄청 잘되서 10시간 이상을 오로지 공부에만 집중했다. 중간에 스윗미가 끝난지도 모르고 공부를 해버린,,🫠

&nbsp; 내일은 특강이 있는 날이기는 하지만, 개인과제를 위한 머신러닝 공부를 시작해야할 것 같다. 이번 주 주말에도 약속이 풀이라서.. 다음주 주말까지는 과제를 끝낸다는 생각으로 공부를 해야할듯..🧐