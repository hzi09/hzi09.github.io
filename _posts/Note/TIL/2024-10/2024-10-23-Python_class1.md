---
title:  "[TIL] 내일배움캠프 사전캠프 3일차_[Python] 강의 1주차" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Python

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL1.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## 0. Jupyter Notebook 실행법

1. Windows에서 'cmd'를 입력하여 명령 프롬프트 실행
2. 'jupyter notebook'을 입력하여 실행
- 안될경우 폴더의 위치 확인 필요
  - 상위 폴더로 이동하는 명령어 'cd ..'
  - 하위 폴더로 이동하는 명령어 'cd ./ 폴더명' (./ 생략가능)

## 1. 변수

<h3> 변수 </h3>

- 데이터를 저장하는 공간
- 값을 저장하고 그 값을 꺼내 사용
  ```python
  a = 10
  b = 'banana'

  # 값을 꺼내서 사용하기
  print(a)  # 10
  print(b)  # banana
  ```

<h3> 변수 선언과 할당 </h3>

- 변수를 선언할 때 별도의 키워드를 사용하지 않고, 사용하고 싶은 이름으로 선언
- `=` 기호를 사용하여 변수를 선언하고 값을 할당
- ⭐할당 연산자 `=`의 의미
  - 연산자는 수학의 등호와 다름
  - 컴퓨터에서 `=`를 "같다"라는 의미가 아닌 **"할당하다"**라는 의미로 해석

<h3> 변수 이름 규칙 </h3>

- 문자(A-Z, a-z), 숫자(0-9), 밑줄(_)만 사용 가능
  - 숫자로 시작X
    - ex. 1st_place(❌), place_1st(⭕)
  - 대소문자 구분
    - ex. Age, age, AGE는 모두 다른 변수로 인식
  - 파이썬의 예약어는 변수 사용 불가
    - ex. for, if, class 등
- 의미를 알기 쉽게, 규칙에 맞게 이름을 짓는 것이 중요
  ```python
  x = 10         # 나쁜 예: 의미를 알기 어려움
  user_age = 10  # 좋은 예: 변수의 역할을 알기 쉬움
  ```

<h3> 여러 번수에 한 번에 값 할당 </h3>

- 동시에 값 할당
  - Python에서는 여러 변수에 동시에 값을 할당 가능
  ```python
  a, b, c = 1, 2, 3
  ```
- 같은 값 할당
  - 여러 변수에 동일한 값 할당
  ```python
  x = y = z = 100
  ```


<h3> 메모리 관리 </h3>

- 변수의 범위
  - 변수는 어디에서 선언되었는지에 따라 접근할 수 있는 범위가 달라지며, 이 범위를 **스코프(Scope)**라 함
- 변수의 스코프
  - 전역 변수(Global Variable) : 프로그램 전체에서 접근할 수 있는 변수
  - 지역 변수(Local Variable) : 특정 코드 블록이나 함수 내에서만 접근할 수 있는 변수
  
  ```python
  def greet():
       message = "Hello" # 지역 변수
       print(message)

  greet()
  print(message)   # 에러 발생: 'message'는 함수 내에서만 사용 가능
  ```

<br>

## 2. 연산자

<h3> 산술 연산자(Arithmetic Operators) </h3>

- 기본적인 수학 연산을 수행 
  
  | 연산자 |   기능   |  예시  | 결과 |
  |:------:|:--------:|:------:|:----:|
  |    +   |   덧셈   |  3 + 2 |   5  |
  |    -   |   뺄셈   |  5 - 2 |   3  |
  |    *   |   곱셈   |  4 * 3 |  12  |
  |    /   |  나눗셈  | 10 / 2 |  5.0 |
  |    %   |  나머지  |  7 % 3 |   1  |
  |   **   | 거듭제곱 | 2 ** 3 |   8  |
  |   //   |    몫    | 7 // 3 |   2  |

  ```python
  a = 10
  b = 3

  print(a + b) # 13
  print(a - b) # 7
  print(a * b) # 30
  print(a / b) # 3.3333...
  print(a % b) # 1
  print(a ** b) # 1000
  print(a // b) # 3
  ```

<h3> 비교 연산자(Comparison Operators) </h3>

