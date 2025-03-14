---
title:  "[TIL] 내일배움캠프 76일차_[ML] 선형 회귀(Linear Regression)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - ML
    - 선형 회귀


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 1. 선형 회귀(Linear Regression)

- 데이터 사이의 관계를 찾고, 이를 기반으로 미래를 예측하는 기법
    - 쉽게 말하면 ‘X’가 변할 때 ‘Y’가 어떻게 변하는가?’ 를 찾는 과정
- 예를 들어, 공부시간이 길수록 시험점수가 높아지는 경향이 있다고 가정
    - X(공부 시간) : 독립 변수(입력)
    - Y(시험 시간) : 종속 변수(출력)
- 이 관계를 설명하는 **직선(회귀선, Regression Line)** 을 찾으면, 새로운 데이터가 주어졌을 때 시험 점수를 예측할 수 있음

<br>

## 2. 선형 회귀의 기본 개념

- 선형 회귀에서 사용되는 공식은 직선 방정식과 같음

$$
y = w_0 + w_1x
$$

- 여기서:
    - y : 예측 값(시험 점수)
    - x : 입력 값(공부 시간)
    - w₀ : 절편(intercept) → 직선이 y축과 만나는 값
    - w₁ : 기울기(slope) → X가 증가할 때 Y가 얼마나 변하는지를 나타냄
- 즉, 내가 해야하는 것은 가장 적절한 w₀(절편)와 w₁(기울기)를 찾는 것

<br>

## 3. 선형 회귀의 종류

### 단순 선형 회귀 분석(Simple Linear Regression Analysis)

$$
y = wx + b
$$

- w : 가중치(weight), b : 편향(bias)
- w와 b의 값에 따라 x와 y가 표현하는 직선은 무궁무진
- 예시 :
    - 강우량과 작물 수확량
    - 어린이의 나이와 키
    - 온도계에서 금속 수은의 온도와 팽창

### 다중 선형 회귀 분석(Multiple Linear Regression Analysis)

$$
y = w_1x_1+w_2x_2+...w_nx_n+b
$$

- y는 1개이지만 x가 여러 개가 된 경우를 다중 선형 회귀 분석이라고 함
    - 여러개의 변수가 결과에 미치는 영향을 모델링 하는 것
- 예시 :
    - 강우량, 온도 및 비료 사용에 작물 수확량에 미치는 영향
    - 식이요법과 운동이 심장병에 미치는 영향
    - 임금 인상과 인플레이션이 주택 대출 금리에 미치는 영향

<br>

## 4. 선형 회귀의 한계

1. 데이터가 선형 관계가 아닐 때 부적합
    
    ⇒ 해결 방법 : 비선형 모델(ex. 다항 회귀, 신경망 모델) 사용
    
2. 이상치(Outlier)에 민감함
    
    ⇒ 해결 방법 : 이상치를 제거하거나 Lasso 회귀 적용
    
3. 다중공선성 문제(독립 변수끼리 너무 비슷하면 문제 발생)
    
    ⇒ 해결 방법: 변수 선택 또는 PCA 사용

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 333
- [x]  SQL 코드카타 110
- [x]  AI 모델 활용 완강
- [x]  딥러닝 복습 : 선형회귀, ANN
- [x]  LLM 특강듣고 정리
- [x]  TIL 작성

## 회고
&nbsp;오늘도 야무지게 할일을 다 끝냈다. 수요일부터 팀과제가 있어서 내일은 더 열심히 공부해야 할 것 같다. 오늘 하루도 마무리🤭