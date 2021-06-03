(※ PDF 캡쳐파일은 저작권 문제로 업로드 하지 않는다)

오늘은 전보다 더 코드 위주로 살펴보면서 수업 진행한다.

- **3.Backpropagation.pdf 보기**

<br/>

딥러닝도 머신러닝인데 머신러닝보다 좀 더 Deep하게 들어갔다는 건

학습방법이 Neural Net을 이용했다는 것.

Neural Net을 이용한건 딥러닝으로 분류된다.

<br/>

Neural Net은 생명체가 가지고 있는 뉴런을 확대해놓은 것이다.

Computer Vision은 기계의 시각화라는 의미

뇌에서 해석 한다는 것은 알고리즘이 돈다는 뜻이다.

<br/>

1. 가지돌기를 통해서 자극을 받는다

2. 핵에서 자극에 대한 해석을 한다. (각각의 신념에 따른 해석) - Functions 1, weight를 곱하는 과정

3. 두번째 해석 (공통의 신념에 따른 해석) - Functions 2 - (프로그램적으로 보면 상수와 같은)bias를 더함

4. 1, 2번째 해석에 따른 결과(최종 값) 축삭을 통해 이동

   축삭에서 걸러주는 역할, Activation 함수(활성화 함수) 사용(ReLU 함수 등)

5. 출력

<br/>

---

이어서...

<br/>

10개짜리 카테고리를 가지고 있는 데이터를 분류하는 것

CIFAR10 데이터셋이다.

