---
title:  "[TIL] 내일배움캠프 27일차_[Python] 리스트(List)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Python
    - 리스트

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 0. 리스트
- 순서가 있는 수정가능한 객체의 집합
- 수정, 삭제, 추가가 가능
- list는 대괄호 `[]`로 작성되어지며, 내부원소는 `,`로 구분됨
  
  ```python
  squares = [1, 4, 9, 16, 25]
  type(squares)  # <class 'list'>
  ```


<br>

## 1. 리스트 선언 및 요소 접근

<h3>리스트 선언</h3>

- 파이썬에서 리스트를 생성하는 방법은 `[]`에 자료를 쉼표로 구분해서 입력
- `[]` 내부에 넣는 자료를 **요소(element)**라고 하고 함
  ```python
  int_list = [1, 2, 3, 4]           # int만으로 구성된 리스트
  str_list = ['a', 'b', 'c', 'd']   # str만으로 구성된 리스트
  ```


<h3>요소 접근</h3>

- 리스트 안에 있는 요소에 접근하기 위해서는 `리스트[숫자]`를 사용한다.
  - 여기서 `[]`안에 들어간 숫자를 **인덱스(index)**라고 부름
- 리스트의 요소는 0부터 시작
- 슬라이싱(slicing)도 사용 가능
  ```python
  str_list = ['a', 'b', 'c', 'd']

  str_list[0]   # a
  srt_list[3]   # d
  str_list[1:2] # ['b', 'c']
  ```

- 요소에는 다양하게 접근이 가능
  - 대괄호 안에 음수를 넣어 뒤에서부터 요소 선택 가능(맨 끝 요소가 '-1')
    ```python
    list_a = ['강아지', '고양이', '햄스터', '이구아나']

    list_a[-1] # '이구아나'
    list_a[-4] # '강아지'
    ```
  - 리스트 접근 연산자를 이중으로 사용 가능
    ```python
    list_a = ['강아지', '고양이', '햄스터', '이구아나']

    list_a[3]      # '이구아나'
    list_a[3][2]   # '아'
    ```
  - 리스트 안에 리스트 사용 가능
    ```python
    list_a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

    list_a[0]     # [1, 2, 3]
    list_a[0][0]  # 1
    ```

<br>

## 2. 리스트 연산
- 문자열에 적용할 수 있는 연산자는 리스트에서도 활용 가능

<h3>리스트 연결</h3>

- 문자열 연결 연산자 `+`를 사용하여 두개의 리스트를 연결 가능
  ```python
  list_a = [1, 2, 3, 4]
  list_b = [5, 6, 7]

  list_a + list_b  # [1, 2, 3, 4, 5, 6, 7]
  ```

<h3>리스트 반복</h3>

- 문자열 반복 연산자 `*`를 사용하여 리스트를 반복 가능
  ```python
  list_a = [1, 2, 3, 4]

  list_a * 3  # [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4]
  ```

<h3>리스트 길이</h3>

- `len()` 함수는 괄호 내부에 문자열을 넣으면 글자 수(=길이)를 세어주는 함수
- 리스트에도 `len()`함수를 사용할 수 있으며 괄호 내부에 리스트를 넣으면 요소의 개수를 세어줌
  ```python
  list_list_a = [1, 2, 3, 4]
  
  len(list_a) # 4
  ```

<br>

## 3. 리스트 메서드
- `list.append(x)`
  - 리스트의 끝에 하나의 요소를 추가
    ```python
    my_list = [1, 2, 3]
    my_list.append(4)  # [1, 2, 3, 4]
    ```

- `list.extend(iterable)`
  - 리스트의 끝에 반복 가능한 객체(iterable)의 모든 요소를 추가하여 확장
    ```python
    my_list = [1, 2, 3]
        my_list.extend([4, 5]) # [1, 2, 3, 4, 5]
    ```

- `list.insert(i, x)`
  - 리스트의 지정된 위치에 요소를 삽입
  - 첫 번째 인자 `i`는 삽입될 위치의 **인덱스**를 나타냄
    ```python
    my_list = [1, 2, 3]
    my_list.insert(1, 5)  # [1, 5, 2, 3]
    ```

