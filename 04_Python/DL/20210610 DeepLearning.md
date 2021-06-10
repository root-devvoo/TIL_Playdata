(※ PDF 파일 캡쳐본은 저작권 사유로 업로드 하지 않고, 메모내용만 업로드합니다.)

<br/>

오늘 Segmentation 들어간다. 

Unet 이라는 새로운 모델이 소개된다. 

ResNet의 Concatentate (copy & crop) 개념도 소개된다.

<br/>

- 첫번째 코드는 쉬운 것.. (어제 다룬 코드 잘 살피기)

- 두번째 코드는 개발용(재사용성 높다) 

  - 구조와 구성 잘 살피기

- 세번째 코드는 Object Detection 코드 개발용(재사용성 매우 높다) 

  - 강사님 :: 구성, 답지 어떻게 구성되어져 있는지 정의하는데 3주 걸리심
  - 어떻게 동작하는지 알아서 얻어가는게 꽤 클 것임

<br/>

AI 과 프로그램은 같이 발전한다. 

하지만, 선택은 반드시 해야함

<br/>

---

- **D:\encore_jwc\util\PDF\DL\7.Segmentation.pdf 파일 보기**

<br/>

Segmentation 활용, 암 진단

<br/>

Segmentation이라고 하면 픽셀에 해당하는 카테고리를 구분한다.

<br/>

Segmentation은 Sementic Segmentation 기술, Instance Segmentation 기술이 있다.

Instance Segmentation은 잘 쓰지 않음, 굳이 쓰지 않고, 바로 옆 Object Detection을 이용한다.

<br/>

여기서 말하는 Segmentation은 Sementic Segmentation 기술을 말한다.

<br/>

Classification은 이미지 전체를 하나로 분류하는 것

Sementic Segmentation은 각 영역의 픽셀값을 통해서 어느 영역에 해당하는지 알아내는 방법

Classification + Localization은 Single Object Detection (그냥 무시... Object Detection을 Single로 할 일이 없기 때문)

<br/>

그래서 우리가 볼 것은 Classification(이미 배웠고), Sementic Segmentation(오늘부터 진행), Object Detection(다음에 진행)

Computer Vision에서 가장 대표적인 Task

여기에 더해서... GAN까지, 하지만 우리는 GAN까지는 안배우고, Object Detection까지

<br/>

 Sementic Segmentation 기술, Instance Segmentation 기술 차이

<br/>

Instance Segmentation은 물체를 각각 구분, Computation Cost가장 많이 든다.

Computation Cost가장 많이 든다는건 비싸고 가장 무거운 컴퓨터가 필요, 그래서 많이 안쓴다.

<br/>

Sementic Segmentation 개체 인식이 안된다, Computation Cost 두번째로 많이 든다.

Object Detection은 Instance Segmentation과 비슷한 기능이지만 Computation Cost가 가장 적게 든다.

그래서, 군사용으로 많이 쓰임... 저렴한 컴퓨터에서도 가능한 기술 + 시장 가치성이 높은 기술(그만큼, 어렵다)

어렵다는 얘기는 Academic한 실력도 좋아야하고, 코딩 실력도 좋아야 한다, 그리고 굉장히 다양한 곳에서 많이 사용

[ex) 교도소 교도관을 대체하는데 Object Detection 기술 기반 AI로 개발중]

<br/>

굉장히 중요

FPS : Frame Per Seconds (초당 프레임수)

1초안에 내가 처리해낼 수 있는 프레임을 말하는 것이다.

