---
title: "Elastic 관련 글 작성기준 - Dev Tools & ver 7.0"
excerpt: "엘라스틱을 향한 첫걸음을 떼기 전"
last_modified_at: 2020-01-21T08:20:02-05:00
categories:
  - Elastic
tags: [JAVA]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

구글링에 의존해서 더듬더듬 elastic을 공부하는데, 구글링의 예제를 동일하게 적용해도 안되는 경우가 많다. 대부분 cURL 명령어를 사용하고, 또 Elastic 5~6버전을 쓰기 때문이다. 
여기에 있는 Elastic 관련 글에서는 아래와 같은 기준으로 작성했음을 미리 밝힌다.

- **cURL 대신 Dev Tools** : Elastic Dev Tools Console은 cURL과 매우 흡사한 명령어를 이해한다. 따라서 굳이 cURL을 설치하지 않고, Dev Tools에 맞춰서 명령어를 정리한다.
- **Elastic 7.5.1** : 대부분의 한글 자료는 5~6version 정도를 기준으로 한다. 하지만 공식 홈페이지의 안내를 보면 7.0 전후로 큰 변화가 있었던 듯 하다. 따라서 본 내용은 2020년 초 기준 최신 버전인 7.5.1을 기준으로 한다.

- 과거 버전으로 작성된 예시를 7.0 이후 버전으로 전환하는 방법은 아래 표를 참고하면 된다.

| Search API       | 6.x 이전                          | 7.0 이후                   |
| ---------------- | --------------------------------- | -------------------------- |
| search           | /{index}/{type}/_search           | {index}/_search            |
| msearch          | /{index}/{type}/_msearch          | /{index}/_msearch          |
| count            | /{index}/{type}/_count            | /{index}/_count            |
| explain          | /{index}/{type}/{id}/_explain     | /{index}/_explain/{id}     |
| search template  | /{index}/{type}/_search/template  | /{index}/_search/template  |
| msearch template | /{index}/{type}/_msearch/template | /{index}/_msearch/template |

| Document API | 6.x 이전                         | 7.0 이후                  |
| ------------ | -------------------------------- | ------------------------- |
| index        | /{index}/{type}/{id}             | /{index}/**_doc**/{id}    |
| delete       | /{index}/{type}/{id}             | /{index}/**_doc**/{id}    |
| get          | /{index}/{type}/{id}             | /{index}/**_doc**/{id}    |
| update       | /{index}/{type}/{id}/_update     | /{index}/_update/{id}     |
| get source   | /{index}/{type}/{id}/_source     | /{index}/_source/{id}     |
| bulk         | /{index}/{type}/_bulk            | /{index}/_bulk            |
| mget         | /{index}/{type}/_mget            | /{index}/_mget            |
| termvectors  | /{index}/{type}/{id}/_termvector | /{index}/_termvector/{id} |
| mtermvectors | /{index}/{type}/_mtermvectors    | /{index}/_mtermvectors    |

| Index API         | 6.x 이전                                | 7.0 이후                         |
| ----------------- | --------------------------------------- | -------------------------------- |
| create index      | /{index}                                | 변경 없음                        |
| get mapping       | /{index}/_mapping/{type}                | /{index}/_mapping                |
| put mapping       | /{index}/_mapping/{type}                | /{index}/_mapping                |
| get field mapping | /{index}/{type}/_mapping/field/{fields} | /{index}/_mapping/field/{fields} |
| get template      | /_template/{template}                   | 변경 없음                        |
| put template      | /_template/{template}                   | 변경 없음                        |



참고자료 : http://kimjmin.net/2019/04/2019-04-elastic-stack-7-release/
