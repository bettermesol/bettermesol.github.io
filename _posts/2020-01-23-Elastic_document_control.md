---
title: "엘라스틱 데이터 구조 및 도큐먼트 컨트롤"
excerpt: "엘라스틱을 위한 나아갈 다음 걸음"
last_modified_at: 2020-01-23T10:20:02-05:00
categories:
  - Elastic
tags: [Elastic, Elasticsearch, Elastic stack, ELK stack, data, DB]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

### Elasticsearch 내 데이터 구조
![document structure](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile22.uf.tistory.com%2Fimage%2F998444375C98CC021F2221)

- 구조 : Cluster > node > index > shard
- index : RDBMS의 database와 유사한 개념, 1개 이상의 primary shard에 매핑되고, 0개 이상의 replica shard를 가질 수 있는 논리적 공간
- type : RDBMS의 table과 유사한 개념
- Document : RDMBS의 row와 유사한 개념, 즉 하나하나의 데이터 포인트를 의미



### Document 추가 
- 문서 색인화 : Restful API를 통해서 index에 document를 추가하는 과정.
- id를 지정해주지 않으면 자동부여
- type을 지정할 필요가 없다. (Elastic 7.0 이후, [이 글](https://bettermesol.github.io/elastic/2020/01/21/Elastic_base/) 참고)

- 추가 방법 : `Dev Tools` > `Console`에 아래 내용 입력 후 `click to send request`  
  ```
  # resident란 index에 1번 id에 이름이 Mesol Yoon인 document 추가
  POST resident/_doc/1
  {
    "name": "Mesol Yoon"
  }
  ```

- 결과 확인법 : `Dev Tools` > `Console`에 아래 내용 입력 후 `click to send request`  
  ```
  GET /_cat/indices?v        #docs.count=1인 index resident 생성
  ```

- 만약 health=yellow라면 [이 글](https://bettermesol.github.io/elastic/2020/01/22/Elastic_Status-check/)을 참고해서 replica shard의 개수를 0으로 바꿔준다.
- json, csv, log 등에서 데이터를 가져온다면 logstash 등의 설정부터 필요하므로, 이건 따로 다룬다.



### Document 간단 조회
- 조회 방법 : `Dev Tools` > `Console`에 아래 내용 입력 후 `click to send request`  
  ```
  # 모든 index에 있는 모든 coument를 조회
  GET _all/_search
  
  # resident란 index에 있는 모든 document를 조회
  GET resident/_search 
  
  # resident란 index에 있는 1번 document를 조회
  GET resident/_doc/1
  
  # resident란 index에 있는 1번 document의 source 정보만 조회
  GET resident/_doc/1?pretty&filter_path=_source
  ```

  

### Document 수정
- Document 추가 방법과 동일
- 수정방법 : `Dev Tools` > `Console`에 아래 내용 입력 후 `click to send request`  
  ```
  # resident란 index에 1번 id에 이름이 Mesol Yoon인 document를 NaNaNa로 수정
  POST resident/_doc/1
  {
    "name": "Better Mesol"
  }
  ```

  

### Document 삭제
- 삭제방법 : `Dev Tools` > `Console`에 아래 내용 입력 후 `click to send request`
  ```
  # resident란 index를 삭제
  DELETE resident
  
  # resident란 index에 있는 1번 document를 삭제
  DELETE resident/_doc/1
  ```

  
