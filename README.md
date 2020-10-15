## 주제  
__U-net알고리즘을 이용한 디노이징된 지정맥 고화질로 복원__  
- __개발환경: python3, tensorflow 1.14.0, keras=2.3.1__    
<br>


------------------------------------

## 사용 알고리즘  

__U-Net__: Convolutional Networks for Biomedical Image Segmentation  
<img src="https://user-images.githubusercontent.com/57060127/89655110-90c2bf00-d904-11ea-9250-1dae9deea8cb.JPG" width="50%">  
* 특징  
  - 의약쪽에서 탁원한 효과를 보이는 Segmentation network  
  - classification + Localization  
  - 활성화함수 relu사용  
  <br>
  
__Mean IoU (평가지표)__  
<img src="https://user-images.githubusercontent.com/57060127/95881039-1a828300-0db3-11eb-8326-f0cb43c91b81.JPG" width="50%">  
<br>


---------------------------------------------------------------------


## 개발 단계
### 1단계 : 데이터 특징점 강화  
<p>
  
> raw 지정맥데이터에 adaptive threshold를 이용하여 특징점 강조   
   
   
(a) __원본지정맥__ |  (b) __(a)를 수동추출__ |
:------------------------------------:|:-------------------------:|
![](https://user-images.githubusercontent.com/57060127/86255296-e8795680-bbf1-11ea-95c9-d8af8b8534f1.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86255546-32fad300-bbf2-11ea-8f59-d7019f45d9df.jpeg)  |
<br>
<br>

### 2단계 : 이미지 증가(image agumentation)  
<p>
  
> Localization을 변화시키지 않는 __brightness, contrast__ 조절을 통해 이미지 증가  
<br>
<br>



### 3단계 : 딥러닝  
<p>
  
__U_net 알고리즘__  
> x_train 1880개, x_test 600개, y_train 1880개  
> batch_size=30, epochs=45  
> pred에서 예측확률이 0.3이상 부분만 출력    
   
(a) __x_train__ |  (b) __y_train__ | (c) __임계값(0.3)이상 예측__ |
:------------------------------------:|:-------------------------:|:--------------------------:|
![](https://user-images.githubusercontent.com/57060127/89191583-192c2180-d5de-11ea-8597-22f691eed448.JPG)  |  ![](https://user-images.githubusercontent.com/57060127/89191580-18938b00-d5de-11ea-905a-afdc52f102bb.JPG)  |  ![](https://user-images.githubusercontent.com/57060127/89191572-16313100-d5de-11ea-8b43-ba7522f5e475.JPG)  
<br>
<br>

### 4단계 : Mean IoU  
<br>


### 5단계 : 세선화  
<p>
  
> 정맥부분만 정확하게 강조함  

<br>

---------------------------------------------------------------------------------


## 결과  
  
> 디노이징된 정맥 원본사진에 정맥특징점 강화    
 
(a) __원본__ |  (b) __예측__ | (c) __(b)에서 임계값이상 특징점 이진화__ |  (d) __세선화__
:------------------------------------:|:-------------------------:|:--------------------------:|:----------------------------:
![](https://user-images.githubusercontent.com/57060127/86254185-6fc5ca80-bbf0-11ea-95c0-b5e69eb57521.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254553-efec3000-bbf0-11ea-9bd4-e90a98270d6f.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254701-2629af80-bbf1-11ea-8fb1-bbc4c9ad926d.jpg)  |  ![](https://user-images.githubusercontent.com/57060127/86254716-2e81ea80-bbf1-11ea-82ee-72c7d823c870.jpg)
<br>
<br>



- [main](https://github.com/Jimin980921/Vein_deblurring/blob/master/main/denselayer_based_Unet.ipynb)= 전체코드  
- [html5up-hyperspace](https://github.com/Jimin980921/Vein_deblurring/tree/master/html5up-hyperspace)= 웹 구현  
- [data augumentation](https://github.com/Jimin980921/Vein_deblurring/blob/master/data%20augmentation.ipynb)= brightness, contrast, mixture기법을 통해 data양을 증가  
- 참고: https://www.kaggle.com/keegil/keras-u-net-starter-lb-0-277  
- [mean_iou 함수화](https://github.com/Jimin980921/Vein_deblurring/blob/master/mean_iou%20%ED%95%A8%EC%88%98%ED%99%94.ipynb): pred사진과 후처리한(정맥추출)사진의 정확도를 계산  
<br>

- [ ] 논문작성예정

