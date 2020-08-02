## 주제  
U-net알고리즘을 이용한 생체정보 지정맥을 고화질로 복원  
------------------------------------

## 사용 알고리즘  

__U-net__:




--------------------------------------------------------------------

## 데이터 처리 
원본 데이터 지정맥데이터 __x_train__ 저장  
모든 지정맥의 특징점 수동 추출 정맥데이터 __y_train__ 저장  
<br>

정맥데이터양의 증가를 위해 __data argumentation__ 진행(10배)
=> x_train, y_train (원본, 특징점 추출 지정맥) 1:1로 대칭  

---------------------------------------------------------------------


## 개발 단계
__1단계__: 데이터 특징점 강화  
y_train의 지정맥데이터에 adaptive threshold를 이용하여 특징점 강조  
원본 지정맥(x_train)과 특징점 강조 지정맥(y_train) 1:1쌍을 이루어 학습    

-__(a)__ 원본지정맥  
<img src="https://user-images.githubusercontent.com/57060127/86255296-e8795680-bbf1-11ea-95c9-d8af8b8534f1.jpg" width="30%">

-__(b)__ (a)를 수동 추출 지정맥  
<img src="https://user-images.githubusercontent.com/57060127/86255546-32fad300-bbf2-11ea-8f59-d7019f45d9df.jpeg" width="30%">

-__(c)__ (b)를 adaptive threshold를 이용한 특징점 강조 지정맥  
<img src="https://user-images.githubusercontent.com/57060127/86256395-40648d00-bbf3-11ea-8be9-a1d5763bf7a1.JPG" width="30%">
<br>

__2단계__: x_train, x_test,y_train 정맥데이터 분리  
<br>

__3단계__: 딥러닝  
__U_net 알고리즘__ 으로 epoch=45, batch_size=30으로 학습하여 x_test 데이터를 예측  
pred에서 threshold ~이상 화솟값만 출력  
<br>
<br>

__4단계__: mean_iou(교집합/합집합) 정확도계산  
정답 데이터(d)와 pred 데이터(e)에서 __d,e화소값 교집합/d,e화소값 합집합__ 로 정확도계산  
d,e 사진추가  
<br>

---------------------------------------------------------------------------------


## 결과
 
(a) __원본__ |  (b) __예측__ | (c) __(b)에서 임계값이상 특징점 이진화__ |  (d) __세선화__
:------------------------------------:|:-------------------------:|:--------------------------:|:----------------------------:
![](https://user-images.githubusercontent.com/57060127/86254185-6fc5ca80-bbf0-11ea-95c0-b5e69eb57521.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254553-efec3000-bbf0-11ea-9bd4-e90a98270d6f.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254701-2629af80-bbf1-11ea-8fb1-bbc4c9ad926d.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254716-2e81ea80-bbf1-11ea-82ee-72c7d823c870.jpg)
<br>
<br>

----------------

html5up-hyperspace= 웹 구현  
<br>

data augumentation= brightness, contrast, mixture기법을 통해 data양을 증가  
<br>

keras_u-net= keras코드 분석 및 실습  
참고: https://www.kaggle.com/keegil/keras-u-net-starter-lb-0-277  
<br>

mean_iou 함수화: pred사진과 후처리한(정맥추출)사진의 정확도를 계산하기위해 하드코딩