- `list.remove(x)`
  - 리스트에서 값이 `x`와 같은 **첫 번째 항목**을 삭제
    ```python
    my_list = [1, 2, 3, 2]
    my_list.remove(2)  # [1, 3, 2]
    ```

- `list.pop([i])`
  - 리스트의 지정된 위치의 요소를 제거하고 반환
  - 인덱스 `i`를 지정하지 않으면, 마지막 요소를 제거하고 반환
  - 만약 리스트가 비어있거나 인덱스 범위를 벗어나면 `IndexError` 발생
    ```python
    my_list = [1, 2, 3]
    item = my_list.pop(1)  # 인덱스 1의 항목 제거

    print(item)     # 2
    print(my_list)  # [1, 3]
    ```

- `list.clear()`
  - 리스트의 모든 요소를 제거
    ```python
    my_list = [1, 2, 3]
    my_list.clear()  # []
    ```

- `list.index(x[, start[, end]])`
  - 리스트에서 값이 `x`와 같은 첫 번째 요소의 인덱스를 반환
  - 선택적 인자 `start`와 `end`를 사용하여 검색 범위 제한 가능
  - 반환된 인덱스는 전체 리스트의 시작을 기준으로 계산
  - 값이 존재하지 않으면 `ValueError` 발생
    ```python
    my_list = [1, 2, 3, 2]
    
    # 첫 번째 2의 인덱스
    my_list.index(2)    # 1

    # 인덱스 2부터 검색
    my_list.index(2, 2) # 3
    ```

- `list.count(x)`
  - 리스트에서 값 `x`가 등장하는 횟수를 반환
    ```python
    my_list = [1, 2, 3, 2, 2]

    # 2의 갯수 세기
    my_list.count(2)  # 3
    ```

- `list.sort(*, key=None, reverse=False)`
  - 리스트의 항목을 정렬
  - `reverse` : `True`로 설정하면 내림차순 정렬, 기본값은 `False`로 오름차순
  - 원본 리스트가 변경되며, 새로운 리스트를 반환하지 않음!
    ```python
    my_list = [3, 1, 2]
    my_list.sort()
    print(my_list)  # [1, 2, 3]

    my_list.sort(reverse = True)
    print(my_list)  # [3, 2, 1]
    ```

  - `key` : 정렬 기준을 정의 
    ```python
    words = ["apple", "banana", "cherry", "date"]
    
    # 길이를 기준으로 정렬
    words.sort(key=len)
    print(words)  # ['date', 'apple', 'banana', 'cherry']

    numbers = [3, -6, 1, -10, 4]

    # 절댓값을 기준으로 정렬
    numbers.sort(key=abs)
    print(numbers)  # [1, 3, 4, -6, -10]
    ```

- `list.reverse()`
  - 리스트의 요소들을 반대로 뒤집어 줌
  - `list.sort()`와 마찬가지로 원본 리스트가 변경되며, 새로운 리스트를 반환하지 않음!
    ```python
    my_list = [1, 2, 3]
    my_list.reverse()
    rint(my_list)  # [3, 2, 1]
    ```

- `list.copy()`
  - 리스트의 복사본을 봔환
    ```python
    my_list = [1, 2, 3]
    new_list = my_list.copy()
    print(new_list)  # [1, 2, 3]
    ```

<br>
<br>

# 💡Today I Thought

&nbsp; 리스트를 많이 쓰지만, 그때그때 검색해보면서 공부를 하다보니 모르는 것이 많았던 것 같아서 다시 한번 정리를 해보았다. 확실히 정리하고 나니까 이해가 더 잘된다.

## 오늘의 체크리스트
- [x] 백준 코딩테스트 2문제
- [x] 클래스 복습
- [x] 리스트 복습
- [x] TIL 작성

## 회고
&nbsp; 오늘은 강아지들이랑 일정이 있어서 나갔다 오느라고 공부를 거의 못했다. 그래도 최근에 백준 코딩테스트를 할 때마다 못풀겠어서 다른 문제로 넘어가서 문제를 풀고 그랬는데, 조금만 생각해도 문제를 풀 수 있게 되었다. 조금 성장해버린~

&nbsp; 내일도 일정이 있어서 오전이랑 저녁에만 공부할 수 있긴한데, 그래도 코딩테스트 열심히 해야겠다. 내일은 머신러닝도 살짝 해봐야지.