# 나 혼자 잘 산다

![image](https://user-images.githubusercontent.com/29085414/148169748-fd2ce905-8296-41d2-809f-3fd7c4ceb6bb.png)


## 목차
* [개요](#개요)
* [주제 선정 배경](#주제-선정-배경)
* [빅데이터 분석](#빅데이터-분석)
  + [이상치 제거](#이상치-제거)
  + [상관관계 함수](#상관관계-함수)
  + [경감 지표 선정](#경감-지표-선정)
    - [CCTV](#cctv)
    - [치안센터](#치안센터)
  + [회귀 분석 및 안전지수 도출](#회귀-분석-및-안전지수-도출)
      * [위해지표](#위해지표)
      * [취약지표](#취약지표)
  + [예측안전지수 부여](#예측안전지수-부여)
* [시각화 구현](#시각화-구현)
  - [맵 시각화](#맵-시각화)
  - [차트](#차트)
* [조원](#조원)

## 개요

 범죄율과 상관관계가 높았던 변수 (CCTV, 가로등, 여성안전지킴이집, 안전비상벨)과 시간별, 장소별을 빅데이터 분석 후 시각화


## 주제 선정 배경

![image-20220103105448924](https://user-images.githubusercontent.com/51068026/147896021-89848c95-3548-4503-969c-cdb80ce50b77.png)

- 1인 가구는 다인 가구에 비해 주거침입, 절도, 폭행, 사기, 강도, 손괴 등이 많음

- 실질적으로 다인 가구와 비교해 성폭력과 괴롭힘 이외의 모든 범죄 비율이 높음

- 범죄율과 상관관계가 높았던 변수 추출하여 시각화한다.

  (범죄율,단란주점,유흥주점,1인가구(여성,남성,노인),CCTV,치안시설비)

- 관련 논문
  
  [1인 가구와 범죄발생에 관한 연구: 서울시 25개 자치구 패널자료를 중심으로]:"https://www.si.re.kr/node/60865"
  
  

## 빅데이터 분석


### 이상치 제거
![image-20220103110025355](https://user-images.githubusercontent.com/51068026/147896035-399c40f7-31e0-45a6-a648-ddb64f9d83b4.png)

- 결측치를 제거 후 이상치를 정리하고 상관분석을 실행한다.


### 상관관계 함수
Corr 이용 -> heatmap 시각화

![image-20220103110053379](https://user-images.githubusercontent.com/51068026/147896052-92dd253a-c317-4392-94bc-3bdfd83870ca.png)

- 1인 가구 비율에 따라 “살인” > ”절도” > “폭력” > “강간 및 강제추행” 범죄의 순으로 상관관계가 높다. 

-  1인 가구(남성)비율에 따라 “살인”범죄가 “0.49”로 높았고, “폭력”,”절도”도 높은 상관관계를 보임.

-  1인 가구(여성)비율에 따라 “폭력”,”절도” 범죄가 높은 상관관계를 보임.

- 1인 가구(여성) 비율과 “강간 및 강제추행”의 비율이 다른 1인 가구에 비해 평균적으로 약 0.17높게 나옴. 총 범죄의 비율은 1인 가구(노인)과 “0.11” 이라는 수치로 상관이 없다고 보인다.



### 경감 지표 선정

#### CCTV

![image-20220103111010449](https://user-images.githubusercontent.com/51068026/147896061-02644d54-a1a9-416f-a174-7fe7651c938d.png)

범죄율에 따라 “CCTV” 범죄의 음의 상관관계가 높다. (-0.42) 각 범죄의 항목 중 “살인”과 “폭력”에 음의 상관관계가 높았다.

#### 치안센터

![image-20220103111055520](https://user-images.githubusercontent.com/51068026/147896062-a4470be0-3eef-4dda-bb8f-d5c0c37ee46a.png)

범죄율에 따라 “치안센터” 범죄의 음의 상관관계가 높다**.** **(-0.34)**각 범죄의 항목 중 “강간및강제추행”과 “절도”에 음의 상관관계가 높았다.



### 회귀 분석 및 안전지수 도출

2017 ~ 2020년 자료로 분석

#### 회귀식, 안전지수 도출 

행정안전부 안전 지수 도출 공식을 활용한다.

![image-20220103111302548](https://user-images.githubusercontent.com/51068026/147896066-92895347-43f0-4632-a201-0cb81324fede.png)

>  위해지표(사망, 건수) + 취약지표 (위해지표 발생원인) - 경감지표 (위해지표 경감요인)

##### 위해지표 
5대 범죄율 (0.5)

##### 취약지표 

- 1인가구(여성) (0.044)

- 치안센터 (0.25)

- 단란주점 (0.156)

- CCTV (0.05)

### 예측안전지수 부여

| 1등급 | 2등급 | 3등급 | 4등급 | 5등급 |
| ----- | ----- | ----- | ----- | ----- |
| 10%   | 25%   | 30%   | 25%   | 10%   |



## 시각화 구현

### 메인

![image-20220103115645033](https://user-images.githubusercontent.com/51068026/147896908-4faeea31-28a5-4595-be99-653d69c27579.png)

태블로로 시각화한 데이터를 보여준다.

- 범죄율, CCTV, 치안시설, 보안등, 유흥업소

- 해당 구에 안전시설이 많은 TOP 3와 WORST 3를 표시한다

### 데이터 대시보드

![image-20220103111941433](https://user-images.githubusercontent.com/51068026/147896073-413f31d6-ca0d-4476-9109-4e259e5b42b7.png)

안전시설 CCTV, 보안등, 여성 안전지킴이 집, 비상 안전 벨의 데이터를 보여준다.

- 지도에 해당 안전시설 마커로 보여줌

- 해당 구에 안전시설이 많은 TOP5

- CCTV 현황 자세히 보기

### 맵 시각화

- ANACONDA : Python 데이터 라이브러리

- Folium : Leaflet.js 기반으로 만들어진 Python 지도 시각화 라이브러리   

- tableau : 데이터 시각화 소프트웨어

### 차트 

 - chart.js : HTML5 Canvas 방식의 **강력한 오픈소스** **라이브러리**

- Simple-DataTables : JS 기반의 데이터 테이블 라이브러리

  

## 조원

이지윤, 정혜빈, 류수민, 정상협 



감사합니다.
