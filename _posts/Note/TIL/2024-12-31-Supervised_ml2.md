---
title:  "[TIL] 내일배움캠프 36일차_[ML] ch2.개인과제 - 1. 지도학습(도전과제)" 

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
## 모델 앙상블
- 배깅 모델과 부스팅 모델을 추가한 후(여기서는 코드 생략), 가중 평균 앙상블을 진행
  - 가중 앙상블 : 성능이 높은 모델 5개를 선택
    ```python
    # r2점수를 저장할 리스트
    model_pred = [y_lr_pred, y_pr_pred, y_tree_pred, y_rf_pred, y_ri_pred, y_ls_pred, y_bagging_pred, y_boosting_pred]
    model_r2_score = [lr_r2, pr_r2, tree_r2, rf_r2, ri_r2, ls_r2, bagging_r2, boosting_r2]

    print(model_r2_score)

    # 성능이 높은 5개 모델 선택
    top_models_idx = np.argsort(model_r2_score)[-5:]  # 상위 5개 모델 인덱스
    top_pred = [model_pred[i] for i in top_models_idx]
    top_scores = [model_r2_score[i] for i in top_models_idx]

    # 가중치 계산 (성능 기반)
    weights = np.array(top_scores) / sum(top_scores)

    # 가중 평균 앙상블
    final_pred = sum(w * pred for w, pred in zip(weights, top_pred))
    
    # 성능평가
    final_mae = mean_absolute_error(y_test, final_pred)
    final_mse = mean_squared_error(y_test, final_pred)
    final_r2 = r2_score(y_test, final_pred)

    print(f'Mean Absolute Error (MAE) : {final_mae}')
    print(f'Mean Squared Error (MSE) : {final_mse}')
    print(f'R² Score : {final_r2}')
    ```
  - 결과
    ```
    Mean Absolute Error (MAE) : 1.920664657312724
    Mean Squared Error (MSE) : 6.670866427584049
    R² Score : 0.8636510323472387
    ```

- 라쏘 모델보다 결과가 낮게 나옴
  - 아마 가중치 부여를 하지 않아서가 아닐까 싶은데 이 부분은 추가 학습 후에 다시 수정이 필요할 것 같음


    |                           | 선형회귀 | 다항회귀 | 의사결정나무 | 랜덤포레스트 | 리지회귀 | 라쏘회귀 | 배깅모델 | 부스팅모델 | 가중평균앙상블 |
    |--------------------------:|---------:|---------:|-------------:|-------------:|---------:|---------:|---------:|-----------:|-----------------:|
    | Mean Absolute Error (MAE) |   2.4453 |   2.1346 |       2.6892 |       1.9230 |   2.4510 |   1.8711 |   1.9380 |     1.9168 |           1.9206 |
    |  Mean Squared Error (MSE) |  13.0004 |   8.7704 |      13.7651 |       6.3052 |  13.0244 |   5.9593 |   6.3964 |     6.4878 |           6.6708 |
    |                  R² Score |   0.7342 |   0.8207 |       0.7186 |       0.8711 |   0.7337 |   0.8781 |   0.8692 |     0.8673 |           0.8636 |


## 하이퍼파라미터 튜닝

- 랜덤포레스트 모델을 이용하여 하이퍼파라미터 튜닝 진행
  - 그리드 서치
    ```python
    from sklearn.model_selection import GridSearchCV

    # 하이퍼파라미터 그리드 설정
    param_grid = {
        'n_estimators': [300], 
        'max_depth': [3, 5, 7, 10], 
        'min_samples_split': [6 ,8, 12, 18],
        'min_samples_leaf': [6, 8, 16, 20],
    }


    rf_clf = RandomForestRegressor(random_state=0, n_jobs=-1) # n_jobs = -1 : 모든 CPU 코어를 사용하여 학습
    grid_cv = GridSearchCV(rf_clf, param_grid=param_grid, cv=5, n_jobs=-1)
    grid_cv.fit(X_train, y_train)

    # 데이터 분할 (훈련 데이터와 테스트 데이터)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    # 데이터 스케일링
    scaler = StandardScaler()
    X_train_scaled = scaler.fit_transform(X_train)
    X_test_scaled = scaler.transform(X_test)

    # 최적 모델로 예측
    best_rf_model = RandomForestRegressor(n_estimators=300, max_depth=10, min_samples_leaf=6, min_samples_split=6)
    best_rf_model.fit(X_train_scaled, y_train)
    y_rf_pred = best_rf_model.predict(X_test_scaled)

    # 모델 평가
    rf_mae = mean_absolute_error(y_test, y_rf_pred)
    rf_mse = mean_squared_error(y_test, y_rf_pred)
    rf_r2 = r2_score(y_test, y_rf_pred)

    print(f'Mean Absolute Error (MAE): {rf_mae}')
    print(f'Mean Squared Error (MSE): {rf_mse}')
    print(f'R² Score: {rf_r2}')
    ```

