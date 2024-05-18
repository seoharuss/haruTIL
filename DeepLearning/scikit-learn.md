## 사이킷런(scikit-learn)이란?

- 머신러닝 오픈소스 라이브러리
- 기본적인 dataset (붓꽃, 보스턴집값, 당뇨병관련 등) 제공
- 머신러닝 API (의사결정트리, KNN, 회귀분석 등) 제공

## KNN (K-Nearest Neighbors)

- 지도 학습의 한 종류로 거리기반 분류분석 모델
- 데이터를 가장 가까운 유사 속성에 따라 라벨링
- 판별하고 싶은 데이터와 인접한 K개의 데이터를 찾아, 해당 데이터 라벨이 다수인 범주로 데이터를 분류하는 방식
- 보통 유클리디안 거리를 사용
    - 사이킷런에서 metric 변수로 `minkowski` 거리에서 p값을 조절하여 거리 알고리즘을 결정
        - p=1 : Manhattan distance
        - p=2 : Euclidean distance

## KNN시 생각할 수 있는 문제점

1. K의 개수가 짝수일 때 동점이라는 문제
    1. 동일 시 사이킷런 KNN은 거리 가까운, 거리가 같다면 훈련 데이터셋에서 먼저 나온 샘플로 판별
2. K 측정 거리가 너무 커지면 데이터 주변의 지역분포에 민감
    1. 적당한 거리를 선택해야 함
3. 항목들이 빈번한 데이터가 예측을 지배할 수 있음
    1. 데이터가 많을 수록 최근접 이웃이 되기 쉬움
    2. 이를 해결하기 위해 KNN의 거리에 따른 weight을 주는 방법이 있

## KNN의 단점

- 훈련 데이터의 양이 늘어나면 데이터를 모두 보유하고 있어야 하는 특성상 메모리 문제가 생김
- 특성이 많아지게 되면 계산의 양도 늘어나고 overfitting의 우려가 커짐

## 사이킷런(scikit-learn) 패키지로 KNN 구현

### KNeighborsClassifier()

- K-NN 모델을 만드는 사이킷런 클래스
- `fit()` : 사이킷런 모델을 훈련할 때 사용하는 메서드

```python
from sklearn.neighbors import KNeighborsClassifier

knn = KNeighborsClassifier()
knn.fit(x_train_data, y_train_data)
```

### score()

- 훈련된 사이킷런 모델의 성능을 측정하는 클래스
- 1은 모든 데이터를 정확히 맞혔다는 것을 의미

```python
knn.score(x_train_data, y_train_data)
```

### predict()

- 사이킷런 모델을 훈련하고 예측할 때 사용하는 메서드
- 데이터의 정답을 예측하는 것

```python
knn.predict([[30, 600]]) # 새로운 데이터
```

### n_neighbors 매개변수

- 참고할 최근접 이웃 수를 설정할 수 있는 매개변수 (default = 5)
- 객체를 생성할 때 매개변수를 통해 몇 개의 데이터를 참고할 것인지 설정 가능

```python
knn = KNeighborsClassifier(n_neighbors=49)
# 가장 가까운 데이터를 49개를 사용하도록 설
```

### 적절한 n_neighbors 찾기

- 반복문을 통해서 n_neighbors값에 따라 정확도의 변동성을 볼 수 있음

```python
knn = KNeighborsClassifier()
knn.fit(x_train_data, y_train_data)

for n in range(5, 50):
	knn.n_neighbors = n
	score = knn.score(x_train_data, y_train_data)
	if score < 1:
		print(n, score)
		break
```