![image](https://user-images.githubusercontent.com/78403443/120603606-2ed0d880-c487-11eb-8299-c33e8ffca726.png)

중간 출력결과를 Feature map이라고 한다.

(중간에 출력했다는 것을 가정했을 때)

기계가 나름 추려서 예측한 결과이기 떄문에 사진이 조금 다르게 나오게 된다.

Feature map은 중간 레이어에서 압축된 특징을 가지고 있는 것이다.

Hidden Layer를 Feature map이라고 생각하면 된다.

<br/>

Hidden Layer는 X 특징을 압축한 게 Hidden Layer

계속해서 점점 압축해나갈 수 있다.

<br/>

어제 코드 실습에서는 Unit 500개 짜리 Hidden Layer 하나 썼다.

Hidden Layer 하나 쓴걸 ANN이라고 한다.

<br/>

Hidden Layer를 하나 더 쓰면, 더 깊게 썼다고해서

DNN 이라고 한다. 

<br/>

Hidden Layer는 점차 압축되기 때문에 첫번째, 두번째 Hidden Layer에서는

어느정도 판별이 가능하지만 점차 갈수록 판별이 어렵다. 

<br/>

![image](https://user-images.githubusercontent.com/78403443/120603923-78212800-c487-11eb-948e-9173b8514be8.png)

Neural Network는 중의적인 표현으로 많이 쓰지만 일반적으로 Fully Connection Network(FCN) 의미로 쓴다.

CIFAR10 데이터셋은 32x32x3 으로 이루어져있다. 

3채널은 첫번째가 R, G, B 순으로 이루어져있다.

사이즈는 거의 같게 해서 사용한다. 

FCN은 이미지를 통으로 못넣기 때문에 데이터를 한줄로 펼쳐서 넣어야한다.

이것을 한줄로 펼친다는 얘기는 (CIFAR10의 경우)3072개의 픽셀값으로 이루어진 데이터로 바꾼다는 것이다.

(픽셀값은 픽셀의 정보(공간(x, y 좌표), 색)를 가지고 있다)

<br/>

한줄로 펼치게 되면 공간정보를 잃어버리게 된다. 

덩어리로 입력이 되지 않기 때문에 공간정보를 담는데 한계가 있기 때문

<br/>

1. FCN은 공간 정보에 약하다

2. 이미지 픽셀 정보는 덩어리로 입력하는게 좋다

   ☞ 그러나, FCN은 이미지 덩어리를 조금씩 잘라서 넣어야한다.

3. 덩어리로 입력하게되면 Computation Cost는 커진다.

   (3072개의 데이터를 한꺼번에 연산해야하기 때문에)

   CNN 대비 100배에서 1000배 가량 커진다.

   동일한 code를 CNN에서 돌리면 수월하지만 FCN에서는 GPU없이는 불가능하다. 

4. 결론 :: CNN을 쓴다

5. 그런데 FCN은 왜 배웠나? CNN을 쓰더라도 FCN 쓰는 경우도 있기 때문에

<br/>

---

**어제 했던 코드 다시보기**

- **04_Deep_FCN_mnist.ipynb 파일 보기 (구글 코랩)**

<br/>

**transforms.ToTensor() 함수가 하는 일 설명**

![image](https://user-images.githubusercontent.com/78403443/120604316-e6fe8100-c487-11eb-9e67-01a6f37fdfbd.png)

transforms는 Data Augmentation(데이터 변형) 관련 모듈

Data 변형에는 여러가지가 있다.

각도회전, 밝기조절, 잘라내기 등이 있다

나중엔 코드로 구현을 해야하는데...

- 각도회전 : transforms.RandomRotation()

- 밝기조절 : transforms.RandomBrightness()

- 잘라내기 : transforms.RandomCrop()

동시적용 가능하다. 1 Epoch 기준

<br/>

ToTensor()는 3가지 기능이 있다.

- 이미지 값이 0~255 사이의 픽셀값은 네트워크에 들어가기엔 너무 큰 값이다, 학습하기 힘든값

  이것을 0~1 사이의 값으로 바꿔준다 → 스케일링

- ToTensor() 하게 되면 채널 값을 앞으로 보낸다. 

  예를 들어, 28x28x1 짜리라고 하면 1x28x28로 바꿈 (마이너한 기능)

- numpy(타입)는 연산이 안되기 때문에 → Tensor 타입으로 변환

  Tensor 타입으로 변환하면 연산이 가능하게 된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120604436-085f6d00-c488-11eb-9ead-deff9ced2341.png)

가장 많이 쓰는 Loss함수 

입력과 출력 사이의 Loss를 구해준다.

<br/>

Hinge Function의 문제점을 극복한게 

Softmax Function 이라고 2.Linear_Classification.pdf 파일 수업했을 때(머신러닝 때)

얘기했었다.

<br/>

CrossEntropyLoss()는 이거 한번만 쓰면

1. softmax에 저장

2. 그리고 loss를 예측한다 

   (p - y)2 이런식으로... (우리가 따로 진행하지 않고 자동)

3. Regularization 해준다

<br/>

![image](https://user-images.githubusercontent.com/78403443/120604674-39d83880-c488-11eb-893d-cb196ec5944b.png)

이 과정이 Forward Path, Propagation 과정

딥러닝에서는 뭐가 입력되고, 출력되는지가 굉장히 중요하다.

<br/>

Batch_size, hidden layer, Epoch... 연산되는 과정

![image](https://user-images.githubusercontent.com/78403443/120604729-48265480-c488-11eb-86bb-81f4ae4e8b84.png)

① NN연산과정

이미지 딱 1장 넣으면 Network에서 이런 연산이 일어난다

Forwarding 과정...

<br/>

② ①번 과정을 통해 (batch_size = 100) 100개가 동시에 나눠지고 연산

100번 예측하게 되고, 100번의 Loss가 나온다. 그리고 Loss의 평균이 나오고 Backward한다.

<br/>

① ② 전체과정이 600번 반복되는 것이 1 Epoch이다.

이 Epoch을 100번 반복하는게 보통이다.

이런 연산안에 hidden layer가 20, 30개가 있다.

<br/>

그만큼 인간의 한계를 넘어갈 정도의 어마어마한 연산이 진행된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120604815-60966f00-c488-11eb-987b-021d4bfdde76.png)

지금까지 우리는 딥러닝 FCN 방법에 대해서 PDF의 중요한 내용과 함께 코드로 배웠다.
