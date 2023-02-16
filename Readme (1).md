

# 와인품질 예측
### 피처 설명
-   fixed acidity(고정산) : 타르타르산, 사과산 및 구연산과 같은 와인의 비휘발성 산의 수준. 와인의 풍미에 중요하며, 시큼털털한 맛에 기여.
    
-   volatile acidity(휘발성산) : 아세트산과 같이 와인의 향과 풍미에 영향을 줄 수 있는 휘발성 유기산. 높은 수준의 volatile acidity는 와인에 불쾌한 와인 맛을 줄 수 있는 반면, 낮은 수준은 와인의 전반적인 균형과 복합성에 기여
    
-   citric acid(구연산) : 와인의 구연산은 타르타르산 및 사과산과 함께 와인에 존재하는 fixed acidity 유형 중 하나. 신선함을 제공하고 와인에 시큼하고 톡 쏘는 풍미를 더함
    
-   residual sugar(잔당) : residual sugar은 포도주 양조 과정 후에 와인에 남아 있는 발효되지 않은 설탕의 양. 와인의 당도에 영향을 미치며 residual sugar가 높으면 더 달콤한 와인이 되고 낮으면 드라이한 와인이 됨
    
-   chlorides(염화물) : 와인의 짠맛의 원인이며 신맛에도 영향을 미침
    

  

-   free sulfur dioxid(유리 이산화황) : 유리 이산화황은 방부제 역할을 하는 유황 화합물의 일종으로 와인이 부패하고 산화되는 것을 방지.이산화황이 너무 많으면 와인에 불쾌하고 쓴 맛이 날 수 있으며, 너무 적으면 부패하고 이취가 남.
    
-   total sulfur dioxide(총 이산화황) : 와인의 총 이산화황은 와인 보존에 중요한 요소이지만 높은 수준은 와인의 풍미와 향에 영향
    
-   density(밀도) : 부피 대비 와인의 무게. 와인의 알코올 함량을 결정하는 데 사용할 수 있으며 밀도가 높을수록 알코올 함량이 높음
    
-   pH(산도) : 대부분의 와인에 이상적으로 간주되는 pH 범위는 3-4로 와인의 산도 또는 알칼리도를 측정. 낮은 pH는 높은 산도를 나타내고 높은 pH는 낮은 산성 와인을 나타냅니다.
    
-   sulphates(황산염) : 와인의 황산염은 발효의 자연 부산물이며 방부제로 첨가될 수도 있음. 황산염 수치가 높을수록 쓴맛이 나고 수치가 낮을수록 더 부드러운 풍미가 생길 수 있음.
    
-   alcohol(알코올) : 발효를 통해 생산되는 와인의 에탄올 양. 알코올은 와인의 바디감, 풍미 및 전반적인 강도에 기여하며, 알코올 함량이 높을수록 더 강하고 풍미가 풍부한 와인이 됨
-   타겟 데이터
	-   Quality : 퀄리티의 값은 연속수가 아닌 3 ~ 8의 정수
    
	-   피쳐 데이터는 모두 연속형 데이터이지만, 타겟 데이터 값을 보면 다중 분류 문제의 형식
### 평가지표
-   Quadratic Weighted Kappa Metric
	-   실제값과 예측값 간의 측정 범주 값에 대한 일치도를 측정
	-   단순 정확도를 사용하지 않고 Cohen Kappa Metric를 사용하는 이유
		-   오분류표에서 정분류된 결과들은 우연에 의해 발생한 것일 수 있기 때문에 이런 가능성을 배제
		-   정분류율(정확도)을 사용하는데 있어서의 문제는 오분류된 결과들을 단순히 바르게 분류되지 못한 것으로서 모든 오류를 동일하게 취급
	-   ex) 신용 등급이 ‘상’인 고객을 ‘중’으 로 분류하는 것보다 ‘하’로 분류하는 것은 그 오류의 정도가 크다고 할 수 있으며 이로 인한 손실도 커질 것
	-   즉, Cohen Kappa Metric은 우연히 분류가 일치할 가능성을 보정 함으로써 분류정확도를 측정한 것이며, 그 값은 (실제 분류정확도-우연에 의해 기대되는 분류정확도) 로 주어진다
	-   분류 범주가 순서화 되어 있을 때, 오분류 결과를 그 정도에 따라 오류를 정량화하여 분류정확도를 측정하는데 사용된다

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964640-d5dc672a-349f-46bd-ad7a-178e08967470.png">

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964675-fa8d35e2-4ba8-4994-b9ca-f741584afc64.png">

## 기본 EDA

