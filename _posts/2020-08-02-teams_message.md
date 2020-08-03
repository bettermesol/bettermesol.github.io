---
title: "MS Teams 채널로 메시지 전송"
excerpt: "마소 세상에서 보낼 수 있는 간단한 알림"
last_modified_at: 2020-08-02T16:20:02-05:00
categories:
  - Data
tags: [webhook, MS, teams]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---




### Teams 설정

1. 앱에서 'Incoming Webhook'에서 앱을 추가할 채널 선택

   ![Teams_setting_1.png](/assets/images/2020-08-02_Teams_setting_1.png)

   ![Teams_setting_2.png](/assets/images/2020-08-02_Teams_setting_2.png)

   

2. 앱 채널에 대한 커낵터 설정 (이름, 이미지)

   ![Teams_setting_3.png](/assets/images/2020-08-02_Teams_setting_3.png)

   

3. URL 복사

   헙, URL을 알아야 하는데 실수로 창을 껐다? 그러면 '채널 우측 상단 기타 옵션 - 커넥터 - 구성됨 -  Incoming Webhook - 구성'으로 들어가서 다시 확인할 수 있다.

   ![Teams_setting_4.png](/assets/images/2020-08-02_Teams_setting_4.png)

   

### python code 작성

```python
#!pip install pymsteams
import pymsteams

teams_url = "복사한 URL"
myTeamsMessage = pymsteams.connectorcard(teams_url)

msg = "테스트용 메시지입니다. Teams에 잘 보내질까요?"

myTeamsMessage.text(msg)
myTeamsMessage.send()
```
