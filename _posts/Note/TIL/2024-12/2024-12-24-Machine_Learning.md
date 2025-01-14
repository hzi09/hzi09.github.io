---
title:  "[TIL] 내일배움캠프 30일차_[ML] 머신러닝 알고리즘" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## 1. 머신러닝 알고리즘의 분류
&nbsp;  지도 학습(Supervised Learning), 비지도 학습(Unsupervised Learning), 준지도 학습(Semi-supervised Learning), 그리고 강화 학습(Reinforcement Learning)으로 분류됨

### 지도 학습
- 지도 학습(Supervised learning)은 입력데이터와 출력 레이블로 구성된 데이터셋을 사용
  - 이러한 데이터셋을 labled data라고 함
- 알고리즘은 두 변수 사이의 관계를 학습하고 새로운 입력변수에 대한 예측 결과를 나타냄
- 예측변수의 유형에 따라 분류, 회귀, 예측으로 분류

<h4>분류 (Classification)</h4>

- 범주형(categorical) 변수를 예측
- 분류하고자 하는 클래스의 수에 따라서 이진 분류(binary classification), 다중 클래스 분류(multi-class classification)가 있음

<h4>회귀 (Regression)</h4>

- 연속적인 값을 예측
- 데이터 포인트 사이의 관계를 찾아내고 각 변수가 다른 변수에 미치는 영향을 모델링 
- 독립변수와 종속 변수 사이의 모델링 방식에 따라 선형 회귀(Linear Regression), 다항 회귀(Polynomial Regression) 등이 있음

<h4>예측 (Forecasting)</h4>

- 과거 와 현재 데이터를 기반으로 미래의 사건을 예측하는 방법
- 기술적으로는 회귀나 분류문제에 속할 수 있음
- 주로 동향(trends) 분석하기 위해 많이 사용
  - 시계열 예측(Time Series Forecasting)을 통한 주식 가격 예측, 기상 조건 예측
  - 사용자의 과거 행동과 유사한 사용자의 데이터를 분석하여 행동을 예측하는 추천 시스템(Recommendation Systems) 등이 있음

<br>

### 비지도 학습
- 비지도 학습(Unsupervised Learning)은 레이블이 없는 데이터로부터 데이터의 패턴, 구조, 관계를 학습
- 군집화(Clustering), 차원 축소(Dimension Reduction) 등이 있음

<h4>군집화(Clustering)</h4>

- 비슷한 특성을 가진 데이터끼리 그룹으로 묶음
- 데이터의 특징적인 패턴을 찾기 위해 개별 그룹으로 군집화하고 분석을 진행
- K-평균(K-Means) 클러스터링, 계층적 클러스터링(Hierarchical Clustering) 등이 있음


<h4>차원 축소(Dimension Reduction)</h4>

- 변수의 개수를 줄이는 방법
- 고차원의 데이터에서 특성을 보존하면서 데이터의 차원을 줄이는 과정
- 차원을 줄이고 중요한 특성만 선택하거나 추출하여 데이터의 잠재된 관계를 더 잘 도출할 수 있음

<br>

### 준지도 학습
- 준지도 학습 (Semi-supervised Learning)은 지도학습과 비지도 학습의 중간 형태
- 일부 데이터만 레이블이 있는 상태에서 학습하는 기법으로 레이블이 없는 데이터를 레이블링 하는 것에 많은 비용이 필요한 상황에서 준지도 학습은 유용한 방법
- 준지도 학습은 레이블된 데이터와 레이블되지 않은 데이터가 유사한 패턴과 구조를 갖는다는 상황을 가정
- 머신러닝 모델은 레이블된 데이터를 통해 초기 학습을 진행하고, 레이블 없는 데이터에 대한 예측을 개선하며 추가 학습을 진행하게 됨

<br>

### 강화 학습
- 강화 학습(Reinforcement Learning)은 에이전트가 환경과 상호작용하며 목표 달성을 위한 최적의 행동이나 정책을 학습하는 과정
- 행동의 결과로 받는 보상을 최대화하는 방향으로 행동하고, 정책을 개선해 나감 
- 명확한 정답이 없거나 탐색과 활용 사이에서 균형을 필요하는 문제에 적합

<br>

## 2. 머신러닝 알고리즘의 특징과 활용
### 선형 회귀와 로지스틱 회귀
- 두 회귀 알고리즘은 예측하고자 하는 값의 특성에 따라 구분하여 사용 가능

