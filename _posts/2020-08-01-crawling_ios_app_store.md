```
​```
---
title: "iOS App Store Reivew Crawler"
excerpt: "using BeautifulSoup & Selenium"
last_modified_at: 2020-08-01T16:20:02-05:00
categories:
  - Data
tags: [Crawling, BeautifulSoup, Selenium]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---
​```
```



### Intro

애플 앱스토어는 상대적으로 크롤링 패키지가 적거나, 기능이 제한적이다. 그래서 직접 크롤러를 만드려고 봤더니, 전체 리뷰에 대한 정보는 동적 페이지로 구성되어 있다. 예를 들어서 [`https://apps.apple.com/kr/app/gs-space/id1475745149#see-all/reviews`](https://apps.apple.com/kr/app/gs-space/id1475745149#see-all/reviews)라는 url을 바로 입력해도 반드시 [`https://apps.apple.com/kr/app/gs-space/id1475745149`](https://apps.apple.com/kr/app/gs-space/id1475745149#see-all/reviews)

를 거쳤다가 re-route된다. 평가 및 리뷰를 `모두 보기`를 선택해도, 스크롤바가 최하단에 있어야 야금야금 다음 앱 리뷰들을 불러온다. 그래서 직접 브라우저를 제어해줄 Selenium이 반드시 필요했다.



### 필요한 정보별로 사용한 방법

- 평점, 평가 개수, 리뷰 개수 : BeautifulSoup으로 HTML 문서를 파싱

- 리뷰 내용 : Selenium으로 모든 리뷰를 불러올 수 있도록 웹 브라우저를 제어한 후, Beautiful Soup으로 HTML 파싱

  

### 수집한 앱 정보의 활용

단순히 앱 정보를 수집만 할 수도 있을 것이고, 전체 리뷰의 텍스트 분석을 할 수도 있다. 나의 경우, 앱 리뷰 현황을 파악하고 새로운 리뷰가 추가되었는지 확인하기 위한 것이다. 따라서 앱 리뷰 현황과 함께 개발자 답글이 달리지 않은 리뷰가 있다면, MS Teams로 메시지를 보내주었다.



### Selenium webdriver install 방법 두 가지

먼저 어떤 웹 브라우저를 사용할지 하나를 먼저 선택해야 한다. 그에 따라서 웹 드라이버도 달라진다.

나는 가장 즐겨 쓰는 크롬을 선택!

웹 드라이버를 설치하는 방법은 아래와 같이 두 가지가 있다. 속도, 배포 여부 등에 따라서 어느 쪽이 더 좋은 방법인지는 달라질 것이다.

1. 웹 드라이버 설치 후 절대경로로 호출 아래 링크에서 다운로드 받은 후 그 위치를 절대경로로 설정하여 호출하는 방법 다운로드 링크 : https://sites.google.com/a/chromium.org/chromedriver/downloads

   ```python
   #from selenium import webdriver
   driver = webdriver.Chrome(executable_path = r"C:\\Users\\user_name\\webdrive\\chromedriver.exe")
   ```

2. 웹 드라이버 매니저 인스턴스를 통한 호출

   ```python
   from selenium import webdriver
   from webdriver_manager.chrome import ChromeDriverManager
   
   driver = webdriver.Chrome(ChromeDriverManager().install())
   ```



### Python Code

```python
# 원하는 앱 선택
lang = "kr"
name = "gs-space"
code = "id1475745149"
app_store_url = '<https://apps.apple.com/'+lang+'/app/'+name+'/'+code+'#see-all/reviews>'
```

```python
# selenium으로 브라우저를 직접 컨트롤하여 모든 페이지를 연 후에 HTML 파싱
#!pip install selenium
#!pip install webdriver_manager
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import Keys
import time
from bs4 import BeautifulSoup

driver = webdriver.Chrome(ChromeDriverManager().install())
driver.maximize_window()
driver.get(app_store_url)
driver.implicitly_wait(10) # re-routing 될 수 있는 시간을 확보
body = driver.find_element_by_css_selector('body')

num_of_pagedowns = 10 # 스크롤바 이동을 10번 반복
while num_of_pagedowns:
    body.send_keys(Keys.PAGE_DOWN) # 스크롤바를 페이지 최하단으로 이동
    time.sleep(0.5)
    num_of_pagedowns -= 1
    
html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')

driver.close()
driver.quit()
```

```python
# 필요한 정보만 선별 및 조건에 따른 액션 수행
import re

review = str(len(soup.findAll('div', {'role':'article'})))
ratings = soup.findAll('p',"we-customer-ratings__count medium-hide")[0].string.split('개의 평가')[0]
average = soup.findAll('span',"we-customer-ratings__averages__display")[0].string
msg =  "[iOS App store] 평점 : "+ average + " / 평가개수 : "+ ratings + " / 리뷰개수 : "+ review
myTeamsMessage.text(msg)
myTeamsMessage.send()

for i in range(0, int(review)):
    if len(soup.findAll('div', {'role':'article'})[i].findAll('blockquote')) >= 2:
        pass
    else : 
        new = soup.findAll('div', {'role':'article'})[i]
        score = re.search('\\d+', str(new.find('span',"we-star-rating-stars-outlines").find('span')))[0]
        userid = new.find('span', 'we-truncate we-truncate--single-line ember-view we-customer-review__user').string.strip()
        time = new.find('time').string
        title = new.find('h3').string.strip()
        contents = new.findAll('p', {'dir':'ltr'})[0].string.strip()
        alarm = "[iOS App store] 개발자 답글이 필요한 리뷰가 추가되었습니다. / 점수 : "+score+" / 아이디 : "+userid+" / 시간 : "+time+" / 제목 : "+title+" / 내용 : "+contents
        myTeamsMessage.text(alarm)
        myTeamsMessage.send()
```