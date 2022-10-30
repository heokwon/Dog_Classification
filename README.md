# Dog_Classification
#### Alpaco Image Classification mini Project
### Team
* 김현나, 손보영, 이종헌, 전영욱, 허 권
<br><br>
## Project
* Dog Image Classification
<br><br>
## Introduction
14종의 강아지 품종 이미지를 분류하는 모델 만들기<br>
|Species|Label|Species|Label|
|:-------:|:-----:|:-------:|:-----:|
|코카스파니엘|1|삽살개|8|
|푸들|2|시베리안 허스키|9|
|그레이하운드|3|말라뮤트|10|
|말티즈|4|닥스훈트|11|
|퍼그|5|웰시코기|12|
|비숑|6|리트리버|13|
|진돗개|7|포메라니안|14|<br>
<br>

## Data and Model
* Data
  + Selenium을 통해 Naver와 Google에서 크롤링
  + 총 14개의 label
  + 11,289장 
* Model
  + ResNet50
  + Transfer learning
    - conv layer 일부 재학습(12층, 15층, 30층) + 분류기 학습
    - Dropout
  + Fine-tuning
<br><br>
## Envs and Requirements
* Google Colab, VScode
* Tensorflow, Selenium, Pickle, OpenCV, Matplotlib, Numpy, Sklearn
<br><br>
## Progress
* Selenium을 통해 Naver와 Google에서 총 14품종의 강아지 이미지를 크롤링
  + 팀원 한명당 2개 이상의 품종 크롤링
  + 평균적으로 label당 100장의 이미지 크롤링, 총 11,289장
* 이미지 전처리
  + Resize
  + Zero-centering
  + Gray scale
* 크롤링한 이미지를 Pickle로 저장
  + 14개의 pickle을 병합
* 학습
  + model : ResNet50
  + conv layer 일부 재학습 + 분류기 학습
  + fine - tuning
<br><br>
## Results 
||150x150, 10e|200x200, 10e|220x220,8e|
|:--:|:-------:|:----------:|:--------:|
|train accuracy|0.9260|0.9387|0.9312|
|test accuracy|0.8136|0.8441|0.8539|
|after fine-tuning||0.8565||<br>   
<br>   

* table 1) 이미지 사이즈 변화에 따른 성능 변화(gray scale, conv layer 15층 + 분류층 학습)
  + 이미지가 커짐에 따라 확실히 정확도가 높아지는 것을 확인
  + RAM에 부담이 안되는 크기에 정확도가 가장 컸던 200x200, 10e 만 fine-tuning진행
  + accuracy가 조금 상승되는 것을 확인할 수 있음   
 <br>   

||12층, Dropout(0.5) 1번|12층, Dropout(0.5) 2번|30층, Dropout(0.5) 1번|
|:--:|:----------------:|:--------------------:|:--------------------:|
|train accuracy|0.7837|0.9633|0.9922|
|test accuracy|0.8667|0.8940|0.8887|
|after fine-tuning|0.8760|0.8920|0.8920|<br>   
<br>   

* table 2) Model 수정에 따른 성능 변화(data > int화, 180x180, Gray scale X)
  + Color image 사용(Gray scale X)
  + Drop out, conv layer 학습하는 층수를 변경
  + 최대 0.89까지 상승
<br><br>
### Reference
* [https://selenium-python.readthedocs.io/index.html](https://selenium-python.readthedocs.io/index.html)
* [https://keras.io/api/applications/resnet/](https://keras.io/api/applications/resnet/)
* [https://docs.python.org/ko/3/library/pickle.html](https://docs.python.org/ko/3/library/pickle.html)