-   결측치가 없기 때문에 별도의 결측치 채워넣는 과정은 필요 없다
-   Categorical Data가 없다 → 타겟데이터(quality : 정수형)을 제외한 모든 데이터가 연속형
-   훈련 데이터 양 자체가 **2056개**로 매우 적음
	-   캐글 사이트의 DATASET에서 추가로 다운받을 수 있음
	-   추가로 다운받은 데이터에 기존 train 데이터와 중복되는 데이터가 존재한다 → 중복값을 제거하지 않으면 중복값 학습시 해당 정보가 가중되어 과적합의 우려가 있다

## 시각화
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964684-fb0c5a7b-70d5-44fc-b45d-ec6f4cc5b404.png">

- 불균형한 타겟 분포
- 타겟 분포가 상당히 불균형하다 (타겟이 3, 4, 8)인 데이터가 현저히 적다
-   따라서 이를 완화해 주기 위해 Stratified Cross-validation / Class Weighting 등을 사용할 수 있다
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964650-91761117-28bf-4775-b70e-1607772478f0.png">
-   비대칭도가 -1 ~ 1 사이 : 정규분포에 가까움 (초록색)
-   비대칭도가 1보다 큼 : 높은 양의 비대칭도 (빨간색)
-   비대칭도가 -1보다 작음 : 높은 음의 비대칭도 (빨간색)
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964671-5a85c840-47e8-45e4-96cb-3be700384fe8.png">
-   첨도가 -3 ~ 3 사이 : 정규분포에 가까움 (초록색)
-   첨도가 3보다 큼 : 높은 양의 첨도 (빨간색)
-   첨도가 -3보다 작음 : 높은 음의 첨도 (빨간색)
-   비대칭도와 첨도를 종합적으로 봤을 때 'sulphates', 'residual sugar', 'chlorides' 3개 피처가 비정상적 분포를 지님 → Quantile Transtorm을 활용한 정규분포화
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964662-28ead60d-6424-43bc-bdbf-4138d3b932b8.png">
- log, boxcox, square root, quatile scaling을 활용한 transforming

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964693-0b65b039-fc70-4a42-85cb-7e72862e2234.png">

- test 데이터와 train 데이터 간 분포는 유사한 경향

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964653-fe724834-a6b6-4ad7-8a69-a4f19a1f3dad.png">

- 피처들간 상관관계가 높지 않다

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964694-ad89fe86-f802-4748-8964-a54625d9e5b9.png">

- alcohol, sulphates가 피처 중요도가 높다



<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964637-7018d6e4-fd59-4849-b9bd-720946ba9d8c.png">

-   z-score 확인
	-   z-score : 값들이 평균으로부터 얼마나 떨어져있는지(표준편차의 몇 배만큼 멀리 있는지) 알려주는 지표
		-   양의 z-score : 측정값이 평균보다 높음
		-   음의 z-score : 측정값이 평균보다 낮음
		-   z-score > 3 or z-score < -3 : 이상치일 가능성이 높음

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218969820-e4be9283-9819-4179-ad95-b5aa8a014de4.png">

-   Robust Scaling 활용
-   이상치를 제거하지 않고 이상치를 포함하여 정규 분포화 시키는 작업을 하기 때문에 Standard Scaling 보다는 Robust Scaling을 활용한다
- 이상치가 정규분포에 가깝게 눌러진 모습

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964646-30f18ff5-3014-4b27-a011-e184ac4e9aa2.png">

- 비대칭 완화(Quantile Scaling 활용)
- 확실히 치우쳐져 있던 피처들의 분포가 정규분포화 되었음



## 파생피처 생성
-   클러스터링 및 PCA
	-   wcss( within-cluster sum of squares) : 클러스터 내의 총변동
	-   elbow - method 활용
		-   군집을 추가로 늘려가면서 군집내 변동성이 급감하는 군집 개수를 찾아내눈 것
		-   군집내 변동성이 급감한다는 것은 유사한 피처들끼리 잘 묶였다는 것
		-   변동성의 감소폭이 미미해지는 지점이 최적 군집개수



<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218964680-c2f69d3f-f6a6-4c12-ace8-a710da77d153.png">
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218970672-cc48e59c-fa22-45cd-9294-98b4c8882cef.PNG">

-   최적 Cluster 수 : 3 / 최적 PCA 수 : 2


## 모델
-   학습에 사용할 데이터 프레임은 두종류
	-   기존의 모든 컬럼과 새로 추가한 컬럼들 모두 학습에 사용할 DF
	-   학습효과가 높은 컬럼과 cluster, pca1, pca2만 학습에 사용할 DF
