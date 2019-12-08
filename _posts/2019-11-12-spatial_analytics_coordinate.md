---
title: "좌표 시스템"
excerpt: "공간 데이터 분석을 위한 좌표 시스템 및 파일 형식"
last_modified_at: 2019-11-12T16:20:02-05:00
categories:
  - notes
tags: [spatial, urban, data]

# table of contents
toc : # true
toc_label : # "toc_label"
toc_icon : # "name_of_icon" from https://fontawesome.com/icons?d=gallery&s=solid&m=free
comments: # 
---


### 공간  데이터 

- 지구 표면에 위치하는 객체, 사건, 현상을 기록한 데이터

- 위치정보(지구좌표) + 속성정보 (객체의 이벤트 또는 현상)

- 유형
  - 벡터 : 실세계를 기하학적인 형태로 표현 (점, 선, 폴리곤)
  - 래스터 : 격자형의 픽셀로 표현 (셀),  고도와 같이 연속적인 값을 표현할 때 주로 사용



### 좌표계

- 공간데이터가 위치를 표시하는 측위의 기준

- 지리좌표계 or 투영좌표계

- 지리좌표계 (Geographic Coordinate System, GCS)

  - 경도(longitude)  + 위도(latitude)를 사용한 3차원의 개념
  - 절대좌표계 : 기준점에 상관없이 달라지지 않음
  - 우리나라 : WGS84 or GRS80 사용

- 투영좌표계 (Projected Coordinate System, PCS)

  - 지구가 타원+찌그러짐으로 인하여 각 지역의 좌표는 잘 표현하지 못하므로 투영좌표계 필요

    ![why PCS](https://news.imaeil.com/inc/photos/2018/07/06/2018070617051205165_l.jpg)

  - 평면 직각 좌표계(Plane Coordinate System) : UTM or TM 등

    - UTM (Universal Transverse Mercator Grid System) : 미국 육군성이 군사용 목적으로 개발한 횡 메르카토르 도법
    - 국내 TM(Transverse Mercator Grid System) : 서부원점, 중부원점, 동부원점, 동해원점

    

### 좌표계 변환

- 우리나라 좌표계

| 좌표계                | 설명                       | 관련 서비스                                          |
| --------------------- | -------------------------- | ---------------------------------------------------- |
| Google  Mercator      | EPSG:3857, EPSG:900913     | Google Maps, Bing Maps, Yahoo Maps, Open Street Maps |
| GRS80 경위도          | EPSG:4019                  |                                                      |
| WGS84 경위도          | EPSG:4326                  | Google Earth                                         |
| UTM-K (Bessel)        | EPSG:5178                  | 새주소지도                                           |
| UTM-K(GRS80)          | EPSG:5179                  | 네이버지도                                           |
| 서부원점(GRS80)       | EPSG:5180(50만), EPSG:5185 |                                                      |
| 중부원점(GRS80)       | EPSG:5181(50만), EPSG:5186 | 국토지리정보원                                       |
| 제주원점(GRS80, 55만) | EPSG:5182                  | 다음카카오 지도 API                                  |
| 동부원점(GRS80)       | EPSG:5183(50만), EPSG:5187 |                                                      |
| 동해(울릉)원점(GRS80) | EPSG:5184(50만), EPSG:5188 |                                                      |



### 공간데이터 파일 유형

| 구분           | 확장자                                           | 특성                                                         |
| -------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| Esri Shapefile | SHP(도형 정보), DBF(속성 정보), SHX(도형 인덱스) | 업계 표준, 반드시 3개가 조합 (SHP, DBF, SHX)                 |
| GeoJSON        | GEOJSON, JSON                                    | 웹 기반에 주로 사용, JSON(JavaScript Object Notation) 형태   |
| TopoJSON       | JSON                                             | 위상을 이용한 GeoJSON의 확장 형식, 중복 제거를 토한 파일 크기 최소화, Power BI의 도형맵에서 사용 |
| GML            | GML                                              | XML 형태로 공간 정보 저장, 텍스트 형식                       |
| KML/KMZ        | KML, KMZ                                         | 구글에서 기본적으로 사용하는 XML 형태, WGS84 형태로 공간정보 정의 |

