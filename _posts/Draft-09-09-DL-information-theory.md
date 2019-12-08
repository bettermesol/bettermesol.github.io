---
title: "[DL] 손실함수"
excerpt: "딥러닝 모형의 평가를 위해서 정보이론 빌려오기"
last_modified_at: 2019-09-14
T16:20:02-05:00
categories:
  - notes
tags: [DL]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---
내가 이해한 원리만 후려치는 딥러닝

모르겠는 부분 
- map랑 cross entropy의 관계
- cross entropy랑 kl divergence가 무슨 상관?
- bias의 의미 : 마이크를 켜고 끄는 거랑 

![neural net component](https://upload.wikimedia.org/wikipedia/commons/b/b6/Artificial_neural_network.png)
![bias variance trade off](https://djsaunde.files.wordpress.com/2017/07/bias-variance-tradeoff.png)

용어
1. batch : 한 번 학습에 사용하는 데이터의 총량
원래 100개 데이터가 있는데
- 한 번에 모두 학습시키면 batch size = 100
- 열 번에 걸쳐서 나눠서 학습시키면 batch size = 10
- 점점 더 데이터의 규모가 크기 때문에 임의로 일부만 골라서 학습을 시키느네, 이렇게 선택된 일부를 mini-batch라고 한다.

2. epoch : 전체 데이터셋이 한 번 학습에 사용되는 것

3. capacity : 다양한 형태의 함수에 fitting 될 수 이는 모델의 능력
- 예를 들어서 1차 선형 함수는 복잡한 함수에 fitting 될 수 없지만, 3차 함수의 경우 상대적으로 잘 fitting 된다. 이렇게 모델의 타고난 능력치를 뜻한다.


# 딥러닝 모형의 평가
### loss fuction = 딥러닝 모형의 평가 지표
- 시험을 보면 100점 만점에 점수를 매기듯, 딥러닝 모형도 평가가 필요하다.   
단, 얼마나 맞았나가 아니라 얼마나 틀렸나를 측정한다.  
원래 정답이 있고, 딥러닝의 학습을 통한 예측값을 찾았을 때 둘 사이의 차이를 측정하는 것이다.
- 후려치자면, **(loss fuction) = (actual Y) - (predicted Y)**
이렇게 틀린 정도를 측정한 수학적 지표를 loss fuction(손실함수, 줄이는 것이 목표라는 의미에서 목적함수라고도 함)라고 한다.

### 목표 : minimize loss fuction
- 틀린 정도를 측정한 것이기 때문에 손실함수를 최소화 하는 것이 목표

### 측정방법과 목표
1. MSE (Mean Squared Error)
- "predicted Y와 actual Y의 차이의 제곱의 합"을 minimize

2. ML : maximum likelyhod
- predicted Y가 actual Y가 될 likelihood를 maximize

3. MAP (Maximum A Posteriori): minimize cross entropy
- Cross Entropy = (predicted Y가 나올 확률) - (actual Y가 나올 확률)
- 'Cross Entropy의 최소화'  
= cross entropy를 미분한 gradient(기울기)가 0
- 즉, MAP는 gradient를 작게 만드는 global optimal을 찾아가기

>0916 업데이트
mse의 경우에는 error의 squared sum이다. 
그래서 error의 크기를 numeric distance로 구할 수 있어야 한다.
근데 만약에 actual Y가 binary여서 1,0,0이고
predicted Y가 0.8, 0.1, 0.3으로 나왔다고 할 때
그 squared sum을 구하는 것은 numeric error의 크기라고 할 수 없기 때문에 한계가 있다.
따라서 MSE가 아니라 ML을 기반으로 하는 cross entropy를 쓴다.

# 정보이론
### shannon entorypy
- 정보의 양을 측정

### 정보의 양
- 무엇이 나올지 모를 때 정보의 크기가 크다
- surprise가 많다 = high entropy = 정보양이 많다

### relative entropy 
- a.k.a Kullback-Leibler (KL) divergence
- extra data의 양을 측정
    - extra anoutn of information needed to send a message when using a code designed to minimize the length of messages
    - sending message : P(x)
    - used message : Q(x)
    - 쉬운 예시 : 중국어로 된 메시지에 한국어로 메시지를 보낸다고 했을 때 추가적으로 필요한 정보의 양
- 두 분포의 거리 차이를 측정 : 하지만 대칭이 아니기 때문에 distance는 아니다
- task : approximate distribution truth p(x) with approximation distribution q(x)


### 목표
- 목표 : 정답을 잘 맞추는 모델 만들기
- 목표세분화 : 학습이 가장 잘 되는 모델의 parameter(weight, bias 이렇게 두 개)를 구하기  
- 기준 : cost function(=loss fuction=average loss)이 최소화
closed answer가 없어서 반복적인 시행을 통해서 답으로 수렴해야 하지만, convex하므로 global optimal이 존재함
문제 1) initial theta(weight, bias)를 어떻게 정해야 할지 모른다.
문제 2) parameter(weight, bias)를 어떻게 수렴시킬지 모른다 >> gradient descent를 통해서 업데이트하면서 찾기

### gradient descent : backprop을 통해서 weight, bias를 보정해가는 것
- 종류
  - SGD(stochastic gradient descent) : 단 한개의 데이터를 이용해서 weight, bias를 보정
  - minibatch gradient descent : 전체 데이터 중 일부를 선택해서 weight, bias를 보정
  - fullbatch gradient descent : 전체 데이터를 한 번에 사용해서 weight, bias를 보정
- 원리
  1. forward propagation
    - 임의의 x를 넣어서 예측 y 구하기  
    - 실제 y와 예측 y를 비교해서 loss를 계산
  2. backward propagation : 
    - loss를 다시 모델에 넣기  
    - 에러를 이용해서 w,b를 업데이트
  3. i, ii)를 반복
- 알고리즘
  1. theta라는 임의의 initional location에서 시작
  2. while :stop 조건을 만족할 때까지 반복
    1. 전체 데이터 중에서 m개의 샘플을 선택
    2. m개의 샘플에 대한 gradient의 평균을 계산 (gradient의 역방향으로, learning rate만큼 이동)
    3. 업데이트
  3. end while

### error vs loss function의 차이
loss fuction과 error는 그 개념 자체는 같지만,  
(산공에서는 risk도 같은 의미)
loss fuction = average error

### backprop
1. frontprop에서 나온 예측 y와 실제 y 사이의 에러와 미분값들을 이용해서 아래의 것들을 보정
- activation function
- bias
- inputs' weighted sum function
- weight
- input x (multi layer일수도 있으니 x도 보정이 필요)
2. back propagation에서 sigmoid처럼 activation function을 통과하려면 sigmoid 함수의 미분값을 곱해준다.  

### learning rate : hiperparameter, 사람이 임의로 입력해주는 값

### regulization
더 robust한 모델을 만들기 위한 방법
regularization methods
 parameter norm penalties
 dataset augmentation
 noise injection
 semi-supervised learning
 multi-task learning
 early stopping
 parameter typing & sharing
 sparse representations
 bagging & ensembles
 dropout
 adversarial training

