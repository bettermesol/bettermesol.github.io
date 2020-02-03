---
title: "코딩 없는 머신러닝 - Google AutoML"
excerpt: "Google AutoML, 코딩 없이 머신러닝을 해보자"
last_modified_at: 2020-02-03T16:20:02-05:00
categories:
  - ML
tags: [ml, no_coding, google, autoML]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

python, C, java와 같은 프로그래밍 언어를 다루지 못하면 머신러닝도 못할 거라고 생각한다.
그렇지 않다!
요즘에는 설치만 하면 되는 소프트웨어도 많고,
Cloud에서 제공해주는 서비스도 많다.

그 중에서도 가장 유명한 것은 Google's AutoML!



### Google's AutoML  (https://cloud.google.com/automl/docs/)

1. **Cloud AutoML Natural Language**
   - AutoML Natural Language 분류 : 정의한 라벨에 따라 문서를 분류
   - AutoML Natural Language 항목 추출 : 영어 텍스트 내에서 커스텀 항목 집합을 식별
   - AutoML Natural Language 감정 분석 : 영어 텍스트 내에서 태도를 분석

2. **Cloud AutoML Tables**
   - AutoML Tables : 전체 팀이 속도와 확장성을 크게 개선시키는 구조화된 데이터 기반 최신 머신러닝 모델을 자동으로 빌드하고 배포

3. **Cloud AutoML Translation**
   - AutoML Translation : 번역 쿼리가 분야에 맞는 결과를 반환

4. **Cloud AutoML Video Intelligence**
   - Video AutoML Video Intelligence 분류 : 직접 정의한 라벨에 따라 동영상의 장면과 세그먼트를 분류
   - Cloud AutoML Video Intelligence 객체 추적 : 동영상의 한 순간부터 다음 순간까지 특정 객체를 따르도록 머신러닝 모델을 학습

5. **Cloud AutoML Vision** : 예시 https://cloud.google.com/vision/?hl=ko#tab4 Try the API에 아무 이미지나 업로드
   - AutoML Vision 분류 : 정의한 라벨에 따라 이미지를 분류
   - AutoML Vision 객체 감지 : 여러 객체를 감지 및 추출하고 이미지 내 위치를 포함한 각 객체의 정보를 제공

   

### AutoML Tables 
각 단계는 Quickstart[(링크)](https://cloud.google.com/automl-tables/docs/quickstart)에 잘 설명되어 있으니, 중요한 개념만 정리한다.

1. 학습 데이터 가져오기 : 
   - 가져오기 방식 : from BigQuery / CSV from Cloud Storage / CSV from local PC
   - 데이터 요구사항 : https://cloud.google.com/automl-tables/docs/prepare?_ga=2.123467531.-1851394170.1580693987

2. 데이터 유형 : https://cloud.google.com/automl-tables/docs/data-types
   - 범주형
   - 텍스트
   - 숫자
   - 타임스탬프
   - List
   - Array

3. 문제 유형 : 타겟열 데이터 유형에 의해서 자동으로 결정 (https://cloud.google.com/automl-tables/docs/problem-types)
   - classification  : 타겟열 데이터 유형이 `카테고리`인 경우 (binary or multiple)
   - regression : 타켓열 데이터 유형이 `숫자`인 경우