-   학습에 사용할 모델 : XGBRegressor + KFold, Stratified-KFold
	-   Stratified-KFold -> 적은 피처를 보정해서 K-Fold를 하는 방식
-   회귀 모델을 사용하면 타겟이 연속형으로 나오기 때문에 Rounding을 하여 결과를 보정해야 한다
	-   단순 Round 함수를 사용하여 반올림하면 데이터 손실이 높아지므로 따로 보정할 함수가 필요 : OptimizeRounder 클래스 생성
	-   OptimizeRounder
		-   kappa_loss 함수 : 평가지표(cohen kappa score)를 보정해줄 계수를 생성하는 함수
		-   fit 함수 : kappa loss의 보정계수를 활용하여 초기 보정값(반올림과 동일)을 최소화하는 목적함수를 생성하여 선형계획을 풀이한다
		-   predict 함수 : fit 함수에서 보정된 계수를 통해 최적화된 Rounding 결과를 추출한다. 
	-   최적 조합 : 모든 피처 + 하이퍼파라미터 탐색시에는 STK, 학습시에는 KF

## 하이퍼 파라미터 튜닝

-   위에서 찾은 최적 조합을 바탕으로 하이퍼 파라미터 튜닝 진행
-   Optuna 활용
	-   베이지안 최적화와 유사한 역할
-   public = 0.59038 : private = 0.59457 → 4등 // BEST SCORE

</br>
</br>
</br>
</br>

------------------------------------

# 뇌졸중 예측

## 피처데이터
- gender: 성별
- age: 나이
- hypertension: 고혈압
- heart_disease: 심장병
- ever_married: 결혼 여부
- work_type: 직업/업무 유형
- Residence_type: 거주 위치(도시, 시골)
- avg_glucose_level: 평균 포도당 수치
- bmi: 비만도
- smoking_status: 흡연 여부
- stroke: 뇌졸중(정답, 타깃)

## 평가지표
-  area under the ROC curve 

## EDA
### 데이터 분석
- 이진형 피처
	- hypertension: 고윳값 0, 1
	- heart_disease: 고윳값 0, 1
	- ever_married: 고윳값 Yes, No
	- Residence_type : 고윳값 -> 제거 후보 피처
		- Urban: 도심값
		- Rural: 시골
- 명목형 피처
	- gender: 고윳값 Male, Female, Other
		- 일반적으로 성별의 경우 Male, Female 두 가지인데, Other라는 성별이 하나 추가되었다.
		- 따라서 해당 Value에 대해 분석하여 이상치일 경우 제거해야 한다.
	- work_type: 고윳값 5개
		- Private: 회사원
		- Self-employed: 자영업
		- Govt_job: 공무원
		- children: 학생
		- Never_worked: 무직
		- 명목형 피처의 값들이 학습에 도움이 되는지 시각화를 통해 확인하고 불필요한 값이 있다면 제거한 후, **One-Hot인코딩** 진행

	- smoking_status
		- 고윳값 4개
		- never smoked: 흡연 경험이 없는 사람
		- formerly smoked: 흡연을 했었던 사람
		- Unknown: Unknown
			- 이상치일 확률이 높기 때문에 데이터 처리 방식에 대해 고려한다. -> 포함해서 진행
		- smokes: 흡연을 하는 사람

- 수치형 피처
	- Age
	- BMI 
	- 수치형(연속형)이긴 하나 나이와 bmi의 기준을 보면 범주형으로 볼 수도 있다. 
- 시각화 과정에서 범주형(이진 피처, 명목형 피처)과 수치형(연속형) 피처를 구분 및 시각화하여 데이터를 분석할 것이다.

## 시각화

### 정답 (stroke) 비율

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219270811-29ddbe9a-c04b-416a-bc7e-790a91e33034.PNG">



## 분석
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/219270796-20324d84-b738-4401-abe4-60d833524506.PNG">
- 나이 데이터 밀도와 분포도
	- 나이는 이상치 없이 고루 잘 분포되어 있다

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/219270783-cc48b0c9-7e95-4286-a766-842ae24a2b70.PNG">

- 나이와  뇌졸중 관계
	- 나이가 들수록 뇌졸중 확률이 올라간다
	- 연속형 데이터이므로 **피처 스케일링**을 진행한다


<img width="863" alt="image" src=" https://user-images.githubusercontent.com/120996995/219270794-51a44109-df2e-47d7-acba-21539772f458.PNG">

-  BMI와  뇌졸중 관계
	- 축을 바꿔보니 양의 기울기를 갖는 선형 그래프가 그려진다
	- BMI수치가 올라갈수록 뇌졸중 확률이 증가한다
	- 연속형 데이터 이므로 **Standard Scaler** 사용하여 학습한다

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219270804-a6e72312-654d-471f-aefc-6f29348b1415.PNG">