- 랜덤 서치
    ```python
    from sklearn.model_selection import RandomizedSearchCV

    # 하이퍼파라미터 분포 설정
    param_dist = {
        'n_estimators': [300],
        'max_depth': [5, 7, 10, 15], 
        'min_samples_split': [4 ,6 ,8, 12],
        'min_samples_leaf': [6, 8, 16, 20],
        'bootstrap': [True, False]
    }


    rf_clf = RandomForestRegressor(random_state=0, n_jobs=-1) # n_jobs = -1 : 모든 CPU 코어를 사용하여 학습
    random_cv = RandomizedSearchCV(rf_clf, param_distributions=param_dist, cv=5, n_jobs=-1)
    random_cv.fit(X_train, y_train)

    # 데이터 분할 (훈련 데이터와 테스트 데이터)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    # 데이터 스케일링
    scaler = StandardScaler()
    X_train_scaled = scaler.fit_transform(X_train)
    X_test_scaled = scaler.transform(X_test)

    # 최적 모델로 예측
    best_rf_model = RandomForestRegressor(n_estimators=300, max_depth=7, min_samples_leaf=6, min_samples_split=4, bootstrap=True)
    best_rf_model.fit(X_train_scaled, y_train)
    y_rf_pred = best_rf_model.predict(X_test_scaled)

    # 모델 평가
    rf_mae = mean_absolute_error(y_test, y_rf_pred)
    rf_mse = mean_squared_error(y_test, y_rf_pred)
    rf_r2 = r2_score(y_test, y_rf_pred)

    print(f'Mean Absolute Error (MAE): {rf_mae}')
    print(f'Mean Squared Error (MSE): {rf_mse}')
    print(f'R² Score: {rf_r2}')
    ```

- 결과
  - 하이퍼 파라미터를 진행했지만 그리드서치 랜덤서치 두개 모두 R²가 떨어진걸 확인
  - 이 부분도 학습이 조금 더 필요

    |                           | 랜덤포레스트 | 그리드서치 | 랜덤서치 |
    |--------------------------:|-------------:|-----------:|---------:|
    | Mean Absolute Error (MAE) |       1.9230 |     2.0244 |   2.0240 |
    |  Mean Squared Error (MSE) |       6.3052 |     8.1637 |   8.0601 |
    |                  R² Score |       0.8711 |     0.8331 |   0.8352 | 


## 시간적 요소 추가
- 데이터 전처리 후에 시간적 요소를 추가
  - 어떤 요소가 가장 적합할지 생각한 끝에 `TAX`로 결정 (TAX: 10,000달러당 재산세율)
- `TAX`를 기준으로 데이터 정렬
    ```python
    # 이상치가 처리된 housing 데이터에서 TAX 값으로 데이터 정렬
    housing_processed = housing_processed.sort_values(by="TAX").reset_index(drop=True)
    housing_processed
    ```
- `TAX`가 올라갈때마다 1이 올라가는 방향으로 진행
  - 실제 년도를 알 수 없어 데이터를 구분하기 위해 1씩 증가하는 것으로 표현함
  - 물론 세금이 떨어질때도 있어 이 데이터를 시간데이터로 바꾸는 것은 올바르지 않은 선택일수도 있음
    ```python
    # TAX값이 올라갈때마다 1을 더하여 시간의 흐름을 표현
    housing_processed['TIME'] = (housing_processed['TAX'] != housing_processed['TAX'].shift()).cumsum()
    housing_processed
    ```
- `MEDV`와 -0.51로 상관관계가 높은 것으로 확인
- 결과 비교
  - 기존 결과

    |                           | 선형회귀 | 다항회귀 | 의사결정나무 | 랜덤포레스트 | 리지회귀 | 라쏘회귀 | 배깅모델 | 부스팅모델 | 가중평균앙상블 |
    |--------------------------:|---------:|---------:|-------------:|-------------:|---------:|---------:|---------:|-----------:|-----------------:|
    | Mean Absolute Error (MAE) |   2.4453 |   2.1346 |       2.6892 |       1.9230 |   2.4510 |   1.8711 |   1.9380 |     1.9168 |           1.9206 |
    |  Mean Squared Error (MSE) |  13.0004 |   8.7704 |      13.7651 |       6.3052 |  13.0244 |   5.9593 |   6.3964 |     6.4878 |           6.6708 |
    |                  R² Score |   0.7342 |   0.8207 |       0.7186 |       0.8711 |   0.7337 |   0.8781 |   0.8692 |     0.8673 |           0.8636 |
    
  - `TAX` 추가 결과

    |                           | 선형회귀 | 다항회귀 | 의사결정나무 | 랜덤포레스트 | 리지회귀 | 라쏘회귀 | 배깅모델 | 부스팅모델 | 가중 평균 앙상블 |
    |--------------------------:|---------:|---------:|-------------:|-------------:|---------:|---------:|---------:|-----------:|-----------------:|
    | Mean Absolute Error (MAE) |   2.8446 |   2.1745 |       2.6267 |       2.0439 |   2.8482 |   3.3502 |   2.0510 |     1.9960 |           1.9760 |
    |  Mean Squared Error (MSE) |  13.6133 |  10.8285 |      11.5584 |       7.5495 |  13.6438 |  17.2110 |   7.6402 |     7.7054 |           7.1979 |
    |                  R² Score |   0.8076 |   0.8469 |       0.8366 |       0.8933 |   0.8072 |   0.7568 |   0.8920 |     0.8911 |           0.8982 |

  - 생각하기에는 너무 상관관계가 조금 있는 데이터가 들어오면서 R²가 높아진게 아닌가 생각이 든다(물론 낮아진 데이터도 있음)
  - MAE와 MSE가 낮아지지 않고 상승했으므로 좋은 모델이라고 판단하기에는 어려울 것 같다.


<br>
<br>


# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 44-46
- [x]  SQL 코드카타 49-50
- [x]  백준 코딩테스트 1문제
- [x]  머신러닝 과제 제출하기
- [ ]  장고 15강까지 듣기
- [x]  TIL 작성

## 회고
&nbsp; 오늘 밍글데이라서 도파민이 터졌더니 장고 강의를 끝까지 못들었다.. 도파민의 노예.. 이래저래 바쁘고, 우울했다가 행복했던 한 해가 저물고 새로운 한 해가 시작된다. 예전엔 한 살 먹는게 정말 컸는데, 지금은 그냥 흘러가는 날짜 중에 하나인 기분. 남은 부트캠프 기간에도 힘내야지! 화이팅!