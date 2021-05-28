오늘 할 수업 내용

![image](https://user-images.githubusercontent.com/78403443/119943690-57138f80-bfce-11eb-8548-a6037366a207.png)

<br/>

1. 딥러닝 전반부의 핵심, Linear Regression

   지도학습 마지막 부분

<br/>

어떤 값이 들어올지 모르지만 어떤 값이 들어와도 값을 정확하게 예측할 수 있는 것..

Linear Regression의 핵심

<br/>

가설(선형) 예측

Accuracy -- 정확도

Loss, Cost -- 얼마나 에러율이 있냐 

(Trade off 관계)

<br/>

Gradient Descent (경사 하강법)

Python Code로 작성, 알고리즘 익힌다.

<br/>

비지도 학습 

2. Collaboraive Filtering System (추천 협업 시스템)

   직접 원리를 알기 위해서 Python 코드로 직접 작성하고 알고리즘 익힌다.

<br/>

---

---

**PDF 파일 보기...(저작권 문제로 올리지 않음)**

**Linear Regression**

<br/>

**Convex Fuction**

<br/>

**Gradient Descent (경사 하강법)**

<br/>

---

**코드로 구현, 실습**

<br/>

### 선형회귀(Linear Regression) - 심화

<br/>

- **10_ML_LinearRegression.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/119944203-efaa0f80-bfce-11eb-8a66-3c01a2e5afc7.png)

<br/>

**Linear Regression을 활용하여 섭씨온도(C, Celsius)를 화씨온도(F, Fahrenheit)로 변환해주는 공식을 만들수 있다.**

