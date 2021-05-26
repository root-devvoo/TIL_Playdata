오늘 할 내용...

![image](https://user-images.githubusercontent.com/78403443/119621205-d1160e00-be40-11eb-8174-0693204a9944.png)

Decision Tree에서 Random Forest를 알아본다.

kaggle 경진대회에서 우승 한 사람들이 많이 쓴.. Boosting 기법

TradientBootMachine

AdaBoostingMachine 이 Boosting 기법에 들어감(?)

<br/>

점점 딥러닝을 하기위한 전문적인 용어들을 설명하고 확장..

성능평가적인 측면에서도

어제 알려준 score() 함수

accuracy_score() 함수 말고도 Evaluation으로 많이 쓰이는 

다른 함수에 대해서도 알아본다.

<br/>

---

어제 팀별로 한 타이타닉 데이터는 D:\encore_jwc\util\ai_util\html_code\03_MachineLearning 폴더에서

팀별 html파일 보기

(kaggle 채점 기준이 올라가서 점수가 낮게 나온다)

---

**Decision Tree**

<br/>

- **특성 중요도**

속성이 30개가 있다. 

속성이 많게되면 데이터도 그만큼 많아진다. 

(속성이 많다는것을 차원이 크다고 하는데, 차원이 많으면 학습하기 굉장히 까다롭다)

(차원이 많다는 건 컬럼이 많다는 얘기)

차원(컬럼)이 많으면 그와 동시에 row(행)도 많아야 한다.

<br/>

특성 중요도를 보면 트리를 구성하는데 얼마나 중요한 속성인가를 알 수 있다.

위 이미지의 특성 중요도 그래프를 보면 암인지 아닌지 판단하는데, 중요한 속성이 무엇인지 알 수 있다.

<br/>

특성 중요도는 Decision Tree 모델 생성하고 나오는 것이다.

그럼 어떨 때 쓸까? 다 돌리고 나오는건데...

조금 더 정확성을 높이기 위해서 특성 중요도에서 중요하다고 판단되어지는 중요한 특성만 가지고 학습을 다시 시켜보는 것이다.

---



------

- **05_ML_DT_cancer.ipynb 파일 보기**

<br/>

sklearn에서 제공되는 유방암 데이터 로드

![image](https://user-images.githubusercontent.com/78403443/119621518-2f42f100-be41-11eb-9774-826508d2ec5e.png)

딕셔너리 형태로 제공된다.

![image](https://user-images.githubusercontent.com/78403443/119621547-3833c280-be41-11eb-8508-3b769c04c4a9.png)

![image](https://user-images.githubusercontent.com/78403443/119621567-3ec23a00-be41-11eb-8ce3-f33a66b477d4.png)

![image](https://user-images.githubusercontent.com/78403443/119621593-4550b180-be41-11eb-98d4-8efda62da0df.png)

![image](https://user-images.githubusercontent.com/78403443/119621617-4c77bf80-be41-11eb-9708-45ab446fdb20.png)

이렇게 감 잡고 가야한다.

![image](https://user-images.githubusercontent.com/78403443/119621653-58638180-be41-11eb-9a7d-a93e8aa7f3b7.png)

![image](https://user-images.githubusercontent.com/78403443/119621678-5f8a8f80-be41-11eb-9600-5c13752472e4.png)

데이터 만든 사람...

95년도 자료임을 알 수 있다.

Describe로 확인하는거 중요하다.. 

많은 정보를 알 수 있다.

<br/>

- **파이썬의 주요 기능**

  - enumerate(), zip(), T(), map()

![image](https://user-images.githubusercontent.com/78403443/119621732-6e714200-be41-11eb-8768-35555e13f96a.png)

![image](https://user-images.githubusercontent.com/78403443/119621754-74ffb980-be41-11eb-91c7-b780de129e99.png)

![image](https://user-images.githubusercontent.com/78403443/119621782-7c26c780-be41-11eb-9a27-9e078df36fd1.png)

<br/>

- **Train, Test Data Split and Shuffle**

![image](https://user-images.githubusercontent.com/78403443/119621879-99f42c80-be41-11eb-8ecd-aa77899f247c.png)

X가 속성, y는 라벨

train은 학습용

test는 테스트용

<br/>

- **Model Generator (모델 학습)**

![image](https://user-images.githubusercontent.com/78403443/119621966-ac6e6600-be41-11eb-85ef-253474e64e58.png)

Evaluation 과정에서 확인한다. (score, accuracy_score 함수 써서)

<br/>

- **Score Evaluation**

  <br/>

accuracy_score() 함수

![image](https://user-images.githubusercontent.com/78403443/119622059-c445ea00-be41-11eb-9b02-c702c86e022e.png)

normalize=True :: DataSet에서 True로 정확히 예측한 데이터의 확률 (기본값)

![image](https://user-images.githubusercontent.com/78403443/119622090-cdcf5200-be41-11eb-8853-3b3ba329fc3c.png)

False를 주게 되면 예상치 못한 값이 나온다. 105

normalize=False :: DataSet에서 True로 정확히 예측한 데이터의 건수

<br/>

**여기까지 어제 배운 내용 정리한 코드...**

<br/>

---

- **06_ML_DT_cancer.ipynb 파일 보기**

<br/>

**Model 생성과 학습하기**

![image](https://user-images.githubusercontent.com/78403443/119622190-e7709980-be41-11eb-96a9-f9856c3a5f07.png)

random_state=42

seed값 주는거... 주는 값에 따라 랜덤하게 섞인다.

accuracy 줄 때 random_state 값을 꼭 줘야 정확도 측면에서 좋다.

음수 값만 주지 않으면 된다.

<br/>

stratify=cancer.target

지정한 데이터의 비율을 유지하는 옵션

stratify 매개변수의 값을 y로 전달하면

훈련세트, 테스트세트 데이터에 있는 라벨(클래스, y)의 비율이

원본 데이터셋 라벨 비율과 동일하게 유지된다.

<br/>

stratify를 주면 학습에 도움이 되는 경우가 많다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119622334-03743b00-be42-11eb-8f51-97b61330574e.png)

학습할 때 속성과 학습할 때 정답을 넣어줘야한다.

![image](https://user-images.githubusercontent.com/78403443/119622380-0d963980-be42-11eb-94c7-065c0335c889.png)

학습했다.

<br/>

**평가하기 - Training VS Test**

![image](https://user-images.githubusercontent.com/78403443/119622439-1be45580-be42-11eb-89ac-ae66d59499b4.png)

100% 나왔다. 

이 말은 일반성이 떨어진다는 말... 지나치게 의존하고 있다.

가지치기를 해줘야한다.

<br/>

가지치기를 한다는 얘기는 위 트레이닝 데이터셋과 테스트 데이터셋 사이의 격차를 줄여줘야 한다는 것이다.

<br/>

**가지치기**

![image](https://user-images.githubusercontent.com/78403443/119622501-2bfc3500-be42-11eb-9fd4-b44ec65187db.png)

옵션.. max_depth, max_features, max_leaf_nodes 가 있다. 

각 원리에 대해서는 전에 다뤘음

<br/>

가지치기 결과 잘 나왔다.

<br/>

이것이 pruning... 100에서 98로 내려갔고

test 데이터 셋은 93에서 95로 올라갔다.

<br/>

min_samples_split 옵션을 줘보자.

정교하게 작업할 때 쓰는 옵션이다.

![image](https://user-images.githubusercontent.com/78403443/119622592-3fa79b80-be42-11eb-8e26-6ab3d7b3c28e.png)

본인 스스로 경험에 의해서 적정한 값을 주어 정교하게 작업할 때 쓴다.

<br/>

**특성 중요도**

![image](https://user-images.githubusercontent.com/78403443/119622638-4d5d2100-be42-11eb-9ca6-b83cce3f3ca5.png)

![image](https://user-images.githubusercontent.com/78403443/119622667-53eb9880-be42-11eb-8ba6-0b8e39494026.png)

모두 더한 값이 1이다.

0~1 사이의 범위에서만 나옴

제일 높은 값 체크해줌

<br/>

**특성 중요도 시각화**

![image](https://user-images.githubusercontent.com/78403443/119622711-5f3ec400-be42-11eb-8996-9fbc52fe4f19.png)

Graphviz 사용

![image](https://user-images.githubusercontent.com/78403443/119622758-6960c280-be42-11eb-9afa-046703ed43b6.png)

![image](https://user-images.githubusercontent.com/78403443/119622790-71206700-be42-11eb-9628-ae44f4edc5ae.png)

<br/>

**정리**

위 특성 중요도 부분 주석 보기...

(+)

![image](https://user-images.githubusercontent.com/78403443/119622832-7f6e8300-be42-11eb-9cd8-295342d2fbc5.png)

데이터 분석 전처리 된 것을 머신러닝에 입력(학습)

머신러닝이 차지하는 비중은 20%

데이터분석이 차지하는 비중 75~80%

그러나, 데이터분석하는 사람과 머신러닝 작업을 하는 사람은 다른 사람인 경우가 많다.

전체적으로 보면 데이터 전처리가 잘못되었을 때 머신러닝에서 특성 중요도를 활용해

걸러내볼 수도 있다.(미루어 짐작 할 수도 있다.) 정도...

<br/>

---

다시 PDF로... (이곳에는 올리지 않음)

**Decision Tree 장점**

직관적, 단순하다. :: 학습이 빠르다

간단하다. 

(간단한 데이터로 해야된다는 말)

<br/>

**Decision Tree 단점**

데이터를 구분하는 기준을 직각으로만 할 수 밖에 없다. 

비선형(곡선)이 안된다. 

유동적으로 해석하지 못한다.

현재 데이터에 Training 의존성이 지나치게 높다.

일반성은 낮다.

데이터 일반화가 어렵다.

<br/>

Training Dataset에 너무 의존적이다.

이 말을 전문적으로 하는 말이...

Data Variance가 큰 모델이다! 라는 말...

<br/>

Variance가 뭐냐? 아웃라이어가 많다. 

아웃라이어가 많아서 그래프의 파형이 들쭉날쭉하다.

따라서 일반성이 높은 결과가 나오지 않는 것이다.

일반성이 높으려면 Variance를 낮게 만들어야 한다. 

그래프의 파형이 최대한 일정하게 나오게 해야한다.

<br/>

Variance를 낮추는게 최대 목표다. 

Overfitting을 낮춰야 하니깐!!!

Overfitting 낮추는 좋은 다른 방법이 Random Forest

<br/>

---

---

Ensemble(앙상블)과 Random Forest의 차이가 뭔가?

Random Forest가 앙상블이다.

(Random Forest is a Ensemble)

결론 == **랜덤포레스트는 앙상블의 한 종류**이다!

<br/>

앙상블에서 Bagging알고리즘을 쓴게 Random Forest고

Boosting 기법을 쓴게 Adaboost 등 이다.

---

**Ensemble(앙상블)**

앙상블에 두가지 알고리즘이 있다. 

- Bagging :: Random Forest
- Boosting

<br/>

**Bagging 알고리즘을 쓰는 Random Forest**

Bagging은 Bootstrap Aggregation(Aggregating)의 약어

Bag -- 가방을 생각하면 된다.

<br/>

여러개의 가방에 속성들을 랜덤하게 꺼낸다.

랜덤하게 꺼내기 때문에 속성이 중복된다.

<br/>

굉장히 중요한 속성이 있고, 상대적으로 중요하지 않은 속성들이 있을 것이다.

그런 상황에서 Random Forest를 어떻게 잘 활용할까?

1. 결정트리의(가방의) 갯수가 많아야 한다.

2. 엄청나게 결과를 잘 예측하진 않는다.

   ☞ 그러나, Overfitting을 꽤 많이 낮출 수 있다.

<br/>

**앙상블 알고리즘이란?**

<br/>

- Bagging 알고리즘으로 추출할 Feature의 개수는 사람이 정할 수 있는가?? 

  - 물론 기본 Default값은 있다. 그러나...

1. Bagging 알고리즘으로 추출할 Random Forest의 Feature의 개수는 사람이 정한다.
2. 몇 개의 Decision Tree를 생성할지도 사람이 결정한다. (기본값은 100개)

이런 것들을 하이퍼 파라미터 값이라고 한다.

일일히 넣어보면서 대조해봐야 적당한 감을 안다. 그래서 Art라고 불린다.

<br/>

**Bootstrap Sampling**

**( == Bootstrap Aggregation)**

**( == Bagging)**

**전부다 Random Forest를 말한다.**

**Random Forest is a Ensemble (꼭 기억하기! ★)**

<br/>

Decision Tree를 모두 합해서 평균 낸 값으로 예측값을 내면

Model의 Variance를 낮출 수 밖에 없다.

일반화 정도는 높이고 Overfitting 낮출 수 있다는 얘기

<br/>

**정리**

우리가 생각하는 것보다 결정 트리를 많이 만들어야함

<br/>

중요한 용어 :: Trade-Off 관계

어떤관계인가? 

하나가 올라가면 하나는 반드시 내려가야되는 관계

ex)

(일상생활) 회사 일이 많으면 아이들과 노는 시간은 줄어든다.

(인공지능) 정확성이 높아지면 에러율이 낮아진다.

<br/>

Random Forest에서 Overfitting은 내려갈 수 밖에 없다. 대신에 연산량은 올라간다.

연산량이 올라가면 학습속도가 내려간다.

<br/>

**Random Forest Parameter**

Overfitting을 막기 위해선 estimator의 개수를 늘릴 수록 좋다.

max_features 만약 30개를 모두 다 쓴다고 하면 랜덤 포레스트 트리들이 매우 비슷해진다. (Overfitting 가능성 높다)

값이 작으면 랜덤포레스트의 트리들이 서로 달라진다.(Overfitting 줄어든다)

작다고 무조건 좋은 것이 아니고, 적당한 값을 찾아서 써야된다는 말...

<br/>

Random Forest는 Classification(분류), Regression(회귀) 둘다 사용가능하다.

<br/>

**Bootstrap sampling**

max_features를 9개로 설정한 것이다.

왼쪽은 총 데이터가 9개

오른쪽은 총 데이터가 9개인데 계속적으로 부분추출하면서 뽑았기 때문에

최종적으로 데이터가 27개가 된다.

오른쪽을 가지고 학습시키면 Overfitting을 줄일 수 있다는 것도 있지만

데이터가 훨씬 많아진다.

머신입장에서는 중복된 것을 갖다 썼다는 것을 모르고 학습을 더 많이 진행 하게되기 때문에..

(적은 데이터일 때 풍부한 데이터 학습을 시킬 수 있다는 이점이 있다)

**정리 :: 매번 트리를 생성할 때 뭔가 새로운 데이터가 들어와서 학습을 더 많이 진행하게 되는 효과를 줄 수 있다! >> 증대**

심지어 약간 데이터를 변형시킬 수도 있다.

이미지로 예를 들었을 때 색을 바꾼다거나 약간 회전시킨다거나 하면

새로운 데이터로 더 학습시키는 것이다.

(데이터 량이 증대되는 것과 동시에 변형시켜서 한다... 다 한다.)

<br/>

왜 하는가?

데이터를 확보하는게 너무 힘들기 때문에 

내가 갖고 있는 데이터의 3배 4배 증폭시켜서 하기 때문에 이런 것들이 필요한것이다.

<br/>

**Bagging**

각각 다른 것을 다 합쳐서 공통적인 평균을 내려서 끌어올리는게 랜덤 포레스트의 방향성이다. 

이 말은... 우리가 원치않는 결과가 나올 수도 있다는 것!

<br/>

**Bagging의 문제점**

비슷하게 나올 바에야 Decision Tree하는게 낫다.

<br/>

비슷하게 나온다는건 Feature가 비슷하게 만들어진다는 것이다. 

어떤 때 비슷하게 만들어질까?

하나의 독립변수 하나의 성향(하나의 Feature의 영향)이 너무나 강할 때 그렇다.

<br/>

이런 문제가 간혹 발생할 수도 있다.

1. 강력한 변수가 있을 때 그 변수의 색깔이 너무 강해서 비슷한 결과가 나와버린다.
2. 연산량이 너무 많다. 그래서 학습 속도가 느리다 (Computation cost ↑)

<br/>

**Random Forest로 구현한 결과 캡쳐**

![image](https://user-images.githubusercontent.com/78403443/119623883-906bc400-be43-11eb-8843-8b64f87a9cc8.png)

훈련 세트 정확도가 100이라는 것은 좋아할 일이 아니다. (앞에서도 많이 얘기함)

높은 Overfitting의 가능성을 바로 생각해내야한다.

<br/>

**n_jobs 옵션**

랜덤포레스트를 쓸 때 n_jobs 옵션을 준다.

n_jobs를 2로 지정하면 cpu코어를 2개만 쓴다는 얘기다.

-1로 지정하면 컴퓨터의 모든 코어를 사용

만약 듀얼코어 컴퓨터라면 옵션값이 2나 -1이어도 똑같다.

n_jobs 옵션은 컴퓨터에서 사용할 코어의 개수를 지정하는 옵션이다.

(n_jobs도 역시 하이퍼 파라미터다)

<br/>

랜덤포레스트는 연산량이 많기 때문에 이러한 옵션이 있는 것...

<br/>

**Random Forest 주의할 점**

random_state값은 모두가 동일하게 가야한다.

<br/>

데이터 차원이 높다?

Feature(컬럼, 속성)의 갯수가 많다.

컬럼의 개수가 많으면 차원이 엄청나게 큰 데이터라는 것이다.

컬럼의 개수가 많아지면 비례해서 자동적으로 데이터(row)의 양도 그만큼 많아져야지만

그에 맞는 데이터가 되기 때문

<br/>

데이터의 차원이 높은데 희소한 데이터?

컬럼은 많으나 데이터(row)의 양은 적은 데이터

그런 데이터에는 Random Forest가 잘 작동하지 않는다.

어울리지도 않고, 무의미하다.

(무의미 하다는 얘기는 학습 자체가 안된다는 얘기)

이런 경우는 전처리로 대책을 세우던지, 선형으로 분리를 한다던지 하는

다른 방법론을 써야한다.

<br/>

랜덤포레스트로 모델을 만들어 볼 것이다.

<br/>

Evaluation 에

score() 함수

accuracy_score() 함수가 있다.

여기에 더해서 (+)

오차행렬(Confusion Metrix Accuracy) 연결해볼 것이다.

<br/>

---

**실습**

- **07_ML_RF_iris.ipynb 파일 보기 (메모에 없는건 파일 들어가서 보면 됨)**

<br/>

**먼저, 머신러닝 플로우를 정리하고 진행한다.**

머신러닝 단계는 크게

데이터 분석 ( 데이터 로더 --> Feature 추출 --> 데이터 전처리 ) --> 모델 생성

--> 모델 학습 --> 예측 --> 평가(Accuracy 측정)

이렇게 크게 프로세스가 나뉜다.

<br/>

이 중에서 성능평가 단계에서 정확도 측정 / 오차행렬(Confusion Matrix)을 주요하게 살펴보겠다

<br/>

**Baggning 기법**

앙상블 알고리즘 중 다양한 영역에서 높은 예측 결과 성능을 보이고 있는

RandomForest이다

RandomForest는 Bagging 알고리즘이 적용된 모델이다.

여러개의 결정트리가 전체 데이터셋에서 Bagging방식으로 각자의 데이터셋을 샘플링해 개별적으로 학습을

수행한 뒤에 최종적으로 투표방식을 통해서 가장 보편적인(다수결의 원칙) 예측 결정을 하게된다.

<br/>

사이킷런은 RandomForestClassifier 클래스를 통해서 랜덤포레스트 기반의 분류를 지원한다.

<br/>

**SKLearn IRIS DataSet Loader**

<br/>

**RandomForest Model 생성**

![image](https://user-images.githubusercontent.com/78403443/119624334-fe17f000-be43-11eb-9b52-d339f6fd7042.png)

<br/>

**Model Accuracy 측정하기**

⑴ 직접 일일히 확인하기

⑵ 사용자 함수 정의해서 확인하기

⑶ score(), accuracy_score() 라이브러리 함수 사용하기

![image](https://user-images.githubusercontent.com/78403443/119624416-17b93780-be44-11eb-97be-bef43be53cdc.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119624452-2273cc80-be44-11eb-9087-38bc89322337.png)

score() 함수는 predict()가 이미 내부적으로 진행

그래서 score안에 함수순서가 X_test, y_test로 가야한다.

반면에, accuracy_score는 predict()가 진행되지 않기 때문에 괄호안에 y_test, y_pred 순으로 들어가야한다.

모듈도 import 해줘야한다.

<br/>

결과 똑같이 출력되었다.

<br/>

**오차행렬 (Confusion Matrix)**

![image](https://user-images.githubusercontent.com/78403443/119624504-30295200-be44-11eb-9869-98c6749b5f87.png)

Confusion Matrix, 왜 이렇게 나왔을까...?

**설명**

![image](https://user-images.githubusercontent.com/78403443/119624532-391a2380-be44-11eb-99e3-813ca2800cbc.png)

위치는 중요하지 않다. 

각각의 데이터는 Accuracy다.

행 인덱스는 label(정답)을 뜻하고,

열 인덱스는 predict(예측값)을 뜻한다.

<br/>

위 그림으로 보면

정답이 2인데 0으로 잘못예측한게 하나 나왔다는 것을 알 수 있다.

정답이 1인데 2라고 잘못 예측한게 하나 나왔다는 것을 알 수 있다.

<br/>

정답이 2인데 2라고 맞춘게 두개 있다는 것을 알 수 있다.

정답이 0인데 0이라고 맞춘게 두개 있다는 것을 알 수 있다. 

위치에 상관없이 맞춘 개수를 알려준다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119624628-4df6b700-be44-11eb-88f2-4d1ac9160822.png)
