---
title:  "[TIL] 내일배움캠프 42일차_[ML] Titanic 데이터를 사용한 머신러닝(1)" 

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
## 타이타닉 데이터 확인
* Passengerid: 탑승자 데이터 일련번호
* survived: 생존 여부, 0 = 사망, 1 = 생존
* Pclass: 티켓의 선실 등급, 1 = 일등석, 2 = 이등석, 3 = 삼등석
* sex: 탑승자 성별
* name: 탑승자 이름
* Age: 탑승자 나이
* sibsp: 같이 탑승한 형제자매 또는 배우자 인원수
* parch: 같이 탑승한 부모님 또는 어린이 인원수
* ticket: 티켓 번호
* fare: 요금
* cabin: 선실 번호
* embarked: 중간 정착 항구 C = Cherbourg, Q = Queenstown, S = Southampton


### 데이터 로드
- 데이터를 알아야 머신러닝을 시작할 수 있기 때문에 데이터를 불러오고 데이터를 확인하는 과정을 거침
    ```python
    import numpy as np
    import pandas as pd

    df = pd.read_csv('./titanic.csv')

    print('Train 데이터 정보')
    print(df.info())
    df.head(3)
    ```
  - 데이터 불러오기
    - Pandas 라이브러리의 `read_csv()`를 통해 CSV 파일의 데이터를 불러옴
  - 데이터 정보 확인하기
    - `info()`를 사용하면 컬럼, Null 값이 아닌 데이터 갯수, 데이터 타입 등을 확인가능
  - 데이터 미리보기
    - `head()`를 사용하면 데이터를 미리볼 수 있음!
    - 기본값은 5개이지만 내가 셋팅한만큼 확인 가능

