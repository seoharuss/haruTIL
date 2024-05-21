## KNN (K-최근접 이웃 알고리즘)

- 분류나 회귀에 사용되는 지도학습 알고리즘
- 새로운 데이터를 입력 받았을 때 K개의 근접한 데이터에 따라 분류, 결정

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6a6865c-4ba6-4522-a8a6-927f097bb32e/10e09fad-406f-4dd5-a86e-3348ff52c3de/Untitled.png)

- K=3 일때 Class B
- K=7 일때 Class A

K가 작을수록 locally sensitive(과적합, 근처 데이터의 영향을 많이 받음) → 적절한 k를 찾아야 한다.