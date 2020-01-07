---
title: "CSV 파일 형태 파악"
excerpt: "필요한 부분만 선택적으로 불러들이기 위하여"
last_modified_at: 2020-01-07T16:20:02-05:00
categories:
  - data
tags: [data, read_csv, csv]

toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: #
---



# CSV 파일 형태 파악

바로 read_csv를 하기에 파일이 너무 무거울 때가 있다. 
그런 때는 csv 파일의 형태를 먼저 확인한 후, 필요한 부분만 선택적으로 read_csv 하는게 좋다.


```python
import csv
import pandas as pd
```


```python
path = r'C:\Users\Jaesik\Desktop\2019-02 GSES\논문투고\공공임대주택 이동성\data\\'
file = '1. 가구통행실태조사_전국_목적통행기준정렬.txt'
encoder = "CP949"
```



### [요약]


```python
headsize = 5
lines = []
with open(path+file, encoding=encoder) as f:
    col_list = next(csv.reader(f))
    fileleng = len(f.readlines())
    f.seek(0,2)
    filesize = f.tell()
    f.seek(0)
    for i in range(headsize):
        lines.append(f.readline())
print('number of column : '+ str(len(col_list)))
print('length : ' + str(fileleng) + ' lines')
print('size : ' + str(filesize//1000) + ' KB')
pd.DataFrame([sub.split(",") for sub in lines])
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

<p># output</p>
<p>number of column : 97</p>
<p>length : 1166951 lines</p>
<p>size : 258488 KB</p>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>87</th>
      <th>88</th>
      <th>89</th>
      <th>90</th>
      <th>91</th>
      <th>92</th>
      <th>93</th>
      <th>94</th>
      <th>95</th>
      <th>96</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>IDX</td>
      <td>행정구역번호</td>
      <td>권역</td>
      <td>총가구원</td>
      <td>5세이상가구원</td>
      <td>가구_행정동코드</td>
      <td>주택종류</td>
      <td>월평균소득</td>
      <td>차량보유</td>
      <td>종류1</td>
      <td>...</td>
      <td>수단통행5_환승지_행정동코드</td>
      <td>수단통행6_교통수단</td>
      <td>수단통행6_도착시각(오전 오후)</td>
      <td>수단통행6_도착시각(시)</td>
      <td>수단통행6_도착시각(분)</td>
      <td>수단통행6_환승지여부</td>
      <td>수단통행6_환승지_행정동코드</td>
      <td>목적통행_도착지_유형</td>
      <td>목적통행_도착지_행정동코드</td>
      <td>탑승인원\n</td>
    </tr>
    <tr>
      <th>1</th>
      <td>186279</td>
      <td>3101355-061A-01</td>
      <td>경기</td>
      <td>3</td>
      <td>3</td>
      <td>4111572000</td>
      <td>1</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>2</td>
      <td>4111568000</td>
      <td>\n</td>
    </tr>
    <tr>
      <th>2</th>
      <td>186279</td>
      <td>3101355-061A-01</td>
      <td>경기</td>
      <td>3</td>
      <td>3</td>
      <td>4111572000</td>
      <td>1</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>4</td>
      <td>4111568000</td>
      <td>\n</td>
    </tr>
    <tr>
      <th>3</th>
      <td>186279</td>
      <td>3101355-061A-01</td>
      <td>경기</td>
      <td>3</td>
      <td>3</td>
      <td>4111572000</td>
      <td>1</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1</td>
      <td>4111572000</td>
      <td>\n</td>
    </tr>
    <tr>
      <th>4</th>
      <td>186279</td>
      <td>3101355-061A-01</td>
      <td>경기</td>
      <td>3</td>
      <td>3</td>
      <td>4111572000</td>
      <td>1</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>2</td>
      <td>4111574000</td>
      <td>\n</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 97 columns</p>



### 단계별 확인

[바이너리와 텍스트의 차이](https://m.blog.naver.com/PostView.nhn?blogId=tipsware&logNo=221353023593&proxyReferer=https%3A%2F%2Fwww.google.com%2F)


```python
# 데이터셋 파일의 크기 확인 1 
import os
fsize=os.stat(path+file)
print('size : ' + str(fsize.st_size//1000) +"KB")
```

    # size : 258488KB



```python
# 데이터셋 파일의 크기 확인 2
with open(path+file, encoding=encoder) as f:
    f.seek(0,2)
    filesize = f.tell()
print('size : ' + str(filesize//1000) + ' KB')
```

    #size : 258488 KB



```python
# 데이터셋의 길이 확인 1
with open(path+file, encoding=encoder) as f:
    filelen = len(f.readlines())
print('length : ' + str(filelen) + ' lines')
```

    # length : 1166952 lines



```python
# 데이터셋의 길이 확인 2
with open(path+file, encoding=encoder) as f:
    filelen = sum(1 for line in f)
print('length : ' + str(filelen) + ' lines')
```

    # length : 1166952 lines



```python
# header 개수 확인
with open(path+file, encoding=encoder) as f:
    col_list = next(csv.reader(f))
print('number of column : '+ str(len(col_list)))
```

    # number of column : 97



```python
# 데이터셋의 header 확인 1
with open(path+file, encoding=encoder) as f:
    col_list = next(csv.reader(f))
print('collums :' + str(col_list))
```

    # collums :['IDX', '행정구역번호', '권역', '총가구원', '5세이상가구원', '가구_행정동코드', '주택종류', '월평균소득', '차량보유', '종류1', '연식1', '종류2', '연식2', '종류3', '연식3', '종류4', '연식4', '종류5', '연식5', '종류6', '연식6', '오토바이 50cc미만(대)', '오토바이 50cc이상 100cc미만(대)', '오토바이 100cc이상 260cc미만(대)', '오토바이 260cc이상(대)', '자전거(동력 전기)(대)', '자전거(비동력)(대)', '기 타(종류)', '기 타(대)', '가구주관계', '가구원구분', '출생연도', '성 별', '운전면허증', '정규교육기관', '학교_행정동코드', '직업', '직업기타', '재택근무(집)', '직장_행정동코드', '근무일수', '근무시간', '많은 통행을 하는 일', '통행일자(년)', '통행일자(월)', '통행일자(일)', '통행일자(요일)', '통행유무', '통행안함', '최초출발지_유형', '최초출발지_행정동코드', '목적통행_통행순서', '통행목적', '목적통행_출발시각(오전 오후)', '목적통행_출발시각(시)', '목적통행_출발시각(분)', '목적통행_출발지_유형', '목적통행_출발지_행정동코드', '수단통행1_교통수단', '수단통행1_도착시각(오전 오후)', '수단통행1_도착시각(시)', '수단통행1_도착시각(분)', '수단통행1_환승지여부', '수단통행1_환승지_행정동코드', '수단통행2_교통수단', '수단통행2_도착시각(오전 오후)', '수단통행2_도착시각(시)', '수단통행2_도착시각(분)', '수단통행2_환승지여부', '수단통행2_환승지_행정동코드', '수단통행3_교통수단', '수단통행3_도착시각(오전 오후)', '수단통행3_도착시각(시)', '수단통행3_도착시각(분)', '수단통행3_환승지여부', '수단통행3_환승지_행정동코드', '수단통행4_교통수단', '수단통행4_도착시각(오전 오후)', '수단통행4_도착시각(시)', '수단통행4_도착시각(분)', '수단통행4_환승지여부', '수단통행4_환승지_행정동코드', '수단통행5_교통수단', '수단통행5_도착시각(오전 오후)', '수단통행5_도착시각(시)', '수단통행5_도착시각(분)', '수단통행5_환승지여부', '수단통행5_환승지_행정동코드', '수단통행6_교통수단', '수단통행6_도착시각(오전 오후)', '수단통행6_도착시각(시)', '수단통행6_도착시각(분)', '수단통행6_환승지여부', '수단통행6_환승지_행정동코드', '목적통행_도착지_유형', '목적통행_도착지_행정동코드', '탑승인원']



```python
# 데이터셋의 header 확인 2
with open(path+file, encoding=encoder) as f:
    line = f.readline()
    print('collums :' + line)
```

    # collums :IDX,행정구역번호,권역,총가구원,5세이상가구원,가구_행정동코드,주택종류,월평균소득,차량보유,종류1,연식1,종류2,연식2,종류3,연식3,종류4,연식4,종류5,연식5,종류6,연식6,오토바이 50cc미만(대),오토바이 50cc이상 100cc미만(대),오토바이 100cc이상 260cc미만(대),오토바이 260cc이상(대),자전거(동력 전기)(대),자전거(비동력)(대),기 타(종류),기 타(대),가구주관계,가구원구분,출생연도,성 별,운전면허증,정규교육기관,학교_행정동코드,직업,직업기타,재택근무(집),직장_행정동코드,근무일수,근무시간,많은 통행을 하는 일,통행일자(년),통행일자(월),통행일자(일),통행일자(요일),통행유무,통행안함,최초출발지_유형,최초출발지_행정동코드,목적통행_통행순서,통행목적,목적통행_출발시각(오전 오후),목적통행_출발시각(시),목적통행_출발시각(분),목적통행_출발지_유형,목적통행_출발지_행정동코드,수단통행1_교통수단,수단통행1_도착시각(오전 오후),수단통행1_도착시각(시),수단통행1_도착시각(분),수단통행1_환승지여부,수단통행1_환승지_행정동코드,수단통행2_교통수단,수단통행2_도착시각(오전 오후),수단통행2_도착시각(시),수단통행2_도착시각(분),수단통행2_환승지여부,수단통행2_환승지_행정동코드,수단통행3_교통수단,수단통행3_도착시각(오전 오후),수단통행3_도착시각(시),수단통행3_도착시각(분),수단통행3_환승지여부,수단통행3_환승지_행정동코드,수단통행4_교통수단,수단통행4_도착시각(오전 오후),수단통행4_도착시각(시),수단통행4_도착시각(분),수단통행4_환승지여부,수단통행4_환승지_행정동코드,수단통행5_교통수단,수단통행5_도착시각(오전 오후),수단통행5_도착시각(시),수단통행5_도착시각(분),수단통행5_환승지여부,수단통행5_환승지_행정동코드,수단통행6_교통수단,수단통행6_도착시각(오전 오후),수단통행6_도착시각(시),수단통행6_도착시각(분),수단통행6_환승지여부,수단통행6_환승지_행정동코드,목적통행_도착지_유형,목적통행_도착지_행정동코드,탑승인원


​    


```python
# 상위 몇 줄 샘플로 확인하기
headsize = 5
lines = []
with open(path+file, encoding=encoder) as f:
    for i in range(headsize):
        lines.append(f.readline()) 
pd.DataFrame([sub.split(",") for sub in lines])
```


```python
# 샘플 몇 줄로 내용 확인하기
import random
samplesize = 5
sample = []
with open(path+file, encoding=encoder) as f:
    sample.append(str(f.readline().rstrip()))  #column name을 첫 줄로 append
    f.seek(0, 2)  # 파일 맨 뒤로 이동
    filesize = f.tell()
    random_set = sorted(random.sample(range(filesize), samplesize))
    for i in range(samplesize):
        f.seek(random_set[i])
        # Skip current line (because we might be in the middle of a line) 
        f.readline()
        # Append the next line to the sample set 
        sample.append(str(f.readline().rstrip()))
pd.DataFrame([sub.split(",") for sub in sample])
```

