---
title: "엘라스틱 스택 = 데이터 수집+검색엔진+대시보드"
excerpt: "엘라스틱을 위한 첫걸음"
last_modified_at: 2020-01-21T16:20:02-05:00
categories:
  - Elastic
tags: [Elastic, Elasticsearch, Elastic stack, ELK stack, data, DB]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

오늘 엘라스틱서치에 대한 이야기를 처음 들었다.
관계형 DBMS이 아니라 DB이면서 검색엔진이라는건 무슨 말이고, 어떤 점이 좋은지 궁금한데 별 수 있나 직접 써봐야지!



### 엘라스틱 스택 = ELK 스택

- 엘라스틱의 주요 제품 삼인방![ELK stack](https://www.guru99.com/images/tensorflow/082918_1504_ELKStackTut2.png)
- Logstash : 서버측 데이터 처리 파이프라인 (데이터 수집, 변환)
- elasticsearch : 검색 및 분석엔진 (정형, 비정형, 위치, 메트릭 정보 등을 검색 및 결합)
- Kibana : 시각화

- 설치도 각각! 사용도 각각!



### 그 외의 엘라스틱 제품

- Prelert : 이상 데이터 및 외부 공격을 감지
- Beats : 엘라스틱서치로 데이터를 보내기. 데이터 종류에 따라 다양한 Beats가 있는 듯
- 그 외에도 X-Pack, Cloud 등 엄청나게 많은 제품이 있다.



###  "elasticsearch를 왜 쓸까?"에 대한 개발자 친구의 답변

![crawling_html](/assets/images//2020-01-21-elastic_what is it.JPG)



### Elasticsearch vs 관계형DBMS

- 용어차이 ![용어의 차이](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/11/10-1.png)