- BMI와 뇌졸중과의 관계 2
	- BMI가 18.5 이하면 저체중(0) ／ 18.5 ~ 22.9 사이면 정상(1) ／ 23.0 ~ 24.9 사이면 과체중(2) ／ 25.0 이상부터는 비만으로 판정(3)
	- 과체중으로 갈수록 뇌졸중 확률이 증가한다


<img width="450 alt="image" src="https://user-images.githubusercontent.com/120996995/219270805-45419d2d-8abe-44bf-bbe7-5c6c2b9450bc.PNG">

- BMI와 뇌졸중과의 관계 3

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219270807-f4788e97-9e79-4460-981f-b09d27c59eea.png">

- 평균혈당과  뇌졸중 관계
	- 혈당이 높아질수록 뇌졸중 확률이 증가한다
	- 연속형 데이터 이므로 스케일러를 사용하여 학습한다

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219252967-9cfe7677-8de1-400e-a0a9-839a8b23b80c.PNG">
																											 
<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219252972-d856ed2e-395c-4d21-902b-98e68bee96f6.PNG">

- 성별과 뇌졸중의 관계
	- 남성이 여성보다 뇌졸중 확률이 높다
	- 세 개의 성별 중, Other은 하나로 학습에 영향을 거의 주지 않을 것으로 예상된다. 
		 - 이상치로 판단하고 최빈값으로 대체
										

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219252967-9cfe7677-8de1-400e-a0a9-839a8b23b80c.PNG">

- 심장병과 뇌졸중의 관계
	- 심장병이 있는 환자일수록 뇌졸중 걸릴 확률이 증가한다	 
																 

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219266341-e756edc1-dc36-4e45-912b-d3252cb8e03a.PNG">

-  결혼과 뇌졸중의 관계
	- 결혼을 한 사람일수록 뇌졸중 확률이 올라간다.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219266334-186bb484-c726-4cb4-96d7-c48974aa65f4.PNG">

- 일타입과 뇌졸중과의 관계
	- 자영업자가 뇌졸중 확률이 제일 높다
	- 무직인 경우 뇌졸중 확률이 없다


<img width="450" alt="image" src="https://user-images.githubusercontent.com/120996995/219266337-155f8c27-70ec-4eb5-ba8b-3722fbe5afc3.PNG">
- 주거 환경에 따른 뇌졸중 관계
	 - 주거 형태에 따른 정답의 비율의 차이가 거의 보이지 않는다.
	 - 시골과 도시에 차이는 없어 보인다. 그러므로 피처 제거를 하도록 하겠다.
	 
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962878-c44c2933-0148-4625-8ba1-530a3e199918.PNG">
- 담배와  뇌졸중 관계
	- 이전에 담배를 피웠었던 사람이 뇌졸중에 걸릴 확률이 높아진다



## EDA결과
###  범주형 피처
- 'gender'-> 원-핫 인코딩한다.
- 'work_type'-> 원-핫 인코딩한다.								- 'smoking_status'-> 원-핫 인코딩한다.			  
- 'hypertension'-> 1, 0로 인코딩한다.
- 'heart_disease'-> 1, 0로 인코딩한다.
- 'ever_married'-> 1, 0로 인코딩한다.
- 'Residence_type' -> 제거한다.
### 수치형 피처
- 'age'-> MinMaxScaler 사용한다.
- 'avg_glucose_level' -> standardScaler 사용한다.
- 'bmi'-> standardScaler 사용한다.


## 베이스 라인 구축/하이퍼 파라미터 튜닝을 통한 모델 성능 향상
### 튜닝 없는 기본 성적
- 학습에 사용할 모델 : XGBRegressor
- public = 0.86422, private = 0.89637 
- **112등**

### 하이퍼 파라미터 튜닝
- GridSearchCV, Bayesian Optimization 활용
	- GridSearchCV와 Bayesian Optimization를 활용하여 찾은 파라미터에서 직접 세부 조정을 통해 성능을 극한으로 끌어올림
- public = 0.87432, private = 0.89959
- **6등** // BEST SCORE

																	  
</br>
</br>
</br>
</br>

------------------------------------
																	  

# 신용카드사기 예측

## 피처데이터
-   Time : 각 트랜잭션과 데이터 세트의 첫 번째 트랜잭션 사이에 경과된 초(second)
-   Amount : 거래 금액
-   Vxx: 28개
-   Class: 타깃

## 평가 지표
    
