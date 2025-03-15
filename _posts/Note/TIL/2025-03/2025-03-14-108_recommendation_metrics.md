---
title:  "[TIL] 내일배움캠프 108일차_[ML] 추천 모델 성능 평가 방법" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝
    - Precision
    - Recall
    - F1-Score
    - Hit Rate


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
- 추천 시스템을 개발할 때, 모델의 성능을 올바르게 평가하는 것은 매우 중요
- 추천 모델의 품질을 판단하는 다양한 평가 지표 중에서 Precision(정밀도), Recall(재현율), F1-Score, Hit Rate는 가장 널리 사용됨

## Precision (정밀도)
- Precision은 추천된 항목 중에서 실제로 사용자가 선호한 항목의 비율을 의미
- 추천 리스트에서 얼마나 정확한 추천이 이루어졌는지를 평가함

### 수식

$$
Precision = \frac{|Relevant \cap Retrieved|}{|Retrieved|}
$$

- `Relevant`: 사용자가 실제로 선호한 항목 (예: 클릭, 구매)
- `Retrieved`: 추천된 항목 (예: 추천 리스트에 포함된 아이템)

### 예시

- 사용자에게 10개의 아이템을 추천했을 때, 그중 4개가 실제로 사용자가 클릭한 아이템이라면

$$
Precision = \frac{4}{10} = 0.4 (40\%)
$$

<br>

## Recall (재현율)

Recall은 사용자가 선호한 모든 항목 중에서 추천된 항목이 차지하는 비율을 나타냅니다. 즉, 사용자가 좋아할 만한 항목을 얼마나 많이 추천했는지를 평가하는 지표입니다.

### 수식
$$
Recall = \frac{|Relevant \cap Retrieved|}{|Relevant|}
$$

- `Relevant`: 사용자가 실제로 선호한 항목 개수
- `Retrieved`: 추천된 항목 개수

### 예시

- 사용자가 실제로 8개의 아이템을 선호했지만, 추천 리스트에서 그중 4개만 포함되었다면

$$
Recall = \frac{4}{8} = 0.5 (50\%)
$$

<br>

## F1-Score

- F1-Score는 Precision과 Recall의 조화 평균(Harmonic Mean)으로, 두 지표 간의 균형을 평가하는 역할을 함
- Precision이 높고 Recall이 낮거나, 반대로 Recall이 높고 Precision이 낮으면 모델이 편향된 성능을 가질 수 있어서, 이를 보완하기 위해 사용됩니다.

### 수식

$$
F1-Score = 2 \times \frac{Precision \times Recall}{Precision + Recall}
$$

### 예시
- 앞선 예시에서 Precision이 0.4, Recall이 0.5라면

$$
F1-Score = 2 \times \frac{0.4 \times 0.5}{0.4 + 0.5} = 0.444 (44.4\%)
$$

<br>

## Hit Rate (적중률)

- Hit Rate는 추천된 항목 중에서 사용자가 하나라도 선호한 항목이 있는지를 측정하는 지표
- Precision이나 Recall이 개별 아이템의 정확성을 평가하는 반면, Hit Rate는 전체 추천 리스트의 유용성을 평가

### 수식

$$
Hit Rate = \frac{\text{Number of Users with at least one relevant recommendation}}{\text{Total Number of Users}}
$$

### 예시

- 10명의 사용자에게 추천을 제공했을 때, 그중 7명이 추천 리스트에서 최소 하나의 유용한 아이템을 찾았다면

$$
Hit Rate = \frac{7}{10} = 0.7 (70\%)
$$

<br>

## 결론

- 추천 시스템의 성능을 평가할 때 단일 지표만 사용하기보다는 Precision, Recall, F1-Score, Hit Rate를 함께 분석하여 균형 잡힌 모델을 개발하는 것이 중요

  - Precision: 추천의 정확도를 평가
  - Recall: 사용자가 원하는 항목을 얼마나 많이 포함했는지 평가
  - F1-Score: Precision과 Recall의 균형을 평가
  - Hit Rate: 추천 리스트의 전반적인 유용성을 평가

- 추천 모델을 평가할 때는 비즈니스 목적과 데이터 특성을 고려하여 적절한 지표를 선택하는 것이 중요

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 2문제
- [x]  중간 발표 자료 수정
- [x]  SA 문서
- [x]  WIL 작성
- [x]  TIL 작성

## 회고
&nbsp;최종 발표때 프론트가 빈약해서 그런가 너무 아무것도 못한 기분이 들어서 조금 쳐졌다. 프론트 Lead가 나여서 그런가 조금 더 위축되었던 것 같다.. 조금만 더 빠르게 했으면 우리도 보여줄 수 있는 거 많았을텐데.. 하는 기분도 들고.. 속상한 하루🤐