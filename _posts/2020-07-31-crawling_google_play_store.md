---
title: "Google Play Store App Review Crawler"
excerpt: "using BeautifulSoup & google_play_scraper"
last_modified_at: 2020-07-31T16:20:02-05:00
categories:
  - Data
tags: [Crawling, BeautifulSoup, Selenium]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---





### Intro

구글 플레이스토어는 많은 사람들이 필요로 해서 그런지 앱 정보 및 리뷰에 대한 크롤링 패키지가 정말 잘 만들어져 있다. 그 중에서 [google_play_scraper](https://pypi.org/project/google-play-scraper/)가 잘 만들어져 있고, 아래와 같이 다양한 레벨의 함수를 제공한다.

- app : 앱의 세부 정보
- reviews : sort 조건에 따른 상위 n개의 리뷰
- reviews_all : 전체 리뷰

만약, 앱의 세부 정보 중 극히 일부만 필요하다면, 굳이 패키지를 사용하지 않고 BeautifulSoup으로 앱 소개 페이지의 HTML 문서를 파싱해서 필요한 정보만 몇 개 간단하게 추려올 수도 있다.



### 필요한 정보별로 사용한 방법

- 평점, 평가 개수 : BeautifulSoup으로 HTML 문서를 파싱
- 리뷰 개수 : google_play_scraper의 review_all 함수 사용
- 리뷰 내용 : google_play_scraper의 review_all의 결과에서 조건에 따른 선별



### 수집한 앱 정보의 활용

단순히 앱 정보를 수집만 할 수도 있을 것이고, 전체 리뷰의 텍스트 분석을 할 수도 있다. 나의 경우, 앱 리뷰 현황을 파악하고 새로운 리뷰가 추가되었는지 확인하기 위한 것이다. 따라서 앱 리뷰 현황과 함께 개발자 답글이 달리지 않은 리뷰가 있다면, MS Teams로 메시지를 보내주었다.



### Python Code

```python
# 원하는 앱 선택
lang='ko'
cont='kr'
loc = 'kr.co.twinspace'
```

```python
# BeautifulSoup을 이용한 Google PlayStore 앱 소개 페이지 HTML 파싱 함수
import requests
from bs4 import BeautifulSoup

def crawler(lang, cont, loc):
    url = 'https://play.google.com/store/apps/details?id='+loc+'&hl='+lang+'&gl='+cont
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    return (soup)
```

```python
# 패키지를 이용한 전체 리뷰 크롤링 함수
#! pip install google_play_scraper
from google_play_scraper import reviews, Sort

review_all, _ = reviews(
    loc,
    lang=lang, # defaults to 'en'
    country=country, # defaults to 'us'
    sort=Sort.NEWEST, # defaults to Sort.MOST_RELEVANT
    #count=3, # defaults to 100
    filter_score_with=None # defaults to None(means all score)
)
review = str(len(review_all))
```

```python
# 필요한 정보만 선별 및 조건에 따른 액션 수행

soup = crawler(lang, cont, loc)
ratings = soup.find('span','EymY4b').text
average = soup.findAll('div', 'BHMmbe')[0].string

msg =  "[Google Play store] 평점 : "+ average + " / 평가개수 : "+ ratings + " / 리뷰개수 : "+ review
myTeamsMessage.text(msg)
myTeamsMessage.send()

for i in range(0,len(review_all)):
    if review_all[i]['replyContent'] != None:
        pass
    else:
        score = str(review_all[i]['score'])
        userid = review_all[i]['userName']
        time = review_all[i]['at'].strftime("%Y/%m/%d %H:%M")
        content = review_all[i]['content']
        alarm = "[Google Play store] 개발자 답글이 필요한 리뷰가 추가되었습니다. / 점수 : "+score+" / 아이디 : "+userid+" / 시간 : "+time+" / 내용 : "+contents
        myTeamsMessage.text(alarm)
        myTeamsMessage.send()
```
