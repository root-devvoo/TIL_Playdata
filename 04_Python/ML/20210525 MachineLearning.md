그동안 배웠던 내용

![image](https://user-images.githubusercontent.com/78403443/119476061-ab2d3280-bd88-11eb-9356-0e40d4fb6506.png)

밑 주황색 부분 1, 2번은 데이터 분석때 이미 한 내용

3번은 머신러닝 내용

<br/>

데이터 전처리 전략 

① 누락데이터 채우기

② Encoding (문자를 숫자값으로 매핑)

③ Binning (구획화)

---

**오늘 진행할 내용은**

![image](https://user-images.githubusercontent.com/78403443/119476139-c009c600-bd88-11eb-9bb3-2c871ba89871.png)

SVM으로 왼편 1번 꼭지를 다 마무리할 것이다.

Kaggle 경진대회 데이터로 Competition... Rank도 얼마나 나왔는지 본다.

<br/>

그리고, 2번까지 쭉... 나가는것이 목표

<br/>

---

- **py_workspace / 03_MachineLearning / 03_ML_SVM_titanic.ipynb 파일 보기**

<br/>

- **데이터분석과 머신러닝 알고리즘으로 타이타닉 해상사고의 생존자를 예측하기**

![image](https://user-images.githubusercontent.com/78403443/119476302-e596cf80-bd88-11eb-8737-fbde9c62e33d.png)

Survival - 생존여부가 Label

C가 제일 비싼 동네, Q 중간, S가 제일 저렴

<br/>

![image](https://user-images.githubusercontent.com/78403443/119476373-f6474580-bd88-11eb-9e4f-f79bbf713f24.png)

TEST 데이터에는 왜 Survived(라벨)이 없을까?

검증데이터에는

1. Validation Data
2. Test Data
3. Inference Data

세가지가 있다. 

(우리는 셋 중에 세가지를 모두 혼용해서 쓴다.)

학습할때는 1번과 3번을 함께돌리고, 딱 한번 테스트한다.

1번은 학습하면서 학습데이터를 쪼개면서 쓰는 데이터

1번으로 모의고사 여러번 보고 실제 수능은 딱 한번본다.

2번은 실제 수능이므로... 라벨이 없다. 

3번은 상용화하기 직전에 돌린다. 

<br/>

### **Data Explore**

![image](https://user-images.githubusercontent.com/78403443/119476558-1ecf3f80-bd89-11eb-9cd3-df797c4c2990.png)

![image](https://user-images.githubusercontent.com/78403443/119476598-27c01100-bd89-11eb-9376-93d29f8075ca.png)

![image](https://user-images.githubusercontent.com/78403443/119476624-2ee71f00-bd89-11eb-8efa-efb3327b2065.png)

![image](https://user-images.githubusercontent.com/78403443/119476649-35759680-bd89-11eb-8227-bc848d2af36c.png)

Pclass가 생존여부에 영향을 미친다는 것을 위와 같이 알았다. 

1등석이 생존확률이 높고, 3등석이 사망확률이 높다는 것을 알았다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119476696-432b1c00-bd89-11eb-8cb9-134b725f7267.png)

빠른 시각화를 위해 bar_chart를 그려주는 함수를 만듬 (★ 중요!!!)

<br/>

**속성 - 좌석등급**

![image](https://user-images.githubusercontent.com/78403443/119477147-ad43c100-bd89-11eb-8ca6-14f36e228d7d.png)

![image](https://user-images.githubusercontent.com/78403443/119477179-b46acf00-bd89-11eb-9650-a93dbf2b5c21.png)

위 시각화결과에 따르면 생존과 사망에 운임료가 영향을 미치기보다는 다른 요인이 있을 것이라고 판단할 수 있다.

다시 자세히 알아보기 위해 다르게 시각화 해본다. 

<br/>

![image](https://user-images.githubusercontent.com/78403443/119477227-be8ccd80-bd89-11eb-9d7e-3e9a342008ab.png)

3등석이 사망률이 꽤 높다는 것을 알 수 있다. 

3등석이라는 요인이 사망에 꽤 영향을 미쳤다는 것을 알 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119477336-d49a8e00-bd89-11eb-88e3-d7ac7ba4e9ab.png)

시각화와 통계수치는 항상 같이 따라다녀야한다.

피벗테이블로 객실등급 수치 분석

<br/>

아래 이미지를 보자

![image](https://user-images.githubusercontent.com/78403443/119477369-dcf2c900-bd89-11eb-9d48-5b7f78af34b0.png)

3등석이 가장 먼저 침몰했다는 것을 알 수 있다. (분홍)

2등석 (노란색)

1등석 (하얀색)

1등석은 좌석이 적을줄 알았는데 생각보다 많다

<br/>

데이터 분석 발표할 때 위와 같은 이미지자료와 시각화자료, 피벗 테이블을 잘 활용하면

효과적으로 발표할 수 있다.

<br/>

**속성 - 운임요금**

![image](https://user-images.githubusercontent.com/78403443/119477441-ec721200-bd89-11eb-8b7f-c9c9697aa115.png)

운임요금은 Pclass랑 직결되므로 정교한 작업을 위해선 살펴봐야한다. 

결측값 채울때도 필요하기 때문에... 살펴봐야한다.

Feature(속성)들 사이의 연관성을 정의하는 것이 Data Explore에서 중요하다!

이러한 사고를 전개하는 것이 중요하다! (정교하게 순차적으로 집중적으로 분석해봐야 안다 == 경험의 축적)

<br/>

**데이터 시각화는 데이터 분석에 필수적이다. 한장의 사진이 천개의 단어보다 더 값어치가 있다!**

FacetGrid 다중plot을 그릴 때 많이 사용된다. 여러 변수를 한꺼번에 비교할 때 유용하다. 구획화를 지정할 때 유용

![image](https://user-images.githubusercontent.com/78403443/119477493-f7c53d80-bd89-11eb-8275-b6f1157beb28.png)

aspect를 4로 줘서 시각화를 길게 뽑은 이유는?

Binning(구획화) 때문에!

<br/>

**속성 - 성별**

![image](https://user-images.githubusercontent.com/78403443/119477621-13304880-bd8a-11eb-9080-4ce4751c6d9a.png)

![image](https://user-images.githubusercontent.com/78403443/119477661-1a575680-bd8a-11eb-90ae-4670a864bb69.png)

![image](https://user-images.githubusercontent.com/78403443/119477688-23482800-bd8a-11eb-8e02-c7ad6eba12ed.png)

![image](https://user-images.githubusercontent.com/78403443/119477712-2b07cc80-bd8a-11eb-97e3-9c1c0a2ce5e0.png)

<br/>

**속성 - 나이**

![image](https://user-images.githubusercontent.com/78403443/119477769-39ee7f00-bd8a-11eb-8130-9af5db733de5.png)

FacetGrid를 쓰는 컬럼들의 공통적 특징이 뭐냐?

바로 분류가 아닌 회귀...

![image](https://user-images.githubusercontent.com/78403443/119477811-4377e700-bd8a-11eb-8460-6375c22bd01c.png)

회귀 데이터에 대한 Binning기법을 적용하기 위해서 Facetgrid쓰는 것이다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/119477871-4ffc3f80-bd8a-11eb-97c0-f21d548ad094.png)

<br/>

**속성 - Title**

![image](https://user-images.githubusercontent.com/78403443/119477931-5d192e80-bd8a-11eb-9d58-249c78e04324.png)

![image](https://user-images.githubusercontent.com/78403443/119477965-630f0f80-bd8a-11eb-8098-a92cbbd2a673.png)

![image](https://user-images.githubusercontent.com/78403443/119478016-6a361d80-bd8a-11eb-846f-1cf6cc714652.png)

name을 나이 결측값 채우기 위해서 title이라는 컬럼으로 새로 가공한 것... 

컬럼을 새로 가공하는 것도 전략으로 쓸 수 있다. (필요한 부분)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119478079-77530c80-bd8a-11eb-82fd-cdd25dc0f1a9.png)

<br/>

**속성 - Family Size**

이것도 컬럼을 재가공함..

![image](https://user-images.githubusercontent.com/78403443/119478143-88038280-bd8a-11eb-905f-191bcee53cc9.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119478185-918cea80-bd8a-11eb-8f3e-a755a3cbb9b4.png)

![image](https://user-images.githubusercontent.com/78403443/119478213-9782cb80-bd8a-11eb-8af0-6c22f9d2d080.png)

동반가족이 없을수록 사망확률이 높았다.

<br/>

**속성 - 선착장**

![image](https://user-images.githubusercontent.com/78403443/119478270-a4072400-bd8a-11eb-90f1-0f9e67a64dc1.png)

![image](https://user-images.githubusercontent.com/78403443/119478297-a9646e80-bd8a-11eb-8162-0168a777540b.png)

<br/>

### **Pre Processing**

![image](https://user-images.githubusercontent.com/78403443/119478377-ba14e480-bd8a-11eb-95dd-0014fb500a7e.png)

![image](https://user-images.githubusercontent.com/78403443/119478514-d6188600-bd8a-11eb-98b9-b3a5c239061e.png)

![image](https://user-images.githubusercontent.com/78403443/119478568-de70c100-bd8a-11eb-89dd-98693c9d5b58.png)

랭킹을 올리기 위한 전략을 스스로 세워서 원래 있는 코드에서 바꿔서

Binning과 Encoding(숫자로 매핑)을 하기... (※ 파일로 보기...)

<br/>

### **Model Generator**

![image](https://user-images.githubusercontent.com/78403443/119478649-efb9cd80-bd8a-11eb-98f4-60deb980324c.png)

![image](https://user-images.githubusercontent.com/78403443/119478694-f8aa9f00-bd8a-11eb-9bb9-7cdb6700a536.png)

![image](https://user-images.githubusercontent.com/78403443/119478725-0102da00-bd8b-11eb-9297-8ec21efa4269.png)

class validation이다. (위 빨간색 사각형)

random_state는 seed값 같은거... 

나중에 다시 설명예정

<br/>

![image](https://user-images.githubusercontent.com/78403443/119478765-0cee9c00-bd8b-11eb-888b-1add19eda8dd.png)

<br/>

나머지는 직접 파일과 (개인)에버노트로 보기



---

---

**Decision Tree**

<br/>

**D:\encore_jwc\util\PDF\ML\03_DecisionTree&Ensemble.pdf 파일 보기**

**(PDF는 업로드 X, 저작권 문제)**

![image](https://user-images.githubusercontent.com/78403443/119479105-458e7580-bd8b-11eb-83e4-61febac64555.png)

위 순서대로 간다.

<br/>

맨 위에 있는 것이 Root Node

각 질문에 대한 마지막 노드를 Leaf Node라고 한다. 

(Terminal node라는 말 잘 안쓴다!)

<br/>

Decision Tree로 분리...

어떻게 분리?

지금 Decision Tree는 분리모델이 아니라 회귀모델로...

조건을 의사 결정 조건으로 달면된다.

<br/>

특정한 영역안에 하나의 카테고리만 있으면 된다. 

그래서 더이상 분기할 필요가 없는 Leaf Node가 되는 것이다.

<br/>

Decision Tree는 직선만... SVM과 다르게 곡선도 주지 못한다.

직선으로만 나눠야한다.

<br/>

graphviz...

기계나 사람이나 왜 딱 반으로 나눌까?

분포가 높은 순으로 선을 긋기 때문 

전문적인 말 :: 순도가 높은 순으로 선을 긋는다.

<br/>

Root Node에서 한 단계 내려간 부분을 Depth 1이라고 한다.

거기서 한 단계 더 내려가면 Depth 2가 된다.

<br/>

0이 나왔다는 것은 Leaf Node라는 뜻이다. 

2, 0 부분과 0, 32 부분은 순도가 100인 Leaf Node이다.

<br/>

Decision Tree는 곡선을 못그리기 때문에 직선으로만 모두 나누어 그리고... 

그렇기 때문에, 결국 Overfitting(과적합) 된다.

Depth와 Overfitting은 연관이 있다!

그래서 중간에서 잘라줘야한다. 

<br/>

이것을 가지치기(pruning)라고 한다.

<br/>

순도 100%짜리 Leaf Node가 있는 것을 Full Node라고 한다. 

중간에서 가지치기 할 수 없다.

따라서 Full Node를 만들어놓은 후 가지치기를 한다.

가지치기를 할 때,

일반성(추상성)을 높이는 기법으로 가지치기를 한다.

맨 오른쪽이 가지치기하여 일반성을 획득한 결과

<br/>

처음부터 못잘라낸다.

Full Node로 완벽한 Decision Tree를 만들어놓고나서 가지치기하고, 일반성 획득한 결과 도출

(가지치기는 무조건 해야된다)

<br/>

depth와 min_sample_split 에 대한 값은 경험과 감에 의해서 부여해줘야한다. 

(지침이 있긴 하지만) 인간이 경험치에 의해서 직접 설정해야 하는 값!

(이러한 값을 **하이퍼 파라미터** 라고 한다!)

어떻게 주냐에 따라서 결과가 확 바뀌기 때문에... 

이 값을 예술적으로 잘 줘야하기 때문에 Art라고도 한다.

<br/>

max_depth는 depth를 제한.. 즉 tree의 깊이를 제한한다.

min_sample_split은 한 노드가 갖는 데이터의 개수를 제한한다! 

<br/>

min_sample_split 설명

![image](https://user-images.githubusercontent.com/78403443/119479476-a4ec8580-bd8b-11eb-8224-cb3134233392.png)

아직 분류하지 않은 데이터 갯수가 100개 들어있다.

각각 분류...

이때 min_sample_split 옵션을 만약 3으로 줬다.

그러면 하나의 노드에 포함되는 데이터가 3이 될 때까지 분기가 된다.

<br/>

3 짜리는 거기서 멈춰야한다. 더이상 진행 x

<br/>

또 다른 설명..

![image](https://user-images.githubusercontent.com/78403443/119479555-b6359200-bd8b-11eb-98d8-5387b93caeb0.png)

min_sample_split 옵션이 만약 30이라면?

값이 크다면... 40, 30, 30이 Leaf Node가 되는것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119479595-c2215400-bd8b-11eb-9dfb-9238363df73e.png)

1, 2의 차이점 :: min_sample_split 값이 클수록 더 섬세한 분류가 된다.

값이 작을수록 세밀한 분류가 된다. 따라서, Overfitting 가능성이 높다!

이 성질을 이해해야한다.

<br/>

Decision Tree에서 선을 긋는 기준

그것이 바로 엔트로피(Entropy) 이론

<br/>

불순도... 서로 다른애들이 얼마나 섞여있는가 수치적으로 나타낸 척도

(혹은 지니 공식이라고 함)

순도가 올라갔다는 것은 불순도가 내려갔다는 뜻

<br/>

불순도를 구하는 공식이 엔트로피(Entropy)이다.

엔트로피가 1이면 불순도가 최대, (한 데이터에 다른게 반반 섞인 경우) 

불순도가 최저가 되는 때는 0에 가까워지는 때 

불순도가 0이 되면 순도가 최고!

<br/>

---

**코드로 실습**

- **py_workspace / 03_MachineLearning / 04_ML_DT_iris.ipynb 파일 보기**

<br/>

![image](https://user-images.githubusercontent.com/78403443/119479713-e3824000-bd8b-11eb-8c25-73e2f9900e6e.png)

sklearn의 datasets을 import해서

filename 경로에 들어있는 iris 데이터를 로드했다.

![image](https://user-images.githubusercontent.com/78403443/119479741-eb41e480-bd8b-11eb-9139-5a7d55370a15.png)

iris에는 속성과 target이 들어있다는 것을 알 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119479805-f7c63d00-bd8b-11eb-9215-a5b0b1cf1ce7.png)

iris.data는 target이 아니라 data만 출력한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119479850-057bc280-bd8c-11eb-905b-39d7f2b546e1.png)

![image](https://user-images.githubusercontent.com/78403443/119479872-0dd3fd80-bd8c-11eb-88bc-68ee870fa011.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119479911-175d6580-bd8c-11eb-883e-14530f50c324.png)

![image](https://user-images.githubusercontent.com/78403443/119479943-1debdd00-bd8c-11eb-8e90-f3139c29070b.png)

<br/>

**Data Split and Shuffle**

![image](https://user-images.githubusercontent.com/78403443/119479998-2a703580-bd8c-11eb-8fab-825bcc790b4d.png)

training_size는 없다... test_size만 옵션이 있다.

random_state는 seed값 주는 것

<br/>

X_train, X_test, y_train, y_test 속성에 순차적으로 들어간다.

y는 1차원이니까 튜플 형식으로 하나만 들어갔다.

<br/>

잘 섞여있는지 확인!

라벨이 섞여져 있는지만 확인하면 된다.

확인해보자.

![image](https://user-images.githubusercontent.com/78403443/119480055-3cea6f00-bd8c-11eb-86a2-2fb8d8b1c9f2.png)

잘 섞임

<br/>

**Model Generator and Training**

![image](https://user-images.githubusercontent.com/78403443/119480097-48d63100-bd8c-11eb-863c-06747d727430.png)

알아서 학습까지 진행

<br/>

**Predict (예측)**

![image](https://user-images.githubusercontent.com/78403443/119480148-5390c600-bd8c-11eb-8418-abc0e68e1d1d.png)

하나 틀림

한 96% 정도 되나...?

원시적인 방법으로 했다.

<br/>

accuracy_score(), score()함수로 정확도를 본다

![image](https://user-images.githubusercontent.com/78403443/119480191-5f7c8800-bd8c-11eb-8544-695e35b02134.png)

<br/>

**Accuracy Evaluation == 정확도 평가 - accuracy_score(), score()**

score() 함수 어떻게 동작하는가?

![image](https://user-images.githubusercontent.com/78403443/119480241-6d320d80-bd8c-11eb-950e-e41389cabfcf.png)

p hat이라고 함 p hat == 예측값

하나하나씩 일일히 비교해서 맞은 부분...

예측값과 실제정답을 각각 비교해서 일치하는 확률을 리턴

내부적으로 predict()를 수행

<br/>

코드로 보자.

![image](https://user-images.githubusercontent.com/78403443/119480291-79b66600-bd8c-11eb-9295-0f12706abed2.png)

3f로 소수점 3자리까지 출력

<br/>

train data 100% 나왔음. 좋은게 아님...

답을 외워서 100% Overfitting 되었다는 뜻이기 때문에...

그래서 가지치기(pruning) 해야된다.

<br/>

 accuracy_score() 함수

![image](https://user-images.githubusercontent.com/78403443/119480349-876beb80-bd8c-11eb-9e96-38833a286d55.png)

<br/>

**Overfitting을 낮추는 방법 ---- max_depth**

![image](https://user-images.githubusercontent.com/78403443/119480396-95ba0780-bd8c-11eb-90ad-5557682ff8eb.png)

가지치기 하는건 위 이미지에 빨간 박스가 전부..

<br/>

**decision tree 를 graphviz로 나타내기**

![image](https://user-images.githubusercontent.com/78403443/119480672-df0a5700-bd8c-11eb-80e1-61c8b8fe735f.png)

![image](https://user-images.githubusercontent.com/78403443/119480709-e7629200-bd8c-11eb-8f25-33f4977adbd1.png)

![image](https://user-images.githubusercontent.com/78403443/119480747-ef223680-bd8c-11eb-839b-70af34c57761.png)

gini(지니), 엔트로피(Entropy)는 불순도를 측정하는 수치

<br/>

1단계

![image](https://user-images.githubusercontent.com/78403443/119480804-fea17f80-bd8c-11eb-9879-c977ccd70970.png)

2단계

![image](https://user-images.githubusercontent.com/78403443/119480831-06f9ba80-bd8d-11eb-87ee-b686e748adba.png)

...

6단계까지 나왔다.

<br/>

이정도면 overfitting 심하다.

2로 가니

![image](https://user-images.githubusercontent.com/78403443/119481100-4c1dec80-bd8d-11eb-9032-fc3cdf06c16d.png)

![image](https://user-images.githubusercontent.com/78403443/119481123-53dd9100-bd8d-11eb-9b3f-491fd27dc093.png)

4단계로 나왔다.

gini 지수값이 점차 작아진다.

순도를 증가시키는 방향으로 전개가 되기 때문

<br/>

여기선 petal(꽃잎) 길이, 넓이 sepal(꽃받침) 길이, 넓이)

어디가 중요하냐? Root Node가 제일 중요하다.

제일 중요한 특성일수록 제일 위에 나온다. 

같은 레벨에서는 뭐가 중요한지 말하기 애매함.

이것이 특성 중요도이다.
