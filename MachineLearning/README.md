# 머신러닝

## AI, ML, DL 차이

### 인공지능

인간의 학습 능력, 추론 능력, 지각 능력, 언어 이해능력 등을 컴퓨터에 구현한 기술

- 가치 판단, 학습, 인식, 의사소통, 심리 상태 추론등 기계로는 할 수 없는 일들을 가능케 하는 기술이다.

- 빅데이터를 기반으로 분석하고, 분석한 데이터를 가지고 학습하며, 학습한 내용을 가지고 문제의 답을 찾고, 가치 판단 하거나, 결과를 예측하는 기술

### 머신러닝

데이터를 구문 분석하고 해당 데이터를 학습 한 후에 정보를 바탕으로 결정을 내리기 위해 학습한 내용을 적용하는 알고리즘

- 정확한 결정을 내리기 위해 제공된 데이터를 통하여 스스로 학습한다. 처리될 정보에 대해 더 많이 배울 수 있도록 많은 양의 데이터를 제공한다.
- 기본적으로 알고리즘을 이용해 데이터를 분석하고, 학습하고 판단이나 예측을 한다.
- 대량의 데이터와 알고리즘을 통해 컴퓨터 그 자체를 '학습'시켜 작업 수행 방법을 익히는 것을 목표로 한다.

### 딥러닝

인공 신경망에서 발전한 형태의 인공지능으로 뇌의 뉴런과 유사한 정보 입출력 계층을 활용해 데이터를 학습한다.

- 딥러닝은 분류에 사용할 데이터를 스스로 학습할 수 있다.
  - 머신러닝은 학습 데이터를 수동으로 제공해야 한다는 점이 딥러닝과의 차이점이다.

## 용어 정리

- Accuarcy: 정확도
- Dataset: 데이터 셋(사례를 모은 것)
- Train: 학습
- Validation: 검증

## Validation

### K-Fold Cross Validation

Train data에서 일부를 떼서 validataion으로 사용한다.

- train을 통해 나오는 accuracy는 validation dataset의 accuracy이다.
- 여기서 train에서 떠에낸 특정 부분만이 accuracy이며, 다른 부분에서 떼어낼 경우 accuracy가 달라지게 된다.
- 즉, bias(편견이 있는) validation

1. 데이터를 k등분 한다.
2. 순서대로 1/k를 validation으로 사용하며, 나머지를 9개를 train으로 사용한다.
3. k번의 validation 결과로 나온 accuracy를 평균 낸다.

## 지도 학습

정답을 알려주며 학습하는 것

### 분류

결과 값에 대해서 정답을 알려주는 것

- 이진 분류: T/F 결과 값을 학습하는 것
- 다중 분류: 리스트중 하나의 결과 값을 학습하는 것

1. KNN(K-nearest neighbor) 알고리즘

- 데이터를 분류하고 새로운 데이터 포인트를 카테고리를 결정할 때 K개의 가장 가까운 포인트를 선점하고 그 중 가장 많이 선택된 포인트의 카테고리로 이 새로운 데이터를 분류하는 방법

- 알고리즘의 핵십 부분이 대상 포인트와의 거리에 대한 측정이고, 무조건 유클리드 거리 측정 방식을 사용하는 것은 자제 한다.
- 모든 데이터 열을 이처럼 같은 방식으로 처리하면 생각하지 못한 변수에 의해 오류가 생길 수 있으므로 거리의 제곱을 합산하기 전 카테고리에 대한 평균 거리를 빼고 계산하는 방식과 같은 다양한 거리 계산 알고리즘이 필요하다

- 실수 데이터는 유클리드 거리 측정 방식
- 이진 데이터는 해밍 거리 측정 방식

2. Decision Tree(의사 결정 트리)

- Root에서 부터 적절한 node를 선택하면서 진행하다가 최종 결정을 내리게 되는 model
- 누구나 쉽게 이해할 수 있고, 결과를 해석할 수 있다.
- yes를 선택했던 것을 no로 바꾸기만 한다면 간단하게 로직을 바꿀 수 있다.
- 가지고 있는 데이터의 특징을 분석해서 Tree를 Build하는 과정이 제일 중요하다

