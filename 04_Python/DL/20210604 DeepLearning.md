(※ 저작권 문제로 pdf 캡쳐본은 올리지 않습니다)

<br/>

- **3.Backpropagation.pdf 파일 보기**

<br/>

Segmentation은 암 진단에 활용

<br/>

모션 감지 (motion classification twentybn)

![1_Y-COnAy9z3kIejQY2pOOvQ](https://user-images.githubusercontent.com/78403443/120779067-a96e2680-c561-11eb-9c67-8b83ac8d1bda.gif)

(출처 : [https://medium.com/twentybn/gesture-recognition-using-end-to-end-learning-from-a-large-video-database-2ecbfb4659ff](https://medium.com/twentybn/gesture-recognition-using-end-to-end-learning-from-a-large-video-database-2ecbfb4659ff)))

CNN중에서도 RNN이라는 종류를 사용해서 손동작 모션을 감지, 학습

![0_jPRhu97XuT81gBrN_](https://user-images.githubusercontent.com/78403443/120779122-b8ed6f80-c561-11eb-92d7-aa2c6c91b2aa.png)

(출처 : [https://medium.com/twentybn/gesture-recognition-using-end-to-end-learning-from-a-large-video-database-2ecbfb4659ff](https://medium.com/twentybn/gesture-recognition-using-end-to-end-learning-from-a-large-video-database-2ecbfb4659ff)))

<br/>

---

- **D:\encore_jwc\util\PDF\DL\5.Convolutional_Neural_Network.pdf 파일 보기**

<br/>

**Fully Connected Network(FCN) 전체 과정**

![image](https://user-images.githubusercontent.com/78403443/120779252-db7f8880-c561-11eb-967a-7e19fe6e9170.png)

각각의 Fully Connected Layer가 모여서 모여서 모여서 Fully Connected Network를 이룬다.

그때, 입력이 뭐고 출력이 뭔지 이것부터 중심을 잡고 설계를 진행해야한다.

Fully Connected Layer 몇 개 쌓을지...

각각의 unit수는 몇 개로 할지

<br/>

중요한 얘기...

특징을 추출 하는데 있어서 공간정보를 잃으면 안된다. 

공간정보를 잃지 않는 방법은 덩어리로 그냥 입력해야한다.

그래서, Filter라는게 개발 됐다. 

(1998년도에 얀 르쿤이 개발, 2012년 Alex라는 사람이 갖다 쓰면서 Alexnet이라고 불렀다)

<br/>

이제 CNN으로 들어간다.

<br/>

CNN에서는 Convolution API를 사용해서 Convolution이 진행되고

Pooling 연산이 진행된다. 

CNN에서 진행되는 대표적인 연산이 Convolution(연산의 원리만 이해하면 된다)

그리고, Pooling연산이 있다. (간단)

<br/>

Feature map은 중간 이미지 출력 결과물 (어제 뭔지 배웠음)

<br/>

**What is CNN ?**

이미지의 부분을 보고 그 부분의 핵심적인 특징을 추출하는 방법이 Convolution!

예를 들어 코끼리 이미지가 있다. 

어떤 사람은 코끼리 코가 길다.(필터1) 어떤 사람은 다른 부분을 보고 몸통이 크다.(필터2) 

어떤 사람은 꼬리가 길다고 말한다.(필터3)

이 부분부분적인 특징을 훓는 것이 필터다!

<br/>

필터는 작은 부분을 훓기 때문에 사이즈가 작다. 

그림 맨 왼쪽이 전체 그림이다. 부분을 훓기 때문에 먼저 가로로 한칸씩 이동하면서 훓고

더이상 갈 곳이 없으면 한칸 내려와서 가로로 한칸씩 이동하면서 훓고 반복... 

이런식으로 동작을 한다. (아래 gif 사진 보기)

<br/>

자른다는 얘기는 부분만 본다는 얘기다. 

이미지 부분의 특징만 훓는다. (코, 다리, 꼬리 같은 부분)

부분만 훓기 때문에 훓는 애들이 여러개 나와야한다.

<br/>

어떻게 훓는지 동작을 보자(Convolution 연산이 어떻게 진행되는지)

![0_dSjXKGG6kJ5kVUgJ](https://user-images.githubusercontent.com/78403443/120779452-0bc72700-c562-11eb-8676-7f4f43993a26.gif)

(출처 : [https://medium.com/@icecreamlabs/3x3-convolution-filters-a-popular-choice-75ab1c8b4da8](https://medium.com/@icecreamlabs/3x3-convolution-filters-a-popular-choice-75ab1c8b4da8)))

<br/>

1,0,1,0,1,0,1,0,1 순으로 곱해서 중요도를 준 것이다

중요도를 곱하게 되면 값이 나오고 그것을 다 더한 것이 최종 결과로 나온다.

<br/>

그리고 이 합성곱이 끝나면 한칸 옆으로 이동한다.

그리고 또 옆에서도 똑같이 Convolution이 진행된다.

![image](https://user-images.githubusercontent.com/78403443/120779678-416c1000-c562-11eb-99cb-38ca3ce51253.png)

그 다음 더이상 진행을 못하니까 한칸 밑으로 내려가서 다시 왼쪽부터 순서대로...

이런 과정으로 Feature map을 추출한다.

<br/>

이런 Filter들이 여러개 있을 것이다. (코끼리 코를 훓는 것 1, 몸통 훓는 것 1, 꼬리 훓는 것 1)

각각 뽑아낸 것들을 다 합쳐서 보면 코끼리다 라는 것을 안다.

<br/>

여기까지 Filter가 뭐고, Filter가 어떻게 이미지를 훓고 지나가는지 동작원리를 보았다.

(큰 이미지에서 각각의 정보를 훓는 방식)

Filter가 여러개 나오면 Feature map도 여러개 나온다.

그 수십개 정보를 종합해서 코끼리 라고 얘기하는가? 그렇다. 

하이퍼 파라미터값으로 주는 것이기도 하다.

<br/>

예를 들어서 다시 설명

![image](https://user-images.githubusercontent.com/78403443/120779773-606aa200-c562-11eb-9635-ba478b43ffa8.png)

3x3 사이즈 필터를 이용해서 원본이미지를 훓어간다.

합성곱 한 결과를 다 더하면 6이 나온다. 

그 6의 값이 원본이미지에 필터를 적용해서 한 부분의 특징을 추출한 결과물의 값이 된다.

이런 결과물의 채널이 여러개 나오고, 이 전체가 Feature Map이다.

<br/>

정리 :: 

Filter가 이미지의 부분부분을 여러번 훓는 것이 Convolution 연산이고

연산 진행한 결과물 전체를 Feature map이라고 한다.

최종 결과 출력된 이미지의 크기는 원본이미지에 비해서 작아진다. (중요한 특징 뽑아낸 것이기 때문에)

<br/>

진짜 잘하는 사람은 결과 값만 보고 어떤 특징을 추출한 Filter인지 바로 아는 사람도 있다.

<br/>

**CNN의 역사**

<br/>

얀 르쿤이 발명한 CNN모델, 1998년

전에 손글씨(0~9) 테스트 동영상에 나왔던 모델이 LeNet(르넷)이라는 모델임

<br/>

2012년 알렉스가 발명한 모델 AlexNet

2012년 ImageNet 대회에서 Alex가 1998년에 얀 르쿤이 만든 CNN모델을

활용해서 ReLU() 함수(Activation 함수)와 Dropout() 함수를 사용한 AlexNet을 만들어서 사용했다.

<br/>

ReLU() 함수는 Activation 함수로 전에 배웠으니 알 것이고,

Dropout()함수는 연결을 중간중간 이빨빠진 것 마냥 끊어주는 역할을 함

Dropout()함수썼더니 학습 효과가 올라갔다고 함.

(에러율을 10%나 낮춤) 

이것은 머신러닝의 Decision tree의 pruning(가지치기) 기법과 흡사한 방식, 효과이다.

<br/>

Dropout() 함수는 완벽한 수학 of 수학에서 나온 것

<br/>

2012년 AlexNet모델에서 ReLU() 함수와 Dropout() 함수를 써서 에러율을 많이 낮추고

학습효과를 올렸던 것은 반드시 기억해야하는 부분이다.

<br/>

CNN기법을 쓴 모델 중에서 가장 기본적으로 알아야되는 것들만 CNN History에 실었다.

<br/>

VGG는 2014년에 나왔다.

<br/>

VGG가 나오고 그 이듬해에

<br/>

ResNet(레즈넷)이 나왔다.

<br/>

ObjectDetection은 인공지능 실력뿐만 아니라 프로그램 개발 실력까지 좋아야 잘 활용할 수 있다.

<br/>

ResNet(레즈넷)은 ObjectDetection, Segmentation

<br/>

backbone은 Transfer Learning 이라는 기법을 쓴다. 

이미 만들어져있는 훌륭한 모델로써 (이미 만들어져있는)훌륭한 모델 뒤에 자기가 직접 만든 모델을 연결해서 쓰는 것을

Transfer Learning이라고 함

backbone은 내가 만든 모델을 연결할 (이미 만들어져있는)모델을 말한다.

<br/>

DenseNet(2016)은 구글에서 만듬

<br/>

이제 CNN을 구체적으로 들어간다.

그전에 Fully Connected Layer가 나옴

<br/>

이미지 정보를 쭉 펼쳐서 만든 것이 Fully Connected Layer

Fully Connected Layer가 하나로 모인 것이 Fully Connected Network라는 얘기를 아까도 했음

공간 정보를 담는데 한계가 있다.

<br/>

Convolution Layer로 만들면 공간 정보를 유지할 수 있다.

<br/>

필터 사이즈는 거의 3x3, 1x1을 쓴다. (강사님의 경우 5x5는 딱 두번정도만 써보심)

하지만, 하이퍼 파라미터에 속하기 때문에 지정할 수 있다.

<br/>

Filter의 채널(Depth)는 3이다. 

이게 왜 3인가? 

왼쪽이 원본이미지다. 

원본이미지를 훓으려면 오른쪽에 보이는 filter로 훓어야한다.

원본이미지의 채널(depth)이 3이라면 filter의 채널(depth)도 3이어야 훓을 수가 있기 때문에!

원본이미지의 채널과 filter의 채널 값이 일치해야한다.

<br/>

필터를 사용해서 훓을 때,

원본이미지의 채널과 필터의 채널이 동일해야 이미지를 훓을 수 있다.

<br/>

5x5 필터로 훓을 때마다 값은 하나씩 나온다.

그렇기 때문에 5x5 필터로 훓은 값... 필터로 추출한 값 하나는 1x1로 나온다.

<br/>

32를 5x5로 훓으면서 한 칸씩 가면 이미지가 가로 세로 28로 해서 나온다.

필터와 원본 이미지의 채널이 3으로 같다면, 필터로 훓고 최종 출력되는 중간 이미지(Feature map)의 채널은 하나만 나오게 되기 때문에 1이 된다.

이러한 것들이 여러개 나온다는 것이다.

<br/>

필터가 6개 쓰였다는 것은 총 특징을 6가지로 분류했다는 것이다.

<br/>

Feature map의 채널이 6이라는 얘기는 filter의 갯수가 6개 쓰였다는 것이다.

필터가 훓으면 1이 된다는 것을 반드시 알아야한다!

<br/>

필터가 맨 처음 훓을 때만 채널 수가 일치하면 된다. (3이든 1이든)

<br/>

중간 추출된 Feature map의 채널 수는 컬러랑 상관없음. 

필터를 몇 개 썼냐 그것뿐...

<br/>

STRIDE 개념

만약에 위와 같이 7x7 원본이미지 사이즈에 3x3 짜리 필터가 두칸을 건너뛰어 훓으면 Stride = 2 가 된다.

세칸 건너뛰어 훓으면 stride = 3이다. 

4는 안된다.. 한 칸을 아예 빠져서 훓었으니까!

<br/>

7x7 원본이미지 사이즈에 3x3짜리 필터, stride를 1로 주면 5번을 훓게 되니까 5x5가 된다.

이게 뭐? Feature map

<br/>

5x5 :: 7x7 원본이미지 사이즈에 3x3필터 stride = 1로 줬을 때 나오는 최종 Feature map 출력값

3x3 :: 7x7 원본이미지 사이즈에 3x3필터 stride = 2로 줬을 때 나오는 최종 Feature map 출력값

7x7 원본이미지 사이즈에 3x3필터 stride = 3으로 줬을 때? 에러난다. 하나가 남으니까...

여기서 알 수 있는 것?

Layer가 거듭될수록(Convolution 연산이 계속될수록) 사이즈가 점점 줄어들기 때문에 stride를 계속적으로 생각해야한다.

<br/>

원본보다 확연히 작은 사이즈를 쓰게되면 중간 출력결과의 사이즈가 작아진다.

어떻게 훓느냐에 따라서 stride가 있다.

<br/>

필터 사이즈와 Feature map의 출력 사이즈에 따른 Stride 공식이다. (빨간 네모박스)

공식을 외워라! 공식을 모르면 모델 설계할 때 에로사항이 있다.

(외우기!!! 쓰다보면 외워진다)

나중에 필요할 때 찾아서 사용할 수 있어야한다.

<br/>

filter를 한 칸씩 건너뛰냐 두 칸씩 건너뛰냐에 따라 Feature map은 점점 작아진다.

어쨋든, 빨간 네모박스 표시된 부분은 Feature map의 사이즈가 어떻게 나오는지에 대한 공식...

변형시킬 수도 있다. 이렇게 잘랐다 저렇게 잘랐다...

<br/>

stride가 클수록 이미지 크기는 작아진다.

원본이미지는 원래 크지만... 최종 출력결과가 아니라 중간 출력결과이기 때문에

그 다음에 최종 결과로 출력하기 위해서 filter로 특징을 한번 더 훓을 때는 stride를 어떻게 줘야하나에 대한 고민이 생긴다.

사이즈가 계속 줄어드니깐... stride와 채널 사이즈를 계속 신경써야한다.

이런 신경 안쓰게 하려면 어떻게 해야할까?

<br/>

![image](https://user-images.githubusercontent.com/78403443/120780718-56956e80-c563-11eb-8a1d-fc33695c2a06.png)

원본 사이즈와 중간 출력 사이즈를 같게...

즉, 중간 사이즈를 안줄어들게 하면 된다.

똑같게하면 신경을 안쓰게 될 것이다.

값에 영향을 안주고 원본 사이즈와 중간 출력 사이즈를 똑같이 하는 방법이 있다.

크기는 똑같이 하고 빈 공간에 의미없는 값으로 테두리를 채운다. 여백을 줘서 사이즈를 똑같이 만듬(화면 만들때 padding 주는 것 같이)

<br/>

원본이미지가 7x7 이라고 가정

여기에 pad를 1로 주면 가로, 세로 테두리에 1칸만 채운다

pad = 2는 두 칸만 채운다.

pad = 3은 가로 세로 3칸 채운다.

<br/>

원본이미지가 7x7 이라고 가정하면 크기는

pad = 1 줄 때 :: 9x9 크기가 된다. 가로 세로 하나씩 채웠으니까

pad = 2 :: 11x11 크기

<br/>

![image](https://user-images.githubusercontent.com/78403443/120780797-6745e480-c563-11eb-85ce-daa0a4465067.png)

우리는 pad를 사용해서 output size를 똑같이 나오게 하려고 하는 것이다.

![image](https://user-images.githubusercontent.com/78403443/120780839-7036b600-c563-11eb-9161-45965beed004.png)

pad = 1을 썼더니 원본 사이즈랑 출력 사이즈가 똑같이 나온다.

원본 사이즈 7x7에 filter의 크기가 3x3일때 pad = 1을 써야한다는 것을 알 수 있다.

![image](https://user-images.githubusercontent.com/78403443/120780878-7d53a500-c563-11eb-9ec1-91274a659b35.png)

pad = 2로 줄때는 filter 사이즈를 5x5로 써야 같은 사이즈로 나오는 것이다.

![image](https://user-images.githubusercontent.com/78403443/120780915-86dd0d00-c563-11eb-9d51-70bc2e3e844d.png)

pad = 3으로 줄 때는 filter 사이즈를 7x7로 써야 같은 사이즈로 나온다.

<br/>

정리 :: filter사이즈에 따라서 pad가 정해진다. 

똑같은 조건에서, stride가 2가 되면 stride 1을 줄 때와 비교했을 때 출력 사이즈가 정확하게 입력 사이즈의 1/2(절반)로 줄어든다.

<br/>

입력과 출력 사이즈를 동일하게 맞춰주는 테크닉을 알야아한다. ☞ pad 옵션을 사용

"패딩값은 필터의 사이즈에 의해서 결정"

<br/>

지금까지 ::

Convolution 연산 뭐하는건지, Filter, Feature map, Stride, pad 에 대해서 설명

<br/>

**Convolution Neural Network(CNN)**

![image](https://user-images.githubusercontent.com/78403443/120781080-ae33da00-c563-11eb-915a-b668cc6f672d.png)

①

Convolution 필터의 개수? 64개

필터의 채널은? 3개

패딩과 스트라이드? 1, 1

<br/>

②

필터 갯수? 128

필터의 채널? 64

3x3 사이즈 필터일 경우

패딩, 스트라이드 → 1, 2

<br/>

③

필터 갯수? 256

필터의 채널 128

3x3 사이즈 필터일 경우

패딩, 스트라이드 1,2

<br/>

④

필터 갯수? 512

필터의 채널 256

3x3 사이즈 필터일 경우

패딩, 스트라이드 1,2

<br/>

⑤

필터 갯수? 512

필터의 채널 512

3x3 사이즈 필터일 경우

패딩, 스트라이드 1,2

<br/>

스트라이드가 1이면 그대로, 스트라이드가 2면 반으로 준다

<br/>

Pooling 연산

<br/>

Pooling 연산은 

- 무조건 사이즈가 2x2, stride = 2이다.
- filter안에 값이 없다.
- max pooling 경우 속성값 중 가장 큰 값 뽑아낸다.
- 출력 사이즈는 입력의 정확히 절반이 된다. 1/2

출력 사이즈의 절반으로 하려면 stride를 2로 주던지, max pooling을 주면 된다

<br/>

큰 특징을 주려다보니까 사이즈가 줄은 것

max pooling은 2x2, stride = 2기 때문에 원본사이즈에서 압축된다!

<br/>

pooling 연산에는 max pooling과 average pooling이 있는데 

max pooling은 최종적으로 큰 값을 뽑아낸다. 

average pooling은 평균적인 값을 뽑아낸다.

결과적으로 max pooling 큰 특징들만 추출 

average pooling은 윤곽선 정도를 추출

![image](https://user-images.githubusercontent.com/78403443/120781250-dcb1b500-c563-11eb-97ac-6e0d7c5ae3e2.png)

max pooling에서 중요한 것은 

크기는 반으로 줄지만 채널 수는 그대로이다.

<br/>

굉장히 중요한 결론

pooling Layer는 (Feature map의) 각 채널별로 동작한다!

max pooling은 사이즈만 딱 절반으로 감소시키고(중요한 특징만 뽑아서 갖다놓으니까),

채널 수는 불변!

<br/>

아까 본 사진에서 사이즈는 1/2 → pad = 1, stride = 2를 줘서 사이즈가 반씩 줄었는데

<br/>

실제로 VGG모델에서는 stride는 1 그대로 쓰고, Max pooling을 썼다.

max pooling으로 이미지 사이즈는 줄이고, 

convolution + ReLU로 convolution 연산으로 (필터 수)채널 수는 늘렸다.

<br/>

poling연산으로는 학습이 안된다. Weight값이 안들어가기 때문에...

convolution 연산으로는 학습이 된다.

<br/>

**위 내용 팀별로 표로 정리해서 나중에 발표**

**(max pooling으로, filter는 3x3크기로)**

![image](https://user-images.githubusercontent.com/78403443/120796846-46d35580-c576-11eb-8d22-cc68db395f1b.png)

앞부분 (14x14x512 까지)

- Convolution 연산이 점점 되면서 사이즈 줄어든다...

  사이즈 줄어든다는 얘기는 특징은 압축했다는 얘기

- 채널이 늘어난다는 것은 특징 분류가 늘어난다는 것임

  (특징의 종류가 늘어난다)

<br/>

결론 : 정확한 분류를 하기 위해서 특징을 추출하는 과정이라는 것이다.

<br/>

패턴을 보면 짝수로 점점 줄어드는 것을 볼 수 있다. 

이 말은, 네트웍으로 어떤 작업을 하기 위해서는 짝수로 가야한다는 얘기

<br/>

뒷 부분(7x7x512 부터 오른쪽 끝까지) 설명...

이렇게 나왔다는 것은 사이즈는 최대한 줄인 것이다. 

특징을 압출, 압축시킨 것이기 때문에

반대로 채널 수는 늘었다.

<br/>

앞 부분은 특징 추출 (핵심!!), 앞 부분까지가 CNN

<br/>

Global Max Pooling은 원본이미지와 똑같은 크기의 Max Pooling... 그래서 무조건 하나씩 뽑는 것이다.

(그렇기 때문에, 1x1 크기로 나오게 된다)

<br/>

뒷 부분은 Global Maxpooling이 들어가는 것이다.

Global Maxpooling 들어가고 나서는 위 경우 사이즈 1x1x4096 나온다 (4096개의 특징으로 세세하게 분류했다는 얘기)

4096개의 특징을 분류할 때는 쭉 펼쳐서 FCN 방식으로 분류해서 softmax 연산해서 1000개의 num classes로 들어가게 되는 것이다.

이를 바탕으로 Loss값을 구할 수 있을 것이다.

<br/>

---

**지금까지 한 내용 코드로 다뤄본다**

<br/>

- **05_Deep_CNN.ipynb 파일 보기 (구글 코랩)**

![image](https://user-images.githubusercontent.com/78403443/120797278-c7925180-c576-11eb-8c78-d2495de8e22e.png)

전에도 했던거... 

1단계 - 물리적인 위치에 데이터 저장

2단계 - 네트워크에 100개씩 잘라서 로드

<br/>

**Convolution NeuralNet Model 생성**

![image](https://user-images.githubusercontent.com/78403443/120797319-d547d700-c576-11eb-928e-fb9c116614b0.png)

nn.Conv2d 인자값의 의미 정확히 알아야한다.

kernel_size = 5x5 의미

우리가 알아야 할 것은 앞에 1, 16 의미

![image](https://user-images.githubusercontent.com/78403443/120797436-00322b00-c577-11eb-937c-f16954146c94.png)

(출처 : [https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html](https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html))

<br/>

첫번째는 입력 채널수, (우리는 흑백인 MNIST로 쓰기 때문에 채널이 1이다)

두번째 인자값 출력 채널수, 

세번째 인자값... kernel_size = 5x5

<br/>

(외우기!!!)

3x3 일때 padding = 1이면 사이즈 변경 없다

5x5 일때 padding = 2면 사이즈 변경 없다

<br/>

코딩에 대한 해석 팀에서 해오기...

지금부터 다시 쭉 코드 들어간다.

![image](https://user-images.githubusercontent.com/78403443/120797501-163feb80-c577-11eb-88a2-a83aa62a38e5.png)

CNN에서는 특징을 추출하고, 최종적으로 분류하기 전에 예측할 때는 FCN 통해서 한다.