![1_FakB5AL1VHxalv-TVzpM0g](https://user-images.githubusercontent.com/78403443/121493835-293d3a80-ca13-11eb-8e68-94a44cccd70b.gif)

(출처 : https://medium.com/@victor.dibia/how-to-build-a-real-time-hand-detector-using-neural-networks-ssd-on-tensorflow-d6bac0e4b2ce)

위 이미지 경우 1초에 10프레임을 처리할 수 있어야 한다는 얘기

FPS가 왜 중요하냐? FPS는 1초마다 처리하는 이미지 개수

<br/>

인간의 눈은 1초에 이미지 10개 이상 처리(하나의 동작이 자연스럽게 이어지게 처리하는 정도)

그래서 FPS  : 10, 하나의 동작이 자연스럽게 이어지는 정도가 되겠다.

(FPS 0.1 = 10초마다 이미지 하나 처리)

<br/>

이 기술은 자율주행에서 가장 중요한 절대적으로 필요한 기술이다.

<br/>

FPS가 높을수록 Computation Cost는 높을까 낮을까?

1초안에 처리할 수 있는 이미지들이 多

1초마다 처리하는데 걸리는 시간이 빠르고, 짧으려면, 모델이 가벼워야 한다.

그러면 레이어는 작아야 가벼울 것이다.

Weight값은 적어야 가벼울 것이다. 

데이터 처리하는데 전처리, 후처리 속도 적고 빨라야한다.

CPU, GPU도 적게들고, Computation power도 작다.

<br/>

결론 : Trade off 관계 :: FPS가 높을수록 Computation Cost도 낮다.

<br/>

FPS를 높이기 위한 다양한 시도.. 이 문제는 속도와 직결된다.

속도가 빠르면 성능이 떨어진다.

속도와 정확도는 Trade off 관계다.

FPS와 Computation Cost는 Trade off 관계다.

속도는 빠른데 정확도는 아쉬운 모델을 LowAndModel이라고 한다.

반대로,

성능은 진짜 좋은데 다소 느리다. 이런 모델을 HighAndModel이라고 한다.

(LowAndModel, HighAndModel은 속도와 연관)

결론, Trade off 관계다.

<br/>

FPS가 높을수록 동작이 더 자연스러워지고, 속도가 빨라야되고, 

속도가 빨라야되면 가벼워야하기 때문에 Weight값, layer, 전처리, 후처리 전부다 간소해져야 한다. 

그러다 보니 성능은 다소 아쉬운 지점이 나타날 수 있다.

<br/>

각각 구분... Computation Power 엄청 든다.

<br/>

그래서 Segmentation 할 때는 답지를 먼저 보여주는데... 

Segmentation 답지는 Mask라고 한다.

<br/>

진짜 답지

![114868515-49c38c80-9df6-11eb-948f-e4f1074e9552](https://user-images.githubusercontent.com/78403443/121494548-cef0a980-ca13-11eb-9e99-a1e01da38f7b.png)

(출처 : [https://github.com/NVIDIA/pix2pixHD/issues/261](https://github.com/NVIDIA/pix2pixHD/issues/261)))

답지는 Grayscale로 나온다. 답지를 컬러로 하게 되면 Computation Cost가 높아서 못돌린다.

그래서 흑백으로 나오는 것

<br/>

왜 Mask라고 하냐면 각각의 인스턴스를 Masking 하는 것이기 때문

<br/>

위와 같은 흑백답지를 아래와 같이 컬러로 바꿔주는 것이 후처리 작업임

![114868697-7e374880-9df6-11eb-95f8-fac7f80a5f04](https://user-images.githubusercontent.com/78403443/121494625-e2037980-ca13-11eb-98ae-a9e2e8d8ccf1.png)

(출처 : [https://github.com/NVIDIA/pix2pixHD/issues/261](https://github.com/NVIDIA/pix2pixHD/issues/261)))

후처리 기술이 높은 작업이 Segmentation이다. 

예전의 정답, 답지와는 다르다!

<br/>

FCN은 공간정보 상실, Computation Cost 크다.

<br/>

CNN은 여러개의 특징을 여러개 종류로 뽑는다.

이미지를 통으로 넣는 것 같지만, 실제로 통으로 들어간 이미지 부분부분을 작은 연산하는 것

<br/>

특징을 작게작게 추출하는데, 종류를 여러개 한다. 

이렇게 하는게 Convolution... CNN 

그리고 최종적으로 분류하는데 FCN이 쓰인다. 그리고, 마지막으로 softmax를 먹여서 

Classification한다.

<br/>

이런 내용이 들어가 있는 대표적 모델이

<br/>

VGG - 가장 기본적...

GoogLeNet(inception) - 구글 개발

ResNet - Microsoft에서 만들었다. 

DenseNet

<br/>

Segmentation에서 가장 대표적인 모델이 U-Net이다.

<br/>

CrossEntropyLoss는 여러개 중에서 하나를 찾는 것

BinaryEntropyLoss는 Binary문제 (이거 아니면, 저것)

이런 것들은 Segmentation에서 쓸 수 없다.

<br/>

그래서 Sementic Segmentation에서 Evaluation(평가)을 어떻게 하는지 알아본다.

Evaluation Matrix를 통해서...

<br/>

컬러 사진으로 채널이 3이 들어가 있다.

원본 이미지 사이즈를 512x512라고 가정, 3x3 필터로 특징을 추출한다고 해보자.

이때 뭐의 변화가 없어야 할까? 이미지 사이즈 변화 없다!

그러므로 연산 시 stride, padding 각각 1씩 주고, 채널은 늘릴 것이다.

<br/>

전에 했던 CNN과 Segmentation의 CNN 과정과는 다른점이 있다.

출력결과 어떻게 가져오나? argmax로 가져왔다. 그게 다른 것

어떻게 출력결과로 나왔는지에 대한 설명...

![image](https://user-images.githubusercontent.com/78403443/121495000-34449a80-ca14-11eb-9b5b-9372fcfb0dc4.png)

픽셀 값 하나를 뽑아내기 위해 위 경우처럼 가정하면

28장의 값을 합친 결과로 뽑은 것일거다. 

argmax로 가장 큰 값을 인덱스(0(tree), 1(sky), 2(grass), 3(cow)) 에 뽑아 넣어줌

인덱스별로 다르게 칠해준다.

결론은 CNN으로 나오고, 그 결과에서 argmax 결과 토대로 인덱스에 맞는 색을 칠하는 것이다.

색을 칠해서 분류

<br/>

CNN이랑 argmax전까지의 과정은 똑같지만, argmax로 결과값 출력하는 부분이 다른 것임

<br/>

결과적으로 Segmentation을 하기 위해서는 CNN 기술만으로 충분하다.

하지만, 이렇게 한다면 돌아가기는 하지만 너무나 큰 Computation Power가 든다.

이유가 뭘까?

1, 2억... 10억짜리 컴퓨터가 필요

결국 이렇게 못쓴다.

연산 사이즈가 너무 방대하다.

![image](https://user-images.githubusercontent.com/78403443/121495087-445c7a00-ca14-11eb-8baf-c59956da34b5.png)

우리가 그동안 사용한 CNN은 사이즈는 줄고, 채널의 갯수는 늘어난다.

이게 CNN...

사이즈를 줄인다는 얘기는 특징을 압축한다는 얘기랑 같고,

채널을 늘린다는 얘기는 특징의 개수를 추가한다는 얘기

<br/>

사이즈 줄어들면 연산량도 줄어든다.

근데, 사이즈가 그대로 가게 된다는 얘기는 연산량이 어마어마하게 든다는 얘기다.

전에는 특징을 뽑아낸다고 CNN에서 사이즈를 줄인다고 했지만, 사실은 연산량을 줄이기 위해서 사이즈를 줄였던 것임

실제로 연구결과를 보면 사이즈를 줄이는 것하고, 특징을 추출하는 것하고 크게 연관성이 없다.

특징은 부분부분에서 나오는 것이기 때문에 필터를 전체 다 돌릴 필요가 없다.

<br/>

두번째, 중요한 얘기

사이즈를 줄이지 않으면 Computer power가 엄청나게 든다고 했는데...

Feature map 채널 수는 늘리면 괜찮은가? 

일단, Computation cost와 직결되는건 image의 size(w, h 크기)이다.

왜? 사이즈가 중요한지 설명한다.

![image](https://user-images.githubusercontent.com/78403443/121495164-5b02d100-ca14-11eb-8549-7216c3f67408.png)

사이즈는 1/4 줄었고

채널은 2배 줄었다.

사이즈를 줄이는건 채널을 줄이는 것보다 훨씬 더 사이즈를 많이 줄이게 되는 것이다.

사이즈를 줄이는건 Computation Cost를 줄이는데 최고의 전략

<br/>

사이즈를 그대로 가는 것이 왜 큰 문제인지 설명했다. 

그리고, Filter의 요소를(채널 개수를) 늘리는 것이 중요하다.

<br/>

결론에 해당하는 얘기

(사이즈 그대로 유지하면서 간다는건 있을 수 없는 얘기이다)

결국 큰 문제이기 때문에...

<br/>

결론적으로는 줄였다가 다시 늘리는 것이다.

가운데 부분을 기점으로, 

H, W는 서서히 줄어들었다가

다시 원래 이미지 사이즈와 동일한 사이즈로

H, W를 늘리는 것이 Sementic Segmentation의 원리가 나온 모티베이션이다.

<br/>

파란색쪽은 어떤 네트워크로 연결? CNN(Convolution)

빨간색을 Convolution의 반대라고 해서 Deconvolution이라고 한다.

사이즈를 늘리는 것이기 때문에 upsampling이라고 한다.

Transpose Convolution == upsampling (Transpose Convolution은 upsampling의 동의어)

학계에서는 Transpose Convolution 이라고 많이 쓰고, 강사님은 upsampling이나 Deconvolution로 쓰신다.

<br/>

핵심 :: downsampling은 사이즈를 줄임(연산량 생각해야), upsampling은 사이즈를 늘림

이 페이지에 대한 정리는 이렇게 하면 Perfect! 끝났다.

<br/>

Convolution에서 사이즈를 절반으로 줄이는 skill (3x3 경우)

- ① stride = 2, padding = 1
- ② max pooling (2x2, 2)

<br/>

Max Pooling은 가장 큰 값을 결과로 추출하는 역할을 하기 때문에

픽셀값 중 가장 큰 값 ☞ 큰 특징을 잡아내는 것이므로

최근 논문에서는 trainable 하지 않다는 이유로 Max pooling 사용하지 않고

stride = 2 로 많이 사용

<br/>

우리는 위 그림에서 Upsampling 제외하고는 다 배웠다.

Convolution Layer + Batch Normalization layer + ReLU + Max Pooling + softmax

이런식으로 레이어를 구성해라, 이게 일반적이다! 라는 얘기를 한번 더 강조한다.

<br/>

①

그리고, Batch  Normalization에 대한 얘기를 안할 수 없는데

Batch size마다(100개씩 layer마다)(같은 말, 레이어를 들어갈 때 마다)

weight 곱하고, bias 더하고 기본적으로 연산이 진행되기 때문에 속성 값이 다시 커진다.

큰 값은 커지고 작은 값은 더 작아지고...

이 얘기는 값의 Variance가 커진다(분산이 커진다)는 얘기.. High Frequency 하다고 얘기한다.

그래서 **이 값을 다시 차분한 값으로 만들어줘야한다.** 

**이 역할을 Batch Normalization이 하는 것이다.**

<br/>

Batch size에 대한 권장값이 있다. 권장값은 16, 32이상해라... 

우리... 그동안 거의 100, 128 잡아서 했지만 이정도로 잡아서 하는 경우는 없다!

<br/>

②

Batch size 100 줬을 이런 경우

![image](https://user-images.githubusercontent.com/78403443/121495659-c3ea4900-ca14-11eb-835b-ca40f805cf1b.png)

위 결과로 보면...

Batch Normalization 안해주면 1000을 제외한 나머지는 의미없는 값(값은 있으나 마나한 값)이 된다.

1000 값이 나머지 값을 압도해버린다. 갑자기 큰 값이 나올 수 있다. → 학습 효과 ↓

**Batch Normalization은 이런 이상치 값을 제거시키는 역할을 한다.**

 <br/>

정리 ::

Batch Normalization은 숨을 죽이는 것과 동시에 이상치 값을 제거시켜서 다른 값들을 살려주고, 학습 효과를 올리는 역할을 한다.

그래서,  Batch Normalization을 슈퍼맨이라고 한다. 

(저번에도 설명했던거지만 한번 더 강조해서 설명함)

<br/>

어쨌든... 그럼 사이즈를 2배로 어떻게 늘릴까?

<br/>

이게 Upsampling...

원래 사이즈가 2x2 이 값을 늘리고 싶다.

<br/>

①번째 방법, 어떻게 하냐? 빈 곳을 0으로 채워서 사이즈를 늘린다. 

의미없는 값으로 채운다(bed of nails)

가장 심플한 방법... 0 값으로 채움

학자들은 트레이닝 하기에 안좋은 방법이라고 한다. 

(그래서, 이 방법... 권장하진 않지만) 하지만, 다른 입장에서 보면 0값으로 채웠다는 점을 주목해야한다.

<br/>

②번째 방법, Interpolation (보간법)

Nearest Neighbor :: 가장 (근사한)근사치 값으로 채워 넣는 방법

<br/>

무작정 0으로 채울 때보다 학습효과 좋다. (Garbage 값으로 채우는것과는 별개의 level로)

학자들의 얘기 :: 학습 되는건 여전히 아니다.

<br/>

③번째 방법, Deconvolution의 대표적 방법 Transpose Convolution

일단 Trainable!(학습 된다!)는 것에 주목

<br/>

Transpose Convolution에서 upsampling을 어떻게 하는지 본다.

<br/>

이것은 downsampling이다. 왜 downsampling이 나왔을까?

downsampling 원리는 이미 다뤄서 잘 알고 있을 것이다.

이 정반대가 Upsampling 그 중에서도 Transpose  Convolution 얘기를 하려고

downsampling을 건드리는 것이다. 

downsampling을 이해하면 upsampling도 이해가 된다!

<br/>

이걸 이제 뒤집어 본다.

뒤집은 그림 - upsampling

설명...

![image](https://user-images.githubusercontent.com/78403443/121496324-51c63400-ca15-11eb-8c20-373d6bd710fa.png)

3x3 필터라고 가정

합성곱이 곱해진 값으로 padding을 제외하고 값이 채워진다.

그러다보면, 반드시 숫자가 겹쳐지는 패턴이 나오게 된다.

4x4로 늘어나서 결과 출력이 되게되고 

겹쳐지는 부분은 각각 더해져서 출력된다.

<br/>

이것이 Transpose Convolution 이다.

이런식으로 업데이트 되어진다.(학습이 되어진다는 말)

<br/>

여기서 정리해야할 부분

1. weight값이 학습
2. 숫자가 겹쳐지는 일정한 패턴이 나타난다.(생긴다.)

![image](https://user-images.githubusercontent.com/78403443/121496397-630f4080-ca15-11eb-802b-ccba5163e23a.png)

맨 왼쪽이 원본이미지...

그 사이에 padding을 줬기 때문에 0값이 채워진다.

그럼 원래 3x3 인데 이걸 찢으면 7x7이 된다.

찢은 것에다가, 3x3 필터를 적용한다.

Convolution 연산 적용한 결과가 위에 찍히는 것 

위 경우 w22가 찍힐 것이다. 

그 다음에는 w21과 w23을 더한 값이 찍힐 것이다.

만약, 위 그림 주황색 부분을 훓는다고 하면?

4행 4열에 w11, w13, w31, w33 값을 모두 더한 값이 찍힐 것이다.

이런식으로 3x3 에서 5x5로 크기가 늘게된다.

<br/>

최근 코드를 보면 ②번째 방법, 을 많이 쓴다. 

Interpolation(보간법) vs Deconvolution 사이에서 굉장히 논란이 핫했다. 

왜 핫했는지?

Interpolation(보간법)은 trainable 하지 않지만 성능과 visual적 측면에선 좋다.

Deconvolution은 성능 좋지 않고, side effect 발생.

![image](https://user-images.githubusercontent.com/78403443/121496960-ea5cb400-ca15-11eb-9af1-0a06a2e70dff.png)

1번과 2번 중에서 2번이 더 좋아보인다. 

1번... checkerboard가 나온다. (격자같은...)

숫자가 겹쳐지는 패턴을 반복하게 되면 겹쳐질 때마다 보이는게 checkerboard라서 

위와 같이 인공적인 느낌의 출력결과가 나와버린다.

checkerboard == side effect

<br/>

반면에, 2번이 Interpolation(보간법)으로 한 방법이다. 상대적으로 깨끗하게 나왔다.

<br/>

1번 같은 현상을 보여주는 이미지(아래)

![다운로드](https://user-images.githubusercontent.com/78403443/121497035-fe081a80-ca15-11eb-8742-064d92d91be4.png)

(출처 : [https://i-am-eden.tistory.com/14](https://i-am-eden.tistory.com/14)))

1. checkerboard가 side effect이다.
2. Trainable → 연산량이 많아진다
3. 성능이 그닥...

그래서 Interpolation(보간법)이 더 좋지 않냐고 논란이 되었던 것이다.

<br/>

결국, Interpolation(보간법)이 이겼다. segmenation에서는 출력결과도 중요하기 때문

그래서, 요즘 나오는 최신 코드들을 보면 Interpolation(보간법)으로 다 바뀌어져있다.

<br/>

마지막 결론 ::

Interpolation(보간법)이 뭐냐면 근사치로 넣어준다. 

이렇게 nearest neighbor 방식으로 넣으면

![image](https://user-images.githubusercontent.com/78403443/121497127-1415db00-ca16-11eb-8a41-d3cdb4dcbbbb.png)

(출처 : [https://www.wikiwand.com/en/Bicubic_interpolation](https://www.wikiwand.com/en/Bicubic_interpolation)))

첫번째 그림과 같은 것이다.

첫번째 그림에 파란선으로 표시한 것처럼 만들어 줄 수도 있을 것이다. (checkerboard를 약간 해결)

<br/>

2x2 출력물을 4x4로 upsampling 해본다. 

어떻게 빈 곳에 값을 채워주면 좋을까? 

평균치는 아니지만 조금씩 근사한(소수점 정도?) 값을 넣어준다

<br/>

Convolution이 사이즈가 줄어드니까 Downsampling이고

이것을 Encoder라고 한다.

Encoder는 압축한다는 것을 뜻한다. 

(Segmentation에서는 용어를 정확하게 짚는 게 중요하다)

<br/>

Upsampling은 Deconvolution이라고 한다.

Upsampling에는 아까 봤듯이 Interpolation(보간법), nearest neighbor 가 있다.

Upsampling은 Decoder라고 한다. 

Decoder는 다시 압축을 푸는 것을 얘기한다.

<br/>

4가지 convolution 종류를 본다.

**Several Types of convolution**

1) Convolution

2) Transpose Convolution

3) Atrous Convolution

4) Separable Convolution

<br/>

Transpose Convolution은 Upsampling을 말한다.

3, 4번은 Advanced 한 내용이므로 Segmentation과 관련 없다.

3번은 성능이 아주 좋다. 

성능이 좋다는 얘기는 Computatin Cost 높다

4번은 속도가 굉장히 빠르다.(기존 속도의 100배는 빠름)

그 말은 굉장히 가볍게 만들어졌다는 얘기

<br/>

어제 다룬 것 중에 MobileNet이라는 모델이 있는데... 이건 모바일에서 사용가능하도록해서 굉장히 빠르다.

MobileNet이 4번 방식 기반이다.

<br/>

**U-Net**

![image](https://user-images.githubusercontent.com/78403443/121498800-be423280-ca17-11eb-9218-b3b48aee5d56.png)

(이미지 출처 : https://creamnuts.github.io/paper/Unet/)

Segmentation의 네트워크 모델이다.

Segmentation을 공부했으면 U-Net을 정확히 알아야한다.

U-Net은 Encoder와 Decoder 이 두개가 합쳐져 있는 독특한 모델이 U-Net이다.

(회색 부분빼고는 다 배운 내용이다.)

<br/>

이것이 U-net 초창기 논문이다. 

U-net 초창기 논문에서는 입력→출력시 padding을 주지 않았다.

Zero padding을 안썼다. 

그래서 572 → 570으로 줄었다.

그 다음에는 568로 줄고 채널수는 그대로 유지되었다.

그 다음 max pooling하고, convolution 진행.. 128로 채널 수 늘었다.

...

28x28, 채널 512.. 

30x30에서 채널을 1024까지 늘렸다가 뒤에 사이즈랑 채널 줄인 것임

<br/>

그 다음 초록색이다. 초록색 처음 나왔다. (up-convolution)

56x56, 512

다시 사이즈 늘리고 convolution에 의해서 채널을 줄인다. 256

다시 사이즈 늘리고 convolution에 의해서 채널을 줄인다. 128

...

맨 마지막 부분 채널 64에서 2로 갈때

2가 의미하는 것이 뭘까?

이건 카테고리 개수가 2개라는 얘기다. (cat이냐 dog냐?, cell이냐 cell아니냐 이런식)

<br/>

그리고 마지막에 사이즈가 안줄었다. (마지막에 사이즈 감소가 없다)

여기서 filter를 바꾼다. 1x1 Filter 사용

사이즈가 바뀌지 않는 이유는 1x1 conv filter를 사용했기 때문이다. 

나중에 코드 작성시 중요하다!

<br/>

위 이미지 (회색) copy and crop 부분 설명 (굉장히 중요한 설명이다)

![image](https://user-images.githubusercontent.com/78403443/121499353-44f70f80-ca18-11eb-9ebb-735a0a999e6f.png)

(cell unet 이미지 출처 : [https://medium.com/@michaelsugimura/segmenting-medical-images-7b1f5e114f79](https://medium.com/@michaelsugimura/segmenting-medical-images-7b1f5e114f79)))

지금 이런걸 U-Net으로 만들었다고 생각하면 된다. 

맨 오른쪽 컬러로 되어있는 부분이 후처리 된 부분이라고 생각하면 된다.

<br/>

copy and crop 설명

![image](https://user-images.githubusercontent.com/78403443/121499417-54765880-ca18-11eb-9070-d2dfdbd82d75.png)

맨 밑 마지막 32x32x10 부분에서 Deconvolution 진행되서 64x64가 됐다.

<br/>

압축을 했던 걸 다시 푸는 과정이니까 ②번의 정보가 더 손실되기 때문에

①번이 예전 원본이미지의 기억을 더 잘 갖고 있을 것이다.(원본의 핵심 정보 간직)

그래서 ①번에서 Concat 해줘서 ②번에서 같이 참고하도록 한다. 

이게 Concatenation이다. 

그 위도 마찬가지... ( 그 부분들이 가운데 화살표들이다)

이런식으로 압축이 좀 덜 된 애들이 Concatenation 하는 것

<br/>

어떻게 합쳐지는지 그림...

<br/>

①번이 앞에 있고 ②번이 뒤에

![image](https://user-images.githubusercontent.com/78403443/121499488-67892880-ca18-11eb-8352-8fe16243429b.png)

이런식으로 되는 것이다. 이게 copy and crop, Concatenation이다.

Concatenation이 뭐냐? 붙인다는 뜻

<br/>

정리 ::

왜 이렇게 하냐? 조금 더 원본 정보에 가까운 정보를 활용하고 싶을 때

이런 방법을 구사한다. ResNet에서 사용해서 히트친 방법

그만큼 압축을 많이 했다는 것은 정보 손실이 많이 이뤄졌다는 뜻

물론 그만큼의 액기스 정보도 가지고는 있지만

원래 가지고 있던 정보도 많이 손실되었음을 뜻한다.

Concatenation을 진행하려면,

Concat하는 애들끼리 사이즈는 같아야하지만, 채널은 달라도 상관없다.
