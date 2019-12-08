---
title: "Unsupervised Clustering Evaluation"
excerpt: "label이 없는 데이터 군집의 내부평가"
last_modified_at: 2019-11-22T16:20:02-05:00
categories:
  - MachineLearning
tags: [ml, clustering]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



label이 없는 데이터의 경우에는 정답과 비교하여 정확도를 평가하는 방식을 쓸 수 없다. 다만 군집이 얼마나 잘 형성되었는지 모델 퀄리티만을 평가할 수 있다. 따라서 (1) 군집 간 거리 (2) 군집의 지름 (3) 군집의 분산 등을 고려하여 군집타당성 지표(Clustering Validity Index)를 계산한다. 이러한 방법을 내부평가(internal evaluation)이라고 한다. 

 

+ 군집이 "잘" 형성되었다의 기준
  - 군집 내 분산 최소화 (inner-cluster variance, cohesion) : 동일 군집 내 개체들이 유사하다
  -  군집 간 분산 최대화 (inter-cluster variance, separation ) : 다른 군집 내 개체와 유사하지 않다.



+ Clustering Model Evaluation Indices
  - Silhouette Coefficient ([`sklearn.metrics.silhouette_score`](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html#sklearn.metrics.silhouette_score)) 
  - Calinski-Harabasz index ([`sklearn.metrics.calinski_harabasz_score`](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.calinski_harabasz_score.html#sklearn.metrics.calinski_harabasz_score)) 
  - Davies-Bouldin index ([`sklearn.metrics.davies_bouldin_score`](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html#sklearn.metrics.davies_bouldin_score)) 
  - Dunn Index



+ 지표 1  : Silhouette Coefficient

  - 군집 내 동질성 : a, 동일 군집 내 점들간의 평균 거리

  - 군집 간 배타성 : b, 가장 가까운 이웃 군집 내 점들과의 평균거리

  - 식 : $$ s = \frac{b - a}{max(a, b)} $$

  - 값 : -1~1, 일반적으로 0.5보다 크면 okay라고 판단

    - -1 : worst value
    - 0 : overlapping clusters
    - 1 : best value

  - Parameters

    -  X (array) : 군집 대상
    - labels (array) : 군집 결과
    - metric (str) : dissimilarity 측정법
      - From scikit-learn: [‘cityblock’, ‘cosine’, ‘euclidean’, ‘l1’, ‘l2’, ‘manhattan’]. These metrics support sparse matrix inputs.
      - From scipy.spatial.distance: [‘braycurtis’, ‘canberra’, ‘chebyshev’, ‘correlation’, ‘dice’, ‘hamming’, ‘jaccard’, ‘kulsinski’, ‘mahalanobis’, ‘matching’, ‘minkowski’, ‘rogerstanimoto’, ‘russellrao’, ‘seuclidean’, ‘sokalmichener’, ‘sokalsneath’, ‘sqeuclidean’, ‘yule’] See the documentation for scipy.spatial.distance for details on these metrics. These metrics do not support sparse matrix inputs.
    - sample_size (int or None) : random subset을 사용한다면 입력
    - random_state (int or None) : random subset을 사용할 때 np.random의 seed로 사용

  - 특이사항 : convex cluster의 경우 높게 나타나므로, DBSCAN 같은 density based clustering을 해야 한다.

  - 예시

    ```python
    from sklearn import metrics
    from sklearn.metrics import pairwise_distances
    from sklearn import datasets
    dataset = datasets.load_iris()
    X = dataset.data
    labels =AgglomerativeClustering(n_clusters=3, linkage="complete", affinity="correlation").fit(x).labels_ 
    metrics.silhouette_score(X, labels,metric="euclidean") 
    # 0.4037607990862609
    # 반환값은 평균 silhouettet score, 각 군집별 스코어를 보고 싶다면 https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html#sphx-glr-auto-examples-cluster-plot-kmeans-silhouette-analysis-py 참고
    # 군집 생성은 correlation을 기준으로 하되, 실루엣 스코어는 euclidean distance를 기반으로 해서 다른 두 score와 같은 방식으로 distace를 계산하도록 함.
    ```

    

    

- 지표 2 : Davies-Bouldin Score

  - 군집 내 동질성 : $$sigma$$, 동일 군집 내 점들과 중심점과의 평균거리

  - 군집 간 배타성 : d, 각 군집의 중심점 사이의 거리

  - 식 : $$ s(k) = \frac{\mathrm{Tr}(B_k)}{\mathrm{Tr}(W_k)} \times \frac{N - k}{k - 1} $$, $$ R_{ij} = \frac{s_i + s_j}{d_{ij}} $$

  - 값 : 0에 가깝게 작아질수록 잘 만들어진 군집

  - Parameters

    -  X (array) : 군집 대상
    - labels (array) : 군집 결과

  - 특이사항 

    -  convex cluster의 경우 높게 나타나므로, DBSCAN 같은 density based clustering을 해야 한다.
    - metric을 Euclidean distance밖에 쓸 수 없다.

  - 예시

    ```python
    from sklearn import metrics
    from sklearn.metrics import pairwise_distances
    from sklearn import datasets
    dataset = datasets.load_iris()
    X = dataset.data
    labels =AgglomerativeClustering(n_clusters=3, linkage="complete", affinity="correlation").fit(x).labels_
    metrics.davies_bouldin_score(X, labels)  
    # 0.9081392925214556
    ```





- 지표 3 : Calinski-Harabasz Score

  - 군집 내 동질성 : $$ W_K $$, 동일 군집 내 분산 행렬

  - 군집 간 배타성 : $$ B_K $$, 다른 군집 간 분산 행렬

  - 식 : $$ s(k) = \frac{\mathrm{Tr}(B_k)}{\mathrm{Tr}(W_k)} \times \frac{N - k}{k - 1} $$

  - 값 : 클수록 잘 만들어진 군집

  - Parameters

    -  X (array) : 군집 대상
    - labels (array) : 군집 결과

  - 특이사항 

    -  convex cluster의 경우 높게 나타나므로, DBSCAN 같은 density based clustering을 해야 한다.
    - metric을 Euclidean distance밖에 쓸 수 없다.

  - 예시

    ```python
    from sklearn import metrics
    from sklearn.metrics import pairwise_distances
    from sklearn import datasets
    dataset = datasets.load_iris()
    X = dataset.data
    labels =AgglomerativeClustering(n_clusters=3, linkage="complete", affinity="correlation").fit(x).labels_
    metrics.calinski_harabaz_score(X, labels)  
    # 358.2588384870082
    ```

    



- 그 외의 지표

  - inertia (= within-cluster sum-of-squares) : 동일 군집 내 오차제곱합, K-means Clustering을 한다면 기본함수로 호출 가능

    $$ \sum_{i=0}^{n}\min_{\mu_j \in C}(||x_i - \mu_j||^2) $$

  - Dunn index 

    - 군집 내 동질성 : d, 각 군집의 중심점 사이의 거리
    - 군집 간 배타성 : d', 동일 군집 내 점들간의 거리

    - 식 : ![Dunn](https://wikimedia.org/api/rest_v1/media/math/render/svg/420730949ae2ca35dc53316964f9c054030026ae)
    - 값 : 클수록 잘 만들어진 군집
    - Dunn Index manual 계산 코드는  https://www.geeksforgeeks.org/dunn-index-and-db-index-cluster-validity-indices-set-1/  참고





참고자료 :

[1] https://scikit-learn.org/stable/modules/clustering.html#silhouette-coefficient 

[2] https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_samples.html#sklearn.metrics.silhouette_samples 

[3] https://scikit-learn.org/0.15/modules/generated/sklearn.metrics.pairwise.pairwise_distances.html 

[4]  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html 

[5]  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.calinski_harabasz_score.html 
