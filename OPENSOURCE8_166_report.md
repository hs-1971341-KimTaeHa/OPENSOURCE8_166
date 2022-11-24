# 오픈소스 소프트웨어 시스템 설계서

#### 8반 16_6조 | 장수빈이현승, 임종혁, 김지훈,김진호,김태하



#### 프로젝트 개요



#### 서비스 설명



#### 유사서비스 분석



#### 오픈소스 설명

### FoodLens 오픈소스

개요 : 기존(''다이어트신'' 등)의 어플에서는 사용자가 직접 먹은 음식을 입력해야하는 번거로움이 있었다. 다음 오픈소스는 사용자로부터 사진데이터를 입력받으면 해당 사진의 음식데이터를 보내주는 기능을 수행한다. 사용자는 사진만으로 자신이 먹은 음식의 종류를 볼 수 있으며, 최종적으로 해당 음식의 정보가 맞는지 확인한 후 영양 정보또한 얻을 수 있다. 해당 데이터는 DoingLab DB를 기반으로 제공되며, MIT라이센스를 제공한다.

오픈소스 라이센스 : MIT라이센스

오픈소스 기능 : 입력된 사진데이터를 바탕으로 음식정보를 추천하고 제공한다.  두잉랩(SDK제공사)에서 제공하는 DoingLab DB를 기반으로 음식의 이름, 칼로리, 탄수화물, 단백질, 지방, 비타민 등의 데이터 값을 리턴받는다. 



(섭취한 영양정보 산출 계산식 [FoodLens 오픈소스 Readme.md에서 발췌])

`for(int i = 0; i < recognitionResult.getFoodPositions().size(); i++) {
	FoodPosition foodPosition = foodPositions.get(i);
	float eatAmount = foodPosition.getEatAmount(); // 사용자가 설정한 1회 섭취량
	Nutrition nutrition = foodPosition.getUserSelectedFood().getNutrition(); `

`// 선택한 음식에 대한 Raw 영양정보 데이터
	eatAmount * nutrition.getCarbonHydrate(); // 1회 섭취한 음식에 대한 탄수화물 섭취량
	eatAmount * nutrition.getProtein(); // 1회 섭취한 음식에 대한 단백질 섭취량
	eatAmount * nutrition.getFat(); // 1회 섭취한 음식에 대한 지방 섭취량
	...
}`

해당 코드를 사용하여 사용자가 섭취한 음식의 **총 칼로리 데이터**를 얻을 수 있다.



[오픈소스 github : https://github.com/doinglab/FoodLensSDK]

#### DFD



#### 결론









