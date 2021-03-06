---
title: "K-means Clustering"
excerpt: "sklearn.cluster.KMeans"
last_modified_at: 2019-11-20T16:20:02-05:00
categories:
  - ML
tags: [ML, clustering]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



Kmeans Clustering은 군집화 방법 중 가장 흔하게 + 쉽게 + 강력하게 사용되고, python user라면 Scikit-learn의 Kmeans을 쓰기 마련이다. 하지만, deterministic하지 않고 random한 결과라는 문제점이 있다. (deterministic = running it multiple times will produce the same result) 그래서 같은 샘플들이 속한 군집이라도 그 이름이 1번이라고 label 될지, 2번이라고 label 될지 알 수 없다. 그리고 seed가 어디에 생기느냐에 따라서 각 군집 변두리에 있는 샘플은 매번 다른 군집으로 분류된다.



- Defalut value

  `KMeans`(*n_clusters=8*, *init=’k-means++’*, *n_init=10*, *max_iter=300*, *tol=0.0001*, *precompute_distances=’auto’*, *verbose=0*, *random_state=None*, *copy_x=True*, *n_jobs=None*, *algorithm=’auto’*) 

- Parameters (가능한 전체 parameters를 다 썼지만, 이해가 안되는건 여전히 물음표로 남아있다)
  - n_clusters (int) : 군집의 개수, evaluation metrics의 elbow method로 결정할 수 있다.
  - init ( ‘k-means++’, ‘random’ or an ndarray)
    - ‘k-means++’  : 서로 거리가 먼 centroid seed를 선택해서, 완전히 random seed에 비해서 더 나은 결과가 나옴.
    - 'random' : 전체 데이터 중 임의의 k번째마다 sample을 seed로 사용 (systematic sampling 개념을 사용하는 듯)
    - ndarray : ?
  - n_init  (int) : 서로 다른 centroid seed로 돌린다고 했을 때, 총 몇 번을 돌려서 inertia 기준의 최적 값을 output 할 것인지
  - max_iter (int) : 한 번의 run에 centroid의 위치를 재조정하는 iteration을 몇 번까지 돌릴 것인지
  - tol (float) : inertia를 계산할 때의 tolerance
  - precompute_distances ('auto', True, False) : distances를 미리 계산하면 빠르지만 메모리가 더 필요한데 이걸 쓸지 말지
    - auto : sample 개수와 cluster 개수에 따라서 알아서 결정
    - True : 항상 사용
    - False : 절대 안사용
  - verbose (int) : 아마도 detailed logging information을 생성할 것이냐는 옵션으로 보임. 잘못입력한다면 온갖 로그 정보와 함께 끔찍하게 느린 프로세싱을 겪게 될 수도.
  - random_state (int) : centroid seed를 결정할 때 사용. centroid seed를 random하지 않고 deterministic하게 결정하고 싶다면 임의의 int 값을 입력. 흔히 사용하는 값은 0 or 42. 하지만 무슨 값을 넣어도 결과가 안정적으로 나오는지를 확인할 필요가 있다.
  - copy_x (boolean) : ?
  - n_jobs (int or None) : 병렬 처리를 위해서 동시수행 프로세스가 사용될지
  - algorithm ("auto", "full", "elkan") 
    - "full" : 모집단을 추정 후 해당 모집단에서 샘플이 추출되었을 확률을 기반으로 하는 EM-style algorithm
    - "elkan" : triangle inequalit(?)를 사용해서 더 효율적이지만, sparse data에는 적당하지 않음
    - "auto" : dense data에는 "elkan", sparse data에는 "full"로 자동 선정



출처

[1] https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html 

[2] https://scikit-learn.org/stable/modules/clustering.html#k-means 

[3]  https://scikit-learn.org/stable/glossary.html#term-random-state 
