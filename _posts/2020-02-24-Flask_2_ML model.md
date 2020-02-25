---
title: "Flask와 머신러닝 모델을 이용한 웹서비스_머신러닝 모델 학습"
excerpt: "웹페이지 구성을 위한 머신러닝 모델 학습"
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

워크플로우는 **데이터 전처리 + 학습 + 모델 추출 > 웹페이지 작성 > release **  
The Street view house numbers 데이터셋을 이용하여, 랜덤포레스트 알고리즘을 사용하여, 사진 속 숫자를 읽을 수 있는 모델을 만든다.



### 학습용 모델 작성 및 저장
1. 학습을 위한 데이터 다운로드 
   - http://ufldl.stanford.edu/housenumbers/에서 `test_32x32.mat` 파일 다운로드. 
   - 73257개의 32x32픽셀 이미지
   - i번쨰 데이터의 구성 : X변수는 이미지를 포함한 4차 행렬로 X(:,:,:,i)로 접근 가능, 이 때 Y(i)는  0~9 사이의 숫자

2. 아래의 코드 실행해서 모델을 학습하고, 추후에 테스트를 위한 이미지를 몇 장 확보해두고, 학습된 모델 저장 (가상환경에서 실행시킬 필요 없음, .ipynb파일을 원한다면 [여기](https://github.com/bettermesol/bettermesol.github.io/blob/master/assets/code/2020-02-24-Flask_2_ML%20model.ipynb))
   ````python
   import numpy
   import scipy.io
   from sklearn.utils import shuffle
   from sklearn.ensemble import RandomForestClassifier
   from sklearn.model_selection import train_test_split
   from sklearn.externals import joblib
   from sklearn import metrics
   
   # train_data : 8비트 부호없는 정수로 이미지를 저장해둔 이미지
   # 이미지 처리 기초 참고 : https://datascienceschool.net/view-notebook/9af8d8e93c084bc49f0ac2bb8a20e2a4/
   train_data = scipy.io.loadmat('./extra_32x32.mat')
   
   # 학습 데이터, 훈련 데이터
   raw_x = train_data['X']
   raw_y = train_data['y']
   
   # 배열요소의 데이터 타입 확인
   # x : (세로픽셀수, 가로픽셀수, 색채널, 레코드 번호)
   # y : (0~10사이의 label, 1), dtype : 부호없는 8비트의 정수
   raw_x.shape, raw_x.dtype, raw_y.shape, raw_y.dtype
   
   # x 이미지 확인을 위하여 첫번째 이미지 열어보기
   img = raw_x[:,:,:,0]
   plt.imshow(img)
   
   # y 라벨 확인
   unique, counts = numpy.unique(raw_y, return_counts=True)
   dict(zip(unique, counts))
   
   # 데이터 전처리 
   # 1) x행렬을 1차원으로 변환
   # x: (32, 32, 3, 26032) > 1차원 전환 x: (32*32*3, 26032) > 라벨이 먼저 오도록 순서 변경 x: (28032, 32*32*3)
   x = raw_x.reshape(raw_x.shape[0] * raw_x.shape[1] * raw_x.shape[2], raw_x.shape[3]).T
   # 2) y : (26032, 1) > 26032 
   y = raw_y.reshape(raw_y.shape[0], )
   
   # 셔플
   x, y = shuffle(x, y, random_state=42)
   
   # 학습 훈련 데이터 분리
   x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.05, random_state=42)
   
   # x_test 중 20개만 나중나중의 서비스를 위하여 export 해두기
   for i in range(20):
       test_img = x_train[i,:].reshape(32,32,3)
       plt.imsave('test_img_'+str(i)+'.png', test_img, format="png")
   
   # 랜덤 포레스트 객체 생성 및 학습
   clf = RandomForestClassifier()
   clf.fit(x_train, y_train)
   
   # 정확도 확인
   # test 데이터로 해보면 정확도 0.67
   # extra 데이터로 해보면 정확도 0.86
   y_pred = clf.predict(x_test)
   print('정확도: ', metrics.accuracy_score(y_test, y_pred))
   
   # 모델 저장 : 학습시킨 모델을 pickled binary file 형태로 저장
   joblib.dump(clf, './model_extra_32x32.pkl')
   ````

