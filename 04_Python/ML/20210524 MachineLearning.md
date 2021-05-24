- **encore_jwc 폴더 / util / PDF / ML 폴더 01_Intro.pdf파일 참고**

**(pdf파일 캡쳐는 저작권 사유로 인한 업로드 금지로 업로드 하지 않음)**

<br/>

Machine Learning (기계 학습)

1. **ML? 개념**

2. **속성 (특징, Feature, X)**

   **정답 (label, Target, Y)**

   **모델**

   **성능평가**

   **1번 개념을 익히면... 이 용어들, 어떤 기능인지 이해하게 될 것이다.** 

3. **학습 방법**

   - **지도학습**

   - - ① SVM

     - ② Classifiztion

     - - Decision Tree
       - Ensemble(앙상블)
       - Boosting

     - ③ Linear

   - **비지도학습**

   - - ① Clustering 추천협업System - Python 구현

   - **강화학습**

   - 현업에선 지도학습 위주로 가고... 비지도 학습도 쓴다.

   - 따라서 지도학습과 비지도 학습을 할 것이다. 가장 기본적인 것 위주로

2. **데이터 분석 어떻게 머신러닝과 연결되는지**

3. **kaggle 데이터 경진대회 데이터 활용**

<br/>

**이러한 내용으로 4일 정도 진도를 나간다.**

모든 작업은 PDF를 바탕으로 이론을 먼저 숙지하고, 이론을 이해한 상태에서 코드를 다룬다

