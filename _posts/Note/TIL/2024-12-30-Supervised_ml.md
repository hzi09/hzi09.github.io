---
title:  "[TIL] 내일배움캠프 36일차_[머신러닝] ch2.개인과제 - 1. 지도학습" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝
    - 지도학습

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 과제 내용
### 💡주제
주택 가격 예측 모델 구축

### 🎯목표
주어진 주택 데이터셋을 사용하여 주택 가격을 예측하는 회귀 모델을 구축합니다.

### 📖학습내용
- 지도 학습의 기본 개념과 회귀 분석을 이해하고, 실제 데이터에 적용하는 능력
- 데이터 전처리 및 탐색: 데이터의 품질을 높이는 방법과 특징 선택의 중요성
- 여러 회귀 모델의 이해: 다양한 회귀 기법의 원리와 적용 방법
- 모델 성능 평가: 성능 지표의 이해 및 비교 분석을 통해 최적의 모델 선택


<br>

## ✍️문제 풀이
### 데이터셋 탐색 및 전처리
#### 1. 데이터 확인

- 머신러닝을 진행하기 전에 데이터를 불러오고 확인
  - CSV 파일 데이터 불러오기 : `read_csv()`
  - 데이터 미리보기(5개의 행만 확인) : `head()`
  - 데이터셋의 기본 정보 확인 : `info()`
    - 데이터 타입, 인덱스 개수, 컬럼명 등을 확인 가능
  - 데이터 정보 탐색 : `describe()` 
    - 각 컬럼별 데이터의 개수, 평균값, 최대값 등을 확인 가능

    ```python
    import pandas as pd

    # 데이터 불러오기
    housing = pd.read_csv('housingdata.csv')

    # 데이터 미리보기
    housing.head()

    # 데이터셋 기본 정보 확인
    housing.info() 

    # 데이터 정보 탐색
    housing.describe() 
    ```


- 위 데이터를 시각화해서 확인
  - 히스토그램(Histogram) : `hist()`
    - `bins` : 가로축 구간의 개수는 좀 여유있게 50으로 결정
    - `figsize` : 가로길이와 세로길이는 작성하면서 여유있게 지정해주었다.(x=20, y=15)

    ```python
    import matplotlib.pyplot as plt

    housing.hist(bins=50, figsize=(20,15))
    plt.show()
    ```

<br>

#### 2. 데이터 전처리

- 결측치 처리
   - 결측치의 개수 확인 : `isna().sum()`
     - CRIM, ZN, INDUS, CHAS, AGE, LSTAT 컬럼에 20개씩의 결측치가 확인됨
        ```python
        # 결측치 개수 확인
        housing.isna().sum()
        ```
   - 결측치 비율 확인 
     - 결측치의 개수를 전체 데이터의 길이로 나눈후 *100을 하면 결측치의 비율을 확인할 수 있음
        ```python
        # 결측치 비율 확인
        missing_percentage= (housing.isnull().sum() / len(housing)) * 100
        ```
    - 결과
      - 그렇게 높은 수치는 아니라서 그냥 삭제를 할까 하다가, 결측치처리를 진행
        ```
        CRIM       3.952569
        ZN         3.952569
        INDUS      3.952569
        CHAS       3.952569
        NOX        0.000000
        RM         0.000000
        AGE        3.952569
        DIS        0.000000
        RAD        0.000000
        TAX        0.000000
        PTRATIO    0.000000
        B          0.000000
        LSTAT      3.952569
        MEDV       0.000000
        dtype: float64
        ```
- 결측치 처리
  - 수치형데이터는 `mean`과 `median` 중 고민하였지만, 데이터 범위가 큰 데이터도 있어서 중앙값으로 대체
  - 범주형 데이터는 `most_frequent`(최빈값)로 대체
    ```python
    # 결측치 처리
    from sklearn.impute import SimpleImputer

    # 수치형데이터 결측치 > 중앙값 대체
    imputer = SimpleImputer(strategy='median')

    for col in ['CRIM', 'ZN', 'INDUS', 'AGE', 'LSTAT'] :
        housing[col] = imputer.fit_transform(housing[[col]])

    # 범주형 데이터 결측치 > 최빈값 대체
    imputer2 = SimpleImputer(strategy= 'most_frequent')

    housing['CHAS'] = imputer2.fit_transform(housing[['CHAS']])
    ```