3. Random Forest

- Decision Tree가 모여서 Forest를 이루게 된다.
- Decision Tree보다 작은 Tree가 여러 개 모이게 되어, 모든 트리의 결과들을 합하여 더 많은 최종 결과로 본다.

4. Naive Bayes (나이브 베이즈)

- 확률을 이용하여 사용 한다.
- 입력값의 특징에 따라서 확률 이론을 계산한다

5. SVM(Support Vector Machine)

- SVM은 기본적으로 Decision Boundary라는 직선이 주어진 상태이다.
- 특정 Decision Boundary를 기준으로 위와 아래를 기준으로 확률을 만든다.

### 회귀

데이터들의 특징을 토대로 값을 예측 하는것

- 그래프 값을 통해서 실수 값을 예측한다.

## 비지도 학습

정답을 알려주지 않고, 비슷한 데이터들을 군집화 하는 것, 그룹핑

### 군집화

x에 대한 레이블이지정되어 있지 않은 데이터를 그룹핑하는 분석 알고리즘

- 데이터들의 특성을 고료해 데이터 집단을 정의하고 데이터 집단의 대쵸할 수 있는 중심점을 찾는 것으로 데이터 마이닝의 한 방법
- 클러스터: 비슷한 특성을 가진 데이터들의 집단
- 데이터의 특성이 다르면 다른 클러스터에 속해야 한다.

1. K-Means(K 평균)

- 군집 중심점이라는 특정한 임의의 지점을 선택해 해당 중심에 가장 가까운 포인트를 선택하는 군집화 기법
- 포인트의 평균 지점으로 이동하고 이동된 중심점에서 가장 가가운 포인트를 선택
- 다시 중심점을 평균 지점으로 이동하는 프로세스를 반복적으로 수행

- 장점: 알고리즘이 쉽고 간결하다.
- 단점: 거리 기반 알고리즘으로 속성의 개수가 매우 많을수록 군집화 정확도가 떨어진다.
  - 반복 수행하는 데 반복 횟수가 많을 수록 매우 느려진다.

2. Mean Shift(평균 이동)

거리 중심이 아니라 데이터의 모여 있는 밀도가 가장 높은 쪽으로 군집 중심점을 이동하면서 군집화를 수행한다.

- 정형 데이터 세트보다 컴퓨터 비전 영역에서 이미지나 영상 데이터에서 특정 개체를 구분하거나 움직임을 추적하는데 뛰어난 역할

- 장점: 데이터 세트의 형재를 특정 형태로 가정한다던가, 특정 분포도 기반의 모델로 가정하지 않기 때문에 좀 더 유연한 군집화 가능
- 단점: 알고리즘의 수행 시간이 오래 걸림, bandwidth의 크기에 따른 군집화 영향도가 매우 크다.

3. GMM(Gaussian Mixture Model)

군집화를 적용한 데이터가 여러 개의 가우시안 분포를 모델을 섞어서 생성한 모델로 가정해 수행하는 방식

- 가우시한 분포: 좌우 대칭형 bell 형태를 가진 연속 확률 함수

- 여러개의 가우시안 분포가 섞인 것으로 간주 -> 섞인 데이터 분포에서 개별 유형의 가우시안 분포를 추출
- 서로 다른 정규 분포를 가진 여러가지 확률 분표 곡선으로 구성되오 있다.

4. DBSCAN(Density Based Spatial Clustering of Applications with Noise)

간단하고 직관적인 알고르즘으로 되어 있음에도 데이터의 분포가 기하학적으로 복잡한 데이터 세트에도 효과적인 군집화가 가능

- 특정 공간 내에 데이터 밀도 차이를 기반 알고리즘으로 하고 있어서 복잡한 기하학적 분포도를 가진 데이터 세트에 대해서도 군집화를 잘 수행한다.

## 강화 학습

자신이 한 행동에 대해 보상을 받으며 학습하는 것을 말한다.

- 현재 상태에서 높은 점수를 얻는 방법에 대해 찾아가며 행동하는 학습 방법으로 높은 점수를 획득할 수 있는 방법을 스스로 찾는다.