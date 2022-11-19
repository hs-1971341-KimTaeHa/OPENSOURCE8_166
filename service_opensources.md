# 오픈소스 소프트웨어 시스템 설계서

#### 8반 16_6조 | 장수빈이현승, 임종혁, 김지훈,김진호,김태하



#### 프로젝트 개요



#### 서비스 설명



#### 유사서비스 분석

국내에서 출시 중인 App으로는 Kakao에서 만든 '스마트홈트', '하우핏' 2개가 다운로드 수도 많고, 평점 수가 
높아 유사서비스 분석 대상으로 선정하였다. 두 App들은 모션인식을 기반으로, 일정 수치 이상의 동작 이상이
없을 경우 동작의 일치함을 인정한다. 또한, 유명 트레이너 및 강사들을 영입하여 운동의 진입장벽을 낮추고
있다. 운동을 마친 이후 소모한 kcal를 알려주며, 운동을 한 분기점 전과 비교하여 감소율을 알려준다.
그렇지만, 운동을 마치고 해당 부위의 다른 운동법 추천이 없는 점이 꽤나 아쉬웠다.
'스마트홈트'의 경우는 자체적인 Ai 인식을 통한 kcal 계산을 할 수 있는 식단 시스템이 있다. 사진을 찍거나,
앨범에 있는 사진을 가져올 시 자체적인 딥러닝을 마춘 Ai가 유사 음식들과 비교하여 kcal를 알려준다.
하지만 음식의 분별력에 있어 한참 부족한 면이 있었고, 이를 보완했으면 더욱 좋다는 생각을 가졌다.

'스마트홈트'의 경우 오픈소스 라이선스를 지니고 있다.
[사용된 오픈소스 목록 및 URL]
firebase : https://github.com/firebase/firebase-android-sdk
facebook sdk : https://github.com/facebook/facebook-android-sdk
kotlinx.coroutines : https://github.com/Kotlin/kotlinx.coroutines
retrofit2-kotlin-coroutines-adapter : https://github.com/JakeWharton/retrofit2-kotlin-coroutines-adapter
RxJava : https://github.com/ReactiveX/RxJava
RxAndroid : https://github.com/ReactiveX/RxAndroid
RxKotlin : https://github.com/ReactiveX/RxKotlin
RxBinding : https://github.com/JakeWharton/RxBinding
Dagger : https://github.com/google/dagger
Retrofit2 : https://github.com/square/retrofit
OkHttp3 : https://github.com/square/okhttp
Glide :https://github.com/bumptech/glide
Exo Player : https://github.com/google/ExoPlayer
Gson : https://github.com/google/gson
Simple XML : http://simple.sourceforge.net
Anko : https://github.com/Kotlin/anko
stetho : https://github.com/facebook/stetho
leakcanary : https://github.com/square/leakcanary
material-calendarview : https://github.com/prolificinteractive/material-calendarview
AutoScrollViewPager : https://github.com/angeldevil/AutoScrollViewPager
ViewPagerIndicator : https://github.com/JakeWharton/ViewPagerIndicator
ExpandableTextView : https://github.com/Manabu-GT/ExpandableTextView
Skeleton : https://github.com/ethanhua/Skeleton
ShimmerLayout : https://github.com/team-supercharge/ShimmerLayout
jglm : https://github.com/jroyalty/jglm
Kakao Open SDK : https://developers.kakao.com/docs/sdk
mace : https://github.com/XiaoMi/mace
tensorflow : https://github.com/tensorflow/tensorflow
FlycoTabLayout : https://github.com/H07000223/FlycoTabLayout
Flurry : https://github.com/flurry/flurry-android-sdk
RealtimeBlurView : https://github.com/mmin18/RealtimeBlurView
CircularProgressView : https://github.com/rahatarmanahmed/CircularProgressView
CircleProgressBar :https://github.com/dinuscxj/CircleProgressBar
Subsampling Scale Image View : https://github.com/davemorrissey/subsampling-scale-image-view
ARCore : https://developers.google.com/ar/reference


#### 오픈소스 설명

운동이 끝난 직후, 추천 영상을 소개해주는 오픈소스를 가져오고자 한다.

Algorithm : 운동 영상이 끝난 직후 적절한 영상감을 찾는 과정을 알려준다.
https://github.com/TheAlgorithms/C-Plus-Plus

Recommend : 'Algorithm'의 결과 값을 바탕으로 '추천'을 하는 소스이다.
https://github.com/hongleizhang/RSPapers.git

#### DFD



#### 결론