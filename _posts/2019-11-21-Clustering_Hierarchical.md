---
title: "Hierarchical Clustering"
excerpt: "scipy.cluster.hierarchy.linkage"
last_modified_at: 2019-11-21T16:20:02-05:00
categories:
  - MachineLearning
tags: [ml, clustering]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---




Hierarchical Clustering은 가장 고전적인+직관적인 군집방법론이다. sklearn에서도 agglomarative clsutering을 제공하지만, dendrogram까지 잘 그려주는 scipy가 더 일반적으로 사용된다.



-  Defalut value

   `scipy.cluster.hierarchy.linkage`(y, *method='single'***,** *metric='euclidean'***,** *optimal_ordering=False***)** 

- Parameters

  - y (ndarray) : 군집을 진행할 데이터

  - method (str) : 균형힌 군집이 만들어진다는 점에서 주로 complete, average, ward를 사용

    - ’single’ :  Nearest neighbor algorithm, 군집 간의 거리를 계산할 때 각 군집에 속한 점 중 가장 가까운 두 점 사이의 거리값을 사용
    - ’complete’ : Farthest Point Algorithm, 군집 간의 거리를 계산할 때 각 군집에 속한 점 중 가장 멀리 있는 두 점 사이의 거리값을 사용
    - ’average’ : 군집 간의 거리를 계산할 때 각 군집에 속한 모든 점 사이의 거리 평균값을 사용
    - ’centroid’ : 군집 간의 거리를 계산할 때 각 군집의 두 무게중심점 사이의 거리를 사용
    - ’median’ : 군집 간의 거리를 계산할 때 각 군집의 두 중앙점 사이의 거리를 사용
    - ’weighted’ : A라는 군집이 ㄱ,ㄴ라는 세부군집으로 만들어졌다면, 다른 군집 B까지의 거리를 ㄱ-B, ㄴ-B의 거리 평균값을 사용
    - 'ward' : 군집내 편차의 제곱합을 고려, 하지만 사용가능한 metrics='eucliean'으로 제한

  - metric (str or fuction) : scipy.spatial.distance.pdist에서 제공하는 모든 metric과 custom distance fuction 입력 가능

    - Distance Based : 'euclidean'(기하거리), 'minkoski', ' cityblock'(맨하탄 거리), 'sqeuclidean'(기하거리제곱) 등

    - Non-Distance Based : 거리차이가 아니라 패턴의 유사성을 찾기 위한 metric
      - 'cosine'
      - 'correlation'
      - ' jaccard'

- Dendrogram의 해석

  - Leaf : 각각의 데이터포인트
  - Branch : 유사한 데이터포인트끼리 합쳐지면서 가지를 형성, 유사한 가지일수록 더 빨리 (Tree 아래쪽에서) 합쳐진다.
  - 즉, 나중에 합쳐질수록 두 가지는 서로 다르다.
  - 단, 가로축에서 Leave의 순서는 의미가 없다.



출처

[1]  https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage 

[2]  https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html#scipy.spatial.distance.pdist 