![image](https://github.com/user-attachments/assets/4e140c3e-4119-47e6-b524-2c1fbc415249){: .align-center style="width:35%;"}

<h4> 선형 회귀(Linear regression) </h4>

- 연속적인 값을 예측하고자 할 때 사용할 수 있음
- 하나 이상의 독립변수와 종속변수 사이의 선형 관계를 모델링 
- 변수 사이의 관계를 이해하고 특정한 변수의 영향력을 분석할 때 유용

<h4> 로지스틱 회귀(Logistic regression) </h4>

- 주로 분류 문제에서 활용
- 선형 회귀에 로지스틱 함수를 붙여 0과 1사이의 확률을 구함
- 이 확률은 특정 클래스에 속할 확률이 됨
- 소프트맥스 함수를 사용하면 다중 분류 문제에 적용할 수 있음


<br>

### 선형 SVM 커널 SVM
- 데이터의 선형성과 선형 분리 가능성, 모델의 해석 가능성 등에 따라 선형 SVM 과 커널 SVM을 선택

![image](https://github.com/user-attachments/assets/98510b23-db0d-42c7-aafc-901a5fb4f94b){: .align-center style="width:35%;"}

<h4>선형(Linear) SVM</h4>

- 선형 분리 가능한 데이터에 적합
- 따라서 비교적 해석이 쉽고 빠르게 학습할 수 있음 
  
<h4>커널(Kernel) SVM</h4>

- 비선형 데이터에 적합
- 분리 가능한 비선형 함수를 고차원의 분리 가능한 선형 함수로 매핑

<br>

### 의사결정 나무와 앙상블 트리(ensemble tree)

- 의사결정나무, 랜덤 포레스트(random forest), 그래디언트 부스팅(gradient boosting) 기법들은 데이터의 특성과 요구되는 정확도, 해석 가능성 등을 고려하여 선택

<h4> 의사결정나무</h4>
- 직관적이고 해석이 용이
- 비선형 데이터 학습에도 효과적이며 데이터 피쳐의 스케일링이 필요 없음 
- 반면 트리가 깊어짐에 따라 과적합 위험이 크게 증가 
- 따라서 해석 가능한 모델일 필요한 경우, 피처의 중요도를 이해하고자 할 때, 간단한 분류나 회귀 문제에 적용하면 좋음

<h4> 랜덤 포레스트(random forest)</h4>

- 여러 개의 의사결정나무를 앙상블 함 
- 다수의 트리를 사용하여 기존 트리의 단점인 과적합을 방지
- 고차원의 데이터에서도 잘 작동하며, 의사결정나무와 동일하게 피처의 중요도를 파악하기 용이하고, 스케일에 영향 받지 않음
- 높은 정확도가 필요한 경우, 고차원의 데이터를 사용하면서 피처의 중요도를 해석하고자 할 때 적합

<h4> 그래디언트 부스팅(gradient boosting) </h4>

- 새로운 트리를 추가하여 이전 트리의 오차를 학습하는 과정을 통해 성능을 향상시킴
- 마찬가지로 높은 정확도를 가지며, 학습률, 트리의 수, 최대 깊이 등 다양한 하이퍼 파라미터 튜닝을 통해 모델을 개선할 수 있음

<br>

### 신경망과 딥러닝

<h4> 신경망 </h4>

- 입력층, 은닉층, 출력층으로 구성된 신경망은 출력층에 따라 다양한 문제에 적용할 수 있음
- 모델의 복잡성 수용력(capacity)에 따라 고차원의 데이터를 매우 잘 처리함

<h4> 딥러닝 </h4>

- 딥러닝은 더 많은 은닉층을 갖는 신경망입니다. 
- 전이 학습(Transfer Learning)을 통해 사전 학습된 모델을 활용하여 새로운 문제를 해결하기에 용이
- 순환 신경망(RNN), 컨볼루션 신경망(CNN) 등 특정 데이터 유형에 특화된 구조를 사용
- 대규모 데이터셋과 다양한 형태의 데이터를 처리
- 딥러닝은 데이터셋의 특징, 문제의 복잡성, 사용 가능한 리소스 상황 등을 고려하여 결정해야 함

### K-평균, K-모드, 가우시안 혼합 모델 클러스터링

<h4> K-평균(K-means) </h4>

- 중심을 기준으로 군집에 할당하는 거리 기반 클러스터링 알고리즘
- 표본은 하나의 군집에만 할당되는데 이를 ‘하드 할당(hard assignment)’이라고 함
- 따라서 클러스터의 수(K)가 사전에 지정된 경우, 클러스터의 모양이 원형일 경우 잘 작동

<h4> K-모드(K-modes) </h4>

- 범주형 데이터 군집화에 적합
- 카테고리별 최빈값을 중심으로 해밍 거리(Hamming distance)를 사용하여 두 범주형 데이터의 차이를 계산

<h4>가우시안 혼합 모델(GMM; Gaussian Mixture Model) </h4>

- 이름에서 알 수 있듯이 데이터 포인트가 여러 가우시안 분포를 따른다고 가정 
- 각 데이터 포인트가 어떤 가우시안 분포를 따르는지 연속확률분포를 추정
- 각 클러스터를 가우시안 분포로 표현하고, 데이터가 여러 개의 클러스터에 속할 수 있음
- 적절한 클러스터 개수를 선택하기 위해 BIC(Bayesian Information Criterion)나 AIC(Akaike Information Criterion)을 사용
- 데이터가 연속형 변수일 뿐만 아니라 정규 분포를 따르고 여러 클러스터에 속할 확률이 있는 경우 적합합니다.

<br>

### DBSCAN

- DBSCAN(Density-Based Spatial Clustering of Applications with Noise)은 밀도 확산(density diffusion)을 사용하여 데이터를 군집화
- 노이즈는 무시하며, 다양한 모양의 클러스터를 형성 가능
- 따라서 노이즈가 있는 데이터, 클러스터의 모양이 다양한 데이터에 적합
- 지리적 데이터에 공간 데이터에도 효과적

<br>

### 계층적 군집화

- 데이터를 계층적인 구조로 클러스터를 형성하는 알고리즘이 계층적 군집화(Hierarchical clustering)하고 덴드로그램(dendrogram)을 통해 시각화
- 클러스터 간의 거리 측정 방법을 조정하는 것이 중요한데, 거리 측정 방법에는 단일 연결(Single Linkage), 완전 연결(Complete Linkage), 평균 연결(Average Linkage) 등이 있음 
- 클러스터의 계층적 구조가 필요한 경우, 클러스터 간 관계를 파악하고자 할 때, 클러스트의 개수가 정해지지 않았고, 크기나 모양이 다양한 경우, 대규모 데이터셋을 클러스터링할 경우 효과적으로 사용할 수 있음
- 조직구조나 생물학적 데이터와 같이 계층구조를 갖는 데이터에 사용됨

<br>

### PCA, SVD, LDA

- 많은 수의 특징 중 일부 특징은 연관이 없거나, 고유한 차원수가 특징 수 보다 적을 수 있음
- 따라서, 머신러닝 알고리즘에 데이터의 특징을 모두 사용하는 것은 대체로 효과적이지 못함
- 3가지 차원축소와 관련한 방법이 있음

<h4> PCA(Principal Component Analysis) </h4>

- 데이터를 저차원 공간으로 매칭
- 데이터의 분산을 최대한 보존하는 하위 공간을 찾음 
- 고차원의 데이터를 시각화하거나, 데이터를 압축
- 주성분만 사용함으로써 노이즈를 제거하는 효과도 있음

<h4> SVD (Singular Value Decomposition)</h4>

- PCA를 수학적 기반으로 사용하여 주어진 행렬을 3개의 행렬로 분해
- 이미지 처리 또는 자연어 처리에서 텍스트의 의미를 추출하는 데 활용

<h4>LDA (Linear Discriminant Analysis)</h4>

- 토픽 모델링 방법으로 잠재 디리클레 할당이라고 함
- 토픽들이 혼합되어 있는 문서에서 확률분포에 기반하여 단어들이 생성된다고 가정
- 검색 엔진, 고객 민원 시스템 등 문서를 주제를 파악하는 곳이 사용

<br>

## 3. 머신러닝 치트 시트

- 가장 확실한 방법은 모든 알고리즘을 시도해 보는 것

![image](https://github.com/user-attachments/assets/32dfd136-f272-469d-af28-6c38363c77c0)

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 32-34번
- [x]  SQL 코드카타 41-42번
- [x]  프로그래머스 코딩테스트 Day 23 → 2개
- [x]  백준 코딩테스트 1문제
- [x]  머신러닝 과제
- [x]  TIL 작성

## 회고
&nbsp; 머신러닝 과제를 시작했는데,, 음,, 시작만 했다. 아무래도 주말까지 싹 머신러닝 과제를 해야 시간 맞춰할 수 있을것 같다. 오늘 크리스마스 이브라 그런가 조금 어수선한 기분,, 크리스마스🎅는 공부 쉬고 신나게 놀아야즤~