![image](https://user-images.githubusercontent.com/78403443/119317600-3dfb9d80-bcb3-11eb-94a5-86d30444e3f2.png)

<br/>

---

기계가 알아서 학습할 수는 없을까? 라는 고민을 Arthur Samuel이 함

<br/>

머신러닝에서 굉장히 중요한 요소!

E = 경험

T = 작업

P = 성능

<br/>

**머신러닝의 정의!** 

<br/>

T = 내가 하려는 Task

P = 퍼포먼스로서 Task에 맞는 학습인지 측정 70%, 99%, 20%

E = Task에 맞는 밀접한 Data가 주어져서 학습해야...

<br/>

**머신러닝 개요**

1. 개발자는 수학으로 인공지능을 접근하는게 아니라, 수학적으로 이런 원리로 돌아가는구나! 라고 이해해야함

<br/>

기계가 학습 할 데이터는 어마어마한 데이터가 필요한데, 

어마어마한 데이터가 옛날에는 없었기 때문에 한동안 주목받지 못한 것이다. 

오랜 시간에 걸쳐 어마어마한 양의 데이터 수집기술이 발달하면서 주목받기 시작한 것이다.

머신러닝은 사람의 개입 없이 모델이 스스로 학습하기 때문에!

(2010년도를 넘어가면서 부터~ Facebook 등이 나옴으로 인해...)

<br/>

input할 많은 양의 Data를 학습 데이터... 앞으로는 Training 데이터라고 한다!

어마어마한 양의 Training Data를 넣어주면 머신,모델이 알아서 학습한다.

학습이 잘되었는지 안되었는지 확인하려면 일종의 모의고사처럼 Test... 

이때는 Training이 아니라 Test Data를 넣는다. 

그리고 학습한 결과를 그대로 돌려서 결과값이 나온다.

<br/>

만약, 결과값이 D로 나왔고

정답이 B라면 퍼포먼스가 확 내려간다. 

퍼포먼스가 내려가면 다시 처음으로 돌아가서 학습하고 다시 테스트 돌아간다.

<br/>

머신이 학습을 하는데

그 학습방법 중에 지도학습과 비지도 학습이 있고 

어떤 학습으로 공부할 것인지 모델을 선택!

<br/>

<br/>

어떤 값이 들어가냐에 따라서 달라지는 것이 프로그래밍이다.

알고리즘을 짜는 것은 개발자... 명시적 프로그래밍

명료하게 알고리즘을 작성하고, 어떻게 결과가 나오는지 알 수 있다. (예상할 수 있는 결과가 나온다)

<br/>

반면에 머신러닝은

Training data를 스스로 학습해서 결과물 출력

<br/>

둘의 차이... 머신러닝에서는 어떤 알고리즘으로 돌아가는지 알 수가 없다.

Data만 잘 넣어준다. 명료한 알고리즘 작성 아니다! 결과값도 어떻게 나올지 알 수가 없음 (예상할 수 없는 결과가 나온다)

그런데 왜 쓰나?

명료하게 못짜는 경우는 인간이 앞을 예측하기 힘든 경우...

선호도(추천 시스템), 바둑, 자율주행 같은 경우... 

이들은 경우의 수가 굉장히 많다. 명료한 알고리즘으로 짜기에 한계가 있다. 

기계가 스스로 학습하게 해야한다.

그래서 머신러닝이 필요한 것이다!!!

<br/>

바둑하면 알파고... 

강화학습으로 만들어졌다. (바둑돌을 두는 행동까지 해야되기 때문에)

<br/>

<br/>

**AI/머신러닝/딥러닝**

<br/>

**AI**

AI는 크게 두가지가 있다. 

1. General AI

   - 로보캅, 터미네이터(인간의 능력치↑)

2. Narrow AI

   - "좁다"
   - 한 부분
   - 바둑, 스피치, 얼굴인식, 자율검색
   - 이런식으로 한 가지 부분에 있어서의 AI
   - 얼굴인식은 얼굴만 인식한다(자동차, 연필 같은 물체는 인식이 안됨)

**현재 현업에서 진행되는 영역, 우리가 배울 영역은 2번 Narrow AI 이다.**

**그러므로, 2번 Narrow AI에 대한 부분을 AI로 짚고 넘어간다!**

<br/>

딥러닝은 머신러닝의 Subset이다.

머신러닝으로 했을 때 Performance가 낮을 때 딥러닝을 이용하면

Performance를 올릴 수 있다. (다는 아니지만...)

<br/>

**머신러닝 학습분류**

- **지도학습 == SVM, Decision Tree, Random Forest, Boosting**
- **비지도학습**
- **강화학습**

**우리는 지도학습 중심으로 짚고 넘어간다.**

**Random Forest, Boosting 이 두개를 Ensemble(앙상블)이라고 한다**

<br/>

**Linear Regression (딥러닝)**

<br/>

<br/>

지도학습과 비지도학습의 차이점?

어떻게 다른가?

<br/>

지도학습은 데이터를 학습시킬 때 답을 알려주는 것

(데이터를 넣을 때 라벨을 넣는다.)

속성에 대한 라벨이 데이터로 주어진다.

<br/>

(데이터는 Feature 혹은 x라고 한다)

(답은 label 혹은 y라고 한다)

속성만 데이터로서 주어진다.

<br/>

비지도학습은 데이터를 학습시킬 때 답을 알려주지 않고...

(데이터를 넣을 때 라벨을 넣지 않는다)

비슷한 애들끼리 그룹화를 시킨다. (이것을 군집화라고 한다)

<br/>

지도학습은 속성에 대한 라벨이 데이터로 주어진다.

비지도학습은 속성만 데이터로서 주어진다.

<br/>

지도학습에서 분류와 회귀로 나뉘는데

분류는 영어로 Classification

고양이이다 강아지이다 분류..

<br/>

회귀는 영어로 Linear Regression

<br/>

비지도학습에서 클러스터링은 군집을 얘기하는 것이다.

<br/>

특정 값을 예측하는 것을 회귀라고 한다.

(시간 대비 몇점인지 점수를 예측하는 것은 회귀)

<br/>

hot이냐 cold냐 예측하는 것은 분류

(성공여부(성공vs실패)를 예측하는 것도 분류)

지도학습에선 반드시 라벨이 있다!

<br/>

군집은 라벨이 없기 때문에 (비슷한 성향끼리) 군집을 이루는 것이다.

이런 성향... 을 말하는 것이기 때문에 답이 없으므로... 라벨 x

<br/>

속성, 특징, Feature... X (대문자 X로 표시) -- 2차원 매트릭스이기 때문에

라벨, 정답, Target은... y(소문자 y로 표시) -- 1차원이기 때문에

<br/>

속성과 라벨을 이 둘을 데이터라고 하고

데이터에는 두 종류가 나뉜다. 

Training Data

Test Data(모의고사)

<br/>

실제 모델은 두가지 측면으로 이해해야한다. 

하나가 Training 모델이고 (학습모델이다)

Test 모델은 학습하지 않은 데이터, 미지의 데이터를 넣어서 결과를 예측!

<br/>

![image](https://user-images.githubusercontent.com/78403443/119319460-6e443b80-bcb5-11eb-9e99-bd83251953ba.png)

fit() 이라는 함수를 써서 학습을 진행시킬 것이다.

fit()이라는 함수를 실행시켜서 학습을 진행하려면 데이터가 있어야 한다. 

먼저 Training Data가 있다.(지도학습 경우) 

Training Data는 답이 정해져있다. (라벨이 있어야 한다는 얘기)

<br/>

데이터에 라벨을 붙이는 것을 라벨링 작업이라고 한다. 

라벨링 작업은 수작업으로 한다...

노가다지만 반드시 필요한 작업이다.

<br/>

이런 모델을 Training Model이라고 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119319515-84ea9280-bcb5-11eb-95d5-4e4c5a203c0c.png)

어느정도 학습이 끝났다면 미지의 데이터(Test Data)를 집어넣는다.

(미지의 데이터는 학습에서 사용하지 않은 데이터)

학습한 결과를 바탕으로 Test Data(미지의 데이터) 입력한 데이터의 결과를 예측

<br/>

Test Data의 예측 결과가 왜 A인가? 

일반성을 찾는 것이 중요하다.

<br/>

예를 들어서, 자동차가 사고나서 바퀴가 하나 빠졌다. 

그것은 자동차인가 오토바이인가? 자동차이다. 

일반성때문에 말할 수 있는 것이다.

<br/>

너무 학습한 데이터에만 의존하게 되면 일반성을 간과해버린다.

(일반성을 잃어버렸을 때) 이것을 Overfitting이라고 한다.

<br/>

머신러닝에서 80% 움직이는 것이... 

Overfitting을 막기 위한 몸부림

![image](https://user-images.githubusercontent.com/78403443/119319655-aea3b980-bcb5-11eb-969b-6d642d1db96d.png)

학습 == Training Model

미지의 데이터를 넣고 결과값 예측(모의고사) == Test Model

<br/>

Overfitting... 중요하므로 꼭 외우기! ★

<br/>

Training Model과 Test Model 사이에 정확도 격차가 크면

Overfitting 된 것이다. 학습을 한게 아니라 답을 외운 꼴이 되버리는 것임...

<br/>

Training때 나는 error 는 별로 중요하지 않다.

Test때 나는 error는 굉장히 중요하다. 잘 봐야한다.

<br/>

학습을 별로 못했기 때문에...

학습 초반부에는 똑같다. 

어느정도 학습이 진행되면 에러율이 낮아진다.

<br/>

트레이닝 에러는 학습할수록 점점 내려가지만

테스트 에러는 올라간다. 

<br/>

Overfitting 정리!!! 

Training error은 거의 없는데, Test error는 매우 높은 것을 Overfitting이라고 한다.

다른말 :: Training Data는 다 맞추는데, Test Data(미지의 데이터)는 잘 못 맞춘다. 

이 격차를 Overfitting이라고 한다. (외우기!)

Overfitting은 너무 Training Data에 의존할 때 발생한다!

<br/>

그럼 Underfitting은 뭘까?

공부 안한거다. 학습이 안된 것...

이때 Underfitting이 되면 어떤 정책을 써야할까? 공부를 더 시킨다. 

데이터를 계속해서 넣어주던지, 기존에 했던 학습을 더 시키던지...

<br/>

**가장 유명한 데이터 셋** 

<br/>

Linear로는 못한다. 회귀때 쓰는건데... MNIST는 분류니까...

MNIST는 데이터 특징이 단순하다. 

특징이 단순하면 학습하기도 더 쉽다. Fasion-MNIST는 더 복잡

<br/>

위가 학습이 쉬울까 아래가 학습이 쉬울까? 위... 

흑백이기 때문에, 흑백보다 컬러인 속성이 학습이 어렵다!

<br/>

MNIST는 정확도 99%

Cifar-10는 정확도 96% 논문으로 확인할 수 있다. (나중에 논문 본다)

<br/>

Cifar-10에서 10의 의미는 카테고리가 10개라는 의미이다. 

Cifar-100은 100개라는 의미

<br/>

속성, 축/칸 

그리고 그보다 더 중요한 카테고리 갯수 굉장히 중요하다!

속성, 축/칸, 카테고리 갯수가 조금이라도 달라지거나 갯수가 많으면 

정확도 높이는 일은 굉장히 어려운 일이 된다.

그래서 카테고리 갯수로 개발자와 사업설계자가 피터지게 싸운다.

<br/>

카테고리 갯수를 정하는 마지노선... 여러경험에 의해서 50이라는 마지노선이 나왔다.

카테고리 갯수가 정확도에 중요한 영향을 준다. 

정확도를 높이기 위해서 50이 마지노선이다!

<br/>

---

**ML 폴더 / 02_SVM_Classification.pdf파일 보기**

<br/>

**SVM - 지도학습 분류모델**

꺾은선은 선형이 아니다!

<br/>

Vector == 1차원

Matrix == 행과 열 2차원 구조

![image](https://user-images.githubusercontent.com/78403443/119320646-c4fe4500-bcb6-11eb-9a74-d689c10b2434.png)

가장 밖, 외곽에 있는 데이터... Vector 데이터들이 선을 이루고 있다

사이 빨간 화살표를 마진이라고 함. 

마진이란 두 데이터군이 결정경계와 떨어져있는 정도를 말한다. (위에 설명있음)

<br/>

결정경계를 중심으로 이진 분류를 할 수 있다!

<br/>

SVM을 쓰면 알아야 하는게 두개 있다. 

cost(비용)와 gamma...

<br/>

cost는

결정선을 어떻게 그어야 하는지 내가 지정할 때 사용하는 옵션

<br/>

cost가 낮으면 세심하게 결정선을 긋지 못한다.

<br/>

cost가 낮으면 outlier(자기건데 바깥에 있는 애들...)를 많이 허용

cost가 높으면 세심한 분류를 한다. outlier가 덜 나온다. 

그러나, 일반적인 경계는 잃어버림

<br/>

cost로 해결 안되는 경우가 있다

<br/>

어떻게 할까? 개인 에버노트 보기...

<br/>

cost는 outlier 경계선을 세심하게 하는 역할, 그러나 집단을 여러개로 구분하지는 않는다.

gamma는 집단을 여러개로 분리하는 것

cost든 gamma든 두 값을 지나치게 주면 알고리즘이 복잡해진다!

적당히 줘야한다. 

적당히는(?) 학습을 하면서 찾아내야한다. 어렵고 시간이 많이 걸리는거지만 해야한다!

<br/>

<br/>

**지도학습 - 특징들로 학습**

지도학습뿐만 아니라 모든 학습은 머신이 스스로 학습하게 되어있다.

이때, 지도학습은 콕 집어서 말하면 특징이다!

<br/>

1. 데이터 연관성이 있는지 없는지 밝혀야...
2. 제거 전략
3. 숫자로 Encoding 만들어줘야한다. (기계는 숫자밖에 인식못함)
4. binning(구간 만들어주기)

<br/>

필요한 속성만 뽑아내고 전처리 하는 것 == Feature Engineering == 머신러닝의 75, 80% 정도 차지

(하지만 노가다... 그렇지만 중요하다!)

15% 전처리

5% 후처리

Feature Engineering은 DB모델링에서 논리적 개념설계랑 비슷한 작업이다.

<br/>

---

---

지금까지 했던 모든 내용을 코드로 해본다!

<br/>

- **py_workspace 폴더 03_MachineLearning 폴더 01_ML_SVM_iris.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/119321205-58377a80-bcb7-11eb-9ad8-c99638a7480b.png)

![image](https://user-images.githubusercontent.com/78403443/119321222-5ec5f200-bcb7-11eb-8178-9543a5e07db0.png)

<br/>

간단하지만 붓꽃의 품종을 구분하는데 훌륭한 데이터다. 

task에 직결된 feature

![image](https://user-images.githubusercontent.com/78403443/119321276-6f766800-bcb7-11eb-9cb6-d963e84b62cb.png)

왜 이런 속성들이 나오는지 확인하라는 얘기

<br/>

![image](https://user-images.githubusercontent.com/78403443/119321330-7dc48400-bcb7-11eb-9e4d-19850b049dd0.png)

속성과 라벨을 분리시켜야한다. 

이런게 전처리...

<br/>

sklearn 데이터는 아래와 같이 데이터가 섞여 나오지 않는다

![image](https://user-images.githubusercontent.com/78403443/119321387-8c12a000-bcb7-11eb-9787-cdff4bd6a8c9.png)

정확한 학습을 시키려면 Shuffle... 섞어줘야한다.

그래야  Overfitting이 안된다. 

인간이 학습을 하는게 아니라 그냥 외워버리는 것과 같이 생각하면 된다. 

외우기는 의미가 없다

<br/>

![image](https://user-images.githubusercontent.com/78403443/119321428-9765cb80-bcb7-11eb-96cd-8b6681e2aa0d.png)

학습을 시키는 것이 fit() 함수

이때 data 줘야한다. 

데이터에는 Feature와 라벨 둘다 줘야한다!

feature가 먼저오고, 뒤에 data가 와야한다!

<br/>

모델을 만드는 것은 쉽다! 

전처리 과정은 굉장히 어렵다. 거기서 시간, 비용 많이 쏟는다...

![image](https://user-images.githubusercontent.com/78403443/119321481-a8164180-bcb7-11eb-9849-20927e3a1af3.png)

출력은 SVC() 만 나온다. 

일단 학습한 상태...

<br/>

**Predict**

학습 때 사용하지 않은 미지의 데이터를 입력해서 예측값을 출력해본다.

![image](https://user-images.githubusercontent.com/78403443/119321536-b6fcf400-bcb7-11eb-91ad-71b18ac0635d.png)

임의로 넣었더니 위와 같은 순서로 예측값을 출력해줬다.

(출력이 잘 안되면 print(pred)로 출력하면 된다!)

<br/>

이 데이터의 구조... (아래 그림)

![image](https://user-images.githubusercontent.com/78403443/119321584-c2e8b600-bcb7-11eb-8425-b20a2dddfdff.png)

이 데이터의 문제점

1. Shuffle이 안되어있다.

2. 150개 데이터를 Training Model로 다 썼다. 

   (이 말은 고3이 공부하고 모의고사 안치고, 바로 수능치러 간 격)

   Test Model에도 몇 개 줘야한다.

   그럼 어떻게 비율을 주고 가야하나?

   디폴트는 트레이닝 75%, 테스트 25%

<br/>

---

다시 pdf

<br/>

라벨값이 임의로 섞여있어야 학습을 제대로한다. 

섞여있지 않으면 그냥 달달 외우는 격...

<br/>

코드는 이런 흐름으로 갈 것이다. (아래)

![image](https://user-images.githubusercontent.com/78403443/119321881-10652300-bcb8-11eb-8355-7872e7918bfa.png)

위가 모든 인공지능(머신러닝) 작업의 기본적인 플로우이다. 

거의 안바뀐다!

<br/>

---

다시 실습!

- **02_ML_SVM_iris.ipynb 파일 보기**

<br/>

**꼭 추가로 더 import해야되는 모듈이 있다. (중요! 외우기)**

![image](https://user-images.githubusercontent.com/78403443/119322008-2f63b500-bcb8-11eb-99aa-97546cab58b8.png)

스플릿과 동시에 셔플해주는 함수

위와 같이 서브모듈 가져오고

![image](https://user-images.githubusercontent.com/78403443/119322048-3985b380-bcb8-11eb-944d-ac1168f99b6c.png)

위와 같이 써주면

아래와 같은 순서로 반환된다!!! (중요하다!!! ★)

<br/>

아래 사진과 같이 1,2,3,4 순서로 반환된다!

![image](https://user-images.githubusercontent.com/78403443/119322113-4b675680-bcb8-11eb-8572-fd8d90d79cb8.png)

<br/>

섞여져 있음을 확인했다! (아래)

![image](https://user-images.githubusercontent.com/78403443/119322174-5b7f3600-bcb8-11eb-94ed-98dfa761b983.png)

test_label도 섞였다 (아래)

![image](https://user-images.githubusercontent.com/78403443/119322233-69cd5200-bcb8-11eb-9551-6889a9dbabc8.png)

75대 25 비율로 나눠졌다.

<br/>

**이 부분은 파이썬에서만 가능 (아래)** 

![image](https://user-images.githubusercontent.com/78403443/119322304-78b40480-bcb8-11eb-9088-0b9caca7d450.png)

<br/>

이 순서 반드시 외워야 한다. 중요하다! ★ (아래)

![image](https://user-images.githubusercontent.com/78403443/119322413-92554c00-bcb8-11eb-88e9-959e81635be5.png)

train_test_split 함수 기능은 train과 Test를 위 순서대로 나눔과 동시에

Shuffle(섞기)한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119322497-a436ef00-bcb8-11eb-9b34-6db2e11f55d0.png)

fit에서는 train_data, train_label 넣는다. 아까랑 달라진다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119322560-b0bb4780-bcb8-11eb-9aac-824307d8678d.png)

테스트 돌려서 예측하였지만, 한눈에 정확도를 일일히 확인하기가 힘들다.

<br/>

정확도를 구하는 함수가 또 있다. 

예측한 값과 정답 사이의 정확도를 구해보자!

<br/>

![image](https://user-images.githubusercontent.com/78403443/119322626-c0d32700-bcb8-11eb-898b-01cf7d529556.png)

![image](https://user-images.githubusercontent.com/78403443/119322645-c7fa3500-bcb8-11eb-9356-465f0d88226c.png)

어떻게 정확도를 100%에 가깝게 하나? 그것이 바로 머신러닝 작업이다!

<br/>

학습, 예측, 성능... 모델을 생성해야한다.

<br/>

트레이닝과 테스트 모델을 분리시켰고, 셔플했던거 정확하게 정리하고 숙지하고 있어야한다!
