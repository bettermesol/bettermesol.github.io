---
title: "Ajax 기반 웹페이지 크롤링"
excerpt: "Ajax 기반 웹페이지 크롤링"
last_modified_at: 2019-12-11T16:20:02-05:00
categories:
  - Data
tags: [data, crawling, html, ajax]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

### Ajax 기반 웹페이지 크롤링

- 원리 : 서버에서 받아온 원본 데이터를 통째로 받아오기

- 원본 데이터 확인 

  1. 개발자도구 > Network > "XHR" 선택 > 웹페이지 새로고침 > Preview나 Response를 이용해서 대상 데이터 확인 
  2. 대상 데이터의 Headers에서 General의 "Request URL"과 Form Data(view source)를 조합해서 request할 URL 확인
  3. reqeust URL로 했을 때 Network의 Response에서 본 것과 같은 결과가 나오는지 확인

- 실습

  1. 서울시 공공임대주택의 일반 정보 크롤링 (https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoListView.do)

     ![crawling_ajax](/assets/images//2019-12-11-crawling_ajax.JPG)

  2. request URL : https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoList.do?pageIndex=1&searchTyId=&brtcCode=11&signguCode=&emdCode=&hsmpNm=&suplyTy=&houseTy=&suplyPrvuseAr=&bassMtRntchrg=

     (여기서 null은 제외하고  https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoList.do?pageIndex=1&brtcCode=11만 입력해도 서울 전체 모든 공공임대주택을 확인할 수 있다.)

  3. 코드

     ````python
     import requests
     import json
     import pandas as pd
     
     ### 검색 조건 설정
     brtcCode = "11"  # 11 서울, 50 제주도 41 경기도
     suplyTy = "05"   # null 전체, 01 영구임대, 02 국민임대 03 50년임대 04 20년임대 05 10년임대 06 5년임대 07 장기전세 09 행복주택 10 공공기숙사
     
     ### 전체 데이터 및 페이지 수 확인
     url = "https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoList.do?pageIndex=1&searchTyId=&brtcCode=" + brtcCode + "&signguCode=&hsmpNm=&suplyTy=" + suplyTy + "&houseTy=&suplyPrvuseAr=&bassMtRntchrg="
     
     data = requests.get(url).json()
     totalpage = int(data['resultCnt'])//10+1
     
     print(data['resultCnt'])
     print(totalpage)
     
     ### 각 페이지별 response를 json > dict > dataframe으로 변환
     result = []
     for pageno in range(totalpage):
         pageno += 1
         pageurl = "https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoList.do?pageIndex=" + str(pageno) + "&searchTyId=&brtcCode=" + brtcCode + "&signguCode=&hsmpNm=&suplyTy=" + suplyTy + "&houseTy=&suplyPrvuseAr=&bassMtRntchrg="
         pagedata = requests.get(pageurl).json()
         for house in pagedata['resultList']:
             num = house['rn']
             ID = house['hsmpSn']
             adrs = house['rnAdres']
             hshl = house['hshldCo']
             typename = house['houseTyNm']
             name = house['hsmpNm']
             typ = house['suplyTyNm']
             supply = house['insttDc']
             result.append([num]+[ID]+[adrs]+[hshl]+[typename]+[name]+[typ]+[supply])
             
     houselist = pd.DataFrame(result[0:],columns=('num','ID','adrs','hshl','typename','name','typ','supply'))
     print(houselist)
     
     ### 그러면 https://www.myhome.go.kr/hws/portal/sch/selectRentalHouseInfoList.do?pageIndex=1&searchTyId=&brtcCode=11&signguCode=&hsmpNm=&suplyTy=05&houseTy=&suplyPrvuseAr=&bassMtRntchrg=에서 보는 것과 같은 결과
     ````

     