- 결과
    ```
    Train 데이터 정보
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
    #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
    0   PassengerId  891 non-null    int64  
    1   Survived     891 non-null    int64  
    2   Pclass       891 non-null    int64  
    3   Name         891 non-null    object 
    4   Sex          891 non-null    object 
    5   Age          714 non-null    float64
    6   SibSp        891 non-null    int64  
    7   Parch        891 non-null    int64  
    8   Ticket       891 non-null    object 
    9   Fare         891 non-null    float64
    10  Cabin        204 non-null    object 
    11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB
    None
    ```

    |   | PassengerId | Survived | Pclass |                                              Name |    Sex |  Age | SibSp | Parch |           Ticket |    Fare | Cabin | Embarked |
    |:-:|------------:|---------:|-------:|--------------------------------------------------:|-------:|-----:|------:|------:|-----------------:|--------:|------:|---------:|
    | 0 |           1 |        0 |      3 |                           Braund, Mr. Owen Harris |   male | 22.0 |     1 |     0 |        A/5 21171 |  7.2500 |   NaN |        S |
    | 1 |           2 |        1 |      1 | Cumings, Mrs. John Bradley (Florence Briggs Th... | female | 38.0 |     1 |     0 |         PC 17599 | 71.2833 |   C85 |        C |
    | 2 |           3 |        1 |      3 |                            Heikkinen, Miss. Laina | female | 26.0 |     0 |     0 | STON/O2. 3101282 |  7.9250 |   NaN |        S |

<br>

## 데이터 전처리
### 결측치 처리
- Age : 평균 값으로 채우기
- Cabin : N으로 채우기
- Embarked : N으로 채우기

```python
def fillna(df):
    df['Age'] = df['Age'].fillna(df['Age'].mean())
    df['Cabin'] = df['Cabin'].fillna('N')
    df['Embarked'] = df['Embarked'].fillna('N')
    return df
```

<br>

### 필요 없는 컬럼 제거
- PassengerId
- Name
- Ticket

```python
def drop_features(df):
    return df.drop(['PassengerId', 'Name', 'Ticket'], axis=1)
```

<br>

### 범주형 데이터 처리
- Sex : 숫자형 변환
- Embarked : 숫자형 변환
- Cabin : 첫 번째 문자만 추출 후 숫자형 변환

```python
from sklearn.preprocessing import LabelEncoder

def format_features(df):
    df['Cabin'] = df['Cabin'].astype(str).str[:1]
    features = ['Cabin', 'Sex', 'Embarked']
    for feature in features:
        le = LabelEncoder()
        df[feature] = le.fit_transform(df[feature])
    return df
```

<br>

### 데이터 전처리 함수
- 위에서 만든 세개의 함수를 하나의 함수로 만들어줌
  - 결측치 처리 함수
  - 필요없는 컬럼 제거 함수
  - 범주형 데이터 처리 함수

```python
def transform_features(df):
    df = fillna(df)
    df = drop_features(df)
    df = format_features(df)
    return df
```

<br>

## 데이터 분리
- 머신러닝 모델로 데이터를 학습/예측하기 위해 데이터셋을 분리
  - 사이킷런의 `model_selection` 의 `train_test_split` 함수를 활용
- `train_test_split()` 함수의 파라미터
  - test_size(기본값 : 0.25)
    - 전체 데이터셋에서 테스트 데이터셋 크기를 얼마로 샘플링할 것인지 결정
  - train_size : 
    - 전체 데이터셋에서 학습 데이터셋 크기를 얼마로 샘플링할 것인지 결정. 
    - test_size를 주로 활용하기 때문에, 잘 쓰이지는 않음
  - shuffle(기본값: True)
    - 데이터를 분리하기 전에 데이터를 섞을지 결정하는 파라미터
    - 데이터를 분산시켜 보다 효율적인 학습/테스트 데이터 세트를 만드는데 사용
  - random_state : 난수값을 지정하면 여러 번 다시 수행해도 동일한 결과가 나오게 해줍니다.
- train_test_split의 반환 값은 튜플형태로 아래의 순서
  - (1) 학습 데이터셋
  - (2) 테스트 데이터셋
  - (3) 학습 데이터셋의 레이블
  - (4) 테스트 데이터셋

```python
y_titanic_df = df['Survived']
X_titanic_df = df.drop('Survived', axis=1, inplace=False)
X_titanic_df = transform_features(X_titanic_df)

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X_titanic_df, y_titanic_df, test_size=0.2, random_state=11)

X_titanic_df
```

<br>

## 모델 학습
- DecisionTreeClassifier
- RandomForestClassifier
- LogisticRegression

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

# 모델 정의
models = {
    'DecisionTree': DecisionTreeClassifier(random_state=44),
    'RandomForest': RandomForestClassifier(random_state=44),
    'LogisticRegression' : LogisticRegression(solver='liblinear')
}
```


<br>

## 평가
```python
def evaluate_models(models, X_train, X_test, y_train, y_test):
    results = {}
    for name, model in models.items():
        model.fit(X_train, y_train)
        pred = model.predict(X_test)
        acc = accuracy_score(y_test, pred)
        results[name] = acc
        print(f'{name} 정확도: {acc:.4f}')
        print("Confusion Matrix:\n", confusion_matrix(y_test, pred))
        print("Classification Report:\n", classification_report(y_test, pred))
    return results

# 모델 평가
results = evaluate_models(models, X_train, X_test, y_train, y_test)
```

- 결과

    ``` 
    DecisionTree 정확도: 0.8045
    Confusion Matrix:
    [[101  17]
    [ 18  43]]
    Classification Report:
                precision    recall  f1-score   support

            0       0.85      0.86      0.85       118
            1       0.72      0.70      0.71        61

        accuracy                           0.80       179
    macro avg       0.78      0.78      0.78       179
    weighted avg       0.80      0.80      0.80       179

    RandomForest 정확도: 0.8436
    Confusion Matrix:
    [[106  12]
    [ 16  45]]
    Classification Report:
                precision    recall  f1-score   support

            0       0.87      0.90      0.88       118
            1       0.79      0.74      0.76        61

        accuracy                           0.84       179
    macro avg       0.83      0.82      0.82       179
    weighted avg       0.84      0.84      0.84       179

    LogisticRegression 정확도: 0.8659
    Confusion Matrix:
    [[108  10]
    [ 14  47]]
    Classification Report:
                precision    recall  f1-score   support

            0       0.89      0.92      0.90       118
            1       0.82      0.77      0.80        61

        accuracy                           0.87       179
    macro avg       0.85      0.84      0.85       179
    weighted avg       0.86      0.87      0.86       179
    ```

<br>

### 결과 시각화
```python
import matplotlib.pyplot as plt

plt.bar(results.keys(), results.values())
plt.title('Model Accuracy Comparison')
plt.ylabel('Accuracy')
plt.show()
```

- 결과

![image](https://github.com/user-attachments/assets/8253fd63-4649-4280-96a9-fef73d19c7b6)


<br>
<br>


# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 81-90
- [x]  SQL 코트카타 59-60
- [x]  백준 코딩테스트 1문제
- [x]  장고 강의 17강까지
- [x]  TIL 작성

## 회고
&nbsp; 장고강의 들으면서 정신없지만, 혹시 나중에 어떤걸 하게 될지 모르니까 머신러닝 공부도 꾸준히 하려고.. 학습반에서 했던 내용을 정리해봤다. 반도 못하긴 했지만..🤔 공부하려고 빌려온 책도 펴봐야하는데 지금은 장고 쫓아가기도 너무 버겁다😰 하루가 40시간이면 좋겠어..