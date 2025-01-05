---
title:  "[TIL] 내일배움캠프 41일차_[Algorithm] 유클리드 호제법(Euclidean algorithm)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Algorithm
    - 유클리드 호제법


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 유클리드 호제법이란?

- 유클리드 호제법(Euclidean Algorithm)은 두 정수의 **최대공약수(GCD, Greatest Common Divisor)**를 효율적으로 구하는 방법
- 기원은 고대 그리스의 수학자 유클리드가 제안한 알고리즘으로, 수학적 원리는 다음과 같음

### 알고리즘 원리

1. 큰 수를 작은 수로 나누는 MOD 연산을 수행
2. 앞 단계에서의 작은 수와 MOD 연산 결괏값(나머지)으로 MOD 연산을 수행
3. 단계 2를 반복하다가 나머지가 0이 되는 순간의 작은 수가 최대공약수


- ex. 270과 192의 최대공약수를 유클리드 호제법으로 찾아보기
    
    ![image](https://github.com/user-attachments/assets/fb800618-5efa-4ab4-85a4-b9a121cbdd42){: width="35%" height="35%"}
    
- 270과 192의 최대 공약수는 **6**

### Python 코드

<h4> 재귀 방식 </h4>

- 재귀 방식은 자기 자신을 호출하는 함수를 이용해 유클리드 호제법을 구현한 방법
- 함수를 반복 호출하면서 a와 b의 값을 좁혀가고, 종료 조건에 도달하면 결과를 반환
```python
def gcd_recursive(a, b):
    # 종료 조건: b가 0이면 a가 최대공약수
    if b == 0: 
        return a
    # b와 a를 b로 나눈 나머지로 다시 호출
    return gcd_recursive(b, a % b)  
```

- 재귀 방식의 특징
  - 코드가 간결하고 읽기 쉬움
  - 함수 호출이 많아지면 스택 메모리 사용량이 증가할 수 있으므로, 입력 값이 매우 클 경우 반복문 방식을 권장


<h4> 반복문 방식 </h4>

- 반복문 방식은 while 루프를 사용하여 동일한 계산을 수행
- 재귀 호출 대신 변수의 값을 직접 갱신하면서 반복문으로 종료 조건에 도달할 때까지 실행
```python
def gcd_iterative(a, b):
    while b != 0:  # b가 0이 될 때까지 반복
        a, b = b, a % b  # a에 b를, b에 a % b를 할당
    return a  # b가 0일 때 a가 최대공약수
```

- 반복문 방식의 특징
  - 재귀 호출을 사용하지 않으므로 메모리 부담이 적음
  - 입력 값이 큰 경우에도 안정적으로 작동



### 전체 코드와 활용 예시

```python
# 재귀 방식
def gcd_recursive(a, b):
    if b == 0:
        return a
    return gcd_recursive(b, a % b)

# 반복문 방식
def gcd_iterative(a, b):
    while b != 0:
        a, b = b, a % b
    return a

# 테스트 예시
a, b = 56, 98
print(f"GCD({a}, {b}) [재귀 방식]: {gcd_recursive(a, b)}")
print(f"GCD({a}, {b}) [반복문 방식]: {gcd_iterative(a, b)}")
```

- 출력 결과
    ```
    GCD(56, 98) [재귀 방식]: 14
    GCD(56, 98) [반복문 방식]: 14
    ```

### 더 알아보기 : 최소공배수

- 유클리드 호제법으로 구한 최대공약수를 이용해 최소공배수를 구할 수 있음

```python
# 최소공배수 계산
def lcm(a, b):
    return a * b // gcd_iterative(a, b)  # 최대공약수 활용

# 테스트 예시
print(f"LCM({a}, {b}): {lcm(a, b)}")
```

- 실행 결과
    ```
    LCM(56, 98): 392
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 6문제
- [x] SQL 코드카타 2문제
- [x] 장고 기초 강의 듣기 10-14강
- [x] 백준 문제 2문제
- [x] TIL 작성 

## 회고
&nbsp; 코딩테스트 하면서 한번씩 만나게 되는 알고리즘들도 정리를 해볼까 했는데, 최근에 최소공배수, 최대공약수 관련된 코딩테스트가 많이 나온 겸 유틀리드 호제법을 정리했다. 아직도 잘 모르겠지만..😫 재귀함수 부분은 아직 어려운 것 같다. 조금 더 공부가 필요한 부분..