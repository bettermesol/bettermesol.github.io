---
title: "크롤링, 스크래핑, 파싱의 차이"
excerpt: "크롤링, 스크래핑, 파싱의 차이를 후려쳐서 설명해보자"
last_modified_at: 2019-09-17T16:20:02-05:00
categories:
  - Data
tags: [crawling, scraping, parsing, data]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

요즘에는 구분해서 쓰지 않지만, 원칙적인 의미는 아래와 같이 후려칠 수 있다.

### 후려치기
- 크롤링 : 링크에 들어가서, 또 다음 링크를 찾아서 계속 타고 들어가는 것
- 스크래핑 : 요청을 해서 데이터를 받아오는 행위, 링크를 타고 들어간 웹페이지에 있는 모든 텍스트 및 메타데이터를 가져오는 것
- 파싱 : 받아온 데이터를 규칙에 따라 실제로 필요한 데이터만 추려내는 행위

### 참고자료
[데이터홀릭 박박사의 자동화특집 1탄 [크롤링] - Ep(9~10)](https://www.youtube.com/watch?v=BiGkVOcpwZE&list=PLOvmIXlrvHO1lpARAL9nQ-Ws1NbDuIA0Q&index=2)

### 소화하기
예를 들어 내 블로그의 모든 포스트의 최종수정일 정보를 모으겠다고 하면
1. 크롤링 : 포스트 아카이브 페이지에 있는 모든 링크로 타고 들어간다.
2. 스크래핑 : 각 링크에 저장된 모든 데이터를 가져온다.
3. 파싱 : 그 중에서 최종수정일 정보만 선택해서 저장한다.
