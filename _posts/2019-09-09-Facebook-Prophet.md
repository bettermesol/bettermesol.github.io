---
title: "[ML/논문/시계열] 시계열 분석을 위한 Facebook prophet"
excerpt: "prophet, 페이스북의 시계열 분석 라이브러리"
last_modified_at: 2019-09-09T16:20:02-05:00
categories:
  - time series
tags: [time series, paper, ml, python]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

### Facebook Prophet
- 페이스북의 시계열 분석 라이브러리
- 페이스북에서 관련 논문도 publish
- 시계열의 세 가지 요소를 모두 함수의 변수로 포함
    - trend(non-periodic change) : sigmoid curve
    - seasonality(weerkly or yearly) : cosign + sign function
    - events(holidays) : 휴일 리스트에 속하면 조정
- 도메인 지식이 있는 사람이 파라미터를 조정하여 분석과 예측에 활용하기 좋은 모형
- R이나 Python에서 라이브러리로 사용 가능

### 관련 자료
- [논문원문](https://peerj.com/preprints/3190.pdf)
- [한국어 번역 요약 by 열정맨](https://gorakgarak.tistory.com/1255)
- [한국어 요약 by zzsza](https://zzsza.github.io/data/2019/02/06/prophet/)
- [Prophet quick start](https://facebook.github.io/prophet/docs/quick_start.html#python-api)

