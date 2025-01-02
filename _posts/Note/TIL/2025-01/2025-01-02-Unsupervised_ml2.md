---
title:  "[TIL] 내일배움캠프 38일차_[ML] ch2.개인과제 - 2.비지도학습(도전과제)" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - 머신러닝
    - 비지도학습


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 다양한 클러스터링 기법 비교
- Gaussian Mixture Model(GMM) 클리스터링 기법을 적용
  ```python
  from sklearn.mixture import GaussianMixture

  # GMM 모델 생성
  gmm = GaussianMixture(n_components=5, covariance_type='full')

  # 모델 학습 및 예측
  mall_processed['Cluster'] = gmm.fit_predict(data_scaled)
  ```
  - 실루엣 계수는 '0.4072'가 나옴
  ![image](https://github.com/user-attachments/assets/1df80739-2fc1-405c-9b4b-442b44a8a81e)

<br>

## 고객 행동 예측 모델 구축
- 계층적 군집화모델이 군집화가 잘되어있다고 생각되어 계층적 군집화 모델의 클리스터를 사용
- Gender을 포함시키는 것이 낫다고 판단되어 Geder 컬럼의 데이터 인코딩을 진행
  - One Hot Encoder를 사용하여 Gender_Male 컬럼을 생성(Gender 데이터가 Male이면 1, Female이면 0)
    ```python
    from sklearn.preprocessing import OneHotEncoder

    one_hot_encoder = OneHotEncoder(sparse_output=False, drop='first', dtype='int')
    gender_encoded = one_hot_encoder.fit_transform(mall[['Gender']])
    gender_encoded_df = pd.DataFrame(gender_encoded, columns=one_hot_encoder.get_feature_names_out(['Gender']))
    mall = pd.concat([mall.drop(columns=['Gender']), gender_encoded_df], axis=1)
    ```

- 분류모델
  - 클리스터를 타겟으로 결정
    ```python
    # 해당 클러스터를 타겟으로 결정
    mall_processed['Target'] = (mall_processed['Cluster'] == 5)
    mall_processed
    ```
  
  - 의사결정나무로 훈련진행
    ```python
    from sklearn.model_selection import train_test_split

    # 입력 변수와 타겟 변수
    X = mall_processed.drop(columns=['Cluster', 'Target']) 
    y = mall_processed['Target']

    # 데이터 분리
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    from sklearn.tree import DecisionTreeClassifier
    from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

    # 모델 생성 및 학습
    model = DecisionTreeClassifier(random_state=42)
    model.fit(X_train, y_train)

    # 예측
    y_pred = model.predict(X_test)

    # 모델 평가
    accuracy = accuracy_score(y_test, y_pred)
    ppv = precision_score(y_test, y_pred)
    recall = recall_score(y_test, y_pred)
    f1 = f1_score(y_test, y_pred)

    print(f"Accuracy: {accuracy}")
    print(f"Precision: {ppv}")
    print(f'Recall: {recall}')
    print(f'F1 scorer : {f1}')
    ```
    - 결과
      ```
      Accuracy: 0.925
      Precision: 1.0
      Recall: 0.7272727272727273
      F1 scorer : 0.8421052631578947
      ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 53 - 60
- [x]  SQL 코드카타 53 - 54
- [x]  백준 코딩테스트 1문제
- [x]  장고 강의 듣기
- [x]  TIL 작성

## 회고
&nbsp; 비지도 학습도 이제 끝! 스탠다드반에서 머신러닝 수업을 진행하고 있는데, 궁금한 것이 조금씩 해결되서 기분이 좋다. 이제 이해가 되는 기분..!
&nbsp; 오늘 장고 강의 실습을 하면서 가상환경 문제가 생겨버렸다. 도대체 무슨 문제인지 알 수가 없당.. 일단 강의 들어야하니까 번거롭더라도 비활성화 하고 제대로 된 위치에서 활성화하는 방식으로 진행중..😫 오늘도 한번에 되는게 없는 나의 코딩라이프