---
title: "[TIL] 내일배움캠프 5일차_[NumPy] NumPy 기초"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - NumPy

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## NumPy

### 1. NumPy란?

- **Numerical Python**의 줄임말로, **과학 계산**에 강력한 성능을 제공하는 파이썬 라이브러리
- 다차원 배열 객체인 **ndarray**와 배열을 효율적으로 처리할 수 있는 다양한 함수들을 제공
- 데이터 분석, 머신러닝, 딥러닝에서 **기초가 되는 라이브러리**로, 판다스와 함께 자주 사용

### 2. NumPy 설치

```bash
pip install numpy
```

### 3. Numpy 사용법

```python
import numpy as np
```

<br>

## 배열 생성

### 1. 배열(array) 생성

- NumPy에서 가장 기본적인 데이터 구조는 배열
- NumPy 배열은 동일한 타입의 데이터를 담는 다차원 배열

```python
# 1차원 배열 생성
arr1 = np.array([1,2,3,4,5])

# 2차원 배열 생성
arr2 = np.array([[1, 2, 3],[4, 5, 6]])

# 3차원 배열 생성
arr3 = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
```

### 2. 배열 크기

- 배열의 크기
  - 1차원 : (칸, )
  - 2차원 : (행, 열)
  - 3차원 배열 : (층, 행, 열)
- shape 를 사용하여 확인 가능

```python
print(arr1.shape) # (5,)
print(arr2.shape) # (2, 3)
print(arr3.shape) # (2, 2, 2)
```

<br>

## 배열 연산

### 1. 기본 연산

- NumPy 배열은 다른 배열 또는 스칼라와의 연산을 지원

  - 스칼라 연산

    ```python
    arr = np.array([1, 2, 3, 4, 5])

    # 각 원소에 2를 더하기
    arr_add = arr + 2 #[3 4 5 6 7]

    # 각 원소에 2를 곱하기
    arr_mul = arr * 2 #[ 2  4  6  8 10]
    ```

- 다른 배열과의 연산
- Numpy 배열의 연산은 배열의 원소별(element-wise)로 이루어짐

  - 행렬의 곱셈이 아님!!

  ```python
  arr1 = np.array([1,4,9])
  arr2 = np.array([1,2,3])

  arr_a = arr1 + arr2 #[ 2  6 12]
  arr_b = arr1 - arr2 #[0 2 6]
  arr_c = arr1 * arr2 #[ 1  8 27]
  arr_d = arr1 / arr2 #[1. 2. 3.]
  ```

### 2. 배열 간의 연산 함수

```python
arr = np.array([1,2,3])

# 합계
sum_arr = np.sum(arr) #6

# 평균
mean_arr = np.mean(arr) #2.0

# 최소값
min_arr = np.min(arr) #1

# 최대값
max_arr = np.max(arr) #3
```

<br>

## 배열 인덱싱과 슬라이싱

> 💡배열의 인덱싱과 슬라이싱은 Python 리스트의 인덱싱과 슬라이싱과 매우 유사

### 1. 인덱싱(Indexing)

- 배열의 특정위치에 접근

```python
arr = np.array([10, 20, 30, 40, 50])


# 첫 번째 원소
arr_srt = arr[0] # 10

# 마지막 원소
arr_end = (arr[-1]) # 50
```

### 2. 슬라이싱(Slicing)

- 배열의 일부분을 잘라냄

```python
arr = np.array([10, 20, 30, 40, 50])

# 두 번째부터 네 번째 원소까지
sliced_arr = arr[1:4] #[20 30 40]
```

### 3. 다차원 배열의 인덱싱 및 슬라이싱

- 다차원 배열의 경우, 콤마를 사용하여 접근 가능

```python
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# 특정 원소 접근 (2행 3열)
print(arr2d[1, 2])  # 6

# 슬라이싱 (2행까지, 2열까지)
sliced_arr2d = arr2d[:2, :2] # [[1 2]
                             #  [4 5]]
```

<br>

# 💡Today I Thought

&nbsp;오랜만에 만나는 Numpy 복습! 초반이라 아직은 쉬운데 뒤로 가는게 조금 두렵기도 하구.. 함수를 빨리 공부해서 예제를 다양하게 풀어보면서 익히는 과정이 필요할 것 같다.이번 일주일 너무 호다닥 지나갔다.. 주말에는 조금 쉬엄쉬엄 공부해야지!
