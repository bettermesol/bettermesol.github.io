---
title: "웹 크롤링의 세 가지 방법"
excerpt: "패키지 vs BeautifulSoup vs Selenium "
last_modified_at: 2020-07-30T16:20:02-05:00
categories:
  - Web
tags: [Crawling, BeautifulSoup, Selenium]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



### 크롤링 방법 결정

크롤링을 하려는 페이지의 특성에 따라서 어떠한 방법을 선택해야 할지도 달라진다.



1. 패키지

   - 사용처 : 구글 플레이스토어처럼 남들도 많이 크롤링을 하는 곳

   - 선택의 이유 : 이미 잘 만들어진 crawler/scraper가 있다면 package install만 하면 되니, 구글링을 잘 해보자

     

2. BeautifulSoup

   - 사용처 : 필요한 정보가 HTML 소스에 모두 담겨 있는 웹의 경우에 사용

   - 선택의 이유 : 가볍게 HTML 소스를 받아와서, 쉽게 파싱할 수 있다!

     

3. Selenium

   - 특징 : 사용자가 Chrome을 열어서 URL을 입력하고, 마우스 휠로 페이지 특정 위치로 이동해서 버튼을 누르는 등, 웹 브라우저를 대신 제어시켜 주는 웹 프레임워크

   - 사용처 : `더 보기` 버튼을 눌러야만 다음 페이지가 야금야금 로딩되는 식의 동적 웹 크롤링에 사용

   - 선택의 이유 : 원해서 하는 선택이 아니다. 시간도 오래 걸리지만 동적 웹을 크롤링 해야 한다면 다른 선택이 없다.

     

하나의 정보를 위해서 한 가지 방법만 사용할 필요는 없다. 더 손쉬운 방법으로 섞어서도 쓸 수 있다.