- 비교 연산자는 두 값을 비교하여 참(True) 또는 거짓(False)을 반환
  
  | 연산자 |   기능   |  예시  | 결과 |
  |:------:|:--------:|:------:|:----:|
  |    +   |   덧셈   |  3 + 2 |   5  |
  |    -   |   뺄셈   |  5 - 2 |   3  |
  |    *   |   곱셈   |  4 * 3 |  12  |
  |    /   |  나눗셈  | 10 / 2 |  5.0 |
  |    %   |  나머지  |  7 % 3 |   1  |
  |   **   | 거듭제곱 | 2 ** 3 |   8  |
  |   //   |    몫    | 7 // 3 |   2  |

  ```python
  x = 10
  y = 5
  ​
  print(x == y)  # False
  print(x != y)  # True
  print(x > y)   # True
  print(x < y)   # False
  print(x >= y)  # True
  print(x <= y)  # False
  ```

  ⭐ ==연산자와 =연산자 헷갈리지 않도록 주의!
   == 연산자는 "같다"는 의미
   = 연산자 "할당"의 의미
  {: .notice--info} 


<h3> 논리 연산자(Logical Operators) </h3>

- 논리 연산자는 논리값(True, False)을 결합하여 새로운 논리값을 반환
- 논리식을 표현할 때 사용

  | 연산자 |    기능   |  예시  | 결과 |
  |:------:|:---------:|:------:|:----:|
  |   and  | 값이 같음 | 3 == 3 | True |
  |   or   | 값이 다름 | 3 != 4 | True |
  |   not  |     큼    |  5 > 2 | True |

  ```python
  a = True
  b = False

  print(a and b) # False
  print(a or b)  # True
  print(not a)   # False
  ```


<h3> 대입 연산자(Assignment Operators) </h3>

- 대입 연산자는 변수에 값을 할당할 때 사용
- 기본적인 = 외에도 여러 복합 대입 연산자가 있음

  | 연산자 |          기능         |   예시  |    결과    |
  |:------:|:---------------------:|:-------:|:----------:|
  |    =   |        값 할당        |  x = 5  |    x = 5   |
  |   +=   |      더한 후 할당     |  x += 3 |  x = x + 3 |
  |   -=   |       뺀 후 할당      |  x -= 3 |  x = x - 3 |
  |   *=   |      곱한 후 할당     |  x *= 2 |  x = x * 2 |
  |   /=   |      나눈 후 할당     |  x /= 2 |  x = x / 2 |
  |   %=   | 나머지를 구한 후 할당 |  x %= 2 |  x = x % 2 |
  |   **=  |    거듭제곱 후 할당   | x **= 2 | x = x ** 2 |
  |   //=  |   몫을 구한 후 할당   | x //= 2 | x = x // 2 |


<h3> 비트 연산자(Bitwise Operators) </h3>

- 비트 연산자는 이진수(bit) 수준에서 연산을 수행

  | 연산자 |             기능            |  예시  | 결과 |
  |:------:|:---------------------------:|:------:|:----:|
  |    &   |           비트 AND          |  5 & 3 |   1  |
  |   \|   |           비트 OR           | 5 \| 7 |   7  |
  |    ^   |           비트 XOR          |  5 ^ 3 |   6  |
  |    ~   |       비트 NOT (보수)       |   ~5   |  -6  |
  |   <<   |   왼쪽 시프트 (Left Shift)  | 5 << 1 |  10  |
  |   >>   | 오른쪽 시프트 (Right Shift) | 5 >> 1 |   2  |

  ```python
  a = 5         # 이진수로 101
  b = 3         # 이진수로 011

  print(a & b)  # 1 (이진수 001)
  print(a | b)  # 7 (이진수 111)
  print(a ^ b)  # 6 (이진수 110)
  print(~a)     # -6 (이진수 보수)
  print(a << 1) # 10 (이진수 1010)
  print(a >> 1) # 2 (이진수 010)
  ```

<h3> 멤버십 연산자(Membership Operators) </h3>

- 멤버십 연산자는 특정 값이 시퀀스(문자열, 리스트, 튜플 등)에 속해 있는지 확인

  | 연산자 |                   기능                  |        예시        | 결과 |
  |:------:|:---------------------------------------:|:------------------:|:----:|
  |   in   |    시퀀스에 값이 포함되어 있는지 확인   |   "a" in "apple"   | True |
  | not in | 시퀀스에 값이 포함되어 있지 않은지 확인 | "b" not in "apple" | True |

  ```python
  fruits = ["apple", "banana", "cherry"]

  print("apple" in fruits) # True
  print("grape" not in fruits) # True
  ```

