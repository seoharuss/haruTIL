## PCA (주성분 분석)

![image](https://github.com/seoharuss/haruTIL/assets/127467806/5edcf342-4623-4cd2-bc6a-70c40bffb1a9)


차원 축소를 통해 최소 차원의 정보로 원래 차원의 정보 모사(approximate)하는 알고리즘

- 다변량 데이터의 차원을 축소하면서 정보 손실을 최소화 하는 방법
- 데이터의 분산을 최대한 보존하는 새로운 축(주성분)을 찾아 원래 데이터를 이 주성분에 투영함으로써 차원을 축소
    - 데이터의 중요한 정보를 유지하면서 차원을 줄이고, 성능 향상 가

### PCA 과정

1. **데이터 전처리 :** 데이터를 표준화(평균 0, 표준편차 1)하거나 정규화 (최소값 0, 최댓값 1)하여 스케일을 조정
2. **공분산 행렬 계산 :** 데이터의 공분산 행렬을 계산, 공분산 행렬은 변수 간의 선형 관계를 나타내며, 이를 통해 데이터의 분포와 구조를 파악 가능
3. **고유값 및 고유벡터 계산** : 공분산 행렬의 고유값과 고유벡터 계산, 고유값은 데이터의 분산을 나타내고, 고유벡터는 주성분의 방향을 나타냄
4. **주성분 선택** : 고유값이 큰 순서대로 주성분 선택, 주성분 개수를 선택하는 방법으로 누적 설명 분산 비율(cumulative explained variance ratio)을 활용 가능
5. **주성분으로 원본 데이터 변환** : 선택된 주성분 (고유벡터)을 이용하여 원본 데이터 변환, 이 과정에서 원본 데이터의 차원이 축소되며, 새로운 주성분 축에 투영된 데이터를 얻게 됨

### 차원 축소 (Dimension Reduction)

- 고차원 벡터에서 일부 차원의 값을 모두 0으로 만들어 저차원 벡터로 줄이는 것
    - 원래 고차원 벡터의 특성을 최대한 살리기 위해 **가장 분산이 높은 방향으로 회줜 변환(rotation transform)**

> 차원 축소를 하는 이유?
> 
- 시각화를 통해 데이터 패턴 쉽게 인지
- 노이즈 제거
- 메모리 절약
- 불필요한 feature 제거로 모델 성능 향상

### 차원의 저주(Curse of Dimensionality)

- 데이터 용량이 커지면서 불필요한 샘플이 많아지는 것
- 데이터 학습을 위해 차원이 증가하며 학습 데이터 수가 차원의 수보다 작아져 성능이 저하되는 형상
- 해결방안?
    - PCA, LDA(Linear Discriminant Analysis), LLE(Locally Linear Embedding), MDS(Multidimensional Scaling), …

## PCA로 차원 줄이기

```python
from sklearn.pipeline import Pipeline
from sklearn.decomposition import PCA
from sklearn.model_selection import GridSearchCV, StratifiedKFold

pipe = Pipeline([
    ('pca', PCA()),
    ('clf', KNeighborsClassifier())
    ])
parameters = {
    'pca__n_components' : [2, 5, 10],
    'clf__n_neighbors' : [5, 10, 15]
}

kf = StratifiedKFold(n_splits=5, shuffle=True, random_state=13)
grid = GridSearchCV(pipe, parameters, cv=kf, n_jobs=-1, verbose=1)
grid.fit(X_train, y_train)

print('Best score: %0.3f' % grid.best_score_)
print('Best parameter set: ')

best_parameters = grid.best_estimator_.get_params()

for param_name in sorted(parameters.keys()):
    print("\t%s: %r" % (param_name, best_parameters[param_name]))
    
print(accuracy_score(y_test, grid.best_estimator_.predict(X_test)))
'''
Fitting 5 folds for each of 9 candidates, totalling 45 fits
Best score: 0.931
Best parameter set: 
	clf__n_neighbors: 10
	pca__n_components: 10
0.929
```
```

## PCA with Python
https://machinelearningmastery.com/calculate-principal-component-analysis-scratch-python/
