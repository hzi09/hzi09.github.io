---
title:  "[TIL] 내일배움캠프 40일차_[ML] 혼동행렬(Confusion Matrix)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝
    - 혼동행렬


toc: True
toc_sticky: True
use_math: true
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 혼동행렬(Confusion Matrix)

|          |     |       **예측**      |                     |
|:--------:|:---:|:-------------------:|:-------------------:|
|          |     |   양성(Posivtive)   |    음성(Negative)   |
| **실제** | T/F |  TP (True Positive) | FN (False Negative) |
|          | F/T | FP (False Positive) |  TN (True Negative) |

- TP(True Positive) : `악당`이라고 예측한 사람이 실제 `악당`인 경우
- TN(True Negative) : `착한 사람`이라고 예측한 사람이 실제 `착한 사람`인 경우
- FP(False Positive) : `악당`이라고 예측한 사람이 실제로는 `착한 사람`인 경우
- FN(False Negative) : `착한 사람`이라고 예측한 사람이 실제로는 `악당`인 경우


### 정분류율
- 전체 데이터 중 정확하게 예측한 데이터의 비율

$$
\frac{TP+TN}{TP+FN+FP+TN}
$$


### - 정확도(Accuracy)
- 얼마나 잘 맞춰는지

$$
TP+TN
$$

- 정확도가 정확하지 않은 이유
  - 데이터셋의 값이 불균형한 경우에 정확도는 좋은 측정이 불가
  - 악당 90명과 착한 사람이 10명 있는 경우, 머신러닝이 모든 사람이 악당이라고 예측할 경우 정확도는 90%가 됨.

### 오분류율
- 전체 데이터 중 잘못 예측한 데이터의 비율

$$
\frac{FN+FP}{TP+FN+FP+TN}
$$


### 정밀도(Precision)
- 참이라고 예측한 것 중에 실제 참인 정도

$$
\frac{TP}{TP+FP}
$$

### 민감도(Sensitivity), 재현율(Recall)
- 실제값이 참인 관측값 중 참이라고 바르게 예측한 정도

$$
\frac{TP}{TP+FN}
$$

### 특이도(Specificity)
- 실제값이 거짓인 관측값 중 거짓으로 바르게 예측한 정도

$$
\frac{TN}{TP+FN}
$$

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 

## 회고
&nbsp; 