<h3> 식별 연산자(Identity Operators) </h3>

- 식별 연산자는 두 변수가 동일한 객체를 가리키는지 확인

  | 연산자 |                  기능                 |    예시    |      결과     |
  |:------:|:-------------------------------------:|:----------:|:-------------:|
  |   is   |      두 변수가 동일 객체인지 확인     |   a is b   | True or False |
  | is not | 두 변수가 동일하지 않은 객체인지 확인 | a is not b | True or False |

  ```python
  x = ["apple", "banana"]
  y = ["apple", "banana"]
  z = x

  print(x is z)       # True (z는 x를 가리킴)
  print(x is y)       # False (x와 y는 내용은 같지만, 다른 객체)
  print(x == y)       # True (x와 y는 값이 동일함)
  print(x is not y)   # True (x와 y는 다른 객체)
  ```


<br>

## 3. 데이터 타입

<h3> 데이터 타입이란? </h3>
- 데이터 타입은 말 그대로 데이터의 종류를 나타냄
- Python에서 변수에 값을 저장할 때, 그 값이 숫자인지, 문자(텍스트)인지, 논리값인지 구분하는 것이 중요
- 데이터 타입을 알아야 해당 데이터에 적합한 연산이나 처리 가능

<h3> 숫자형(Numeric Types)  </h3>

- 숫자형 데이터는 기본적인 산술연산자(+, -, *, /) 사용 가능
- 정수형 (int)
  - 정수형은 소수점 없이 정수를 나타냄
  - ex. 10, 5, 0
- 실수형(float)
  - 실수형은 소수점을 포함한 숫자를 나타냄
  - ex. 3.14, 0.001, 2.0
- 복소수형(complex)
  - Python은 복소수(complex number)도 지원
  - ex. 1 + 2j, 3 - 4j


<h3> 문자형(String Type) </h3>

- 문자형(String) 
  - 문자, 단어, 문장을 저장하는 데이터 타입
  - 작은따옴표 `'` 또는 큰따옴표 `"`를 사용하여 표현
  ```python
  name = "Alice"
  greeting = 'Hello, World!'
  ```

- 여러 줄 문자열
  - 여러 줄에 걸쳐 텍스트를 작성하려면 삼중 따옴표 `'''` 또는 `"""`를 사용
  ```python
  message = """삼중 따옴표를 사용하면
  여러줄에 걸쳐 텍스트 작성이 가능합니다."""
  ```

- 문자열 연결과 반복
  - 연결(Concatenation) : + 연산자로 문자열을 연결
  - 반복(Replication) : * 연산자로 문자열을 반복
  ```python
  full_name = "Alice" + " " + "Smith"  # Alice Smith
  repeated_greeting = "Hello! " * 3    # Hello! Hello! Hello!
  ```

- 문자열 인덱싱과 슬라이싱
  - 문자열은 인덱스를 통해 개별 문자에 접근할 수 있으며, 슬라이싱을 통해 부분 문자열을 추출
  ```python
  text = "Python"
  print(text[0])   # 'P'
  print(text[1:4]) # 'yth'
  ```

<h3> 불리언(Boolean) </h3>

- 불리언(Boolean)
  - 참(True) 또는 거짓(False)을 나타내는 데이터 타입
  - 불리언 값은 주로 조건문에서 사용되며, True와 False 두 가지 값만 가질 수 있음
  ```python
  is_sunny = True
  is_raining = False  
  ```

- 불리언 연산
  - 불리언 타입은 논리 연산자(and, or, not)와 함께 사용
  
  ```python
  a = True
  b = False

  print(a and b)  # False
  print(a or b)   # True
  print(not a)    # False
  ```

- 비교 연산 
  - 비교 연산자(==, !=, >, < 등)를 사용한 결과는 불리언 값으로 반환
  
  ```python
  x = 10
  y = 20
  
  print(x == y)  # False
  print(x < y)   # True
  ```


<br>
​

# 💡Today I Thought

&nbsp; Python의 기본을 공부했다. 아직은 쉬운 부분이라 막힘없이 잘 해내고 있다. 항상 문제인건 반복문이랑 조건문이던데.. ㅎㅎ 걱정스럽다.주피터 노트북은 예전에 일주일동안 배우면서 사용해서 쉬운데 VSCode나 파이참이 아직 어렵다. 계속 사용하다보면 익숙해지지 않을까..