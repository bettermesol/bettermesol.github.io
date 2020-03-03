---
title: "pyinstaller+flask_파이썬으로 웹을 여는 .exe 빌드하기"
excerpt: "pyinstaller를 이용해서 .html과 .py를 .exe로!"
last_modified_at: 2020-03-03T20:20:02-05:00
categories:
  - app
tags: [pyinstaller, exe, build, app, desktop app]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---

flask를 이용하면 파이썬 코드의 결과물을 html로 작성한 웹 환경에서 볼 수 있다.
이 글을 따라하기 전에 [flask](https://bettermesol.github.io/web/2020/02/23/flask_1_venv/), [pyinstaller](https://bettermesol.github.io/app/2020/03/03/pyinstaller/)가 각각 설치되어 있어야 하므로, 설치 방법은 링크를 참고합시다!



1. `venv` 폴더 하위에 `executable_hello` 폴더 생성

2. HTML 작성하여 1의 폴더에 저장
   - 아무 text editor에서 아래의 코드를 작성하여 1의 폴더 하위에  `index_hello.html`로 저장
     ````
     <html>
     <title>Hello from Flask</title>
     {% if name %}
       <h1>Hello {{ name }}!</h1>
     {% else %}
       <h1>Hello, World!</h1>
     {% endif %}
     </html>
     ````

3. Flask를 이용해서 HTML을 불러오기
   - 아무 text editor에서 아래의 코드를 작성하여 `venv` 폴더 하위에 `app_hello.py`로 저장
     ````python
     import sys
     import os
     import webbrowser
     from threading import Timer
     from flask import Flask, render_template
     
     #https://github.com/smoqadam/PyFladesk/issues/9
     #template의 directory를 불러오도록 하는 코드'''
     if getattr(sys, 'frozen', False):
         template_folder = os.path.join(sys._MEIPASS, 'templates')
         app = Flask(__name__, template_folder=template_folder)
     else:
         app = Flask(__name__)
     
     @app.route('/')
     @app.route('/<name>')
     def hello_world(name=None):
         return render_template('index_hello.html', name=name)
     
     def open_browser():
           webbrowser.open_new('http://127.0.0.1:'+str(port)+'/') 
     #https://stackoverflow.com/questions/54235347/open-browser-automatically-when-python-code-is-executed
     #세션 종료 후가 아니라 코드 실행 후 자동적으로 웹 페이지가 열리도록 하기 위하여
     
     port=9000
             
     if __name__ == "__main__":
         Timer(1,open_browser).start();
         app.run(port=port, debug=True)        
     ````

4. 폴더 정리
   ````
   D\project\enev\executable_hello
       .
       ├── app_hello.py
       │   ├── templates
       |   |   ├── index_hello.html
   ````

5. pyinstaller로 exe build
   - `cmd`에서 `executable_hello` 폴더 위치까지 찾아간 다음, 아래 코드를 실행
     ````
     D\project\enev\executable_hello> pyinstaller --add-data "templates;templates" --add-data "static;static" app_hello.py 
     ````
   - 그럼 `executable_hello` 하위에 `build`, `dist`폴더가 생성된다.
   - `dist`를 배포받은 누구나 `app_hello.exe`를 실행하면 웹 브라우저에서 아래 화면이 뿅!
     ![installer+flask](/assets/images/2020-03-03-pyinstaller-flask.png)

   

   
