---
title: "Clustering"
excerpt: "clustering의 이해와, Hierarchical vs Partitional의 차이 비교"
last_modified_at: 2019-11-19T16:20:02-05:00
categories:
  - ML
tags: [ML, clustering]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---



### Clustering

- 정답(label)이 없이 비슷한 특성을 가진 데이터끼리 묶어 나가는 비지도학습(unsupervised learning)

- 비슷함의 기준

  - 군집 내 분산 최소화 (inner-cluster variance, cohesion) : 동일 군집 내 개체들이 유사하다
  -  군집 간 분산 최대화 (inter-cluster variance, separation ) : 다른 군집 내 개체와 유사하지 않다.

  

- Clustering 방법의 구분

  - 군집화 방법에 따라
    - Hierarchical Clustering : 매단계마다 모든 점의 거리를 계산하여 군집을 생성하는 bottom-up approach (ex. scipy)
    - Partitional Clustering : 입력된 군집 개수에 따라서 임의의 중심점을 선택하고, 그를 기반으로 개선된 군집을 찾아나가는 top-down approach (ex. K-means)
  -  중복 허용에 따라
    - Hard Clustering : 한 개체가 특정 군집에만 배타적으로 속한다고 결정 
    - Soft Clustering : 한 개체가 각 군집에 속할 가능성을 확률을 반환 (ex. Fuzzy C-means clustering, GMM)
  - 분포를 정의한 확률 모형에 기반하느냐에 따라
    - probabilistic clustering(=Model based Clustering) : 모집단의 분포를 추정하고, 개체별로 각  군집에 속할 가능성을 확률로 계산하여 가장 확률이 높은 군집에 배정 (ex. GMM)
    - non-probabilistic clustering 

  

- Hierarchical vs Partitional 선택 시 고려사항

  - 데이터의 규모 : Hierarchical은 계산량이 많다.
  - 군집 개수의 사전정의 : Hierarchical은 군집의 개수를 미리 지정할 필요가 없다. 
  - 유사도의 기준 : Hierarchical은 변화 패턴이 비슷하다는 것을 측정하기 위한 correlation- based metric(Non Euclidean Distances)을 쓸 수 있다. 
  - Deterministic result : Hierarchical은 deterministic하게 항상 동일한 결과를 얻을 수 있다. (Partitional도 deterministic 하게 할 수 있지만, initiation이 필요)
  - 사용할 Package : Hierarchical은 `sklearn`보다는 `linkage`명령으로 덴드로 그램까지 그릴수 있는  `scipy.cluster.hierarchy`가 주로 쓰이는 듯 하다. ( `sklearn.cluster.AgglomerativeClustering` 으로도 가능은 함)
  - 데이터의 특성 : Hierarchical은 서로 다른 기준의 군집이 섞여 있는 데이터에는 부적절할 수 있다. 예를 들어, 여성+남성, 흑인+황인+백인이 모두 포함된 데이터라면 Partional은 군집의 개수가 2개인 경우 성별 기준, 개수가 3개인 경우 인종 기준으로 군집이 생성되겠지만, Hierarchical은 그렇지 않다.
  - 하지만 동일 데이터+유사 조건으로 K-means와 Hierarchical을 모두 적용해본 결과, 대세에는 큰 영향이 없더라.

  

- Partitional Clustering 중 세부 선택 시 고려사항

  - 이건 Sckit-learn의 Clustering Methods overview를 보면 된다. 데이터 분포의 특성, 사용할 dis-similarity metric (geometry) 등에 따라서 선택하면 된다. 헷, 잘 모르겠으면 K-means가 제일 대표적! 

  - ![Overview of clustering methods](https://scikit-learn.org/stable/_images/sphx_glr_plot_cluster_comparison_0011.png)

  - | Method name                                         | Parameters                                                   | Scalability                                                  | Usecase                                                      | Geometry (metric used)                       |
    | --------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------------- |
    | K-Means                                             | number of clusters                                           | Very large n_samples,  medium n_clusters with MiniBatch code | General-purpose, even cluster size, flat geometry, not too many  clusters | Distances between points                     |
    | Affinity propagation                                | damping, sample preference                                   | Not scalable with n_samples                                  | Many clusters, uneven cluster size, non-flat geometry        | Graph distance (e.g. nearest-neighbor graph) |
    | Mean-shift                                          | bandwidth                                                    | Not scalable with n_samples                                  | Many clusters, uneven cluster size, non-flat geometry        | Distances between points                     |
    | Spectral clustering                                 | number of clusters                                           | Medium n_samples, small n_clusters                           | Few clusters, even cluster size, non-flat geometry           | Graph distance (e.g. nearest-neighbor graph) |
    | Ward hierarchical clustering                        | number of clusters or distance threshold                     | Large n_samples and n_clusters                               | Many clusters, possibly connectivity constraints             | Distances between points                     |
    | Agglomerative clustering (=Hierarchical clustering) | number of clusters or distance threshold, linkage type, distance | Large n_samples and n_clusters                               | Many clusters, possibly connectivity constraints, non Euclidean  distances | Any pairwise distance                        |
    | DBSCAN                                              | neighborhood size                                            | Very large n_samples, medium n_clusters                      | Non-flat geometry, uneven cluster sizes                      | Distances between nearest points             |
    | OPTICS                                              | minimum cluster membership                                   | Very large n_samples, large n_clusters                       | Non-flat geometry, uneven cluster sizes, variable cluster density | Distances between points                     |
    | Gaussian mixtures                                   | many                                                         | Not scalable                                                 | Flat geometry, good for density estimation                   | Mahalanobis distances to centers             |
    | Birch                                               | branching factor, threshold, optional global clusterer.      | Large n_clusters and n_samples                               | Large dataset, outlier removal, data reduction.              | Euclidean distance between points            |

