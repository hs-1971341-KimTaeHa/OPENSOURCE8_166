# 오픈소스 소프트웨어 시스템 설계서

#### 8반 16_6조 | 장수빈이현승, 임종혁, 김지훈,김진호,김태하



#### 프로젝트 개요



#### 서비스 설명



#### 유사서비스 분석



#### 오픈소스 설명


### Open Pose를 이용한 모션인식  

#### 개요

 현재 PT 관리 서비스를 통해 사용자에게 제공하려는 것은 카메라를 통해 사용자의 몸과 움직임을 인식하여 운동 동작이 제대로 되었는지 체크를 하고 교정해주는 것이다. 사용자와의 상호작용을 통해 잘못된 동작을 지적해주고 직접 헬스장을 가지 않더라도 디지털 기술을 활용해 현장에서 트레이너의 지도를 직접 받지 못한다는 한계를 극복하여 집에서도 편하게 이용할 수 있다. 뿐만 아니라 개인이 원하는 운동을 선택할 수 있고 추천해주는 서비스를 통해 개인 맞춤형을 제공한다. 이러한 서비스를 제공하기 위해 제일 핵심적인 부분은 카메라를 통해 사용자를 인식하는 것이다. 이를 위한 오픈소스로 Open Pose를 알아보았다.

### OpenPose란?

<b>OpenPose</b>는 인간 자세 예측 (Human Pose Estimation)의 한 분야로 오로지 카메라 한대로만 가지고 사람의 몸, 얼굴, 손가락마디를 정확하게 예측하는 <b>real-time multi-person 오픈소스 라이브러리</b>이다. 기존 키넥트 센서를 사용해서 사람의 스켈레톤 데이터를 따오는 과거의 현실에 비해 Open Pose는 일반 카메라로도 사람의 스켈레톤 데이터를 따올 수 있게 만든 딥러닝 네트워크이다.

> 전통적인 방식의 Human Pose Estimation

기존 전통적인 방식은 사람 몸에 무언가를 부착하고 하기에 돈이 많이 들고 공간의 제약, 사람 체형에 따라 달라지는 장비로 많은 불편함이 있었다.

하지만 컴퓨터 성능의 발전으로 인해 컴퓨터비전(Computer Vision)에 딥러닝(Deep Learning) 기술이 사용되었고. 이러한 기술을 조합하여 영상으로만 이 Human Pose Estimation을 정확하게 할수 있게 되었다.

> 업그레이드 된 Human Pose Estimation -> OpenPose

OpenPose 전에도 이렇게 인간의 스켈레톤을 찾는 방법은 연구가 되었지만 그 전에는 사람을 검출하고, 검출된 사람에 대한 자세를 찾도록 반복 수행하는 Top-Down 방식을 사용 하였지만 OpenPose는 Bottom-Up 방식으로 반복처리 없이 수행을 한다.

<hr>


### 자세 추정 방식

- <em>Top-Down</em>

  - 이미지에서 사람을 먼저 찾고, 찾은 사람의 Bounding Box에서 자세를 추정
  - 사람을 먼저 찾고, 사람안에서 joint들을 찾기 때문에 정확도가 Bottom-up방식보다 높다
  - 검출된 사람들을 순회하며 joint들을 찾기 때문에 속도가 Bottom-up방식보다 느리다

- <em>Bottom-up</em>

  Bottom-up 방식은 이미지 상에서 모든 신체 부위를 먼저 찾아내고, 이후에 찾아낸 신체 부위가 어떻게 연결되는지 추론 하는 방법을 말한다.

  		- 이미지에서 joint들을 먼저 찾고, joint들의 상관관계를 분석하여 이들을 연결하여 자세를 추정

  - 정확도는 Top-down 방식에 비해 떨어지지만, Object Detection 과정이 없기 때문에 속도가 빨라 실시간 처리에 사용 가능

<hr>


### Realtime, Multi-Person ( Runtime Analsis )

Openpose의 저자는 Openpose 모델이 Realtime, Multi-Person 환경에서도 우수한 성능을 보여준다는 점을 논문의 제목에서부터 강조하고 있다. 저자는 다른 Human Pose Estimation 모델인 AlphaPose와 Mask R-CNN과 성능을 비교하여 이를 근거로 들었다. 자료는 아래와 같습니다.