![image](https://user-images.githubusercontent.com/78403443/119944248-fd5f9500-bfce-11eb-9559-b5cabcc8ac36.png)

화씨온도 구하는 공식 :: 섭씨온도 * 1.8 + 32

<br/>

**Configuration (or prerequisite)**

![image](https://user-images.githubusercontent.com/78403443/119944287-094b5700-bfcf-11eb-98c3-06cc382466a7.png)

<br/>

**Generate Dataset**

![image](https://user-images.githubusercontent.com/78403443/119944324-16684600-bfcf-11eb-80be-80dfa29e0d2e.png)

섭씨온도 랜덤으로 뽑아냈다.

<br/>

**섭씨온도 데이터에 상응하는 화씨온도를 생성**

![image](https://user-images.githubusercontent.com/78403443/119944359-23853500-bfcf-11eb-81ac-74b48e7ea244.png)

<br/>

화씨가 y(Label, target)

섭씨는 X(Feature)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944404-31d35100-bfcf-11eb-930e-f4daeffabd15.png)

화씨도 구했다.

<br/>

**Visualization**

![image](https://user-images.githubusercontent.com/78403443/119944495-4d3e5c00-bfcf-11eb-94ea-eb247d277802.png)

<br/>

우리가 만들지 않은 잘 모르는 화씨, 섭씨온도 데이터라고 가정하고...

오차를 확인하고, 오차를 줄여보도록 한다.

<br/>

**Bias (편향 찾기) -- Weight는 1.8**

Weight는 1.8로 주고 Bias를 직관적으로 한번 찾아보겠다.

![image](https://user-images.githubusercontent.com/78403443/119944537-5d563b80-bfcf-11eb-9207-025ee49c9a06.png)

왜 uniform이라는 함수를 쓰는가?

uniform 함수는 정규분포에 기반한 랜덤한 값을 가져온다. 

이것을 안쓰면 학습이 안된다. 

실세계의 데이터에는 다양한 분포가 있다. 그걸 정규분포로 나타냄. 

그렇기 때문에 학습할 데이터에는 분포를 가지는 데이터인 정규분포가 있는 데이터가

들어가야 학습이 된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944584-6810d080-bfcf-11eb-8f18-b8c2fc5a5a2b.png)

![image](https://user-images.githubusercontent.com/78403443/119944610-6e9f4800-bfcf-11eb-9033-97e569a6a46d.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944648-7a8b0a00-bfcf-11eb-8c29-9c7ef3dd55ca.png)

보는 것 처럼 오차가 생겼다.

y_predict - y 만큼의 오차...

w(weight)와 b(bias) 중에서 b 생긴 오차이기 때문에

b - (y_predict - y ) 로 계산해주면 오차만큼 bias에 보정(수정)해줄 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944683-88408f80-bfcf-11eb-92d2-e17c35c3893a.png)

이 공식이 핵심이다. mean()은 꼭 붙여야한다.

<br/>

**위에서 보정한 bias값으로 예측값을 다시 만든다**

![image](https://user-images.githubusercontent.com/78403443/119944710-92fb2480-bfcf-11eb-8551-2006ab05f9a7.png)

<br/>

머신러닝의 학습법으로 제대로 사용해서 보정하고 시각화 해보겠다.

<br/>

**가중치(Weight, W), 편향(Bias, B) 찾기**

<br/>

**정규분포에 해당하는 w,b값을 랜덤하게 지정해서 초기화**

실제값과 예측치 결과값과의 차이를 시각화해서 확인

<br/>

아무리 랜덤한 값으로 학습을 한다고 하더라도 데이터의 특정한 분포가

없다면 학습이 이뤄지지 않는다.

앞에서와 마찬가지로 w, b에 해당하는 값을 랜덤하게 추출할 것이지만

여전히 uniform() 함수를 이용해서 값을 추출하도록 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944783-a8704e80-bfcf-11eb-86e9-f3cc1aea0075.png)

둘다 같은 범주로 만들어서 추출했다.

w를 안가르쳐주고(학습 시키지 않고) 랜덤하게 추출했으니까 격차가 많이 벌어질 것이 예상된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944816-b45c1080-bfcf-11eb-99b0-58032bd91ba2.png)

격차가 벌어졌다.

이 격차를 좁혀본다. 

좁히는데 Gradient Descent 알고리즘을 써서

학습을 여러번 돌려서 격차를 좁힌다.

(머신러닝 알고리즘 적용)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944861-c2119600-bfcf-11eb-8697-cdbe9df0e664.png)

**Gradient Descent**

![image](https://user-images.githubusercontent.com/78403443/119944915-cdfd5800-bfcf-11eb-8b11-5cba0da854c6.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119944949-d81f5680-bfcf-11eb-94d1-0df3b51107c0.png)

num_epoch로 학습을 몇번 반복할지 횟수를 지정한다. 

10만번으로 지정했다. (10만번은 많은 횟수가 아니다)

<br/>

learning_rate :: 학습이 진행됨에 따라서 보폭을 결정하는 하이퍼 파라미터

<br/>

for문을 통해 10만번 돌 것이다. 

for문 처음에 (랜덤한 값의) 예측한 가설을 세운다.

그리고 오차를 구해볼 것이다.

error 변수에 오차 구하는 공식을 저장했다. 양의 정수로 오차를 나타내기 위해 abs() 함수 썼다.

멈추는건 0에 가까워졌을 때 멈추면 되므로, 0에 가까워질때 학습을 멈추도록 설정한다.(if문)

if 조건이 만족될 때까지 w, b 값을 보정해 나가야 한다.

아까썼던 보정공식에 learning_rate를 곱해주는 것만 추가하면 된다.

(w 공식에는 X 도 추가로 곱해야함...) 

![image](https://user-images.githubusercontent.com/78403443/119944995-e66d7280-bfcf-11eb-89a4-26d41820ecf9.png)

오차보정하는 공식...

MSE() 함수(Mean Square Error) 대신 abs()함수와 mean()함수를 써서 했다.

<br/>

결과를 출력시키도록 한다.

![image](https://user-images.githubusercontent.com/78403443/119945092-fdac6000-bfcf-11eb-9305-a84ea800ae5d.png)

(1만번째 횟수마다 출력시키도록... epoch 5로 포매팅 설정함)

67272번까지 돌았다는 것을 알 수 있다.

<br/>

**Predict**

![image](https://user-images.githubusercontent.com/78403443/119945148-0bfa7c00-bfd0-11eb-9fba-84519bb8a698.png)

<br/>

**DataFrame and Plot Visulization**

데이터프레임으로 한번 만들어보려고 한다.

![image](https://user-images.githubusercontent.com/78403443/119945192-174da780-bfd0-11eb-8137-98a883eb23da.png)

괄호 안... 속성, 라벨, 예측값(가설 H(x)) 순

값은 강사님이랑 다르므로 신경쓰지말 것(위 이미지는 강사님 화면 캡쳐본)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119945237-259bc380-bfd0-11eb-8d16-2ec1327951bf.png)

시각화 해보니 가설과 일치되었다. 

이것이 Linear Regression !!!

<br/>

---

- **11_ML_LinearRegression.ipynb 파일 보기**

<br/>

**예측 함수**

![image](https://user-images.githubusercontent.com/78403443/119945321-3d734780-bfd0-11eb-9cbe-cbf3d45b1c11.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119945347-45cb8280-bfd0-11eb-87a6-1aa2b66d748f.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119945363-4f54ea80-bfd0-11eb-81c0-b767d6748e11.png)

![image](https://user-images.githubusercontent.com/78403443/119945379-554acb80-bfd0-11eb-8428-1c22820fceaf.png)

epoch이 5000이라는 얘기는 예를 들어 5만개의 Training 데이터가 있다면

5만개의 데이터를 1회 훓는게 1 epoch

5만개의 데이터를 5000번 훓는게 5000 epoch

5000번 훓고 여기에 Test는 1만개 데이터를 갖고 딱 1회만 한다.

(수능 1회만 하는 것과 같다)

그래서 우리는 이 Training을 학습할 때

별도의 모의고사 같은 비정식적인 시험을 따로본다.

이걸, Validation Test라고 한다.

이걸 안보면 1회만 보는 Test(수능)에서 절대 좋은 결과를 얻을 수 없다.

<br/>

상용화 되기 직전에 하는 Test를 Inference Test라고 한다.

<br/>

Inference Test는

1. 상용화 되기 직전이나
2. 경진대회 제출 전에 한다.

<br/>

우리가 말하는 test는 다 혼용해서 쓴다. 헷갈리면 안된다.

<br/>

5000번이나 학습을 하지만 테스트는 딱 한번 한다는 것... 알아두기

![image](https://user-images.githubusercontent.com/78403443/119945467-757a8a80-bfd0-11eb-8e45-5a547b6312a9.png)

다시 공식확인... (아래)

![image](https://user-images.githubusercontent.com/78403443/119945500-7f03f280-bfd0-11eb-8c9c-0f413934dd26.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119945524-89be8780-bfd0-11eb-9da9-186f949a838c.png)

출력결과(아래)

![image](https://user-images.githubusercontent.com/78403443/119945556-9216c280-bfd0-11eb-95d6-2a3218eec68a.png)

![image](https://user-images.githubusercontent.com/78403443/119945575-993dd080-bfd0-11eb-8598-3eef146f976b.png)

<br/>

---

---

**Collaborative Filtering (추천 협업 시스템)**

- **D:\encore_jwc\util\PDF\ML\06_CollaborativeFiltering.pdf 파일 보기**
- **(pdf 캡쳐파일은 저작권 문제로 업로드 하지 않았습니다)**

<br/>

**사용사례**

넷플릭스 (영화 추천)

유튜브에서도 이 알고리즘 사용

<br/>

굉장히 광범위한 알고리즘이다.

<br/>

선호도 조사

<br/>

세탁기를 사는 사람이 공통적으로 함께 사는게 있다.

빨래 전조대, 건조기, 세제, (이유는 모르겠지만) 공기 청정기, 세탁망

이렇게 구매하는 추세를 보이고 있다.

<br/>

어떤 사람이 건조기를 구매했다. 그러면 그 사람한테 세탁기, 공기청정기 이런거

추천할 수 있다. 이게 **상품 기반**이다.

<br/>

어떤 사람이 구매한 제품이 있고, 어떤 사람이 구매한 제품이 있다. 

둘이 구매한 물건이 비슷하다.

그러면 서로 다른 사용자가 산 다른 물건을 추천해준다. 

이것이 **사용자 기반**이다.

<br/>

처음에 좋아하는 영화를 미리 고르지 않으면 가입이 안되는 사이트가 있음 (왓챠나 스포티파이 같이...)

사용자 정보를 얻기 위함...

아마존 경우... 사용자 정보가 어마어마 할 것이다. (수천만...)

그러므로, 연산량이 어마어마 할 것이다.

<br/>

사용자 정보를 얻는게 힘들고 연산량이 어마어마하기 때문에, __기업 입장에서는 상품 기반이 쉽다.__

<br/>

정보는 크게 직접적인 명시적 정보(explicit ratings) 가 있고 추론에 기반한 암시적 정보(implicit ratings)가 있다.

Data확보가 그만큼 중요하다는 얘기

그만큼 데이터 확보가 어렵기도 하다는 얘기

<br/>

나머지 PDF 내용 봐서는 모른다... 

직접 코딩해봐야 안다.

그 말은 원리를 이해해야 한다는 말. 파이썬 함수 알아야...

<br/>

비슷한 애들끼리 묶어야 하기 때문에 유사도를 구할 수 있어야 한다.

대표적으로 코사인 유사도와 피어슨 상관계수 많이 쓴다.

우리는 대표적으로 코사인 유사도를 써서 문제를 해결해본다.

피어슨 상관계수는 나중에 팀 작업에서 별도로 유사도 구하는 작업해보기...

<br/>

책 평점..

코드로 구현해본다.

<br/>

---

**코드로 구현, 실습**

<br/>

### 협업 필터링 (Collaborative Filtering) 구현하기

<br/>

- **12_ML_CollaborativeFiltering.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/119946188-54ff0000-bfd1-11eb-98a1-6db197288853.png)

<br/>

**Data Loader**

![image](https://user-images.githubusercontent.com/78403443/119946233-5fb99500-bfd1-11eb-95a1-b315fd2a2f2e.png)

![image](https://user-images.githubusercontent.com/78403443/119946264-67793980-bfd1-11eb-8156-0db7fb5016da.png)

위 23행 3열짜리 데이터 프레임을 그림과 같이 바꾸려면 어떤 함수 써야할까?

Pivot Table 써야한다.

![image](https://user-images.githubusercontent.com/78403443/119946294-706a0b00-bfd1-11eb-868e-e54b04f4d7ee.png)

이렇게 해놔야 뭔가 진행이 된다.

<br/>

유사도를 측정할 때 굉장히 중요한게 있다.

결측데이터(0이 아니다)가 있는 컬럼은 벗겨내야한다.

NaN 값이 있는 컬럼은 다 지워야한다. 그것을 Mask 씌운다고 한다.

<br/>

인덱스가 뭐냐에 따라서 아이템 중심이냐, 사용자 중심이냐를 알 수 있다.

현재는 사용자 중심..

<br/>

다시 정리...

유사도를 계산할 때

평점이 0인 것과 NaN인 것은 상당히 큰 차이가 있다.

0은 유사성 값이 존재하는 반면에, NaN은 유사성 값이 존재하지 않는 것이기 때문에

NaN값에 해당하는 컬럼을 없애고나서 유사도를 계산해야 한다.

<br/>

결론은 NaN값을 가지고 있는 컬럼은

유사도를 계산하는 데이터로 판단될 수 없다. 제외시킨다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119946372-88418f00-bfd1-11eb-9555-6dc21e8e31fc.png)

u라는 사용자 v라는 사용자가 있다고 가정.

u 사용자는 두개 입력, 하나는 아예 입력안함

v 사용자는 모두 입력함

<br/>

이럴 때 mask는 np.isfinite

finite는 유한하다는 뜻, 반대 무한하다는 뜻은 infinite

<br/>

유사도라는 것은 나만 존재하는게 아니라 나와 다른 1명, 전체 2명 이상의 유사도...

따라서 NaN값이 있는 컬럼은 제끼고, 있는 것끼리 유사도를 찾야아함.

u와 v 둘의 유사도를 측정할 거기 때문에...

NaN 값이 들어있는 컬럼은 완전히 벗겨낸다.  (아래)

![image](https://user-images.githubusercontent.com/78403443/119946438-97284180-bfd1-11eb-96ba-7c42e7c30302.png)

벗겨내었다.

<br/>

**mask 씌우기**

평점이 입력되지 않은 컬럼은 유사도 계산에서 제껴버리자

<br/>

![image](https://user-images.githubusercontent.com/78403443/119947426-ae1b6380-bfd2-11eb-8230-d52ce4ac18ab.png)

![image](https://user-images.githubusercontent.com/78403443/119947479-becbd980-bfd2-11eb-8cd8-7045df12e657.png)

위와 같이 코사인 유사도 공식을 적용한다. 

![image](https://user-images.githubusercontent.com/78403443/119946519-ae672f00-bfd1-11eb-9d23-42b2f5532260.png)

유사도가 나왔다.

유사도는 0~1 사이로 나오고

1에 가까울수록 유사도가 높은 것이다.

<br/>

함수로 다시 정의했다.

![image](https://user-images.githubusercontent.com/78403443/119946615-c63eb300-bfd1-11eb-9f6d-56fd37fd7eb8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119946679-d9518300-bfd1-11eb-8921-ccc4c647cbd0.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119946711-e2425480-bfd1-11eb-97bd-3b86444df34b.png)

여기서 민수를 u로 민지를 v로 해서 NaN값이 있는 컬럼은 mask를 하고 유사도를 검증해보도록 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119946745-ed958000-bfd1-11eb-8844-e4727d8b3f8e.png)

민수와 민지의 가로행 정보를 갖고왔다.

<br/>

유사도 검증

![image](https://user-images.githubusercontent.com/78403443/119946781-f7b77e80-bfd1-11eb-82d8-56afe81c49a5.png)

유사도 93% 정도로 확인된다. 이 정도면 둘 사이에 유사하다고 볼 수 있다.

<br/>

조합...

![image](https://user-images.githubusercontent.com/78403443/119946834-043bd700-bfd2-11eb-83f7-e4d15d188257.png)

모든 사람들과의 유사도를 다 검색해야한다.

<br/>

**모든 사람의 유사도를 검색**

파이썬에서는 조합, 순열을 만들 때 사용하는 유용한 모듈이 있다.

Itertools 모듈을 이럴 때 사용한다.

지금의 경우는 조합을 알아보는 계산

민수-민지, 민수-민수, 민수-지민, 민수-지현....

<br/>

조합을 알아봐야하기 때문에 ratings.index

ratings.index에서 2명씩 묶겠다...

![image](https://user-images.githubusercontent.com/78403443/119946896-11f15c80-bfd2-11eb-8b17-e545ce40f0e2.png)

조합을 두명씩 만들었다.

<br/>

이 조합을 index_combinations라는 변수로 묶는다

![image](https://user-images.githubusercontent.com/78403443/119946933-1cabf180-bfd2-11eb-9c90-290ce85071a0.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/119946961-26355980-bfd2-11eb-978e-d320534826ef.png)

둘 간의 유사도를 돌리기 위해서 for문에 uname, vname에 넣는다

for문 돌려서 모든 조합이 u와 v에 넣을거고,

각각의 유사도를 score에 넣는다.

<br/>

list로 바로 넣으면 문제가 발생하기 때문에

JSON 형식으로 변경(가공)해서 넣는다.

그리고, append해서 넣어주고 데이터 프레임으로 출력

<br/>

맨 밑에 데이터프레임 출력되었으나

<br/>

유사도를 확실하게 파악하기위해서

구조를 좀 바꿔본다. pivot table형태로...

<br/>

출력결과(아래)

![image](https://user-images.githubusercontent.com/78403443/119947039-3fd6a100-bfd2-11eb-8e3f-69b76005ebc3.png)

결과가 나왔다.

대각선은 자신과의 유사도를 나타낸 것임

<br/>

위에서 한 것을 모든 사람의 유사도를 알아내는 함수로 다시 정의하였다.

![image](https://user-images.githubusercontent.com/78403443/119947075-4f55ea00-bfd2-11eb-82e8-379a731c3f7a.png)

![image](https://user-images.githubusercontent.com/78403443/119947098-567cf800-bfd2-11eb-8b23-984e419f5ac2.png)

<br/>

**잠깐 다시 pdf**

코사인은 벡터 방향으로...

<br/>

두개의 방향이 같으면 유사한 것으로 만들어져있다.

1에 가깝게 나오면 유사

0에 가까우면 독립성이 높다 (유사성이 없다) 보면 됨

<br/>

![image](https://user-images.githubusercontent.com/78403443/119947257-80361f00-bfd2-11eb-8e2b-09109a85a489.png)

코사인 유사도 위 이미지 참고하면 된다.

<br/>

**다시 코드로...**

<br/>

**평점 예측하기**

![image](https://user-images.githubusercontent.com/78403443/119947743-094d5600-bfd3-11eb-8d28-68acd4292e1c.png)

민지가 노인과바다 평점을 어떻게 줄지 예측해보자. 

어떻게 하냐? 민지와 유사한 케이스를 참고해서...

민지와 유사한게 현우...

현우가 노인과바다에 대해서 몇점을 줬는지 예측

만약에 현우가 3점을 줬다고 하면 민지는 3점보다 조금 낮거나 높거나한 값이 나올 것이다.

이런 예측 가능하다.

![image](https://user-images.githubusercontent.com/78403443/119947777-136f5480-bfd3-11eb-9c35-c210c042f2d1.png)

<br/>

모든 사람들의 유사도를 파악한 결과를 바탕으로

민지의 노인과바다 책에 관한 평점을 예측해보자

<br/>

민지와 유사도가 가장 높은 사람, 현우

현우의 노인과바다 평점이 가장 많이 적용될 것이다.

![image](https://user-images.githubusercontent.com/78403443/119947820-22560700-bfd3-11eb-8c5a-d674025c5af9.png)

민지를 제외한 다른 사람의 평점 정보를 받아와야하기 때문에 민지는 drop시킴, neighbors_ratings변수로 받아옴

민지를 제외한 나머지 사람들의 유사도도  받아서, neighbors_similarity변수로 받아옴

<br/>

그리고 나서, 

(민수평점 * 민수 유사도) + (지민평점, 지민 유사도) + (지연평점 * 지연 유사도) 해서 nominator 만들었다.

<br/>

민지가 노인과바다에 평점을 몇점 줄지 예측한 결과 나왔다. 

3.671361398092429

<br/>

이런식으로 다른 NaN값에 대해서 예측해볼 수 있다.

<br/>

위 과정을 함수로 정의해서 만들었다. (아래)

![image](https://user-images.githubusercontent.com/78403443/119947877-33067d00-bfd3-11eb-9e64-e949ef4d61bc.png)

![image](https://user-images.githubusercontent.com/78403443/119947902-38fc5e00-bfd3-11eb-9c8b-d37237283afa.png)

값이 잘 나오는 것을 확인했다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/119947946-47e31080-bfd3-11eb-9c8a-caa484228830.png)

민수는 흥부전에 대한 평점을 2.75정도 줄 것으로 예상했다.

<br/>

**모든 사용자와 상품에 대한 평점 검색**

특정 사용자가 넣은 평점 값이 아니라, 유사도 알고리즘을 활용해서 

우리가 함수를 통해 예측한 평점 값을 전부 넣은 데이터를 만들어보자

![image](https://user-images.githubusercontent.com/78403443/119947995-55989600-bfd3-11eb-8558-5796ceaebdc7.png)

사람과 책 조합 검색,출력

![image](https://user-images.githubusercontent.com/78403443/119948023-5fba9480-bfd3-11eb-86ed-f911d5ba7bd6.png)

아까 말한대로 특정 사용자가 직접 넣은 평점 값이 아니라, 유사도 알고리즘을 활용해서 

우리가 함수를 통해 예측한 평점 값을 전부 넣은 데이터를 만들어보았다.

<br/>

이런게 나오면 뭐가 가능한가?

<br/>

**Case 1. 지금 민지에게 가장 추천해주고 싶은 책은?**

![image](https://user-images.githubusercontent.com/78403443/119948075-6ea14700-bfd3-11eb-8a7a-3acfb3644268.png)

k는 추천하는 책의 갯수... (키워드매개변수로 변경가능)

![image](https://user-images.githubusercontent.com/78403443/119948106-782aaf00-bfd3-11eb-92a0-8ad5ce6b3406.png)

<br/>

**Case 2. 지금 백설공주 책에 가장 관심이 있을 것 같은 사용자는?**

![image](https://user-images.githubusercontent.com/78403443/119952043-8da1d800-bfd7-11eb-9804-cdaf048c8b9c.png)

<br/>

---

---

다음주 월요일 딥러닝 들어간다.
