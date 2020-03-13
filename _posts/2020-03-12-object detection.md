---
title: "object detection, ojbect detection models"
excerpt: "object detection은 무엇이고, 어떤 방법들이 있는가"
last_modified_at: 2020-03-12T16:20:02-05:00
categories:
  - Vision
tags: [object detection, DL, CNN, RCNN, SDD, YOLO]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---

## Object Detection이 왜 어렵냐면?
Object Classification은 CNN으로 잘 해결할 수 있게 되었다.  
그렇다면 이제 Object Detection의 문제로 넘어가본다.  
Object Detection의 문제는 "주어진 이미지에서 **뭐**가 **어디**에 있는지 알아야 한다."  
따라서 사물의 위치를 찾아서 네모(bounding box)를 쳐주는 것(=Localization=Region Proposal)이 다음 과제다.  
요약하자면,  
**Object Detection = Region Proposal + Classification**



## Object Detection Data Label
전체 100x100 이미지 속에 **고양이**가 **50, 50** 위치에 **20, 30** 크기로 있다.  
즉, 총 5가지  
- bounding box의 x, y좌표 (중심 혹은 정해진 위치)  
- bounding box의 width, height  
- bounding box 내 object의 class  
![label](https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo3.jpg)



## 1-stage vs 2-stage detector
Ojbect Detection의 두 가지 접근법이 있다.  
- 2-stage detector : 먼저 Region Proposal을 마친 후, Classification을 순차적으로 진행, 느지만 높은 정확도
- 1-stage detector : Region Proposal과 Classification이 동시에 진행, 빠르지만 낮은 정확도  
![milestone of object detection](/assets/images/2020-03-13-R-CNN.jpg)  
[이미지 출처 : Zou, Z., Shi, Z., Guo, Y., & Ye, J. (2019). Object detection in 20 years: A survey. *arXiv preprint arXiv:1905.05055*.]
