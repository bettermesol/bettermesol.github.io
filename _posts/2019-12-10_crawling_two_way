---
title: "크롤링의 두 가지 방법"
excerpt: "HTML & AJAX"
last_modified_at: 2019-12-10T16:20:02-05:00
categories:
  - Data
tags: [data, crawling, html, ajax]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---


### 웹데이터 크롤링 

- 웹에 존재하는 데이터를 수집하는 것
- 과정 : 웹 페이지에 접속 > 페이지 구조를 분석 > 원하는 데이터를 추출 > 정리 및 저장



### 관련 패키지

- requests : 원하는 url의 웹페이지의 결과를 받아보도록 요청
- JSON : java에서 JSON으로 작성된 자료를 python의 딕셔너리형으로 변환

- urllib : 웹에 접속해서 페이지를 로딩하는데 사용되는 모듈을 포함
- BeuatifulSoup : 파싱(parsing, HTML 코드를 python이 이해하는 객체구조로 변환)



### 웹페이지 구성 방식

웹에 관련된 전문 지식이 없지만, 필요할 때마다 ~~울면서~~ 크롤링을 하면서 두 가지 큰 방법이 있고, 이것은 웹 페이지를 어떻게 구성했느냐에 따라 달라진다는 것을 알았다. 

1. HTML 기반 웹페이지
2. AJAX 기반 웹페이지

이것은 웹페이지를 어떻게 구축했느냐에 따라서 달라지는 듯 하다. 모든 데이터를 미리 저장해두고, 매 요청마다 웹페이지 전체를 새로 갱신하게끔 하는 HTML 방식이 있고, 백그라운드에서 서버와 통신하여 그 결과만을 웹 페이지 일부분만 갱신해서 표시하는 AJax 방식이 있다.

![ajax vs html](https://4.bp.blogspot.com/-2lj4k_WTH6c/XD12vqzu9oI/AAAAAAAABBs/ZZ8Sdxml2q4CeQgXWlRmEM4koLXj7GWfACLcBGAs/s640/Screen%2BShot%2B2019-01-15%2Bat%2B2.58.05%2BPM.png)



이걸 확인하는 방법은 아래와 같다.

1. "검색" 등의 버튼을 눌렀을 때 전체 페이지가 새로 로딩되는지(HTML), 특정 표와 같이 일부분만 로딩되는지(AJAX) 

2. 개발자 도구 > Elements에서 "ajax" 관련 명령어 검색해서 찾는 정보가 $.ajax에 의해서 get, post 되는지 확인
