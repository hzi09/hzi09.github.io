---
title: "[TIL] 내일배움캠프 4일차_[NumPy] 브로드캐스팅"

categories:
  - TIL
tags:
  - TIL
  - 내일배움캠프
  - Python
  - NumPy
  - 브로드캐스팅

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## 1. 배열의 크기

- 1차원 : (칸, )
- 2차원 : (행, 열)
- 3차원 : (층, 행, 열)

![image](https://i.imgur.com/GSBLoiK.png)

## 2. 브로드캐스팅?

- NumPy에서는 배열 간의 연산을 매우 효율적으로 수행 가능
- 특히 브로드캐스팅(Broadcasting) 기능은 크기가 다른 배열 간의 연산을 가능하게 함
- 브로드캐스팅의 조건
  - 원소가 하나인 배열은 어떤 배열이나 가능
  - 하나의 배열이 1차원 배열이거나 차원의 짝이 맞을 때 가능

### 예시 1

```python
arr1 = np.array([1, 2])              # np.shape(arr1) >> (2,)
arr2 = np.array([[1, 2], [2, 3]])  # np.shape(arr2) >> (2, 2)

np.add(arr1, arr2) # [2, 4],
                    # [3, 5]
```

### 예시 2

```python
arr1 = np.array([[2], [3], [4]])                    # np.shape(arr1) >> (3, 1)
arr2 = np.array([[1, 2, 3], [2, 3, 4], [3, 4, 5]])   # np.shape(arr2) >> (3, 3)
```

<br>

# 💡Today I Thought

&nbsp;Numpy를 공부하면서 브로드캐스팅 부분에서 꽉 막혀버렸다. 튜터님께 help를 하여서 이해까지 완료 하였다. 일단 내가 헷갈려했던 부분이 배열의 크기 부분이었다.(기초가 모자랐다는 소리..)

&nbsp;이해가 잘 안되서 그림으로 그려가면서 공부를했다. 그림처럼 짝이 맞아야 연산이 가능하다. 행렬처럼 생각해서 조금 더 어렵게 생각했던 것 같다.

![image](https://i.imgur.com/8T8AUI9.png)
