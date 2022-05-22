### Project (2022.03.17 ~ 2022.03.22)
- - -
# GAN을 이용한 자동차 이미지 생성

### 모델 선정 과정
- GAN 이란?
  - 데이터 셋과 유사한 이미지를 만든다.
  - Generator (생성자)는 실제 데이터 분포를 학습 -> 이미지를 잘 생성해서 속일 확률을 높이는 것이 목적
  - Discriminator (판별자)는 원래의 데이터인지 생성자로부터 생성이 된 것인지 구분 -> 제대로 구분하는 확률을 높이는 것이 목적
  - ![image](https://user-images.githubusercontent.com/78893090/169685408-3b628c9e-ba3f-4c0e-9c33-dd4d8ec5b0b2.png)
  - 이러한 특징으로 `GAN 모델이 이미지 생성에 적합한 모델`

- 다양한 GAN 모델 (일부 예시)
  - DCGAN : 조작된 가짜 이미지 생성
  - SRGAN : 저해상도 이미지를 고해상도 이미지로 변환
  - StackGAN : 입력된 문장과 단어를 해석해 이미지를 생성
  - 3D-GAN : 2D 이미지를 3D 이미지로 전환
  - CycleGAN : 이미지의 스타일을 다른 이미지로 변환 (밤 사진 -> 낮사진, 모네풍을 피카소 풍)
  - DiscoGAN : 서로 다른 객체 그룹 사이의 특성을 파악하여 양자 사이의 관계를 파악 (가방 이미지로, 유사느낌 신발 이미지 생성)

### 데이터
- 데이터 출처 : https://www.kaggle.com/datasets/jessicali9530/stanford-cars-dataset
- ![image](https://user-images.githubusercontent.com/78893090/169685550-69746b15-31e7-4c3f-b95e-3191a9c427ff.png)

### 모델 구성 과정
- 이미지 전처리
  - image size -> 128 x 128으로 통일
  - image 정규화 (-1, 1) -> 활성화 함수 tanh사용으로 인한 범위 와 일치 
- 모델
  - generator(생성자) -> generator_loss(loss -> BinaryCrossentropy) -> generator_optimizer(Adam)
  - discriminator(판별자) -> discriminator_loss(loss -> BinaryCrossentropy) -> discriminator_optimizer(Adam)

### 결과물
- 차 이미지가 잘 나오지 않아 비교를 위해 애니메이션 데이터를 같은 모델에 적용
- ![dcgan-2 (epoch1000) - 용량down](https://user-images.githubusercontent.com/78893090/169686246-98676570-0e5c-4b1b-aad1-7b6d613d0d62.gif)
- ![ani-4 (epoch1000) - 용량down](https://user-images.githubusercontent.com/78893090/169686251-b2a9a9cb-706d-4f8b-9ce4-9fd2bbd97585.gif)


