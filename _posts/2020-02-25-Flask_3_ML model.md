---
title: "Flask와 머신러닝 모델을 이용한 웹서비스_웹페이지로 뿅"
excerpt: "학습된 모델과 HTML페이지를 연결"
last_modified_at: 2020-02-24T16:20:02-05:00
categories:
  - Web
tags: [Flask, ML, SVHN, pickle]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

웹서비스에서 보여줄 `index.html`을 만들고  
이미 만들어둔 `model.pkl`과 html을 연결하면 웹서비스가 뿅!  


### HTML 작성
1. 아무 text editor에서 아래의 코드를 작성하여 `index.html`로 저장
   ````html
   <html>
   
   <head>
       <title>number image reader</title>
       <link rel="stylesheet" href="{{ url_for('static', filename = 'style.css') }}">
       <meta charset="utf-8">
       <meta name="viewport" content="width=device-width, initial-scale=1">
   </head>
   
   <body>
   <h1>Number Image Predictor based on SVHN data</h1>
   <div class="agile-its">
       <h2>ML Web Service with Flask</h2>
       <div class="w3layouts">
           <div class="photos-upload-view">
   
               <form id="upload" action="/predict" method="POST" enctype="multipart/form-data">
                   <div class="upload-btn-wrapper">
                       <button class="btn">이미지 업로드</button>
                       <input type="file" value="Upload" name="image">
                   </div>
                   <input type="submit" value="예측 결과">
                   {% if label %}
                       <span class="result_lable">
                           {{ label }}
                       </span>
                   {% endif %}
               </form>
           </div>
       </div>
   </div>
   </body>
   
   </html>
   ````



### 학습된 모델과 HTML페이지를 연결
1. 아무 text editor에서 아래의 코드를 작성하여, `main.py`로 저장
   ````python
   import flask
   import imageio
   from flask import Flask, request, render_template
   from sklearn.externals import joblib
   import numpy as np
   
   app = Flask(__name__)
   
   # index 페이지 라우팅
   @app.route("/")
   @app.route("/index")
   def index():
       return flask.render_template('index.html')
   
   # 이미지 업로드에 대한 예측값 반환
   @app.route('/predict', methods=['POST'])
   def make_prediction():
       if request.method == 'POST':
   
           # 업로드 파일 처리 분기
           file = request.files['image']
           if not file: return render_template('index.html', label="No Files")
   
           # 이미지 픽셀 정보 읽기
           # 알파 채널 값 제거 후 1차원 Reshape
           img = imageio.imread(file)
           img = img[:, :, :3]
           img = img.reshape(1, -1)
   
           # 입력 받은 이미지 예측
           prediction = model.predict(img)
   
           # 예측 값을 1차원 배열로부터 확인 가능한 문자열로 변환
           label = str(np.squeeze(prediction))
   
           # 숫자가 10일 경우 0으로 처리
           if label == '10': label = '0'
   
           # 결과 리턴
           return render_template('index.html', label=label)
   
   # 미리 학습시켜서 만들어둔 모델 로드
   if __name__ == '__main__':
       model = joblib.load('./model_test_32x32.pkl')
       app.run(host='0.0.0.0', port=8000, debug=True)
   ````

2. 폴더 정리
   - 가상폴더 하위 어떤 폴더 내에 `main.py` 파일, `model.pkl` 파일, `templates`폴더가 있고, `templates`폴더 하위에 `index.html`이 위치
     ````
     D\project\enev
         .
         ├── main.py
         ├── model_test_32x32.pkl
         │   ├── templates
         |   |   ├── index.html
     ````

3. `cmd`에서 [여기](https://bettermesol.github.io/web/2020/02/23/flask_1_venv/)에서 미리 만들어 둔 가상환경을 열어서, `main.py` 실행
   ````shell
   D:\project\venv>Scripts\activate
   (venv)D:\project\venv>cd (폴더가있다면폴더이름)
   (venv)D:\project\venv\(폴더가있다면폴더이름)> python main.py
   ````

4. 아무 인터넷 브라우저를 열고, 주소창에 `http://localhost:8000`혹은 `127.0.0.1:8000`입력



### 웹서비스를 열어서 예측 실행
1. 아무 인터넷 브라우저를 열고, 주소창에 `http://localhost:8000`혹은 `127.0.0.1:8000`입력
2. `이미지업로드`의 `찾아보기`버튼을 눌러서 [여기](https://bettermesol.github.io/web/2020/02/24/Flask_2_ML-model/)에서 미리 만들어놨던 테스트용 이미지 선택
3. `예측결과` 버튼을 눌러서 입력한 이미지의 숫자와 일치하는지 확인!
