# 오픈소스 소프트웨어 시스템 설계서

#### 8반 16_6조 | 장수빈이현승, 임종혁, 김지훈,김진호,김태하



#### 프로젝트 개요



#### 서비스 설명



#### 유사서비스 분석



#### 오픈소스 설명

## **Talend Open Studio for Data Integration**

#### Talend Open Studio란?

Talend는 오픈소스 ETL 데이터 통합 솔루션으로 온프레미스와 클라우드 모두에서 호환된다. 데이터 통합, 데이터 프로파일링, 클라우드 통합 및 빅데이터 등을 위한 개방형 아키텍쳐이다. Apache License를 사용하며 Oracle, Microsoft SQL server, MySQL 등 다양한 데이터베이스와 연결되어 이용 가능하다. 

#### **ETL** 

ETL은 추출(Extract), 변환(Transform), 적재(Load)로 여러 데이터 소스에서 데이터를 추출하여 사용자가 원하는 형태로 변환 후 데이터 웨어하우스, 데이터베이스 등에 적재하는 것을 말한다. 처리해야하는 데이터의 양의 폭발적으로 늘어나면서 데이터 분석에 많은 비용이 들게 되었는데 ETL 툴을 이용하여 데이터를 효율적으로 활용할 수 있다.

![image-20221112231455901](C:\Users\eltm5\AppData\Roaming\Typora\typora-user-images\image-20221112231455901.png)

#### **장점**

\-   코딩을 하지않고 drag & drop으로 사용가능해 사용자 친화적인 GUI를 지원한다-

\-   이클립스 기반으로 구현되어서 JAVA코드와 매핑되고 jar파일을 생성 가능하다.

\-   1000개 이상의 사전 구축된 커넥터를 제공하여 파일 변환, 데이터 로드 등의 작업을 쉽게 수행가능하다.

\-   다양한 소스의 데이터를 쉽게 결합, 변환 및 업데이트 할 수 있다.

#### **용도**

본 서비스에서는 운동 정보나 음식의 영양 정보를 가지고 있는 데이터베이스에서 필요한 정보만을 추출해낸다. 그 후 운동 부위별, 음식은 영양소별(탄수화물, 단백질, 지방 등)으로 구분하여 새로이 데이터베이스에 저장하는 용도로 사용한다. 사용자가 운동이나 식단에 대해 물었을 때 미리 재구성한 데이터베이스에서 정보를 제공한다.

 #### 공식홈페이지

https://www.talend.com/

#### 소스코드

https://sourceforge.net/projects/talend-studio/

MediaPipe 포즈 감지(Pose)

Licence
Apache License Version 2.0, January 2004

Mediapipe 깃 허브 주소
https://github.com/google/mediapipe.git

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

출처
https://google.github.io/mediapipe/solutions/pose_classification.html
https://google.github.io/mediapipe/solutions/pose
#### DFD



#### 결론









