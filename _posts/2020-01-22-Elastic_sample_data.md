--
title: "샘플 데이터로 엿보는 kibana의 주요 기능"
excerpt: "엘라스틱을 위한 아직도 첫걸음"
last_modified_at: 2020-01-22T10:20:02-05:00
categories:
  - Elastic
tags: [Elastic, Elasticsearch, Elastic stack, ELK stack, data, DB]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---


### 샘플 데이터로 엿보는 kibana의 주요 기능
Kibana까지 제대로 설치되었다면, 샘플 데이터를 이용하여 구동법을 확인할 수 있다.



### 1. Kibana 접속 
1. 명령 프롬프트 관리자 권한으로 실행
2. 아래와 같이 해당 폴더 찾아가서 `bin\kibana.bat`실행
   ```
   C:\WINDOWS\system32>cd c:\elastic\kibana-7.5.1
   C:\elastic\kibana-7.5.1>bin\kibana.bat
   ```
3. 설치 확인 : 크롬 브라우저에 `http://localhost:5601`을 입력



### 2. 샘플 데이터 열기
1. 제일 좌상단의 kibana hompage icon 선택
2. "Add Data to Kibana"라는 창 인쪽 하단에 작게 `Add sample data` 선택
3. `sample eCommerce orders`, `sample flight data`, `sample web logs`라는 세 개의 샘플 데이터 중 원하는 것을 선택
![sample](https://www.elastic.co/guide/en/kibana/current/images/add-sample-data.png)


### 3. Kibana 구성
- dashboard : 중요지표들을 한눈에 볼 수 있는 대시보드, visualization의 요소들로 구성되어 있음
- visualization : area chart, heat map, region map, gauge, pie chart, markdown 등 보여주고자 하는 내용에 알맞은 시각화 자료 
- canvas : 동적 프레젠테이션을 위한 툴, 기능적으로는 visualization + dashboard
- dev tools : cmd에서 cURL 명령을 쓰는 대신, dev tools의 콘솔창을 통하여 데이터를 바로 사용할 수 있음



### 4. kibana를 위한 팁!
- 만지다보면 감이오지만 그래도 복잡하다면 https://www.elastic.co/guide/en/kibana/current/tutorial-sample-data.html
- 인덱스가 잘 로드 되었나 확인하는 법 : `http://localhost:9200/_cat/indices?v`에서 원하는 index 이름을 찾고, docs.counts가 0이 아닌지 확인 
- 메뉴를 보기가 불편하다면, 왼쪽 하단의 햄버거 아이콘의 `Expands`를 선택
