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
- 자동차 데이터
- ![dcgan-2 (epoch1000) - 용량down](https://user-images.githubusercontent.com/78893090/169686246-98676570-0e5c-4b1b-aad1-7b6d613d0d62.gif)
- ![image](https://user-images.githubusercontent.com/78893090/169686321-09afc96c-a948-41ea-95f4-c9bec890f137.png)
- 애니메이션 데이터
- ![ani-4 (epoch1000) - 용량down](https://user-images.githubusercontent.com/78893090/169686251-b2a9a9cb-706d-4f8b-9ce4-9fd2bbd97585.gif)
- ![image](https://user-images.githubusercontent.com/78893090/169686348-f7cf19ac-6051-4fb8-a6e4-c2f57f5b13cf.png)

### 입력 이미지 데이터 비교
- ![image](https://user-images.githubusercontent.com/78893090/169686403-6588d5e7-cc47-4f6d-befd-3860188b7206.png)
- 다른 결과가 나오는 이유는?
  - 차량의 너무 다른 각도와 배경도 너무 달라 복합적인 이미지가 되어 알아보기 힘든 이미지로 생성이 됨

### 진행 한계점
- 데이터 수 부족
  - 논문 참조시 약 300만 image사용 
- 컴퓨터 성능 문제
  -  6000 image 사용
  -  image size : (256 x 256) -> (128 x 128)
  -  간단한 Test 진행도 시간이 오래걸리는 문제로 다양한모델 구성 및 하이퍼 파라미터 조절이 어려움

### 개선방향
- 한층 더 개선된 styleGAN2와 같은 모델 사용
- Segmentation으로 car를 인식하여 배경을 제외 후 학습
- 중고차 사이트이미지 사용 (일반적으로 하나의 각도의 사진 사용) 
- 차 종류 분류 후 진행 (세단 SUV 트럭 기타 등등)
- 연도별 자동차이미지로 시계열 모델을 적용하여 차세대 이미지 예측 생성
