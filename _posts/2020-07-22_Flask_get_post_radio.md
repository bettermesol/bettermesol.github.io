---
title: "Flask_GET, POST로 입력 받아 HTML 출력하기 "
excerpt: "Flask "
last_modified_at: 2020-07-22T16:20:02-05:00
categories:
  - Web
tags: [Flask, Web]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



### 오늘의 목표

- GET, POST의 차이를 (대충) 안다.
- Flask에서 Radio Button을 만든다.
- Form 형식으로 Radio Button의 입력값을 GET or POST로 받는다.
- 입력값을 화면으로 출력한다.





### GET? POST?

- HTTP method
  - GET : resource 취득
  - POST : entity body 전송
  - PUT : file 전송
  - DELETE : file 삭제
  - HEAD : message header 취득
  - TRACE : 경로 조사
  - CONNECT : 프록시에서의 터널링 요구
  - OPTIONS : 응답 가능 method 요청

- GET vs POST
  - 모든 파라미터를 header에 담아 url로 보내서 요청하는 형태
  - 간단하지만 url만 있으면 모든 정보를 알 수 있으니 보안에 취약
- POST
  - 모든 파라미터를 body에 담아서 보내는 형태
  - 많은 양의 데이터를 보내기에 적합



### 폴더 트리

```
$tree -- dirsfirst
├── templates
│   └──  control.html
└── flask_getpost.py
```



### Flask에서 Radio Button 만들기

- control.html

  ```html
  <!doctype html>
  <html lang="ko">
    <head>
    <meta charset="utf-8">
      <title>HTML</title>
      
      <!-- CSS style 적용-->
      <style>
        * {
          font-size: 16px;
          font-family: Consolas, sans-serif;
        }
      </style>
    </head>
  
    <body>
      <form method="POST" action="/control">
      <!--<form method="GET" action="/control"> 
  
      <p>켤까 끌까</p>
          
        <label><input type="radio" name="onoff" value="on"> On</label>
        <label><input type="radio" name="onoff" value="off" checked> Off</label>
        <p><input type="submit" value="Submit"> <input type="reset" value="Reset"></p>
      </form>
      <div>
          <p>
              <!-- javascript 조건문 작성 -->
              {% if onoff == None %}
                  <h5> on/off 선택 후 submit을 눌러주세요.</h5>
              {% elif onoff == 'on' %}
                  <h5> {{onoff}}를 입력 받았습니다.<br>
                       시작합니다. </h5>
              {% else %}
                  <h5> {{onoff}}를 입력 받았습니다.<br>
                       종료합니다.</h5>
              {% endif %}
          </p>
      </div>
    </body>
  </html>
  ```

  

### 입력값을 받아서 출력하기

- flask_getpost.py

  ```python
  from flask import Flask, request, render_template
  
  app = Flask(__name__)
  
  @app.route('/input')
  def start(onoff=None):
      return render_template('control.html', onoff=onoff)
  
  @app.route('/control', methods=['POST', 'GET'])
  def control(onoff=None):
      if request.method == 'POST':
          status = request.form['onoff']
          return render_template('control.html', onoff=status)
      elif request.method == 'GET':
          status = request.args.get('onoff')
          return render_template('control.html', onoff=status)
  
  if __name__ == '__main__':
       app.run(host = '0.0.0.0') 
  ```

  

### 결과 확인해보기

![image-20200722154539826](/assets/images/2020-07-22-Flask_get_post_radio_input.png)![image-20200722154555488](/assets/images/2020-07-22-Flask_get_post_radio_control.png)
