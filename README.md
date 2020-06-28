__주제__: 생체정보 지정맥을 고화질로 복원


main= 지정맥 data, U-net코드

지정맥 data: x_train와 x_test data로 분리하여 저장한다. y_train은 각 지정맥데이터의 정답을 만들기위해 모든 지정맥의 특징점을 수동으로 그린 data를 저장한다.
data의 양을 늘리기위해 정답 정맥을 data agumentation하여 갯수를 증가(y_train증가)시키고, 해당 지정맥원본 또한 같은 양으로 증가(x_train)시킨다.

1. train data의 정답으로 잘 학습시키기위해 특징점을 추출하여 그린 data에 전처리 후, 학습을 진행한다. 
특징점을 수동으로 그린 데이터에 adaptive threshold함수를 사용하여 특징점을 더 뚜렷하게 만들어주는 전처리 방법을 한 후, 정답(y_train)으로 학습한다. 즉 원본 지정맥(x_train)과 전처리를 통한 뚜렷한 지정맥(y_train)이 쌍을 이루어 학습을 한다.


2. U_net 알고리즘으로 학습하여 x_test 데이터를 예측한다.
- U_net이란? 방법은? 

- 결과: 

- 정확도 계산: mean_iou방법, 즉 교집합/합집합으로 계산. 결과 data와 예측 data에서의 전체 정맥중에 정말 정맥인 부분이 얼마나 존재하는지 계산한다. 

----------------
data augumentation=지정맥 data가 적기때문에 brightness, contrast, mixture기법을 통해 data양을 증가

----------------

keras_u-net= keras코드 분석 및 실습

참고: https://www.kaggle.com/keegil/keras-u-net-starter-lb-0-277

-----------------

mean_iou 함수화: pred사진과 후처리한(정맥추출)사진의 정확도를 계산하기위한 코드


