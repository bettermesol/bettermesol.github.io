```
​```
---
title: "Windows Task Scheduler를 이용한 자동 실행"
excerpt: "윈도우즈 세상에서 시킬 수 있는 가장 쉬운 자동 실행"
last_modified_at: 2020-08-03T16:20:02-05:00
categories:
  - Data
tags: [windows, task scheduler, RPA]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---
​```
```



### 자동 실행시킬 파일 생성

pyinstaller를 이용해서 `.exe` 파일을 생성할 수도 있겠지만, 그마저도 귀찮으니 아래처럼 해보자!

1. `.py` 파일 생성

2. `.bat` 파일 작성

   ```
   ".py 파일을 실행할 python.exe의 위치\\python.exe" "실행할 .py파일의 위치\\파일명.py"
   pause
   ```

3. 위 코드에서 `pause`는 에러가 있을 때 디버깅을 위한 것이니, 문제가 없다는 것을 다 확인했다면 지워도 된다!



### Windows Task Scheduler 설정

윈도우즈 기본 프로그램인 작업 스케줄러(Task Scheduler, taskschd)를 실행하여 '동작-작업 만들기'에서 아래와 같은 설정으로 `.bat`를 주기적으로 실행시키면 된다.

![Windows Task Scheduler1.png](/assets/images/2020-08-03_Windows Task Scheduler1.png)

![Windows Task Scheduler2.png](/assets/images/2020-08-03_Windows Task Scheduler2.png)

![Windows Task Scheduler3.png](/assets/images/2020-08-03_Windows Task Scheduler3.png)



### 서버를 이용한 자동 실행

서버가 있어서 `.py` 파일을 non-stop으로 실행시킬 수 있다면, 굳이 windows task manager를 쓰지 않아도 된다. APScheduler 등을 이용해서 python code 자체에 scheduler를 심은 다음에 서버에서 실행시키면 되니까. Heroku 등 거의 혹은 무료로 사용할 수 있는 클라우드 서비스도 많으니, 이것도 좋은 옵션이 될 것이다!