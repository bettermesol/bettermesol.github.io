---
title: "엘라스틱 스택 설치"
excerpt: "엘라스틱을 위한 아직도 첫걸음"
last_modified_at: 2020-01-22T16:20:02-05:00
categories:
  - Elastic
tags: [Elastic, Elasticsearch, Elastic stack, ELK stack, data, DB]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

### Elasticsearch 설치
1. C 혹은 D 드라이브 하위에 `elastic`  폴더 생성
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/elasticsearch
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. 명령 프롬프트 관리자 권한으로 실행
5. 아래와 같이 해당 폴더 찾아가서 `bin\elasticsearch.bat`실행
   ```
   C:\WINDOWS\system32>cd c:\elastic\elasticsearch-7.5.1
   C:\elastic\elasticsearch-7.5.1>bin\elasticsearch.bat
   ```
5. 설치 확인 : 크롬 브라우저에 `http://127.0.0.1:9200`을 입력해서 화면 확인

   

### Logstach 설치
1. (C 혹은 D 드라이브 하위에 `elastic`  폴더 생성)
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/beats/logstash
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. text파일로 config file 생성
   - 파일 이름 : `logstash-simple.conf`
   - 내용
     ```
     input { stdin { } }
     output {
       elasticsearch { hosts => ["localhost:9200"] }
       stdout { codec => rubydebug }
     }
     ```
   - 저장 위치 : 3의 폴더 아래 config 폴더 (ex. `C:\elastic\logstash-7.5.1\config`)
5. 명령 프롬프트 관리자 권한으로 실행
6. 아래와 같이 해당 폴더 찾아가서 실행
   ```
   C:\WINDOWS\system32>cd c:\elastic\logstash-7.5.1
   C:\elastic\logstash-7.5.1>bin\logstash -f config\logstash-simple.conf
   ```



###  Kibana 설치
1. (C 혹은 D 드라이브 하위에 `elastic`  폴더 생성)
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/kibana
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. 명령 프롬프트 관리자 권한으로 실행
5. 아래와 같이 해당 폴더 찾아가서 `bin\kibana.bat`실행
   ```
   C:\WINDOWS\system32>cd c:\elastic\kibana-7.5.1
   C:\elastic\kibana-7.5.1>bin\kibana.bat
   ```
5. 설치 확인 : 크롬 브라우저에 `http://localhost:5601`을 입력해서 로딩 확인

   
