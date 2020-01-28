---
title: "엘라스틱 머신러닝 - 시계열 이상징후 탐지"
excerpt: "엘라스틱에서 머신러닝을?"
last_modified_at: 2020-01-27T20:20:02-05:00
categories:
  - Elastic
tags: [Elastic, Elasticsearch, Elastic stack, ELK stack, data, DB, ML]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---


### Machine Learning in Elastic
물론 ES에서 데이터를 추출하여 분석에 이용할 수도 있지만, Kibana에서 머신러닝 분석툴도 제공한다. 
주로 시계열 자료에서 이상 탐지 (anomaly detection)에 사용하는 듯 하다.



### 일반적인 시계열 이상징후 탐지법
[이전 글]()에서 시계열 데이터의 구성과 이상징후 탐지법이 주로 아래와 같이 구분되며, 원리를 자세히 설명했었다.
- 시계열 데이터 : 시간에 따라서 변화하는 데이터
  - Trend
  - Seasonal
  - Random (= Residual)
  - ![time series](https://datadotblog.files.wordpress.com/2018/07/jetpack_decomposition.png?w=500&h=330)
- anomaly detection : 일반적인 outlier를 찾는 것이 아니라, time series data에서 outlier를 찾는 것
- 필요성 
  1. 평소보다 데이터가 심하게 크거나 작은 경우
  2. 데이터의 패턴 변경
- 주요 탐지기법 
  1. 상태 공간 모델(state space models) : exponentail smoothing, Holt-Winters, ARIMA
  2. 분해 (decomposition) : STL 등 고전적인 분해 기법들
  3. 딥러닝 : RNN
  4. 차원감소 (demension reduction) : RPCA, SOM, discords, piescewise linear



### Elastic에서 제공하는 시계열 이상징후 탐지법
- **Machine Learning anomally detection **
  - 사용법 : `Maching Learning` 탭에서 job으로 지정
  - 사용예시 : KPI 값의 비정상적인 변동에 대한 알림
  - 문제점 : **어떤 알고리듬을 쓰는지 알 수가 없다**. 때로는 false anomaly alert가 뜰 수도 있는데, 원리를 설명 안해두면 이게 false인지 어떻게 알 수 있단 말인가.
  ![elastic anomaly detection](https://www.elastic.co/guide/en/kibana/current/user/ml/images/ml-single-metric-viewer.jpg)
- **Prelert**
  - 원래 X-pack에 포함된 기능으로 이상징후에 대한 알람으로 보이는데 자세한 내용을 찾을 수 없다.



### 대안, 혹은 원래부터 좋은 선택
- `elasticsearch`에서 실시간으로 인덱싱 하고 있는 데이터를 `rest api`로 추출하여, facebook의 `prophet` 패키지를 이용하여 python으로 시계열 분석을 마친 뒤 이상 징후가 있다면 알림을 표시한다. `jenkins` 패키지를 이용하여 주기적으로 실행시킬 수 있다.
![better option](https://taetaetae.github.io/2018/05/31/anomaly-detection/forecast_graph.png)
- 내가 생각한 방법을 실제로 적용한 예시가 있어서 첨부! 
https://taetaetae.github.io/2018/05/31/anomaly-detection/
