---
title: "지오코딩 / 역지오코딩"
excerpt: "주소 좌표 변환을 위한 방법"
last_modified_at: 2019-11-06T16:20:02-05:00
categories:
  - spatial analysis
tags: [spatial, urban, data, geocoding]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

### 지오코딩 / 역지오코딩

- geocoding : 주소나 이름을 이용해서 위도와 경도의 좌표값을 얻는 것

- reverse-geocoding: 위도와 경도의 좌표값을 이용해서 주소를 얻는 것

  

### 주소변환 

- 상황에 따라 주소변환이 필요하기도 하다. 그러면, 
- 행정안전부 : http://www.juso.go.kr/openIndexPage.do#
- 오픈메이트 :  http://www.geocoding.co.kr/xga/index.jsp 



### 지오코딩 방법 : 쉽다. 서비스도 많이 제공하고, 샘플도 많다.

1.  웹서비스 이용
    - [국토연구원](http://geeps.krihs.re.kr/geocoding/service_page) : 조금 느리지만 무료 
    - [오픈메이트]( http://www.geocoding.co.kr/xga/index.jsp ) :  사용법이 쉽지만 유료, 주소 정제 서비스도 제공
2.  API 이용 : reverse geocoding의 API 사용법 응용
3.  소프트웨어 
    - biz-gis
      -  http://www.biz-gis.com/index.php?mid=pds&document_srl=187250 
      -  무료
      -  x-ray map / 1회 100건
      -  GeocodingTool64.exe/1일 1만건 제한 (IP 기준)
    - 지오서비스 (공간정보시스템 기반 기술 연구소)
      - Geocoder-Xr 2019
      - http://www.gisdeveloper.co.kr/?p=4784 
      - 건수 제한은 없지만,  변환 건마다 0.4초씩 딜레이 
4.  Google Geocoder (Geocode by Awesom Table App)
    - 무료지만 몹시 느림 : 200건에 20분 정도
    - 구글 스프레드시트에서 "Start geocoding"



### 역지오코딩 방법 : 툴을 쓰거나 코드를 짜야해서 상대적으로 번거롭다.

1. Software 사용 (좌표 > 주소 확인) : 지오코딩의 지오서비스
2. GIS software 사용 (좌표>행정구역 확인)
   - ArcGIS, QGIS 등 GIS software을 쓸 줄 알고, 설치가 되어 있다면
     - 1) 좌표를 이용해서 point 생성
     - 2) 행정구역 polygon 열기
     - 3) spatial join을 통해서 각 point에 해당하는 행정동 확인
3. geopandas를 사용  (좌표>행정구역 확인) : 다른 GIS software와 원리는 같다. ([관련 코드]())
4. API 사용 ((좌표 > 주소 or 행정구역 확인) :

- 네이버, 구글 등에서 지도 관련 API를 제공 
- 횟수 제한이 적고, 구글이나 네이버에 비해서[1] 카카오 API를 추천 (2019.11.05 기준) ([관련 코드]())



[1] 서울 빅데이터기획팀장님 피셜
