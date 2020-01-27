---
title: "시계열 이상 탐지"
excerpt: "time series anomaly detection"
last_modified_at: 2019-09-10T16:20:02-05:00
categories:
  - time series
tags: [time series, paper, ml, python]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

### 시계열 데이터의 특성
- 시계열 데이터 : 시간에 따라서 변화하는 데이터
- 구성  
  1. Trend
  2. Seasonal
  3. Random (= Residual)
  ![time series](https://datadotblog.files.wordpress.com/2018/07/jetpack_decomposition.png?w=500&h=330)



### anomaly detection methodology
- anomaly detection : 일반적인 outlier를 찾는 것이 아니라, time series data에서 outlier를 찾는 것
- 필요성 
  1. 평소보다 데이터가 심하게 크거나 작은 경우
  2. 데이터의 패턴 변경
- 주요 탐지기법 
  1. 상태 공간 모델(state space models) : exponentail smoothing, Holt-Winters, ARIMA
  2. 분해 (decomposition) : STL 등 고전적인 분해 기법들
  3. 딥러닝 : RNN
  4. 차원감소 (demension reduction) : RPCA, SOM, discords, piescewise linear



### 쉬운 방법들
- STL decomposition
  - time series = sesonal + trend  구분하여, random graph에서 비정상 포인트를 발견
  - ![STL](https://t1.daumcdn.net/cfile/tistory/99A769335A26A5B32E)
- CART (classification and regresion trees)
  - classification에 따라서 regression을 통해 각 weight를 계산
  - supervised learning이기 때문에 labeled data가 필요하다.
  - ![CART](https://s3-eu-west-1.amazonaws.com/ppreviews-plos-725668748/737225/preview.jpg)
- Moving Average (=roling average)
  - 특정 기간의 평균값을 데이터로 취하여 이동평균선을 구하고, 각 지점에서의 표준편차를 이용해 신뢰구간을 그린 다음 실제 값이 이 신뢰구간을 벗어난다면 비정상이라고 판단.
  - 이동평균선을 그릴 기간(흔히 window size라고 표현)을 얼마로 할 것인가가 중요한 문제
  - ![moving average](https://www.investopedia.com/thmb/G0sJ5M7lr_947rvQBJ60s3IU98E=/1543x905/filters:no_upscale():max_bytes(150000):strip_icc()/SMA-5c535f2846e0fb00012b9825.png)



### 개선된 방법
- Prophet 
  - 페이스북에서 만든 비정상탐지 알고리즘
  - 자세한 설명은 [지난 글](https://bettermesol.github.io/time%20series/2019/09/09/Facebook-Prophet/)에 정리되어 있다.
- Clustering
  - 시간에 따라서 패턴이 크게 달라지는 경우, 군집 분석을 통하여 먼저 시간의 구간을 구분한 뒤, 각 구간별로 시계열 분석을 실시
  - ![clustering](https://www.researchgate.net/profile/Stan_Salvador/publication/221438301/figure/fig1/AS:305617894952968@1449876392445/Main-steps-in-time-series-anomaly-detection-Gecko-which-is-designed-to-identify.png)
