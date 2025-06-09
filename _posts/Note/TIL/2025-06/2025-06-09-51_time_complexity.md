---
title: "[TIL] 시간 복잡도(Time Complexity)"

categories:
  - TIL
tags:
  - TIL
  - Python
  - 시간 복잡도

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL3.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## 시간 복잡도란?

- 프로그래밍에서 알고리즘의 성능을 평가할 때, 가장 중요하게 보는 지표 중 하나가 시간 복잡도(Time Complexity)
- "입력 크기(n)가 커질 때, 알고리즘이 얼마나 빠르게 느려지는지"를 수학적으로 표현한 것
  - 단순히 코드 실행 시간을 의미하는 것이 아니라, 입력 크기에 따라 실행 횟수가 얼마나 증가하는지를 나타냄
  - 보통 **최악의 경우(Worst Case)** 를 기준으로 계산

<br>

## 자주 등장하는 시간 복잡도 정리

- 입력이 조금만 커져도 성능 차이가 극심하게 발생

| 표기법     | 이름           | 예시 (입력 크기 n = 10, 100, 1000일 때) |
| ---------- | -------------- | --------------------------------------- |
| O(1)       | 상수 시간      | 항상 같은 횟수 (빠름!)                  |
| O(log n)   | 로그 시간      | 이진 탐색                               |
| O(n)       | 선형 시간      | 한 번씩 전부 순회                       |
| O(n log n) | 선형 로그 시간 | 정렬 알고리즘 (merge sort 등)           |
| O(n²)      | 이차 시간      | 중첩 for문                              |
| O(2ⁿ)      | 지수 시간      | 모든 조합 탐색 (재귀)                   |
| O(n!)      | 팩토리얼 시간  | 순열 탐색 (브루트포스)                  |

## 시간 복잡도 계산하는 방법

### 1. 반복문

```python
for i in range(n):       # O(n)
    print(i)
```

- 중첩 루프는 곱하여 계산
  ```python
  for i in range(n):       # O(n)
      for j in range(n):   # O(n)
          print(i, j)      # 총 O(n²)
  ```

### 2. 조건문, 변수 대입, 비교 등

- 조건문, 변수 선언, 단일 연산 등은 대부분 O(1)

```python
x = 3             # O(1)
if x > 0:         # O(1)
    print(x)
```

### 3. 리스트 연산 시간 복잡도

| 연산                 | 시간 복잡도                              |
| -------------------- | ---------------------------------------- |
| `arr[i]`, `len(arr)` | O(1)                                     |
| `arr.append(x)`      | O(1) 평균                                |
| `arr.pop()`          | O(1)                                     |
| `arr.pop(0)`         | O(n) ❗ (앞에서 제거하면 뒤가 다 당겨짐) |
| `arr.insert(0, x)`   | O(n)                                     |
| `' '.join(arr)`      | O(n)                                     |

- 문자열은 불변(immutable)이므로, 덧셈(+)보다 `'join()'`이 더 빠름

### 4. 문자열 연산

- 문자열 결합은 길이 전체를 복사하므로 O(n)

```python
nums = [5, 2, 9, 1]
nums.sort()            # O(n log n)
sorted(nums)           # O(n log n)
```

### 5. 정렬

```python
nums = [5, 2, 9, 1]
nums.sort()            # O(n log n)
sorted(nums)           # O(n log n)
```

- 파이썬의 내장 정렬인 `sorted()` 나 `.sort()`는 **Timsort**를 사용
- 평균/최악 모두 O(n log n)

### 6. 해시 기반 자료구조 (dict, set)

| 연산             | 시간 복잡도 (평균) |
| ---------------- | ------------------ |
| `x in my_set`    | O(1)               |
| `my_dict[k]`     | O(1)               |
| `my_set.add(x)`  | O(1)               |
| `del my_dict[k]` | O(1)               |

- 최악의 경우는 O(n)까지 가능하지만, 거의 발생하지 않음

<br>

## 실전 계산 팁

1. 중첩 반복문은 곱하기
2. 정렬이 들어가면 무조건 n log n
3. 자료구조별 연산 시간 외우기 (list vs set/dict)
4. 문자열 덧셈은 느리다 → join() 사용하기
5. 재귀는 호출 횟수 × 깊이로 계산

<br>

## 📚 예시

### 예시 1: 문자열 압축

```python
def compress_string(s):
    result = []
    count = 1

    for i in range(1, len(s)):    # O(n)
        if s[i] == s[i-1]:
            count += 1
        else:
            result.append(s[i-1] + str(count))  # O(1)
            count = 1
    result.append(s[-1] + str(count))          # O(1)

    compressed = ''.join(result)               # O(n)
    return compressed if len(compressed) < len(s) else s
```

- 총 시간복잡도: O(n)

### 예시 2: K번째로 작은 수 찾기 (heap 사용)

```python
import heapq

def kth_smallest(nums, k):
    heapq.heapify(nums)               # O(n)
    for _ in range(k - 1):            # O(k log n)
        heapq.heappop(nums)           # log n
    return heapq.heappop(nums)        # log n
```

- 총 시간복잡도: O(n + k log n)

<br>

# 🎯 Today’s Goals

- [x] SA문서 : 요구사항 명세서 작성
- [x] Python 알고리즘&자료구조 공부
- [x] 시간 복잡도 공부
- [x] TIL 작성
