---
title:  "[TIL] 내일배움캠프 49일차_[Python] 추상 클래스(Abstract Class)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Python
    - Class


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 추상 클래스(Abstract Class)란?
- Python에서 추상 클래스는 객체 지향 프로그래밍의 중요한 개념으로, 공통적인 인터페이스를 정의할 수 있도록 도와줌 
- 추상 클래스는 스스로 인스턴스화될 수 없으며, 자식 클래스에서 반드시 구현해야 할 메서드를 정의
- Python에서 객체 지향 설계를 더 깔끔하고 강력하게 만들어주는 도구
- 올바르게 사용하면 코드의 재사용성과 유지보수성을 크게 향상시킬 수 있음

<br>

### 추상 클래스의 주요 특징
1. 인스턴스화 불가: 추상 클래스 자체로는 객체를 생성할 수 없음
2. 공통 인터페이스 제공: 여러 클래스가 동일한 인터페이스를 갖도록 강제
3. 부분 구현 가능: 추상 클래스는 추상 메서드뿐만 아니라 일반 메서드도 포함할 수 있음


### Python에서의 추상 클래스 정의
- Python에서는 abc 모듈을 사용하여 추상 클래스를 정의
- 예시
    ```python
    from abc import ABC, abstractmethod

    class Animal(ABC):
        @abstractmethod
        def sound(self):
            pass
    ```
    - 위 코드에서 Animal 클래스는 추상 메서드 sound를 포함하고 있으며, 이를 구현하지 않은 채로는 인스턴스화할 수 없음

### 추상 클래스의 활용

- 추상 클래스는 공통된 인터페이스를 제공하여, 다양한 클래스가 동일한 방식으로 동작하도록 만듦
    ```python
    class Dog(Animal):
        def sound(self):
            return "Woof"

    class Cat(Animal):
        def sound(self):
            return "Meow"

    # Usage
    animals = [Dog(), Cat()]
    for animal in animals:
        print(animal.sound())
    ```
- 출력
    ```
    Woof
    Meow
    ```

### @abstractmethod 데코레이터
- @abstractmethod는 메서드가 반드시 하위 클래스에서 구현되어야 함을 명시
- 이를 구현하지 않으면 오류 발생
    ```python
    class Bird(Animal):
        pass

    # TypeError: Can't instantiate abstract class Bird with abstract methods sound
    bird = Bird()
    ```

### 일반 메서드 포함
- 추상 클래스는 일반 메서드도 포함할 수 있음
    ```python
    class Vehicle(ABC):
        @abstractmethod
        def start_engine(self):
            pass

        def stop_engine(self):
            print("Engine stopped.")
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 161-170
- [x]  SQL 코드카타 79-80
- [x]  백준 코딩테스트 1문제
- [x]  장고 심화 강의 10강까지
- [ ]  장고 메인과제
- [x]  TIL 작성

## 회고
&nbsp; 오늘 공부 열심히 못한 거 같다.. 조금 반성. 언능 강의 듣고 장고 과제 해야지 했는데, 강의 듣기 싫어서 밍기적 거렸더니 하루가 후딱 지나가버렸네ㅎㅎ 앱만 만들고 끝나버린 나의 하루.. 정처기도 해야하는데 할 수 있을까 엉엉.. 하고싶은건 많고.. 쌓였는데.. 난 너무 게으르다.. 언제쯤 부지런할 수 있을까🥹🥹

![image](https://github.com/user-attachments/assets/da0bc8d8-6eb6-4446-8ffd-30a0dc18b518){: .align-center style="width:35%;"}