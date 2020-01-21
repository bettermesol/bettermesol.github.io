---
title: "엘라스틱 스텍 설치"
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
1. C 혹은 D 드라이브 하위에 `elasticsearch`  폴더 생성
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/elasticsearch
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. 명령 프롬프트에서 아래와 같이 해당 폴더 찾아가서 `bin\elasticsearch.bat`실행
   ```
   C:\WINDOWS\system32
   C:\WINDOWS\system32>cd..
   C:\WINDOWS>cd..
   C:\>cd elasticsearch
   C:\elasticsearch>cd elasticsearch-7.5.1
   C:\elasticsearch\elasticsearch-7.5.1>bin\elasticsearch.bat
   ```
5. 설치 확인 : 크롬 브라우저에 `http://127.0.0.1:9200`을 입력해서 화면 확인

   

###  Kibana 설치
1. (C 혹은 D 드라이브 하위에 `elasticsearch`  폴더 생성)
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/kibana
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. 명령 프롬프트에서 아래와 같이 해당 폴더 찾아가서 `bin\kibana.bat`실행
   ```
   C:\WINDOWS\system32
   C:\WINDOWS\system32>cd..
   C:\WINDOWS>cd..
   C:\>cd elasticsearch
   C:\elasticsearch>cd kibana-7.5.1
   C:\elasticsearch\kibana-7.5.1>bin\kibana.bat
   ```
5. 설치 확인 : 크롬 브라우저에 `http://localhost:5601`을 입력해서 로딩 확인



### Beats 설치
Beats는 흔히 말하는 ELK stack에는 포함되지 않으며, 데이터 타입에 따라서 다양한 beat가 있다. 
그러니 반드시 설치할 필요는 없다.
하지만 난 샘플로 시스템 모니터링을 하려고 하니 metrixbeat를 설치!

1. (C 혹은 D 드라이브 하위에 `elasticsearch`  폴더 생성)
2. 설치파일 다운로드 : www.elastic.co/kr/downloads/beats/metricbeat
3. 2의 다운로드 파일을 1의 폴더에 압축 풀기
4. 명령 프롬프트에서 아래와 같이 해당 폴더 찾아가서 `setup` 실행
   ```
   C:\WINDOWS\system32
   C:\WINDOWS\system32>cd..
   C:\WINDOWS>cd..
   C:\>cd elasticsearch
   C:\elasticsearch>cd metricbeat-7.5.1
   C:\elasticsearch\metricbeat-7.5.1>.\install-service-metricbeat.ps1
   C:\elasticsearch\metricbeat-7.5.1>.\metricbeat.exe modules enable system
   C:\elasticsearch\metricbeat-7.5.1>metricbeat.exe setup -e
   ```
5. 설치 확인 : 
   크롬 브라우저의 kibana에서 `Metricbeat System`이 들어간 Dashboard와 연동여부 확인, 미리 설정된 다양한 정보를 볼 수 있다.
   한눈에 보이는건 Dashboard 중 `[Metricbeat System] Overview ECS`
   이렇게 하면 metricbeat 데이터가 바로 elasticsearch로 보내짐  
 (참고 : https://www.elastic.co/kr/blog/get-system-logs-and-metrics-into-elasticsearch-with-beats-system-modules)


### Logstach 설치
1. (C 혹은 D 드라이브 하위에 `elasticsearch`  폴더 생성)
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
   - 저장 위치 : 3의 폴더 아래 (ex. `C:\elasticsearch\logstash-7.5.1`)
5. 명령 프롬프트에서 아래와 같이 해당 폴더 찾아가서 실행
   ```
   C:\WINDOWS\system32
   C:\WINDOWS\system32>cd..
   C:\WINDOWS>cd..
   C:\>cd elasticsearch
   C:\elasticsearch>logstash-7.5.1
   C:\elasticsearch\logstash-7.5.1>bin\logstash -f logstash-simple.conf
   ```

   
