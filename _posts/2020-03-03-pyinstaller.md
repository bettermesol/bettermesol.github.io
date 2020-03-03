---
title: "pyinstaller_파이썬으로 .exe 빌드하기"
excerpt: "pyinstaller를 이용해서 .py를 .exe로!"
last_modified_at: 2020-03-02T16:20:02-05:00
categories:
  - app
tags: [pyinstaller, exe, build, app, desktop app]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

파이썬으로 작성한 코드를 서비스로 만들거나, 혹은 파이썬을 설치하지 않은 사람에게 배포해야 할 상황이 생긴다. 
혹은 내가 게으름뱅이라서 .py 파일을 매번 실행시키기 귀찮거나!
아무튼 pyindtaller를 이용해서 .py를 .exe로 build해본다!



0. 환경
   - 운영체제 : windows 10
   - 파이썬 버전 : python 3.7

1. pyinstaller 패키지 설치
   - `cmd`를 열어 아래 명령어 입력
     ````
     pip install pyinstaller
     ````

2. 샘플 파이썬 코드 만들기
   - 적당한 샘플을 만들다보니 `time` 패키지가 필요하다. `cmd`를 열어 아래 명령어도 입력
     ````
     pip install time
     ````

   - 아무 텍스트 에디터를 열어 아래 내용을 입력하고 적당한 위치에 `time.py`라는 이름과 확장자로 저장
     ````
     import time 
     if __name__ == "__main__" : 
          print("10초 카운트 시작!") 
          print("시작시간 : " + time.strftime('%c', time.localtime(time.time())))
          i = 0
          while i <10:
              i += 1
              print(str(i)+"초 경과")
              time.sleep(1)
          print("종료시간 : " + time.strftime('%c', time.localtime(time.time())))
          print("10초 카운트 완료! 3초 후 프로그램이 종료됩니다.")
          time.sleep(3)
     ````

3. exe로 만들기
   - `cmd`를 열어 2의 파이썬 파일이 저장된 위치로 찾아가서 아래 명령어 입력
     ````
     pyinstaller time.py
     ````

   - 원하는 조건에 따라 옵션을 추가한다면, 아래 명령어 추가 입력
     - 부수적인 파일을 모두 하나의 exe 파일 생성 : `--onefile` 혹은 `-F`
     - Dos console 없이 실행 :  `--noconsole`  혹은 `-w`
     - 관련 옵션 : https://stackoverflow.com/questions/19225132/pyinstaller-not-working-on-simple-helloworld-program
     ```` 
     pyinstaller --onefile time.py
     ````

4. exe 실행
   - 2에서 정한 폴더 내 dist 폴더 내에 `time.exe`를 실행!
   - 그럼 아래와 같은 창이 뿅! 떠서 혼자서 10초 세고, 3초 후 뽕하고 사라진다!!
     ![result](/assets/images/2020-03-03-pyinstaller.png)
