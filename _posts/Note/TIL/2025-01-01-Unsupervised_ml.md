---
title:  "[TIL] 내일배움캠프 37일차_[Python] 제목" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 1. 데이터 불러오기 및 확인
- 학습을 진행하기 전에 데이터를 불러오고 확인
  - CSV 파일 데이터 불러오기 : `read_csv()`
  - 데이터 미리보기(5개의 행만 확인) : `head()`
  - 데이터셋의 기본 정보 확인 : `info()`
    - 데이터 타입, 인덱스 개수, 컬럼명 등을 확인 가능
  - 결측치 확인 `isna().sum()`
    - 결측치는 0으로 확인되어서 따로 처리할 필요가 없음

    ```python
    import pandas as pd

    # 데이터 불러오기
    mall = pd.read_csv('CSV/Mall_Customers.csv')

    # 데이터 미리보기
    mall.head()

    # 데이터 정보확인
    mall.info()

    # 결측치 확인
    mall.isna().sum()
    ```

## 2. 데이터 전처리
- 데이터 분석에 사용하지 않는 컬럼 제거 : `drop()`
  - 그냥 인덱스 역할을 하는 `CustomerID`와 0, 1로 될 `Gender`는 제외
    ```python
    # 분석에 사용하지 않는 컬럼 제거
    mall = mall.drop(columns=['CustomerID', 'Gender'])
    ```

- 이상치 확인 및 처리
  - 이상치 처리 전에 기존의 데이터와 비교를 하고 싶어서 `mall_processed` 변수를 만들어서 데이터를 복사(`copy()`)해 넣어줌
  - 이상치는 IQR 방식으로 처리하였으며 상한 및 하한값으로 대체하는 방법을 채택 
    ```python
    import numpy as np

    numerical_columns = mall.select_dtypes(include=[np.number]).columns
    mall_processed = mall.copy()

    for col in numerical_columns:
        Q1 = mall[col].quantile(0.25)
        Q3 = mall[col].quantile(0.75)
        IQR = Q3 - Q1
        lower_bound = Q1 - 1.5 * IQR
        upper_bound = Q3 + 1.5 * IQR
        outliers = ((mall[col] < lower_bound) | (mall[col] > upper_bound))
        if outliers.sum() > 0:
            # 이상치를 상한 및 하한값으로 대체
            mall_processed[col] = np.where(mall_processed[col] < lower_bound, lower_bound, mall_processed[col])
            mall_processed[col] = np.where(mall_processed[col] > upper_bound, upper_bound, mall_processed[col])
    ```

  - 이상치 처리 전 후를 시각화하여 표현
    ```python
    import matplotlib.pyplot as plt

    # 이상치 처리 전 데이터 시각화
    mall.boxplot()
    plt.xticks(rotation=90)
    plt.title('Before Boxplot')
    plt.tight_layout()
    plt.show()

    # 이상치 처리 후 데이터 시각화
    mall_processed.boxplot()
    plt.xticks(rotation=90)
    plt.title('After Boxplot')
    plt.tight_layout()
    plt.show()
    ```
    ![image](https://github.com/user-attachments/assets/e728ac21-2e57-4181-ae45-b58638632d79)


- 스케일링
  - StandardScaler를 사용하여 숫자형 피처 값들을 평균이 0이고 표준편차가 1이 되도록 변환
    ```python
    from sklearn.preprocessing import StandardScaler

    # 숫자형 컬럼 선택 및 스케일링
    scaler = StandardScaler()
    data_scaled = scaler.fit_transform(mall_processed[numerical_columns])
    ```

## 3. 클러스터링 기법 적용

- K-means
  - 최적의 k를 찾기위한 '엘보우 방법' 사용
    ```python
    from sklearn.cluster import KMeans

    # 최적의 k찾기 (엘보우 방법)
    inertia = []
    K = range(1, 11)
    for k in K:
        kmeans = KMeans(n_clusters=k, random_state=42)
        kmeans.fit(data_scaled)
        inertia.append(kmeans.inertia_)
    
    # 엘보우 그래프
    plt.figure(figsize=(10, 5))
    plt.plot(K, inertia, 'bx-')
    plt.title('Elbow Method for Optimal k')
    plt.xlabel('Number of Clusters (k)')
    plt.ylabel('Inertia')
    plt.show()
    ```
  - 엘보우 그래프
    - 4~6이 적당하다고 판단했지만, 정확하게 알 수가 없어서 실루엣 계수를 확인
    ![image](https://github.com/user-attachments/assets/08515199-80fa-4ede-a649-9bec7e0167fc)
  - 실루엣 계수
    ```python
    from sklearn.metrics import silhouette_score

    # 최적 클러스터 수(k = 6)로 모델 생성 및 학습
    optimal_k = 6
    kmeans = KMeans(n_clusters=optimal_k, random_state=42)
    kmeans_labels = kmeans.fit_predict(data_scaled)
    kmeans_silhouette = silhouette_score(data_scaled, kmeans_labels)
    print(f'실루엣 계수: {kmeans_silhouette}')
    ```
    - 실루엣 계수가 6이 가장 좋은 결과를 보여주어 k = 6으로 시각화
      | 클러스터 수 |      4 |       5 |       6 |
      |------------:|-------:|--------:|--------:|
      | 실루엣 계수 | 0.4045 | 0.40922 | 0.43194 |

  - 계층적 군집화, DBSCAN도 진행


## 4.결과 시각화
- 세개의 모델 모두 Annual Income vs Spending Score의 군집화가 가장 잘 되어있는 것을 확인
  ![image](https://github.com/user-attachments/assets/15dc40c3-79b6-4522-8c60-6f4180e94696)
- 각각의 모델의 실루엣 계수를 비교
  ```python
  # 모델별 성능 저장
  results = pd.DataFrame({
      'Model': ['K-means', 'Agglomerative Clustering', 'DBSCAN'],
      'Silhouette_score': [kmeans_silhouette, hc_silhouette, best_DBSCAN_silhouette]
  })

  # 서브플롯 생성
  fig = plt.figure(figsize=(18, 5))  

  plt.bar(results['Model'], results['Silhouette_score'], color='purple', width=0.5)
  plt.title('Silhouette_score Comparison')
  plt.ylabel('Silhouette_score Value')
  plt.xlabel('Model')
  plt.grid(axis='y', linestyle='--', alpha=0.7)

  # 레이아웃 조정 및 출력
  plt.show()
  ```
  ![image](https://github.com/user-attachments/assets/9cc3e2ea-94d0-4b18-a496-370479ccfd47)

- KMeans의 실루엣 계수가 가장 높음

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 4~5문제
- [x] SQL 코드카타 2문제
- [x] 백준 코테 1문제
- [x] TIL

## 회고
&nbsp; 신년..! 또 나이를 먹어버렸다.. 아직 정신은 21살인 나 이대로 괜찮은가. 오늘 사실은 장고 들으려고 했는데 낮잠을 너무 많이 자버려가지구 하나도 못들었다. 내일부터는 열심히 들어야징..ㅎㅎ 2025년에는 행복한 일들만 가득한 한해이길!