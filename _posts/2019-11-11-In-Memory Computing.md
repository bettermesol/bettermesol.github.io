---
title: "Disk-based Computing vs In-Memory Computing"
excerpt: "인메모리 컴퓨팅은 왜 등장했고, 어떻게 다르게 쓰이나"
last_modified_at: 2019-11-11T16:20:02-05:00
categories:
  - notes
tags: [devlog, data]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



### 주요하드웨어 

- CPU(중앙처리장치, 연산), 메모리(처리작업), 저장장치(하드 디스크)
- 연산속도 : CPU > 메모리 > 저장장치



### Disk-based Computing vs In-Memory Computing

- Disk-based Computing : 데이터를 디스크에 저장하고 필요에 따라 메모리에 적재하여 처리하고, 백업을 위해 테이프를 사용

- In-Memory Computing : 어플리케이션을 구동하는 컴퓨터의 메인 메모리에 데이터를 저장하고 처리하며, 백업을 위해서 디스크나 테이프를 사용 

  ![인메모리 컴퓨팅](https://t1.daumcdn.net/cfile/tistory/036D8B4D51CA40A22E)



### In-Meory Computing 등장배경

1. Disk-based Computing의 문제점 : 속도가 느린 저장장치에서 데이터를 불러오기 위한 지체 발생
2. 대용량 데이터의 등장 
3. 메모리 기술의 발전 및 가격의 상대적 빠른 하락 : 여전히 메모리가 더 비싸긴 하지만, 가격의 하락이 훨씬 빨라



### In-Memory Analytics Platform

- 인메모리 분석 플랫폼 : 다양한 데이터 소스로부터 데이터를 메모리에 적재하여 대용량 데이터에 대한 빠른 조회 및 연산 성능을 제공하는 기술
- 별도의 Data Mart에 밀 모델을 반영해서 Data Warehouse에 있는 데이터를 추출 및 집계하는 과정이 필요없이, 데이터를 직관적이고 빠르게 조회하고 분석할 수 있다.

![인메모리 분석 기술과 기존 분석 기술의 비교](https://t1.daumcdn.net/cfile/tistory/237F084D51CA419E2A)