- 이상치 처리
  - 이상치 처리 전에 기존의 데이터와 비교를 하고 싶어서 `housing_processed` 변수를 만들어서 데이터를 복사(`copy()`)해 넣어줌
  - 이상치는 IQR 방식으로 처리하였으며 경계값으로 대체하는 방법을 채택 
    ```python
    import numpy as np

    numeric_cols = housing.select_dtypes(include=[np.number]).columns # 수치형 데이터를 가진 열들의 이름 가져오기
    housing_processed = housing.copy()


    for col in numeric_cols:
        Q1 = housing[col].quantile(0.25)
        Q3 = housing[col].quantile(0.75)
        IQR = Q3 - Q1
        lower_bound = Q1 - 1.5 * IQR
        upper_bound = Q3 + 1.5 * IQR
        outliers = ((housing[col] < lower_bound) | (housing[col] > upper_bound))
        outlier_count = outliers.sum()

        if outlier_count > 0:
            # 이상치를 경계값으로 대체 (Winsorization)
            housing_processed[col] = housing_processed[col].clip(lower=lower_bound, upper=upper_bound)
    ```

  - 이상치 처리 전 후를 시각화하여 표현
    ```python
    # 이상치 처리 전 데이터 시각화
    housing.boxplot()
    plt.xticks(rotation=90)
    plt.title('Before Boxplot')
    plt.tight_layout()
    plt.show()

    # 이상치 처리 후 데이터 시각화
    housing_processed.boxplot()
    plt.xticks(rotation=90)
    plt.title('After Boxplot')
    plt.tight_layout()
    plt.show()
    ```
    - 결과
        ![image](https://github.com/user-attachments/assets/8d30ff39-9477-4947-9d3f-f26e1fdfae7e)

- 상관관계
  - 학습을 시작하기 전에 타겟 데이터와 상관관계를 확인 : `corr()`
  - 상관관계가 높은 순으로 데이터 확인하기
    - 데이터를 절대값으로 바꾸어준 후 : `avs()`
    - 값을 기준으로 내림차순 정렬 : `sort_values(ascending=False)`
        ```python
        # 데이터 상관관계 확인
        corr_matrix = housing_processed.corr()
        corr_matrix['MEDV'].abs().sort_values(ascending=False)
        ```
    - 결과
        ```
        MEDV       1.000000
        LSTAT      0.782941
        RM         0.697645
        INDUS      0.553140
        TAX        0.543545
        PTRATIO    0.523993
        CRIM       0.522140
        NOX        0.506505
        AGE        0.454330
        RAD        0.452679
        DIS        0.333079
        B          0.321250
        ZN              NaN
        CHAS            NaN
        Name: MEDV, dtype: float64
        ```
  - 시각화 분석 : 선형 회귀선 확인
    - MEDV와 얼마나 선형적인 관계가 있는지 확인
      - `ZN`과 `CHAS`는 선형관계가 없다고 판단되어서 추가하지 않음
      - 오른쪽 아래로 내려가는 선 : 음의 상관관계
      - 오른쪽 위로 올라가는 선 : 양의 상관관계
        ```python
        import seaborn as sns

        # 시각화 분석
        plot_cols = ['MEDV', 'LSTAT', 'RM', 'INDUS', 'TAX', 'PTRATIO', 'CRIM', 'NOX', 'AGE', 'RAD', 'DIS', 'B']
        plot_housing = housing.loc[:, plot_cols]

        # 선형 회귀선 표시
        fig, axs = plt.subplots(figsize=(16, 10))
        for i, feature in enumerate(plot_cols[1:]) :
            ax1 = plt.subplot(3,4,i+1)
            sns.regplot(x=feature, y=plot_cols[0], data=plot_housing, ax=ax1)
        ```
        ![image](https://github.com/user-attachments/assets/8063c063-441f-4cc4-84f6-9ef0813b44d9)

  - 상관관계 히트맵 확인
    - 상관관계를 시각적으로 명확하게 확인할 수 있는 히트맵을 사용
    - `DIS`와 `B`가 상관관계가 낮은 걸 확인 가능
        ```python
        # 상관관계 히트맵
        plt.figure(figsize=(8, 6))
        sns.heatmap(plot_housing.corr(), annot=True, cmap='coolwarm', fmt='.2f')
        plt.title('Correlation Heatmap')
        plt.show()
        ```
        ![image](https://github.com/user-attachments/assets/f0ba40d7-80d2-45a5-9d75-1ac1bd4b9c00)

<br>

#### 3. 특성과 타겟 변수 분리
- 사용할 특성(독립변수)는 'LSTAT', 'RM', 'INDUS', 'TAX', 'PTRATIO', 'CRIM', 'NOX', 'AGE', 'RAD'
- 타겟 변수(말그대로 예측할 데이터)는 'MEDV'
    ```python
    # 특성과 타겟 변수 분리
    X = housing_processed[['LSTAT', 'RM', 'INDUS', 'TAX', 'PTRATIO', 'CRIM', 'NOX', 'AGE', 'RAD']]  # 독립 변수
    y = housing_processed['MEDV']  # 타겟 변수
    ```

<br>

#### 4. 모델 선택 및 훈련
- 선형회귀, 다항회귀, 의사결정나무, 랜덤포레스트, 리지 회귀, 라쏘 회귀에 대해서 훈련을 진행
- 이 내용은 작성하기에는 너무 길어서 깃허브에만 올려놨음!
  - 참고 링크 : [hyunji's github](https://github.com/hzi09/Assignment/tree/main/CH2_Assignment)

<br>

#### 5. 모델 평가
- 모델 별로 성능(MAE, MSE, R2)를 구하여 결과를 비교
    ```python
    # 모델별 성능 저장
    results = pd.DataFrame({
        'Model': ['Linear Regression', 'Polynomial Regression', 'Decision Tree', 'Random Forest', 'Ridge Regression', 'Lasso Regression'],
        'MAE': [lr_mae, pr_mae, tree_mae, rf_mae, ri_mae, ls_mae],
        'MSE': [lr_mse, pr_mse, tree_mse, rf_mse, ri_mse, ls_mse],
        'R2': [lr_r2, pr_r2, tree_r2, rf_r2, ri_r2, ls_r2]
    })

    # 서브플롯 생성
    fig, axes = plt.subplots(1, 3, figsize=(18, 6))  

    colors = ['skyblue', 'green', 'purple']

    # 그래프를 각각 생성
    for ax, metric, color in zip(axes, ['MAE', 'MSE', 'R2'], colors):
        ax.bar(results['Model'], results[metric], color=color, width=0.5)
        ax.set_title(f'{metric} Comparison')
        ax.set_ylabel(f'{metric} Value')
        ax.set_xlabel('Model')
        ax.grid(axis='y', linestyle='--', alpha=0.7)
        # x축 기울기
        ax.set_xticks(np.arange(len(results['Model'])))
        ax.set_xticklabels(results['Model'], rotation=70)

    # 레이아웃 조정 및 출력
    plt.tight_layout()
    plt.show()    
    ```
    ![image](https://github.com/user-attachments/assets/70521ddb-ffc9-46f1-af3d-983b2c4827fb)


- 라쏘회귀가 R2값이 가장 높은 것으로 확인되었다.
  
    |                           | 선형회귀 | 다항회귀 | 의사결정나무 | 랜덤포레스트 | 리지회귀 | 라쏘회귀 |
    |--------------------------:|---------:|---------:|-------------:|-------------:|---------:|---------:|
    | Mean Absolute Error (MAE) |   2.4453 |   2.1346 |       2.6892 |       1.9230 |   2.4510 |   1.8711 |
    |  Mean Squared Error (MSE) |  13.0004 |   8.7704 |      13.7651 |       6.3052 |  13.0244 |   5.9593 |
    |                  R² Score |   0.7342 |   0.8207 |       0.7186 |       0.8711 |   0.7337 |   0.8781 |


<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 41-44
- [x]  SQL 코드카타 47-48
- [x]  프로그래머스 입문 DAY 25 → 2문제
- [x]  백준 코딩테스트 1문제
- [x]  머신러닝 과제 마무리하고 README 작성하기
- [x]  장고 강의 1-4강
- [x]  TIL 작성

## 회고
&nbsp; 틀린 부분이 많아서 부족한 지도학습이지만, 그래도 기록용으로 작성..! 나중에 머신러닝을 제대로 공부하면 이 내용을 제대로 수정하고 싶다. 못했던 도전과제도 같이ㅎㅎ

&nbsp; 내일 머신러닝 과제 제출이라서 호다닥 제출하기 위해서 README까지 야무지게 작성중이다. 오늘은 스탠다드반에서 머신러닝에 관련된 내용을 배웠는데, 과제를 하기 전에 배웠으면 훨씬 더 의미가 있지 않았을까 싶다. 그래도 과제하면서 접했던 것들을 다시 봐서 반가웠다.