![Realtime, Multi-Person](https://velog.velcdn.com/images%2Fmarkany%2Fpost%2F6e11738e-80be-4bf4-871e-199220d1dfff%2Fimage.png)

Openpose(아래쪽 평평한 두 개의 선)의 추론 시간은 이미지 내의 사람이 몇명이든 일정한 것이 가장 큰 특징이다. 위에서 설명했듯이 Bottom-up방식의 장점중 하나라고 할 수 있다. 반면 AlphaPose와 Mask R-CNN의 경우 이미지에 등장하는 사람 수에 비례해서 추론 시간이 늘어나는 것을 확인할 수 있다. 이를 통해 Openpose가 Realtime, Multi-Person 환경에서 유리하다는 것을 알 수 있다.

<hr>


### OpenPose의 딥러닝 네트워크 구조

![Realtime, Multi-Person](https://post-phinf.pstatic.net/MjAyMDAzMjBfMzQg/MDAxNTg0Njg3MzE5NDY5.6IwpJitMU6uSdP4RS_vuKaAGaVglQArkZ8WESZh3pfQg.c1fMTKvu_L5NOcJk4qTYjtwYtfV_EkDff5aqz1k5uJog.JPEG/humanpose_03.jpg?type=w1200)

네트워크의 입력은 높이(h) x 폭(w) 크기의 컬러 이미지이고 VGG-19 네트워크의 일부를 통과하게 된다. VGG 네트워크는 옥스포드대학교의 Visual Geometry Group에서 개발했다. 세계 최대 이미지 인식 경연대회인 ILSVRC(ImageNet Large Scale Visual Recognition Competition) 2014년 행사에서 GoogleNet과 함께 주목을 받으며 근소한 차이로 2위를 차지했지만, 구조가 간단하여 이해하기 쉽고 변형을 시켜가면서 테스트하기 용이한 장점이 있다.

이미지가 VGG-19 네트워크의 입력으로 들어가면, CNN의 Convolution Layer(C)와 Pooling Layer(P)를 거쳐서 특징맵(F)을 생성하게 된다. 특징맵(F)은 처음에는 큰 의미 없는 내용이 담겨 있지만, 그 내용을 학습 데이터와 비교하며 차이점을 점점 줄여나가는 방향으로 최적화를 하면 학습 데이터에 맞는 특징을 갖게 될 것이다. 그리고 이 특징맵(F)은 Stage 1의 입력으로 들어간다.

Stage 1은 2개의 브랜치로 나누어진다. 첫 번째 브랜치의 CNN(p1)은 모든 사람의 관절 위치를 결정하는 Confidence Map(S)을 생성한다. Confidence Map은 특정 신체부위가 위치할 가능성에 따라 높은 값(최저 0 ~ 최고 1)을 갖는 흑백 이미지라고 할 수 있다. 관절이 위치한 픽셀을 중심(중심 값은 1.0)으로 퍼지면서 값이 감소하는 Heatmap을 만든다. 예를 들어 아래 그림은 왼쪽 어깨에 대한 Confidence Map과 실제 데이터를 겹쳐서 표현한 이미지이다. 왼쪽 어깨에 해당하는 부분이 높은 값을 갖는 것을 볼 수 있다. 이 Confidence Map을 학습시켜서 사진으로부터 각 관절의 위치를 추정할 수 있다.

두 번째 브랜치의 CNN(ф)에서는 Part Affinity Fields(PAFs)를 예측하는데, PAFs(L)는 한 파트에서 다른 파트로 이어지는 방향(Position and Orientation)을 인코딩한 2D 벡터로 인체 부위 사이의 연관 정도를 나타낸다. 이 정보는 관절이 연결된 정보를 담고 있고 누구의 것인가를 파악하는 데 사용된다. 예를 들어 아래 [그림 5]는 왼쪽 어깨와 목의 Part affinity이다. 같은 사람의 인체 부위(목, 어깨)가 크게 연관되어 있는 것을 볼 수 있다.

이후 Stage 2부터는 Stage 1의 출력인 Confidence Map(S)과 PAFs(L), VGG Network의 출력인 특징맵(F)을 조합해서 CNN의 입력으로 사용한다. 네트워크가 깊어질수록 앞에 위치한 layer는 학습의 영향이 줄어들기 때문에 좀 더 나은 결과를 얻기 위해 매 Stage마다 특징맵(F)을 사용한다. 네트워크의 각 Stage에서는 예측한 수치와 실제 훈련 데이터에 있는 정답과 비교를 통해 오차값을 구하고 이를 최소화하는 방향으로 네트워크를 학습시킨다.

<hr>


### 한계

- 학습되지 않은 희귀한 자세 (추정은 어느정도 하지만 떨리는 현상)
- 몸의 일부가 잘 안보이게 될 시 (잘려서 나오거나 스켈레톤이 떨림)

- 사람 형태를 하고 있는 경우 (옷, 마네킹 등)

- 원거리 스켈레톤 검출 잘 안됨 (원거리의 기준은 카메라 해상도, FOV마다 다르다.)

<hr>


### 사용 결과 및 실행 결과

사람의 몸에 장비를 장착하지 않고 사진이나 영상으로 사람의 자세를 추출할 수 있다.

- #### Whole-body (Body, Foot, Face, and Hands) 2D Pose Estimation

![Result1](https://github.com/CMU-Perceptual-Computing-Lab/openpose/raw/master/.github/media/pose_hands.gif)

- #### Whole-body 3D Pose Reconstruction and Estimation

  ![Result2](https://github.com/CMU-Perceptual-Computing-Lab/openpose/raw/master/.github/media/openpose3d.gif)

- #### Google에 push up을 검색한 것 중 gif 파일을 Webcam에 비춘 모습

![Result](https://velog.velcdn.com/images%2Foneul1213%2Fpost%2Fd8e515b8-addd-41c5-968e-163b4704cfc8%2Fpushup-openpose.gif)

MediaPipe 포즈 감지(Pose)

Licence
Apache License Version 2.0, January 2004

MediaPipe
MediaPipe란 구글에서 제공하는 AI 프레임워크로서, 비디오형식 데이터를 이용한 다양한 비전 AI 기능을 파이프라인 형태로 손쉽게 사용할 수 있도록 제공된다. AI 모델개발 및 수많은 데이터셋을 이용한 학습도 마친 상태로 제공되므로 간편하게 호출하여 사용하기만 하면 된다.
기본적인 얼굴인식 이외에도 Pose 인식 등 다양한 비전AI 기능들이 제공되는데 본 서비스에서는 Pose만 사용한다.

Pose Land Mark
포즈 랜드마크의 리스트이다.. 각 랜드마크는 다음과 같이 구성된다. 
x와 y : 랜드마크의 좌표는 각각 이미지의 너비와 높이로 [0.0, 1.0]로 표준화된다.
z : 엉덩이 중간 지점의 깊이를 원점으로 하여 랜드마크의 깊이를 나타내며, 랜드마크가 카메라에 가까울수록 값이 작아진다. z의 크기는 x와 거의 비슷한 척도를 사용한다.
Pose Land Mark를 통해 영상 속 사람의 Skeleton Model을 추출할 수 있다. 추출된 Skelton Model의 Pose Land Mark의 반복적인 움직임을 통해 올바른 동작 자세를 추출할 수 있다.

Pose Classification
MediaPipe를 활용하면 포즈 분류가 가능하다. 각 운동의 최종 상태( 팔굽혀 펴기를 예로 들면 위, 아래의 위치)에 대한 수백개의 샘플을 추출해낸다.
Pose Land Mark를 특징 벡터로 변환하기 위해 손목과 어깨, 두 손목 사이의 거리와 같이 미리 정의된 포즈 관절 목록 사이의 쌍별 거리를 사용한다. 알고리즘은 거리에 의존하기 때문에 모든 포즈는 변환 전에 동일한 몸통 크기와 수직 몸통 방향을 갖도록 정규화된다.

Repetition Counting
반복적인 움직임을 채크한다. 이를 통해 Pose Land Mark의 x,y,z 축의 움직임을 측정할 수 있다.

활용방안
운동 영상을 통해 데이터를 구축한다.
Pose Classification를 통해 동작을 분류하고, Repetition Counting을 통해 반복적인 움직임을 관측한다. 그 후 Pose Land Mark을 통해 x,y,z,의 움직임을 수집한다.


#### DFD



#### 결론









