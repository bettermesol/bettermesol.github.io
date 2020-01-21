---
title: "JAVA 설치 및 환경설정"
excerpt: "엘라스틱을 향한 첫걸음을 떼기 전"
last_modified_at: 2020-01-21T18:20:02-05:00
categories:
  - Elastic
tags: [JAVA]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---




JAVA를 여러 버전 설치하면서  환경설정이 꼬여 있었는데 싹 지우고 다시 설치했다.  
그 기념으로 기억해두려고 쓰는 JAVA 설치 및 환경설정법



### 1. 설치파일 다운로드
https://www.oracle.com/technetwork/java/javase/downloads/index.html
최신 버전을 받는다면 로그인 불필요!
OS 확인> License Agreement 체크 > exe 파일 다운로드



### 2. 환경설정
`내 PC` 우클릭 > `자세히` > `속성` > `고급 시스템 설정` > `환경 변수`

1. 시스템 변수 설정 
   - `새로 만들기` > 
   - 변수 이름 : `JAVA_HOME`, 변수 값 : JAVA 설치 위치 (ex. `C:\Program Files\Java\jdk-13.0.2`) > 
   - `확인`

2. 사용자 변수 설정 
   - `Path` 선택해서 편집 >
   - `새로 만들기` : `%JAVA_HOME%\` 입력 >
   - `확인`

이렇게 해도 안된다면, 아래 과정도 해보기

3. 시스템 변수 추가 설정
   - `Path` 선택해서 편집 >
   - `새로 만들기` : `%JAVA_HOME%\bin` 입력 > 
   - `확인`

4. 시스템 변수 추가 설정
   - `새로 만들기` >
   - 변수 이름 : `CLASSPATH`, 변수 값 : `%JAVA_HOME%\lib`) > 
   - `확인`



### 3. 설정이 잘 되었다면
`명령 프롬프트(cmd)`에서 
```
java -version
```
이라고 입력해서, 에러 메시지가 아니라 설치된 자바 버전 정보가 쭉 뜨면 잘 설치된 것!
