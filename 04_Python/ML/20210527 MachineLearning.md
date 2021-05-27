**오늘 할 수업 내용**

Random Forest의 오차행렬 - Evaluation 이어서... ①

GradientBoostingMachine - ②

&

선형 회귀 모델

Linear Regression - (Deep Learning) - 경사하강법(Gradient Descent) - ③

![image](https://user-images.githubusercontent.com/78403443/119784697-70063d00-bf09-11eb-8888-8a588b39d5e7.png)

<br/>

---

---

**오늘 수업 내용**

<br/>

**Random Forest 예제, 예측결과**

Confusion Matrix (오차행렬)

![image](https://user-images.githubusercontent.com/78403443/119784877-9a57fa80-bf09-11eb-92ef-57a4370f877e.png)

Confusion Matrix의 Confusion은 사전적 의미로 혼란, 혼동이라는 뜻

Model이 True로 분류, 얼마나 혼동을 가지고 결과를 예측했는지 여부를 단적으로 보여준 것

<br/>

Accuracy(정확도)가 높게 나오면 Precision(정밀도), Recall(재현율)도 높게 나온다.

Precision과 Recall 둘 중에 좀 더 객관적으로 확인해볼 수 있는 것은 Recall이다.

<br/>

Precision(정밀도)는 모델이 True라고 분류한 것 중에서

실제로 True인 것의 비율을 알 수 있는 것이 정밀도이다.

<br/>

Recall(재현율)은 실제 True인 것 중에서

모델이 True라고 예측한 것의 비율이다.

<br/>

둘다 포커스는 True

False에는 관심이 없다.

바라보는 입장이 다르다.

<br/>

예를 들어, 날씨 예측하는 모델이라고 해보자.

실제 날씨(Label)가 있을 것이고, 모델이 예측(Predict)한게 있을 것이다.

<br/>

모델이 정확하게 맞춘 부분은 가운데... 

가운데를 C라고 해보자.

C는 실제로 맑은 날씨를 모델이 맑다고 잘 예측한 값이다.

<br/>

이때, Precision은 맞추는 관점이기 때문에 C는 C이지만, 모델 입장이다. 

Precision = C/C+B

<br/>

Recall은 실제 정답 관점에서 봤다.

Recall = C/C+A

모델 vs 실제 정답

<br/>

결론적으로 Accuracy가 높으면 기본적으로 모두 높게 나온다. 

하지만, Precision과 Recall의 차이를 얘기하는 것

왜 굳이?

<br/>

결론 :: 정확도는 Positive 관점에서 본거지만

Precision과 Recall은 모델과 실제정답 사이의 각각 다른 관점으로 본 것이다.

<br/>

---

**코드로 실습**

- **07_ML_RF_iris.ipynb 파일 보기**

<br/>

**정밀도, 재현율**

<br/>

지금 우리 정답률은 92%

Precision과 recall도 거의 같게 나올테지만, 미묘하게 다른 값의 차이가 있을 것이다.

![image](https://user-images.githubusercontent.com/78403443/119785061-d12e1080-bf09-11eb-9443-dd35bcdab156.png)

<br/>

정답과 예측값을 줘서 confusion_matrix로 나타내본다.

![image](https://user-images.githubusercontent.com/78403443/119785110-ddb26900-bf09-11eb-9256-6dbf6d969d98.png)

confusion_matrix는 정확하게 맞춘 것뿐만 아니라 모델이 실제 값을 뭐랑 혼동했는지도 나타낸다.

<br/>

labels 옵션을 주면 내가 원하는 label 옵션을 줄 수 있다.

임의적으로 바꿀 수 있다.

![image](https://user-images.githubusercontent.com/78403443/119785160-e99e2b00-bf09-11eb-83a1-b76a68586fa9.png)

아까랑 결과값이 다르지만, 원리는 똑같다.

<br/>

**실제 Iris 데이터에 적용해보자**

confusion_matrix 함수가 리턴하는 값은 2차원 배열이다.

![image](https://user-images.githubusercontent.com/78403443/119785224-f7ec4700-bf09-11eb-808e-2a66ad58d3d4.png)

바로 confusion_matrix()

괄호 안에 정답이 먼저 오고, 그 뒤에 예측값이 온다.

<br/>

데이터프레임 형식으로 바꿨다. (heatmap으로 출력하기 위해서) -- (아래 이미지)

![image](https://user-images.githubusercontent.com/78403443/119785272-05093600-bf0a-11eb-84ec-18aed8713680.png)

<br/>

**HeatMap Visualization**

![image](https://user-images.githubusercontent.com/78403443/119785314-0fc3cb00-bf0a-11eb-95ab-bb23ed15e7ca.png)

<br/>

---

**Bias vs Variance**

Variance는 앞에서 보았다.

모델의 Variance가 높다는 것은 Overfitting이 높다고 생각하면 된다.

<br/>

Bias는 뭐냐?

Bias는 편향이라는 뜻을 가지고 있다.

하지만, 여기선 편향이라는 의미가 아니다. 

Overfitting의 반대를 의미한다. <u>Underfitting</u>

Underfitting은 학습량이 적을 때 일어난다.

<br/>

Bias가 높다는 것은 High Bias

학습이 많이 진행되지 않았다는 것을 의미

<br/>

Variance가 높다는 것은 High Variance

High Variance는 Overfitting이 되었다는 뜻이다.

<br/>

머신러닝 모델의 에러는 두가지로 분류할 수 있다.

High Bias, High Variance

따라서 Bias와 Variance의 두 접점을 잘 잡아야 한다.

<br/>

Underfitting일 경우에는 training을 많이 시켜야한다.

Overfitting일 경우에는 추상성을 높여줘야 한다. 

(가지치기 등)

<br/>

**결론(마무리)**

Baggning(+Random Forest)는 Variance를 감소시켜준다. Overfitting을 줄여준다.

대신에 연산량이 많아지니, 학습시간이 길어진다. 

학습시간이 길어지니까... Bias에 문제가 생긴다.

<br/>

Boosting은 학습시간이 짧아진다.

따라서 Boosting은 Bagging(+Random Forest)의 한계인 Bias문제를 해결해준다. (Bias 감소시켜준다)

<br/>

어떻게 하면 학습시간이 짧아지나? 그것이 Key Point

<br/>

---

**Boosting**

- **AdaBoost, XGBoost, GradientBoost**

사용하기는 까다롭지만 지금까지 배운 것 중에서 성능이 가장 좋다.

코드라인을 길게 넣어야 해서 까다롭다는게 아니다.

하이퍼 파라미터 값 잘 조정해서 써야한다는 얘기

**Boosting is a Ensemble**

<br/>

single은 어떻게 학습되었을까?

데이터를 입력으로 해서 Iterator를 한번 돌고 결과가 나왔다.

<br/>

Bagging은?

왼쪽과 비슷한 방법으로 각각 다른 애들을 여러개 만들어서

(랜덤하게 뽑아서 여러개 만들었으니까 각각 다른 것) Iterator 돌림

다 쓴건 아니다.

<br/>

Boosting은 하나의 데이터에서 Iterator 돌린다. 

학습해보고 결과가 시원찮으면 결과를 도출하지 않고

다시 Back.. 돌아가는 것이다. (속성을 바꾸는건 예측 후에 바꾸는 것)

다시 돌아가서 속성에 대한 중요도를 바꿔서 Iterator를 또 돌린다. 아쉬우면 다시.. 

이런식으로 여러번 하는 것이다. (여러번 == 수천, 수만번) --이 과정을 반복

최종적으로 결과가 좋으면 도출한다. 

(속성에 대한 중요도를 바꾸는게 공부이다.)

<br/>

하나 가지고 조지기 때문에, 효율성이 극대화된다.

여기서 나오는게 GradientDecsent..(나중에 설명예정)

<br/>

오답노트와 같은 것이다. 

그래서 맞추기 어려운 문제를 맞추는데 boosting을 활용해서 좋은 결과가 나올 수 있다.

그렇기 때문에 데이터 경진대회에서 많이 쓰이는 것

<br/>

**Boosting Algorithm Implement**

코드 쳐서 실행만 하면된다. 

하지만.. 정확도 100은 좋은게 아니다. 

그럴땐 Pruning(가지치기) 쓰면 된다. 

<br/>

기존에 쓰던 하이퍼 파라미터 옵션도 쓰고, 새로운 하이퍼 파라미터도 써라

여기서 새로 나온 하이퍼 파라미터 중에 하나가 위에 예시든 learning_rate 옵션

learning_rate 옵션은 학습 속도를 조절하는 매개변수이다.

<br/>

이게 Accuracy를 도출하는데 막강한 영향을 끼치는 것이다.

<br/>

어떤 값을 주는게 좋은가... 논문자료에 범주가 다 있다.

(그건 딥러닝 할 때 다뤄볼 예정)

<br/>

학습속도 조절하는게 왜 중요하냐?

예를 들어 산을 내려온다고 했을 때, 경사가 완만한 곳에서는 보폭을 줄여서 내려와야 한다.

너무 빨리 내려오게 되면 지나쳐서 튕겨져 나가기 때문

<br/>

따라서, 학습을 거듭할수록 속도를 줄여야한다. 

학습을 거듭한다는건 학습속도가 점점 빨라진다는 얘기

경사가 완만한 목적지 근처에서는 지나쳐가지 않도록 보폭을 줄여서 천천히 내려가야 한다.

<br/>

**특성의 중요도**

Decision Tree, Random Forest, Boosting에도 각각 특성 중요도가 있다. 

하지만, 알고리즘을 뭐 쓰냐에 따라서 특성 중요도가 달라지지는 않는다.

따라서 다 거의 똑같다...

<br/>

---

**코드로 구현해보자**

- **08_ML_Boosting_cancer.ipynb 파일 보기**

<br/>

**GradientBoostingMachine**

**(GBM)**

![image](https://user-images.githubusercontent.com/78403443/119786439-261e5680-bf0b-11eb-80e8-19c07d4c25a3.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119786472-2fa7be80-bf0b-11eb-9668-1aafcd1a33f9.png)

하이퍼 파라미터값 안주고 정확도 측정...

100나왔기 때문에 가지치기(Pruning) 해야한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119786509-3a625380-bf0b-11eb-8ff9-adc3c6f797b9.png)

두 옵션을 어떻게 주냐에 따라 Accuracy 값이 확확 바뀐다. 

그래서 교차검증을 해서 좋은 값을 주어야 한다. 

그렇기 때문에 Art라는 말이 나오는 것... (많이 해봐야 안다)

<br/>

**특성 중요도 시각화하기**

![image](https://user-images.githubusercontent.com/78403443/119786560-477f4280-bf0b-11eb-8368-7358c5e30303.png)

<br/>

**정리**

![image](https://user-images.githubusercontent.com/78403443/119786603-536b0480-bf0b-11eb-8d42-ce8160188490.png)

아무리 안하더라도 하이퍼 파라미터 값 몇개 줘야하는 일이 생긴다. 

써야되는 대표적인 것들이다...

<br/>

하이퍼 파라미터가 3개 이상이 넘어가면 교차검증이 필요하다.

교차검증 했을 때 가장 최적의 값을 뽑아야한다.

<br/>

그렇게 했을 땐 값이 다르게 나온다.

<br/>

주로 인공지능 공부한 학생들은 Grid Search 알고리즘을 얘기한다.

교차검증해서 최고의 Best Parameter값(조합)이 나온다. 

이거 써야할까 말아야할까?

강사님은 써본적이 없다. 

왜 안썼는지... 

구글이나 이런데는 어떻게 하는지도 

코드로 해보고 얘기

<br/>

강사님이 안쓰는 이유 :: 코드로 구현, 실습 부분에도 나오지만

데이터가 많은 경우 시간이 꽤 오래걸리기 때문

<br/>

잘 쓰는 사람도 있긴하다.

<br/>

---

**코드로 구현, 실습**

- **08_ML_Boosting_cancer.ipynb 파일 이어서 보기**

**Grid Search**

Grid Search 알고리즘은 우리가 지정해준 몇가지 잠재적인 Parameter

후보군 조합 중에서 가장 Best 조합을 찾아내는 교차검증 알고리즘이다.

(격자판에서 교차검증 돌린다)

<br/>

우리가 직접 하나하나 값들을 대입해가면서 Loss가 가장 낮게 나오는

파라미터의 조합을 찾아야 하는데 이걸 대신해준다고 생각하면 된다.

<br/>

Sklearn 패키지에서 제공하는 라이브러리를 import만 하면 되기 때문에

상대적으로 손쉬운 방법이다.

<br/>

단점은 최적의 조합을 찾기까지 시간이 오래 걸린다는 점이 있다.

<br/>

데이터가 많으면 시간이 오래걸리기 때문에 데이터 많을 때는 적합치 않다.

<br/>

하이퍼 파라미터의 조합 3가지 옵션만 넣어본다.

옵션으로 줄 값들 갯수는 현재로선 상관없다. (같을 필요 없다는 뜻) 

(갯수 많으면 오래걸림...)

값을 정할 때도 범위는 스스로의 경험(감)에 의해서 줘야하는데.. 

(그 범위는 연구나 경험에 의해서 생기기에..) 경험이 적은 우리들한테 적합하지는 않다.

이것도 그래서 Art다.

![image](https://user-images.githubusercontent.com/78403443/119786839-8a411a80-bf0b-11eb-8de8-d0211fed2a58.png)

<br/>

verbose 옵션을 넣으면 detail한 설명이 나온다고 했지만... 안나왔다. (바뀐듯.. 파일에 있는건 걍 무시하면된다)

![image](https://user-images.githubusercontent.com/78403443/119786876-975e0980-bf0b-11eb-8832-d443d68a1cde.png)

grid_search.best_params_ 를 쓰면 찾아서 설정한 최적의 값 옵션이 나온다.

<br/>

(나는 강사님이랑 다르게 나왔다... 강사님은 n_estimators 값이 250으로... 난 200

컴퓨터 파워나 경우에 따라서 차이가 나는 경우도 있지만, 크게 신경쓸건 아니라고 한다.)

<br/>

**Best Parameter를 이용해서 GBM 생성**

![image](https://user-images.githubusercontent.com/78403443/119787034-be1c4000-bf0b-11eb-838e-d78fa9d24efa.png)

<br/>

**정리**

![image](https://user-images.githubusercontent.com/78403443/119787116-d55b2d80-bf0b-11eb-991c-125ea4062493.png)

GridSearch 사용하지 않는 이유

강사님이 안쓰는 이유 :: 데이터가 많은 경우 시간이 꽤 오래걸리기 때문

잘 쓰는 사람도 있다. 그래서 꼭 안좋다고 짚어서 말할 수는 없지만, 강사님의 경우는 안쓴다는 얘기

<br/>

하이퍼 파라미터 for문으로 돌린다는 생각도 하지만... 

그건 잘못된 생각, for문이랑 애초에 다른 것이고, 시간이 더 걸린다.

일일히 노가다 해야된다. 

알고리즘을 쓰고 싶어도 못쓴다. 그래서 수작업으로 함

시간의 한계때문에 못쓴다. 

하나를 고정해놓고 교차검증 하는게 Grid Search 쓰는것보다 더 빠르고 정확하며 시간이 덜 걸림

<br/>

AutoML: 인공지능이 알고리즘 정해놓고 Best 하이퍼 파라미터를 직접 찾아준다.

(사람이 하는 것보다 성능 떨어진다)

구글이나 페이스북 같은데서 쓸 것이다.

(최근에는 사람이 하는 것보다 성능이 올라갔다고 한다)

(앞으로는 이런 것들이 더 발전될거라는 얘기)

<br/>

그러나 최소 cpu 100개 이상은 써야한다.

가격은 어마어마 할 듯...

인공지능은 돈 없으면 못한다... (😭)

<br/>

어쨋든 결론은 불가피하게 결국 수작업으로 다 해야된다는 얘기

<br/>

---

지도학습 마지막...

**Linear Regression**

- **D:\encore_jwc\util\PDF\ML\04_LinearRegression.pdf 파일 보기**

(전부터 그렇지만 PDF 파일이나 캡쳐본은 저작권 문제로 올리지 않는다, 메모내용만 올림)

<br/>

고양이 vs 강아지

암 vs 암 X 

이런걸 Binary Classification (이진 분류)라고 한다

<br/>

A B C 

0 1 2 3 4 이런식으로 하는걸 Multi Label Classification 이라고 한다.

<br/>

**Linear Regression은 선형 회귀라고 하는데,**

**예측을 위해서 직선을 그리는 것이다.**

직선을 잘 그리게 되면 내가 선상에 있는 값을 잘 예측, 입력할 수 있기 때문에

이게 회귀...

<br/>

딥러닝의 Base는 Linear Regression이다!

Linear Regression은

1. Deep Learning 의 핵심

2. 미분, 적분, 편미분... 그러나 이런건 안함, 원리이해만 하면 된다.

   오히려 인문학적으로 접근해야함

<br/>

특정한 구간에 있는 선형의 값을 도출해내는게 선형 회귀 (Linear Regression)

Logistic Regression은 특정한 값으로 분류한 것. (Classification이랑 같다)

<br/>

Linear Regression에선 독립변수와 종속변수가 뭔지 알아야한다. 

**독립변수, 종속변수**

학생들의 기말고사 성적은 공부한 시간에 따라 다르다 라고 하면

공부한 시간은 X, 성적은 Y이다. 

공부한 시간인 X는 독립변수, 성적은 종속변수이다.

독립변수(X)가 변함에 따라 종속변수(Y) 값도 변한다.

<br/>

선형회귀는 독립변수 X를 이용해서 종속변수 Y를 예측하고 설명하는 작업을 말한다. 

그래서 독립변수와 종속변수가 중요!

<br/>

Cost Function은 얼마나 못했는가를 나타낸다.

선에 있는 값과 실제 데이터 사이의 거리를 다 비교

거리를 비교하려면 빼야한다. 

예측값에서 실제값 빼야한다.

거리는 마이너스가 나오면 안되니까 뺀 거에 제곱을 해야한다.

각각 예측값과 실제값을 뺀 거에 제곱을 해서 모든 값에 대해 나눠주면 직선이 데이터를 잘 표현하고 있는지 알 수 있다.

<br/>

loss가 올라가면 

1. 양의 값
2. 패널티를 강하게 적용 

틀릴수록 오차의 간격이 더 벌어지기 때문에 패널티가 강하게 적용되는 것이다.

이 결과를 보고 오차를 조정할 수 있는 것이다. (오차를 줄여나간다)

0과 최대한 가까이 줄인다.

<br/>

Cost Fuction :: 모든 값들의 예측 값에서 실제 값을 뺀 오차를 제곱으로 모두 더 한 것

<br/>

Cost에선 W(Weight)와 b(bias)에 대한 값이 중요하다.

Linear Regression은 Cost값이 0에 가장 가까운 값을 가지는 W와 b를 구하는 것이다. 

<br/>

---

**코드로 실습**

- **09_ML_LinearMSE.ipynb 파일 보기**

<br/>

**예측선 그리기**

![image](https://user-images.githubusercontent.com/78403443/119787799-8cf03f80-bf0c-11eb-8440-5982cd469248.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119787839-97123e00-bf0c-11eb-905f-84212eb7f879.png)

![image](https://user-images.githubusercontent.com/78403443/119787876-9ed1e280-bf0c-11eb-8356-211660b6e81b.png)

Linear Regression은 데이터를 가장 잘 표현하는 선형을 그려내는 것이다.

<br/>

일단 먼저 가설을 세운다.

가설은 (위에 파란 네모친) H(x)나 H(Wx)가 가설을 뜻한다.

<br/>

가설을 구할 때 최소제곱법이라는 공식으로 구한다.

이 직선을 그리기 위해서는 기울기와 절편을 어떻게 넣어야 하는지 나올 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119787957-b0b38580-bf0c-11eb-82c0-c1f139f785e0.png)

**최소제곱법**

![image](https://user-images.githubusercontent.com/78403443/119788008-ba3ced80-bf0c-11eb-9544-a29aab20e149.png)

기울기와 절편을 구했다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788068-c759dc80-bf0c-11eb-9787-fc50b725a7dc.png)

numpy array에 넣은 값을 가져와서 가설을 (predict변수에 넣은 것 처럼) 이렇게 넣는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788110-d2ad0800-bf0c-11eb-922a-645734512f84.png)

이제 오차의 범위를 줄이기 위해서 Cost Function 구해본다.

<br/>

**평균제곱 오차**

**Cost fuction을 구하는 가장 보편적인 방법**

![image](https://user-images.githubusercontent.com/78403443/119788166-df316080-bf0c-11eb-86e5-4674b6e464d8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788219-e8bac880-bf0c-11eb-8937-17d53053ca4a.png)

함수이름을 그대로 mse라고 정의한다.

나누는 것이기 때문에 mean() 함수 바로 쓴다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788271-f53f2100-bf0c-11eb-9920-3e572f6c4fad.png)

정답에서 8.29정도의 오차가 발생했다는 것을 알 수 있다. 

8이면 0에서 한참 떨어져있다. 

Gradient Descent 방법으로 오차를 줄여야한다. (이건 내일 다룬다)

<br/>

**MSE 실습하기**

![image](https://user-images.githubusercontent.com/78403443/119788346-04be6a00-bf0d-11eb-8865-89c21683e4f1.png)

공부시간, 성적 순으로 데이터를 2차원으로 입력했다.

<br/>

이번에는 임의로 기울기와 bias값을 지정해본다.

![image](https://user-images.githubusercontent.com/78403443/119788399-130c8600-bf0d-11eb-86ef-9933bae066b6.png)

임의로 주면 cost값이 굉장히 크게 나올 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788469-215aa200-bf0d-11eb-893d-c40cfc102304.png)

일차방정식 함수를 predict(x) 라고 만들었다.

평균제곱근(MSE)공식도 만들었고,

값을 입력해서 최종값을 구하는 함수도 만들었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119788536-2f102780-bf0d-11eb-8be4-9e53d5cd95de.png)

예측점수 나온 것을 바탕으로 오차를 구해본다.

<br/>

예측값 넣고 실제값 넣어서 cost function 이 나타내는 값 도출

![image](https://user-images.githubusercontent.com/78403443/119788600-3df6da00-bf0d-11eb-97c3-dfb1edd15e4d.png)

이렇게 오차가 나왔으면...

<br/>

**MSE 함수에 의해서 발생한 오차를 앞으로 어떻게 줄여갈 수 있을까?...미분/편미분 사용**

미분 / 편미분 사용

경사하강법(Gradient Descent)을 사용한다.

Gradient Descent는 미분임...

그러나, 실제로 편미분의 원리로 돌아간다.

<br/>

차원이 많아지면 편미분을 써야한다. (딥러닝의 경우 100차원도 감)

<br/>

---

**다시 PDF로...**

- **Gradient Descent**

- **Convex Fuction**

<br/>

밥그릇모양의 그래프가 Weight과 cost를 나타낸다

고도가 cost를 나타내게 되어있고

고도를 낮춘다는 건 cost가 최대한 0이나 0에 가깝게하겠다는 얘기

(오차를 줄이겠다는 얘기)

cost가 0이 된다는건 예측값이 높아진다는 걸 뜻함

0에 가까이 갈 수록 신중하게 내려와야한다.

내려온다는 얘기는 경사를 조절하면서 내려와야한다.

<br/>

이게 Accuracy를 높이는 방법

<br/>

이런식으로 학습하는 방법이 Gradient Descent 

오차를 어떻게 줄이는 지에 대해서 내일한다...

<br/>

<br/>

** **저작권 문제로 자세한 개인 노트는 에버노트에 노트하였음**