[area under the ROC curve](http://en.wikipedia.org/wiki/Receiver_operating_characteristic)

##  EDA 과정
###  데이터 분석
- 전체 피처: 수치형 데이터
- VXX 피처 칼럼명 데이터의 의미를 추론하기 어렵다. 
- Time과 Amount의 경우 대략적인 의미를 유추할 순 있지만, 시각화를 통해 직접적으로 데이터의 특성을 파악해봐야 할 것이다.
- 캐글 데이터셋 설명에는 **금융 기업 보안상 이유**로 데이터 자체가 PCA 되어 제공됐기 때문에 **피처 자체의 의미를 파악하는 것은 어려울 것**으로 예상된다. 따라서 전체적인 데이터의 분포와 형태를 보고 어떠한 방향으로 피처 엔지니어링 할 것인지 정해야 한다.

###  EDA 결과
- Time과 Amount를 제외한 V 피처는 기본적으로 스케일링이 되어있다. 하지만 어느 정도 value 편차가 존재하는 피처가 있고, 따라서 Time과 Amount와 함께 value 편차를 줄이기 위한 스케일링이 필요하다고 판단했다.
	- 따라서, 전체적인 데이터의 분포가 정규분포 형태를 띠고 있기 때문에, value의 편차를 줄이기 위해 StandardScaler를 사용했다.

## 시각화

### 정답 분포
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962650-7697daaa-f55c-4f0f-9f20-98473d0a5663.PNG ">

### Vxx 피처
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962657-1847ac67-c52f-4b89-baa3-3d01cee94bb7.PNG ">
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962664-13064d6b-84fd-4846-b3e3-8922e506065d.png ">

- 대부분의 피처가  **정규 분포** 의 형태를 띠고 있다.
- 수치의 분포(주황색 점)는 대역폭에서 크게 벗어나는 **이상치가 거의 없음** 
	 - 모든 피처 활용
	 - value 편차를 줄이기 위해 StandardScaler 사용

### 상관관계 
<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962666-8fa4c30d-7cdf-47d4-9b90-0d239d2111e7.png ">

- 각 피처가 **0을 기준으로 분포**하고 있다.
- 강한 상관관계를 갖는 피처가 없다. 
	- 모든 피처 사용

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962670-cab54619-da1f-4052-93c6-64fe28cb63a9.png ">

- 해당 차트로는 의미있는 데이터 분석이 어렵다. 

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962672-5c61b43b-bebc-4eef-8748-8049baea607e.png ">

- 축변환을 하고 난 후, 의미 있는 데이터 분석이 가능하다고 판단하였다.
- 타깃값의 확률이 증가할 때 피처 value의 변화가 생긴다면 ->의미 있는 피처
- 변화가 생기지 않는다면 -> 의미 없는 피처라고 판단하였다.
	- 수평선이 나오는 피처는 정답 분류에 도움이 되지 않을 확률이 높다. 
	- 하지만 우선 모든 피처를 학습에 활용한다.

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962675-d54a0f0f-f97e-4949-b5c8-c04cd40cad5d.png ">
<img width="863" alt="image" src=" https://user-images.githubusercontent.com/120996995/218962675-d54a0f0f-f97e-4949-b5c8-c04cd40cad5d.png">

- Time의 경우 Value의 빈도 분포가 대략적으로 정규 분포의 형태를 띠고 있다.
- Amount의 경우 전체적으로는 매우 넓은 범위에 빈도가 분포하고 있지만, 0에 가까운 지점에서 많은 value가 찍힌 것으로 보인다.
	- 따라서 두 피처의 **커널 밀도 시각화**를 진행한다.

<img width="863" alt="image" src="https://user-images.githubusercontent.com/120996995/218962676-18d139f4-695a-4c10-8436-509be66b0b09.png ">

- Time:대역폭 내에 수치가 거의 일정하게 분포하고 있다. 
- Amount: 벗어나 있는 값이 많은 것을 확인했다.
	- 피처 value 편차를 줄이기 위해 **StandardScaler**를 사용한다.


## 결과
###  베이스 라인 구축/하이퍼 파라미터 튜닝을 통한 모델 성능 향상
-   학습에 사용할 모델 : XGBRegressor
### 기본 성적
- public = 0.83656 : private = 0.82317 → 60등

### 하이퍼 파라미터 튜닝
-   그리드서치, 베이지안 최적화 활용
	-   단, 그리드서치와 베이지안을 활용하여 찾은 파라미터에서 직접 세부 조정을 통해 성능을 극한으로 끌어올림 
-   public = 0.82754 : private = 0.83538 → 1등 BEST SCORE



