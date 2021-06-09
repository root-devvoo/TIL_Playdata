(※ 오늘은 이론수업만 진행되었음)

(※ 저작권 사유로 pdf 캡쳐본은 업로드 하지 않음)

<br/>

**오늘과 앞으로의 딥러닝 수업 내용**

![image](https://user-images.githubusercontent.com/78403443/120157939-858fa580-c22e-11eb-88c6-8bd6272fb81d.png)

Deep Learning

1. Intro

   - AI / 우리는 어떻게 적용할 것인가

2. Linear Regression (딥러닝에선 Linear가 중요한 개념)

   - 행렬 연산 그 외 등등... (그림 참고)

3. 옵티마이제이션

   - cost / loss
   - Gradient Descent

4. 뉴럴 네트워크 학습법

   - FCN
   - ANN
   - DNN
   - CNN (Convolation의 약자 - 합성곱)
   - 이것들이 뭔지, 전문적으로 이해

<br/>

이론없이 코드 안만들어진다.

똑같이 이론 먼저하고 코드로.. 

CNN까지가 기초... 

CNN부터 조금 더 전문적으로 들어간다.

<br/>

5. Custom Data

   - MNIST
   - CIFAR10, 100 등
   - 데이터 수집할 때 Custom Data 중요하다. (직접 수집하고 만들어야)
   - 어떻게 수집하고 만들어야 하는지 배운다.

6. Segmentation

7. Object Detection

<br/>

요런 것들은 최종적으로 코드를 본다.

<br/>

코드로 할 때 우리가 쓰는 **딥러닝 프레임워크**

- Tensorflow(구글)

  - 다소 좀 복잡, 코드가 직관적이지 않다, 무겁다(연산에 있어서 다소 오래 걸리는 면이 있다)

- PyTorch(페이스북 개발)

  - 직관적, 가볍다 

- 전문가용으로 둘 중에 하나를 쓴다. 

- 우리는 PyTorch를 쓴다

- 구글 내부 개발자가 PyTorch를 쓸 정도로 PyTorch가 좋다.

- Keras라는 것도 있다.

  - 직관적.. 이것도 살짝 써 볼 것이다.

<br/>

**Code Level**

1단계 :: 인공지능 학부생 정도 레벨

2단계 :: 석사

3단계 :: 현업용 (Apple社), (Naver社)

<br/>

모든 내용은 논문... 논문출처는 PDF에 있으니 알아서 볼 것

<br/>

---

- **D:\encore_jwc\util\PDF\DL\1. Overview.pdf 파일 보기**

<br/>

**2010 - 2012년 3차 Boom**

이때 무슨일이 일어났는지 알아야한다.

<br/>

1940년대에 인공지능 첫 시작... 

그러나 프로그래밍과 다르게 주목과 발전이 더딤

사례 :: 영화 이미테이션 게임...

거기에 나온 기계... 암호 해독 컴퓨터, 연합군 승리

이 컴퓨터가 구한 사람이 숫자적으로 몇 백만명...

<br/>

2012년대에 3차 붐 일어났다.

이 때 왜 일어났을까?

2016년 3월에는 이세돌 9단을 이긴 알파고의 출현

<br/>

어마어마한 데이터셋을 분석하려면 컴퓨터의 성능파워가 좋아야한다.

알고리즘... (코딩테스트 그 알고리즘 아님), CNN을 말하는 것이다.

이 세가지 파워가 맞물려서 머신러닝과 딥러닝이 가능하다.

이 모든 것이 맞물려서 딥러닝이 가능하게 되었다.

<br/>

구글의 딥마인드 팀이 발명한 알파고...

알파고는 인공지능 바둑프로그램

바둑은 경우의 수를 예측하는데 굉장히 어려운 분야 중 하나

딥마인드는 원래 영국의 스타트업 기업...

2014년에 구글이 인수

2016년에 알파고 공개

이때 쓰였던 인공지능 기법이 강화학습

알고리즘으로 끝나는게 아니라 내가 구현한 알고리즘이 행동력까지 영향

![image](https://user-images.githubusercontent.com/78403443/120158613-4877e300-c22f-11eb-8898-85f3a5532c74.png)

(출처 : http://news.unist.ac.kr/kor/column_202/)

<br/>

Linear Regression 

Gradient Descent

어떤식으로 이미지를 분석해나가는지 CNN

학습방법들, Polling 연산 등...

기사 내용 쭉 보기...

이승철 교수팀에서 기고한 내용들을 우리가 일주일동안 다 다루게 된다.

그림도 눈에 잘 익혀두기

<br/>

**What Can we do?**

우리가 딥러닝 기술로 어떤 작업을 할 수 있는가?

**Classfication**

분류문제...

지도학습의 가장 대표적인 방법론

<br/>

알약을 구분할 수도 있음

<br/>

사람이 분류하는데 어려움이 있을 수 있기 때문에...

인공지능으로 정확도를 높일 수 있다.

N.N (neural network, 인간신경망)

<br/>

**Segmentation**

모든 픽셀을 카테고리로 분류

<br/>

Segmentation은 암 진단 등에 많이 활용된다.

<br/>

**Image Generation**

스타일 변형

이미지 변환 기술

**ex) Deepart.io 사이트**

![image](https://user-images.githubusercontent.com/78403443/120158857-88d76100-c22f-11eb-9137-18367a5edbc3.png)

사진을 업로드하고, 스타일을 고르면 그에 맞는 그림으로 변형

구매하도록 하는 사이트...

CSS, HTML5, Bootstrap 썼음

<br/>

**Natural Language Processing (NLP)**

인공지능 스피커 같은 경우... 챗봇이라고 생각하면 됨

인간언어 이해, 해석... 대화까지 가능하다

<br/>

위 그래프는 인간의 언어가 여러가지 있는데, 

언어별로 머신이 얼마나 잘 이해, 해석, 대화 하는지 나타낸 것

<br/>

아직까지 인간을 다 따라잡지 못했지만

거의 따라잡음...

<br/>

영어에서 불어, 불어에서 영어는 거의 인간의 수준을 따라왔다고 보면 된다.

<br/>

**Project Example**

인간이 운전하는 과정을 예로 든 것

(인간입장)

<br/>

자율주행의 눈도 Computer Vision에 속한다. 

(Computer Vision에 속하지 않는 것이 거의 없다)

<br/>

상황인식을 근거로 행동결정

결정된 것을 기반으로 행동을 실행

<br/>

여기서 딥러닝 학습에 해당되는 번호

2번, 3번 

특히, 3번 행동결정과 연관된 부분은 강화학습으로 한다.

4번 행동실행은 기계공학 부분

<br/>

머신관점에서 주행

<br/>

센서를 통해서 상황에 대한 인식

2, 3번 부분이 딥러닝 학습

행동은 기계학적인 측면이기 때문에,

컴퓨터 공학적인 기술은 2, 3번에서 쓰인다.

<br/>

자율주행의 경우에는 여러가지 학문 분야가 모여야한다.

<br/>

우리가 말한 것이

자연어처리를 제외하고는 Computer Vision과 직결

<br/>

2단계까지는 사실상 일부 기능만 들어간 비자율주행

<br/>

3, 4단계 차이 

3단계는 조건부 자율주행

고속도로 자율주행

4단계는 국도 자율주행

운전자가 탑승은 해야함, 핸들에 손은 올려져있어야한다.

<br/>

5단계는 운전자가 필요없음 (뒷 좌석에서 자도된다)

<br/>

지금 상용화는 3, 4단계까지 되어있고,

기술적으로는 5단계까지 나와있다.

<br/>

---

- **D:\encore_jwc\util\PDF\DL\2.Linear_Classification.pdf 파일 보기**

<br/>

**Computer Vision**

기계의 시각화

<br/>

강사님은 심리학에 관심이 크다.

<br/>

인공지능과 심리학 무슨 관련이 있나?

통계 데이터!

과학적으로 접근할 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120159450-3185c080-c230-11eb-9638-3a67d3f3735f.png)

(출처: 위키백과)

<br/>

Edge

모서리는 밝기의 변화율

(이거하면 생각나는 수학 공식? 미분)

전에 말했던 Object Detection 같은 것(?)도

Edge 알고리즘에서 나오게 된 것...

<br/>

그러나 모서리 정보만으로 사물을 분류하려니 한계가 있더라 

그래서 나온 알고리즘이 CNN(Convolution, 합성곱)

<br/>

인공지능의 본고장... 캐나다

토론토 대학교, 몬트리올 대학교

<br/>

딥러닝의 3대 대가

(스승) 제프리 힌튼 (토론토 대학)

(제자) 얀 르쿤 -- 이미지 처리

오슈아 벤지오 (몬트리올 대학) -- 언어학(자연어 처리)

<br/>

얀 르쿤이 CNN을 1998년도에 만들었고, 그 아키텍쳐가 위 그림

얀 르쿤이 만든 최초의 CNN 테스트 영상

http://aidev.co.kr/deeplearning/8840

<br/>

그러나 이때, 빛을 보지 못하고 2012년 3차 붐이 일어났을 때 다시 주목받음

그리고, 알파고가 2016년 3월에 나와서 모든 사람의 이목을 집중적으로 받음

<br/>

2011년에서 2012년 사이에 에러율이 10%나 낮아짐

10% 낮아졌다는건 엄청 대단한 일...

그리고, 해를 거듭할수록 CNN 알고리즘을 쓰면서 에러율을 혁신적으로 낮추기 시작함

그리고 대회폐지

<br/>

왜?

위 그래프를 보면 사람의 에러율이 5.1%인데, 3%대까지 에러율을 낮췄고

더 이상 의미가 없다고해서 폐지시킴

<br/>

MNIST

CIFAR10

CIFAR100

Fashion MNIST

등의 데이터셋을 가지고 대회를 진행하였음

폐지 후에는 일부 데이터셋 공개

<br/>

**Classification**

FCN

딥하면 DNN

하나가 ANN

Deep + Convolution → CNN

이러한걸 전부다 뉴럴 네트워크라고 한다.

연산을 여러개가 하냐, 하나가 하냐 등등에 따라서 다름

<br/>

Input Data 

이미지(속성, Feature)

라벨(Target)

<br/>

우리가 보는 고양이, (인간시각)왼쪽

컴퓨터가 보는 고양이, (Computer Vision)오른쪽

0에서 255 사이의 픽셀값으로 본다(컴퓨터는 숫자로만 인식하니까)

<br/>

x 3은 채널이 3이라는 뜻

3장.. RGB 조합

색깔을 나타내기 위해서 뒤에 오른쪽 사진과 같은게 세 판 더 있는 것

800 X 600은 사이즈 

정리 :: 800 x 600 x 3 (Width x Height x 색상)

<br/>

고양이 사진 하나에 들어가는 숫자는 총 몇개일까?

800 곱하기 600 곱하기 3하면 알 수 있다. 

답 : 약 1,440,000개

거기에 W(weight) + Bias... 

어마어마한 연산이 들어가는 것이다.

<br/>

고양이 사진 명암에 따른 변형...

분류하는데 난이도가 꽤 있다.

<br/>

Deformation

<br/>

고양이가 자주 취하는 포즈

데이터를 변형하기 위해 이런 것도 꼭 학습 시켜야된다.

<br/>

Occlusion

<br/>

인공지능은 이렇게 숨어있거나 매몰되있는 데이터도 예측해서 다 맞춘다... 

아까 위에서 봤듯이 인간의 오류율 5%보다 인공지능 3%로 낮다는 것은

다 맞춘다는 얘기인 것이다.

<br/>

Intraclass Variation

<br/>

군집이 모여있는 경우도 다 구별해서 테스트할 수 있어야한다.

<br/>

옛날에는 Edge Ditection 알고리즘을 써서

모서리를 본따서 구별하였지만, 한계점이 많기 때문에

딥러닝의 Data-Driven 기반 접근...

<br/>

모델은 크게 트레이닝 모델과 테스트 모델로 나뉜다.

<br/>

이런 이미지로 학습할 때 크기와 컬러 중요하다.

<br/>

**Nearest Neighbor**

<br/>

지양해야할 것도 있고, 지향해야할 것도 있다. 

<br/>

step 1.

Classification을 가장 심플하게 할 수 있는 방법

5만개 데이터를 모델에 저장했다고 가정하자

모든 속성들과 라벨을 저장(암기)했다... Training

<br/>

step 2. 미지의 데이터를 넣는다... 테스트 모델

미지의 데이터랑 5만번을 일일히 검사 및 대조해서 유사도를 다 계산

다 더해서 특정 라벨데이터 중에 유사도가 제일 높은 것을 라벨로 출력함

<br/>

문제점 :: 비효율적이다.

<br/>

L2 loss로 많이 쓴다.

<br/>

유사도를 정말 정확하게 예측했다고 하면 L2 loss 결과는 0이 나온다.

숫자가 작을수록 예측을 정확히했다는 얘기.

빼서 제곱한 것을 다 더한 다음에 루트를 씌움

<br/>

비효율적이라는 것을 떠나서 가장 치명적인 문제는

원본이미지와 서로 같은 이미지임에도 불구하고, 유사도 측정에서 픽셀값이 밀리거나

색상이 다크해지거나 하면 완전히 다른 이미지로 본다. (Loss가 굉장히 크게 나온다 (↑))

<br/>

**Cross Validation**

<br/>

하이퍼 파라미터 정의가 뭔가?

학습에 의해서라기보다는 우리가 지정, 산정해줘야하는 옵션이다

(학습에 의해서 알아지는 값이 아니다)

휴리스틱 value다. == 인간의 경험적인 값으로 매겨진다.

<br/>

K가 1이라는 얘기는 전체를 학습하는 데이터로 썼다는 말이다. 

그래서 BAD

<br/>

**Cross Validation에 대한 설명**

![image](https://user-images.githubusercontent.com/78403443/120160613-634b5700-c231-11eb-9df1-966facddcbd0.png)

1번은 가장 이상적인 Data Set의 모습 → 총 5억개의 Data Set이 있다고 가정하자.

5억개의 데이터 중 10%는 Training 데이터로, 10%는 Validation 데이터로

나머지 80%를 Test 데이터로 쓴다. 

데이터 셋이 1번처럼 충분하다면 위의 비율이 가장 이상적인 학습도 충분히 하고, Test도 실컷한다.

그러나, 현실적으로 불가능하다. 이렇게 학습데이터 구축 불가능...

<br/>

2번, 현실적인 데이터셋 구성

(현실적으로 생각해봤을 때...)

Train 데이터셋이 500 Validation 100개, Test 100개

이런 경우가 오히려 흔히 있는 경우...

이런 경우 Data Set이 너무나 부족한 경우

이정도 데이터 셋이라면 딥러닝 사용하면 안된다. 

이럴때는, Train 할 때 500개... 너무 작다. 

너무 트레이닝 할 데이터 수가 너무작은데

Validation 데이터로 100개까지 내주는 것은 무리수이다. 너무 힘들다.

<br/>

결론 :: 학습용 데이터는 턱없이 부족하고, Validation Test는 해야되겠고

이럴 때 사용하는 방법이 Cross Validation

<br/>

결론적으로 Cross Validation은 데이터는 부족하고 Validation Test는 해야될 때

사용한다!

<br/>

이럴 때 Cross Validation을 어떻게 하느냐?

![image](https://user-images.githubusercontent.com/78403443/120160674-79f1ae00-c231-11eb-9959-aa872cd7d5a2.png)

3번째, Cross Validation

전체 데이터 500이라고 가정했을 때 500전체를 5등분해서 보자

각각 100개씩 5개

(첫번째 학습할 때)마지막을 Validation으로 == 1 Epoch

이번엔 4번째에... == 2 Epoch

...

이런식으로

학습데이터를 바꿔 돌아가면서 테스트한다.

<br/>

전체를 트레이닝 데이터로 쓰는데, 

학습이 거듭될 때마다 Validation을 서로 cross해서 돌려서 쓴다는 얘기

<br/>

결론 :: 학습 데이터셋이 부족하기 때문에 별도의 Validation DataSet을 두지 않고,

학습데이터를 Epoch를 거듭할수록 서로 바꿔가면서 Validation Test를 한다. (이게 핵심!)

이렇게 하면, 어느 한쪽으로 치우친 결과가 나오지 않을 뿐더러 학습 데이터를 잘라서 쓸 일도 없다.

<br/>

k-fold라는 하이퍼 파라미터 옵션...값

트레이닝 데이터 셋을 몇개로 했냐? 

위의 경우는 5라고 설정되있는 경우

k=5 == Training DataSet이 5

그럼 Test는 언제할까?

Test는 모든 학습이 다 끝난다음에 딱 한번만 한다.

그래서 Validation이 중요한 것이다.

![image](https://user-images.githubusercontent.com/78403443/120160778-97267c80-c231-11eb-81da-68875d1adfaa.png)

그래서 Training DataSet에 Validation이 같이 들어간다.

그러고 나서 테스트는 딱 한번한다. 이때 정답이 있다. 

그리고 InferenceTest가 또 있다. 이건 정답이 없다.

이 4가지가 구분이 되어서 이해가 되어져야 한다.

<br/>

k-fold 옵션은 5~7 사이를 주라는 얘기... 

7이상 주니 결과가 좋지 않았기 때문

<br/>

데이터 로드하고나서 

Feature Engineering, Pre processing(이 과정에서 핵심은 Data Argumentation(데이터 변형!)) 해야한다.

여기까지가 데이터 전처리!

그러고 나서 Neural Network 통해서 학습, 테스트(테스트는 단 한번)

마지막으로 상용화 하기 전에 Inference한다.

<br/>

**Linear Classification**

<br/>

실질적으로 딥러닝은 하나하나 Linear 된게 쌓여진 것

블럭 하나가 Linear 하나

블럭이 여러개 쌓여져 있는 것을 Deep 하다고 한다. 그래서 DNN

블럭이 하나면 ANN

블럭은 Linear를 뜻한다

<br/>

CIFAR10의 총 데이터 갯수는 6만개이다.

이런 경우 정확도가 얼마나 나왔는지 보자

![image](https://user-images.githubusercontent.com/78403443/120160976-d3f27380-c231-11eb-84f6-bfb65c3fc154.png)

이 사이트 꼭 알아야한다.

(오픈된 DataSet에 대한 Accuracy(정확도) 정보 제공해주는 사이트)

![image](https://user-images.githubusercontent.com/78403443/120161211-0603d580-c232-11eb-91fe-58da66b73233.png)

CIFAR10 정확도

동그라미 친 것은 최신 논문들에서 결과 발표한 것

강사님은 모델명 훓으신다. 새로운 모델들 눈에 익히는 것

<br/>

MNIST정확도는 더 높다.

MNIST 데이터는 이미지가 흑백 (얀 르쿤이 했던 흑백 손글씨 학습데이터)

MNIST와 같이 속성이 단순하면 단순할수록 정확도는 높아진다.

<br/>

반면에 CIFAR100은 EffNet-L2 모델 썼을 때 정확도 96.08%

<br/>

위와 같은 홈페이지 보는 것... 그냥 감을 익히는게 아니라 

실질적인 최신 논문에 실려져있는 모델들을 확인해봐야한다.

<br/>

**행렬연산**

![image](https://user-images.githubusercontent.com/78403443/120161445-46fbea00-c232-11eb-9199-8ac91b15c16f.png)

둘다 2행 2열...

행렬연산은 노란색 화살표와 같이 그리고

초록색 화살표와 같이 곱해진다.

a(*)e+bg af+bh

ce + dg cf+dh

둘다 2행 2열이라고 가정

앞의 2열과 뒤의 2행이 일치해야

출력 행렬은 앞의 행 2, 오른쪽 열 2이므로

출력 행렬에는 2x2가 나와야한다.

<br/>

2행 2열, 3행 2열같은 경우에는

연산이 안된다. 둘이 다르니까... 

(앞의 2열 뒤의 3행으로 숫자가 다르니깐..)

출력이 안된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120161488-567b3300-c232-11eb-8bd4-7544a838e345.png)

2행 1열, 1열 2행은 연산이 되고

출력은 2행 2열로 나온다.

결과는 위와 같이...

<br/>

중요...

![image](https://user-images.githubusercontent.com/78403443/120161532-61ce5e80-c232-11eb-9dd9-4241c4bbd504.png)

일단 연산이 가능한지 부터.. 

3x4, 4x1 이므로 연산이 가능하다

최종 연산 결과는 3x1이다.

<br/>

독립변수에 따라서 종속변수(답) 나온다

<br/>

고양이 이미지의 모든 픽셀값이 Feature(속성)이 된다.

4x1짜리가 X가 된다.

왼쪽 3x4가 W(Weight 중요도)가 된다.

맨 오른쪽 3x1이 b가 된다.

<br/>

첫번째는

(2x2)+(3x2)+(1x3)+(1x3)의 결과 16이 된다.

16+1.0 = 17이 된다.

<br/>

(0.5x2)+(4x2)+(1x3)+(2x3) = 18

18+2.0 = 20이 된다.

<br/>

마지막은

(3x2)+(2x2)+(1x3)+(1x3) = 16

16 - 1.0 = 15가 된다.

<br/>

학습이 이런식으로 진행된다.

![image](https://user-images.githubusercontent.com/78403443/120161616-7a3e7900-c232-11eb-8e92-c81426c74190.png)

이것이 행렬연산에 의한 결과값

결과값이 3개라는 것은 Label의 카테고리가 3개라는 뜻이다.

<br/>

이미지를 넣었는데 가장 큰 값은 Dog이다. 

Dog으로 결과값 예측을 한 것임

<br/>

완벽하게 숙지해오기

행렬연산을 완벽하게 숙지해야 내일 하는 굉장히 중요한 내용을 나갈 수 있다.