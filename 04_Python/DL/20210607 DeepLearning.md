(※ PDF 캡쳐본은 저작권 문제로 올리지 않습니다)

<br/>

오늘 수업 내용

![image](https://user-images.githubusercontent.com/78403443/120989535-9d30d600-c7ba-11eb-9d80-67e0c8987201.png)

- 딥러닝 아키텍쳐(네트워크) 설계는 오늘 발표할 그것... (6월 4일 만든 팀별 발표자료들)
- 코드로 디버그 하는 방법 :: pdb 모듈 설치
- 구글 Keras... 바로바로 써보면서

<br/>

오늘 수업 내용은 딥러닝 석사 과정 한 학기라고 해도 과언이 아님 

<br/>

---

**팀별 발표 (딥러닝 아키텍쳐(네트워크) 설계)**

<br/>

Max Pooling 은 이미지 사이즈를 반으로 줄인다. 채널은 그대로 유지한다.

Convolution 연산은 사이즈도 줄일 수 있는데, Feature map에서 사용하는 채널 수(필터 개수)를 늘리면서

특징을 계속적으로 사용하는 특징을 지닌다.

<br/>

MNIST 데이터셋 바탕으로 정리 (구글 코랩 1. Pytorch, Keras Tutorial 폴더 05_Deep_CNN.ipynb 파일)

![image](https://user-images.githubusercontent.com/78403443/120989639-b8034a80-c7ba-11eb-9a89-dda6736fdf60.png)

28x28x1 MNIST데이터셋이다.

<br/>

Convolution 연산 5x5 사용했다.

torch.mm.Conv2d(in_channel, out_channel, kernel_size, stride = 1, padding = 2) - outchannel = 피쳐맵 채널, kernel = 필터 사이즈

2차원이기 때문에 Conv2d 쓰는 것이다. 

3d 경우는 게임 개발에서 많이 사용

<br/>

max pooling (2x2, stride = 2)

사이즈만 반으로 줄인다.

<br/>

Linear.. FCN 만들때 쓰인다. 

1차원으로 늘림

<br/>

앞부분까지는 (Conv + ReLU + MaxPooling) * 7 → 특징을 추출, 사이즈를 줄여가며 특징을 추출함

이미지 줄이면서 이미지 정보는 손실되나, 어떤 특징을 추출하느냐에 대한 특징 카테고리의 종류는 늘어난다.

<br/>

이 과정이 어느정도 진행되면 뽑아진 특징을 가지고 분류를 진행해야한다.

분류를 하려면 확률로 바꿔야한다. 

그게 FCN에서 하는 것이다. FCN에서 확률로 바꿔서 값 예측

이 역할은 FCN에서 하는 것... 

<br/>

결론 :: 

CNN은 Convolution, ReLU, Max Pooling 반복, 반복하면서 특징들을 추출

CNN의 맨 마지막 부분을 보면 FCN이 나온다. 

FCN에서는 분류를 위한 추출작업이 진행된다. 그리고 맨 마지막에 softmax를 해서 예측한다.

<br/>

세 과정이 CNN에 다 합쳐져있다.

<br/>

VGG16모델로 설명

![image](https://user-images.githubusercontent.com/78403443/120989758-d79a7300-c7ba-11eb-8180-84c17a8e095e.png)

Max pooling만 해줘서 7x7x512 나왔다

<br/>

7x7x512하면 4096보다 더 많이나온다.

7x7x512와 1x1x4096 사이에 중간에 7x7x4096이 빠진 것이다.

채널 수는 늘어났다. (Convolution 적용)

<br/>

그리고, Global Max Pooling을 적용했다. 

Global Max Pooling 뭔가?

7x7 이미지라고 가정...

여기에 원본이미지 사이즈와 똑같은 필터를 돌린다.

딱 7x7 필터가 돌아가는 것이다. 이중에서 제일 큰 값 뽑아냄

Global Max Pooling은 사이즈가 1x1 으로 나온다. 필터의 사이즈가 원본이미지가 똑같다.

<br/>

필터의 사이즈가 원본 이미지 사이즈와 같은 것 == Global Max Pooling

채널수는 똑같고 사이즈는 절반이 아닌 1로 확 줄여버린다. 이 과정이 빠져있는 것

<br/>

1x1x4096을 쭉 세웠다. 

1x1x1000은 output이 1000, 라벨의 갯수

<br/>

Weight Edge 들어가서 최종적으로 softmax 들어간다.

<br/>

이 내용에 대해서 완벽하게 이해한 것이면, VGG16에 대해서 이해가 다 된 것이다.

<br/>

Average Pooling 은 안쓰거나 Max Pooling으로 바꿔서 쓴다.

<br/>

이 부분을 적용하느냐 마느냐가 Accuracy를 90에서 92로 94에서 96으로 올릴 수 있는 중요한 포인트가 된다.

이런 설명을 해주는 곳이 있고 안해주는 곳이 있다.

<br/>

지금 보고 있는 이런 Neural Net 연산

크게보면 FCN(Fully Connected Network)

![image](https://user-images.githubusercontent.com/78403443/120989935-087aa800-c7bb-11eb-9af9-a253915ef5be.png)

여기서 학습을 한다는 얘기는 

각각의 속성 값을 중요도에 각각 곱한다.

그래서 어떤 결과가 나오고, 그리고 최종적인 결과 그리고 중요도를 곱해서

최종적인 결과가 나온다. 

결과가 나오면 Loss가 나오고, Loss가 나오게 되면 이 Loss에 대한 책임을 W에게 묻기 때문에

곱할 중요도 값이 수정된다. 이를 바탕으로 다시 Forward, Backward 진행

<br/>

학습을 한다는건 계속적으로 W값을 보정하면서 진행

이것이 Backward과정

<br/>

얘는 첨부터 1차원으로 들어가지만...

<br/>

반면에 CNN은

Convolution...

이미지 덩어리로 들어가는 것이다. 

필터로 이미지 부분을 훓는다. 그 안에 값이 들어있다. 

이 값이 Weight값이라고 보면 된다. 이 값이 변경되면서 다시 filtering 하고... 반복

<br/>

FCN은 연산량이 어마어마하기 때문에 똑같은 코드여도 FCN방법으로는 하다가 터짐...

CNN은 수월하게 돌아간다.

<br/>

사실은 같다... 방법의 차이

FCN은 공간 정보를 잃는다. 

CNN은 정보 손실이 적다. 

하지만... CNN으로 특징을 뽑아낸 후 FCN을 적용해서 결과를 출력

<br/>

---

- **코랩 구글 코랩 1. Pytorch, Keras Tutorial 폴더 05_Deep_CNN.ipynb 파일 보기**

<br/>

**디버깅을 어떻게 하는지? (굉장히 중요)**

![image](https://user-images.githubusercontent.com/78403443/120990127-3233cf00-c7bb-11eb-8d27-42a333db9e7e.png)

디버깅 모듈 pdb 설치

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990172-3c55cd80-c7bb-11eb-9f82-2e974a24cd96.png)

이 함수는 Convnet 함수니까 자동으로 호출

![image](https://user-images.githubusercontent.com/78403443/120990211-4677cc00-c7bb-11eb-844c-e833ccdd6fc3.png)

이 함수는 언제 호출?

![image](https://user-images.githubusercontent.com/78403443/120990246-50013400-c7bb-11eb-82d7-00cea4243490.png)

모델에 데이터를 입력해서 예측값 반환되는 이 부분... 

이 코드에서 뭐가 생략 되있냐면 model.forward(images) 이것이 생략된 것이다.

<br/>

이 모델에 입력해서 예측값을 얻을 때 forward함수 호출된다.

중간에 model.forward(images)가 생략되었다고 보면 된다.

<br/>

Network... 코드가 어떻게 전개되는지 알아야 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990341-68714e80-c7bb-11eb-9487-1a86dd4d067b.png)

이 부분은 모델 인스턴스를 메모리에 올려놓는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990394-74f5a700-c7bb-11eb-9b0e-4da95ba61ca3.png)

test부분에서 이 부분 모르면 안된다. (전에 설명하셨음)

<br/>

with torch.no_grad() 부분은

Backpropagation하지마라 내가 다 학습한 것까지 갖다 쓰겠다. 라는 얘기

<br/>

학습하는데 있어서...

누구나 다 디버깅을 반드시 해야되는 부분이 어디냐 하면

![image](https://user-images.githubusercontent.com/78403443/120990434-8343c300-c7bb-11eb-9bf5-e63ca59b3831.png)

이 부분이다. 

총 6만개 트레이닝 데이터를 넣는데, batch_size로 100개씩 잘라서 넣는다. 

batch_size로 준 이미지가 들어가는데... 

images.shape 찍게 되면 어떻게 나와야 하냐?

(디버깅 해보면서 공부해야한다. 이걸 못하면 논문, 이론은 알아도 개발은 못한다)

1x1x1568... (?) 아니다. 1x1로 reshape 하기 전이니까...

그래서 찍어봐야한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990477-90f94880-c7bb-11eb-80e1-f4cf619a619a.png)

이 부분에서 디버그를 건다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990537-9eaece00-c7bb-11eb-8759-4349dd6e211c.png)

pdb.set_trace() 에서 걸린 것... 

pdb 아래 라인이 outputs = model(images) 라는 얘기이므로

pdb.set_trace() 에서 걸린 것이라는 것... 꼭 명심

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990638-b8e8ac00-c7bb-11eb-8909-a3d9bdab749a.png)

l(소문자 엘)을 입력하면 pdb로 어느부분을 디버깅 하려하는지 알 수 있다.

![image](https://user-images.githubusercontent.com/78403443/120990702-c736c800-c7bb-11eb-9f69-b6efbccdd08b.png)

.size()(위 경우 images.size())를 찍어보면

shape를 알 수 있다.

<br/>

6만장이 한꺼번에 로드되면 CNN터지기 때문에 100개씩 로드

이게.. Batch_size

그래서 네트워크에 입력하는 사이즈는 총 4차원으로 나온다. (굉장히 중요!)

맨 앞 = Batch_size

channel

height

width 순

<br/>

100x1x28x28 씩 로드 되는 것이다. 600번씩

이게 1 Epoch, Epoch이 5번 진행된다는 것이다.

<br/>

물리적 데이터를 변환.. ToTensor() 

1. 0~255 스케일링
2. Channel을 앞으로 바꾼다
3. Tensor 테이블로 변환

<br/>

라벨 사이즈는?

![image](https://user-images.githubusercontent.com/78403443/120990797-e59cc380-c7bb-11eb-810f-88afdb74c123.png)

100 나온다. 

이런식으로 한 단계 한 단계 알고 들어가야한다.

<br/>

그리고 q 쓰면서 에러뜨면서 빠져나온다.(에러 신경안써도 됨)

![image](https://user-images.githubusercontent.com/78403443/120990821-f1888580-c7bb-11eb-958e-2170e769199c.png)

그리고 pdb.set_trace() 부분을 주석으로 막아놓아야 한다.

![image](https://user-images.githubusercontent.com/78403443/120990858-fbaa8400-c7bb-11eb-9f46-e3d3b4cdecd6.png)

<br/>

네트워크에 입력될 때 어떤 shape로 입력되는지 디버깅을 통해 파악해야한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120990914-10871780-c7bc-11eb-8100-89006b53a9c1.png)

그리고, 위 레이어별로 어떤 흐름으로 출력이 되는지 봐야한다.

<br/>

살펴본다.

![image](https://user-images.githubusercontent.com/78403443/120990963-1da40680-c7bc-11eb-9475-901bb565caf1.png)

<br/>

실행했는데 아무것도 안나온다. 

왜? 호출이 안됐으니까

이 부분 호출하려면

![image](https://user-images.githubusercontent.com/78403443/120991019-298fc880-c7bc-11eb-8b96-dbeb4dce5f62.png)

이 부분 실행되도록 해야한다. (아까 위에서 설명)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120991051-33b1c700-c7bc-11eb-8acf-8a2b72f1708a.png)

이 부분에서 걸려서

![image](https://user-images.githubusercontent.com/78403443/120991087-3dd3c580-c7bc-11eb-996d-e432e44d84e8.png)

여기서 걸렸다!!!

x.size() 하면 shape 어떻게 나와야 하는가?

100x1x28x28로 똑같이 나와야한다. (입력 사이즈니깐)

![image](https://user-images.githubusercontent.com/78403443/120991112-462c0080-c7bc-11eb-9ca4-b2e09e42a4ff.png)

첫번째에서 100x1x28x28이 출력되어서 2번째 속성값으로 들어간다는 것을 알 수 있다.

<br/>

n하면 다음을 가리키게 된다

![image](https://user-images.githubusercontent.com/78403443/120991179-57750d00-c7bc-11eb-8fea-9832ef30c548.png)

다음 shape을 출력했다

![image](https://user-images.githubusercontent.com/78403443/120991218-6065de80-c7bc-11eb-8556-ac4f2f1bef68.png)

다음을 또 출력

![image](https://user-images.githubusercontent.com/78403443/120991265-6c51a080-c7bc-11eb-8853-8474a3a6dd98.png)

max pooling만 진행됐다는 것을 알 수 있다

다음...

![image](https://user-images.githubusercontent.com/78403443/120991302-74114500-c7bc-11eb-8b9c-4ce7d0f6b19d.png)

convolution 됐다는 것을 알 수 있다.

다음...

![image](https://user-images.githubusercontent.com/78403443/120991338-7c698000-c7bc-11eb-9488-6d2784865800.png)

Max pooling으로 사이즈가 줄었다는 것을 알 수 있다 4차원...

![image](https://user-images.githubusercontent.com/78403443/120991389-8b503280-c7bc-11eb-96cc-b45b4dce2912.png)

batch_size가 있기 때문에 1차원이 더 늘어... 4차원이 됐다는 것...

<br/>

![image](https://user-images.githubusercontent.com/78403443/120991435-9905b800-c7bc-11eb-8967-4a4e25b28cf0.png)

out.size 찍어보니 0

<br/>

n하고 out.size() 찍어보자

![image](https://user-images.githubusercontent.com/78403443/120991487-a8850100-c7bc-11eb-9339-a4c11badffd8.png)

batch_size 100을 제외한 나머지 출력... 32x7x7로 1568 나왔다.

<br/>

다음하고 또 size(), shape 찍어본다

![image](https://user-images.githubusercontent.com/78403443/120991551-b63a8680-c7bc-11eb-83f8-379497e5a80c.png)

row 100개... 100x10 나옴... 

정답이 10개 나온다. 

요런게 100개 있는 것

![image](https://user-images.githubusercontent.com/78403443/120991590-bdfa2b00-c7bc-11eb-8440-3d0ad4284b78.png)

인덱스는 100이 [0], 10이 [1] 이다

가장 큰 값의 인덱스 값이 정답이 되는 것이다

최종 출력값 파악 중요!

<br/>

![image](https://user-images.githubusercontent.com/78403443/120991639-c94d5680-c7bc-11eb-8f9b-0f961714697b.png)

확인 다 했으면 q로 끝내고, 다시 주석을 막는다.

![image](https://user-images.githubusercontent.com/78403443/120991840-fac62200-c7bc-11eb-8c9d-aef9259dcf45.png)

<br/>

또 궁금한 부분... 디버깅

![image](https://user-images.githubusercontent.com/78403443/120991897-06b1e400-c7bd-11eb-8f1f-337a7373d33f.png)

예측을 하고 나서도 궁금...

![image](https://user-images.githubusercontent.com/78403443/120991926-0e718880-c7bd-11eb-9ac5-22ce56a28952.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120992237-5ee8e600-c7bd-11eb-9cfd-ee95757a32cd.png)

n으로 다음으로 넘어가서 loss값 보고싶다

![image](https://user-images.githubusercontent.com/78403443/120992278-68724e00-c7bd-11eb-8f3b-57b34fea9d2b.png)

loss값 확인해보았다.

q로 끝내고 주석처리한다.

![image](https://user-images.githubusercontent.com/78403443/120992317-71fbb600-c7bd-11eb-992d-c652002fb9f5.png)

![image](https://user-images.githubusercontent.com/78403443/120992351-7a53f100-c7bd-11eb-85d0-198018137354.png)

<br/>

마지막 셀에 와서 size찍어본다

![image](https://user-images.githubusercontent.com/78403443/120992397-86d84980-c7bd-11eb-8115-87e9060d9468.png)

확인

<br/>

numpy, matplotlib 추가

<br/>

height, width 사이즈 확인

![image](https://user-images.githubusercontent.com/78403443/120992815-edf5fe00-c7bd-11eb-8622-432b2bac304d.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120992953-0c5bf980-c7be-11eb-844f-e0960926830c.png)

image show하기 전에 이 과정 해줘야한다.

![image](https://user-images.githubusercontent.com/78403443/120993128-37dee400-c7be-11eb-8b11-c0361a3ad57d.png)

<br/>

for로 한번 돌려본다

![image](https://user-images.githubusercontent.com/78403443/120993187-43caa600-c7be-11eb-8935-ad9b27d4701d.png)

예측값 뽑아보니 정말 헷갈리는 한 두개 빼고 다 잘 예측값을 뽑아냈다 (그게 정상)

![다운로드 (1)](https://user-images.githubusercontent.com/78403443/120993584-a328b600-c7be-11eb-80a8-150378bd85d3.png)

위 : 잘못 예측한 경우 

아래 : 잘 예측한 경우

![다운로드 (2)](https://user-images.githubusercontent.com/78403443/120993638-b3d92c00-c7be-11eb-84e1-2ec9210fee68.png)

<br/>

---

Validation Test, Test와 Batch_size의 관계

<br/>

Epoch 100

Train Data 4만개

Validation Test Data 1만개

Test Data 1만개

batch_size 100개 라고 가정

Validation Test는 왜 하냐? 어차피 학습 안되지 않나... 왜 합니까? 라는 질문이 석사 과정에서 많이 나옴

<br/>

학습되지 않는데 Validation Test를 Training 데이터와 함께 왜 하느냐?

<br/>

(서론)

4만개의 Training 데이터, Validation Test 데이터 1만개, Test 데이터도 1만개

총 6만개의 데이터

batch_size가 100 이라는건 Training 데이터셋 중에서 100개씩 400번 로드된다는 얘기다. 

Validation 데이터셋도 Epoch에서 같이 된다는건 100개씩 100번 로드된다는 것이다.

Test는 모든 Epoch이 다 돌고나서 한번 돌아간다.

코드를 돌려본 사람만이 알 수 있다.

<br/>

(본론)

![다운로드 (1)](https://user-images.githubusercontent.com/78403443/120993911-f438aa00-c7be-11eb-834b-d24d2021e5de.png)

설명 들어간다. 

첫번째 Batch_size... 100개가 돌아간다. 

그때를 w1이라고 치고, forward연산을 통해서 convolution, max pooling, Relu쓰고 FCN 변환해서 예측

그리고 100개의 Loss가 구해져 나올 것이다. 

만약 Loss가 7이면 이 7에 대한 책임을 묻는다. 이것을 Backward라고 한다.

Backward하게 되면 값이 책임 물은 만큼 수정된다. 이것을 w2라고 한다...

w1이 w2로 업데이트 되고, 그 다음 100개 할 때는 w2로 돌아간다.

그 다음에는 Loss가 좀 줄었다. 여기서 Backward해서 또 업데이트 시켰다... w3

...

이 과정을 400번 반복 (1 Epoch)

이렇게 되면 w400(번째)값이 나올 것이다.

w400에서 Loss를 뽑아봤더니... 예를 들어 3이다. 여기까지가 1 Epoch

1 Epoch의 결과로 나온게 Loss 3

<br/>

그 다음 Validation 으로 간다.

<br/>

w400부터 시작 예를 들어 Loss 3.1 하지만 얘는 backward를 안한다. 

backward를 안한다는 얘기는 w400의 값이 그대로라는 얘기 

두번째 Validation으로 간다. 똑같이 w400을 쓴다. Loss가 2.7 나왔다. 

Backward 안한다. w400 그대로 

세번째... 똑같이 w400을 쓴다. Loss 3.3 

이 과정을 100번 반복 w400(Weight 값은 그대로 가고) 노이즈가 낀 Loss 값이 나올 것이다. 

이 값의 평균을 출력해서 2.9라는 평균값을 갖는다. 여기서 1 Epoch이 끝난다.

<br/>

2 Epoch 간다... 똑같은 과정 반복 (그림 아래)

Training 데이터셋에서 w401~w800까지 진행될 것이다. 

그다음 Validation 간다. 

w800으로 100번 간다. Loss의 평균... 한 2.5 나왔다, 2 Epoch...

<br/>

3 Epoch...

w801~w1200, Loss의 평균 1.8나왔다.

Validation w1200으로 100번 진행, 여기서 만약 평균이 2.7 나왔다.

이때 w1200에 대한 2.7이라는 Loss는 버려버린다. 

그리고 2 Epoch에 나온 2.5로 저장

<br/>

그래서 Validation에선 100개 Loss의 평균 낸 값을 저장하는데 

이전 값으로 Loss값이 크게 나오면 점점점 작은 값으로 저장하는 것... 

이게 Validation이다. Loss값은 점점 작은 값으로 Validation에서 저장하게 된다.

<br/>

(결론)

![image](https://user-images.githubusercontent.com/78403443/120994113-277b3900-c7bf-11eb-9483-d66b2b79391a.png)

만약에, Validation Test가 없다면?

100번 돌렸다 Train이 w400, Loss 9

100번 또 돌려서 w800, Loss 8

w1200 일 때, Loss 6

w2400 일 떄, Loss 7이 나왔다고 하면

Loss는 전반적으로 일정하게 가줘야 하는데, 변동폭이 크게 그려질 수 있다. 

변동폭이 크게 나온 그 상태에서 Test를 돌려버릴 수도 있다.

<br/>

Validation Test는 Loss를 점점 낮게 만들어주고, 가장 낮을 때 Test를 돌릴 수 있도록 도와주는 역할을 한다. 

Loss의 값이 하향곡선을 그리도록 유도하는게 Validation!

그래서, Validation을 쓰게되면 중간에 갑자기 크게 나온 Loss값을 무시해버린다(없애버린다)

Loss가 올라가는 노이즈를 해결~!

<br/>

Loss는 이전보다 낮은 Loss로 Test할 수 있도록 도와주는 역할

<br/>

이것이 Validation Test와 Batch_size의 역할!

이 코드가 나중에 우리가 다룰 코드로 나올 것이다...(CNN 확실히 끝내고) 개발자용에서 

지금까지는 학생이 코드 공부하는 수준으로 나온 것... 

개발자용 코드에서는 재사용성이 나온다.

이때는 코드를 배포시켜서 각자 돌려본다.

<br/>

---

---

**Keras 설치하기**

구글 검색

(출처 : https://like-edp.tistory.com/3)

블로그에 나온 것처럼 가상환경은 만들지 말라... 그렇게 잘 안씀

<br/>

anaconda prompt 열어서

![image](https://user-images.githubusercontent.com/78403443/120994231-45489e00-c7bf-11eb-8b60-71c5cf740c14.png)

conda list 찍었을 때 아래와 같이 나와야 설치된 것

![image](https://user-images.githubusercontent.com/78403443/120994272-4e396f80-c7bf-11eb-88d1-18ab08832f34.png)

<br/>

강사님과 똑같이 파이썬 버전 3.8.10으로 해야한다.

![image](https://user-images.githubusercontent.com/78403443/120994356-5db8b880-c7bf-11eb-87a2-5202e4d34968.png)

확인했다.

<br/>

---

- **D:\encore_jwc\util\PDF\DL\6.Training_Neural_Network.pdf 파일 보기**

<br/>

![image](https://user-images.githubusercontent.com/78403443/120994436-7032f200-c7bf-11eb-9be6-14eb651f61c8.png)

Batch Normalization 무조건 쓴다. 

정확도는 높이고 에러율은 낮춘다.

<br/>

Babysitting... 아기돌보기, 하루종일 손이 많이가고, 눈을 뗄 수 없다... 딥러닝도 마찬가지, 그래서 이런 제목이 붙음

<br/>

이 내용들이 석사과정 한 학기를 꽉 채울 수 있는 내용

너무 깊이 있거나, 어려운 부분은 빼셨다.

<br/>

굉장히 중요한 부분임, 이러한 내용을 가지고 진짜 제대로된 CNN 마무리

<br/>

2단계는

- Custom Dataset + Colab 사용법

  - 여기서 중요한 부분, 재사용성 있는 개발자용 Code로 살펴본다

- segmentation

- Object Detection

  - Apple 개발자가 만든 코드로 살펴본다

코드레벨도 높아지고 내용도 디테일해진다.

<br/>

2단계 들어가기 전 마무리로 위 내용을 다룬다.

<br/>

**Classification**

**앞에 배웠던 내용들 간략 정리**

<br/>

Fully Connected Network는 Fully Connected Layer를 여러개 쌓았다는 뜻

2-layer Neural Network 뜻은 2(개의) Fully Connected Layer 라는 뜻

<br/>

공간정보유지

Computation cost 적게 든다. (부분 연산이므로)

Convolution - ReLU - Max Pooling 계속 반복

특징을 추출해내는 일, 

이것을 충분히 한 다음에 한줄로 쭉 펼친다. 

Fully Connected Layer를 쌓고 Full Connected Network를 만들어서 분류

마지막에 softmax() 함수로 확률값으로 바꿔준다.

<br/>

그게 Fully Connected Network에서 하는 일

예측하고자 하는 갯수만큼 값을 분류하고, 최종적으로 확률값을 나타낸다.

<br/>

Optimizer 그 안에서 각각은 고도이다. 고도 = Loss값

<br/>

Backpropagation

1,2,3,4 이 4개가 분명한 연관이 그려지면서 이해가 되어야 한다.

<br/>

Optimizer는 하산법

Loss는 학습을 잘했는지 못했는지(예측을 잘했는지 못했는지) 정량화시킨 값, 고도

고도가 낮아질 수록 Loss가 줄어드는 모양새...

Backpropagation은 가장 가파르게 하산하는 방법

(딥러닝적으로, 가장 가파른 기울기를 찾아내는 것, Cost.. Loss가 가장 최소가 되는 Weight값을 찾는 알고리즘, 이때 실제로 편미분이 쓰인다)

<br/>

Optimization의 방법이 Gradient Descent, 그 안에 종류가 Adam, SGD

Adam, SGD 이 둘의 차이점..?

[아래 이미지 출처 https://nittaku.tistory.com/271]

![9977E1365B627B470F](https://user-images.githubusercontent.com/78403443/120994853-dc155a80-c7bf-11eb-82d3-43284934d57e.gif)

sdg는 느림... 

adam은 빠르게 내려옴

<br/>

2번 Data Augmentation

transforms 모듈이 Data 변형(Data Augmentation 기법)

Random.Brightness() 함수

Random.Rotation() 함수

Random.Crop() 함수

Shuffle (순서섞기)

<br/>

변형해서 학습하게 되면 새로운 데이터로 인식...

학습데이터가 많아자면 학습효과가 늘어나는 효과 발생

3번 Deep Neural Network Training with Training with Training Data, Validation Data... 학습단계

<br/>

빨간박스 친 부분, 빨간박스 친 이유? Looping이 된다... Batch_size = 100 지정하면 100개씩 로딩, 100개씩 결과출력

<br/>

4번 5번은 1,2,3번에서 괜찮은 성능 나오면 하지 않음. 

4번 Deep Neural Network Testing with Testing Data는 정답이 있는 테스트

5번은 Inference with verified Deep Neural Network는 정답이 없는 Inference 최종 테스트(수능?)

<br/>

지금부터 본격적으로 들어간다

현실적인 이야기...

동일한 Network이더라도 어떻게 학습하냐(학습시키냐)에 따라서 

Acc 80% 나올 수도 있고, 95% 나올 수도 있다.

이 부분은 나중에 인공지능 개발자가 됐을 때 다시 한번 꼭 정리해봐야하는 부분이다.

<br/>

여기서부터는 중요한 내용만 짚는것...

<br/>

인간신경망에서 나온 얘기였음

가지돌기를 통해서 자극 들어온다. 

각각 신념을 곱하고 영역에 있는 공통적인 값을 더해서 출력하기 전에

활성화 함수에 의해서 걸러진 값이 출력이 된다는 얘기였다.

<br/>

Activation 함수를 왜 쓰는가?

① threshold(역치값) 큰 값과 작은 값 거르기 위해서(?)

그리고...

②

뉴런은 계속 연결되어있다.. 

또 다른 뉴런의 입력 출력, 또 다른 뉴런의 입력 출력 

이런식으로 또다른 뉴런의 출력은 또다른 뉴런의 입력이 되고... 

결론적으로는 선형의 한계를 극복해야... 선형을 아무리 쌓아도 결국 선형이다.

그래서,

선형의 한계를 극복하기 위해서 Activation 함수를 넣는 것이다.

그럼 이런 형태를 띄게 된다.

<br/>

선형 + 비선형 + 선형 + 비선형 

이렇게 선형을 분리시킨 것이다.

그러면 데이터를 좀 더 풍부하게 학습시킬 수 있는 결론이 나온다.

<br/>

비선형은 곡선이거나 꺾은선 파형을 가진다.

아래와 같이...

<br/>

여기서 Alex Net 모델이 나오기 전까지는 Sigmoid나 tanh를 많이 썼다. 

생명체와 흡사한 것은 Sigmoid

둘 차이는 0~1사이의 값, -1~1사이의 값을 가진다는 점

2012년 Alex Net 모델이 나오고 나서는 ReLU를 많이 쓴다.

<br/>

이렇게 쓰고...

Accuracy를 96 → 97, 98% 좀 더 올리고 싶다. 

오른쪽에 있는 3개의 방법을 썼더니... 올라갔다. 

왜(?) 몰라.. 그냥 써보니까 올라갔다 (이게 제일 정직한 말)

정확도를 조금 더 올리고 싶으면 우측 3개의 함수를 하나씩 써봐야 한다.

<br/>

그리고, 

Sigmoid함수를 Activation함수로 쓴다고 했나 안했나? 안쓴다.

지금은 무조건 ReLU를 쓴다. 머리에 박아 넣어라...

<br/>

그런데... Sigmoid를 쓸 때가 있다. (Activation으로는 아니지만) 

언제 쓰나? 

출력값이 하나인 경우

<br/>

정리 ::

딥러닝에서는 Activation Function으로 Sigmoid()함수 안쓰고 ReLU()함수 사용한다.

그러나, Sigmoid() 함수를 사용하는 경우가 있다. Activation용도는 아니다!

<br/>

어떨때?

ex1) 딥러닝으로 학습하고나서 Training모델에 입력값을 넣으면 예측값이 나온다.

이 예측값이 예를 들어 3, 7, 9가 나왔다. 

이중에 가장 큰값은 9이다. 인덱스가 0, 1, 2다. 

0은 dog, 1 frog, 2 cat이라고 가정했을 때 cat으로 예측한 것이다.

모델이 어느정도 잘 예측한건지 확실하게 알 수 있는 값은 아니기 때문에 softmax를 적용한다.

softmax 는

- 첫번째, 값을 극대화 시키고
- 두번째, 확률값으로 나타낸다.
- 내부로직 :: e9 / e3 + e7 + e9 가 되겠다

<br/>

그런데,

ex2) 예측 값이 값 하나다... 하나만 출력하는 경우? 뭘 의미?

값이 하나라는 거는 고양이 이거나 / 고양이 아니거나... 이것

암이거나 / 암이 아니거나

악성이거나 / 악성이 아니거나

이것을, 바이너리 문제라고 한다. 바이너리 문제...0, 1

그러나 이것은 0... 하나를 얘기한다.

<br/>

바이너리 문제인데 classification 예측값이 하나다. 

그 하나 나온 예측값이 3이면 고양이 일까, 아닐까? 특정할 수 없다.

그럴 떄는 기준값이 필요하다. 예를 들면 음수 / 양수 0.5 기준으로 한다던지...

그리고, 이 기준값이 threshold 값이다.

<br/>

그때 Sigmoid() 함수를 쓴다

![image](https://user-images.githubusercontent.com/78403443/120995581-7d9cac00-c7c0-11eb-9831-19a93efd0e04.png)

Sigmoid() 함수는 파형이 0에서 1사이의 값을 가진다.

근데 지금 3이라는 값이 나왔다.

<br/>

언제 제일 애매한 값이 나올까? 0일 때, 0.5...

0.5 == 가장 애매한 값

결론 :: 

바이너리 문제이고 출력값이 하나일 때는 softmax를 쓰지말고,

이걸 sigmoid로 바꿔서 사용해야한다.

<br/>

이때 중요한게... 기준값을 뭘로 정하는가를 잘 봐야한다. 

기준값은 0과 1 사이인데 기준값을 0.5로 잡는지, 음수로 잡는지 이걸 잘 봐야한다. 

(threshold가 가장 중요한데, threshold는 나중에 깊게 설명)

<br/>

**활성화 함수로는 ReLU()를 쓰는데**

**가끔가다가 Sigmoid 함수가 출력 앞단에서 사용될 때가 있다!**

**이때는, 바이너리 문제이고 출력값이 1(하나)구나 라는 것을 꼭 기억하기!!!**

**그때 softmax 대신에 쓰이는 것이다~!**

<br/>

다음...

결론 : 

Activation 쓸 때는 ReLU 써라

Sigmoid 쓰지마라

Sigmoid 쓰일 때는 Binary 문제일 경우 쓰이긴 한다라는거 아까까지 설명함...

<br/>

Data Preprocessing (데이터 전처리)

<br/>

값이 0~255인 경우...

이런 파형을... 

Data Variance하고, High Frequency 하다고 한다. 

이런 경우는 학습이 잘 안된다. 결론적으로 Overfitting 발생

<br/>

그래서 Network에 들어갈 때 값의 범위를 0~1로 정해줬다.

(반드시 스케일링해서 써라...권장)

전처리에서 무조건 ToTensor() 들어간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120995978-e08e4300-c7c0-11eb-8924-67630a78686f.png)

Deep Learning의 3 part

1. Pre Processing(전처리) -- 75% 비중
2. Deep Learning -- 20%
3. Post Processing(후처리) -- 5%

딥러닝은 크게 세 파트로 이루어져있다고 보면된다.

<br/>

Deep Learning은 모델 설계해서 weight값 뽑아내는 과정

후처리는 깔끔하게 정제, 시각화 작업

<br/>

제일 중요한게 Pre Processing...

① 값을 스케일링 0~1로 → Network

② Data Augmentation(데이터 변형) transforms.brightness, rotation, crop

③ 데이터 로딩할 때마다 Shuffle(섞기)해줘야

④ "Data Cleansing" (데이터 검수) : 수많은 데이터가 들어오면 라벨을 다 붙여야한다. 잘못된 라벨링 검수

(깨끗한 작업을 위해서 라벨링 작업을 일일히 확인... 사람이 일일히 확인(노가다)

⑤ 데이터의 비율 맞춰줌 : 8만개 데이터가 있다. dog, 6만개 데이터 cat, 5천개 데이터... 학습이 안된다.

⑥ 어떤 데이터냐에 따라서 도메인 전문지식 or 전문가 필요

<br/>

이 작업 순서로 간트차트를 만든다. 

앞에 말한 순서대로 딥러닝 작업 순서도를 정한다.

![image](https://user-images.githubusercontent.com/78403443/120996139-06b3e300-c7c1-11eb-9e21-b613e712e6dc.png)

Data Augmentation(데이터 변형)으로 예를 들면,

밝기 조절을 안했다가 추가를 한다... 밝기 조절해서 모델을 돌렸더니 성능이 잘 안나온다. 

그러면 다시 모델로 돌아가서 Brightness 값을 높게 혹은 낮게 조절하던지, 아예 빼버리던지 해야한다.

<br/>

딥러닝 작업은 크게 세 가지있는데, 각 과정들이 중첩되서 진행된다는 점 명심...

<br/>

딥러닝 인재? = 도메인 전문가 + 딥러닝 전문가 (예, 의사 + 딥러닝)

이런 케이스는 사실 드물다.

그래서, 특수한 데이터셋인 경우에 인공지능이나 데이터분석가나, 딥러닝 공부한 친구 뽑아서

도메인지식을 입힌다. (가성비 좋다) 이렇게 돌아간다...

<br/>

Pre Processing 여기까지 설명함.

<br/>

**Batch Normalization :: 딥러닝의 Superman**

상당히 중요한 내용

Batch Normalization은 모든 레이어에 반드시 들어가야한다. (안들어가면 안된다, 별명이 슈퍼맨)

→ 성능이 좋아진다.

<br/>

VGG16의 구조

![다운로드](https://user-images.githubusercontent.com/78403443/120996406-4084e980-c7c1-11eb-8768-06662a7f8b36.png)

(이미지 출처 : [https://bskyvision.com/504](https://bskyvision.com/504)))

VGG16은 Layer가 16개라는 의미

1. 첫번째 질문,

   연산이 진행된다는 얘기는 속성값에 Weight값이 곱해지고 bias가 더해진다는 얘기(속성 * weight + b)

   값이 커지나 작아지나? 이미지는 점점 작아진다. 거듭할수록 값은 커질까?

   굉장히 중요한 중요도 높은 것은 레이어를 거칠수록 커진다. 

   중요도가 작은 픽셀일 경우에는 점점 작아져서 0에 가까워진다.

   값이 격차가 커져서 variance가 커진다. 

   차이가 커져서 Overfitting이 커진다.

   <br/>

   그래서 Batch_Normalization은 뭐냐면 레이어를 거쳐서 나온 값의 숨을 죽인다. 

   큰 값은 값을 내리고 작은 값은 값을 올려준다. 레이어마다마다 한다. 

   격차가 계속계속 벌어지니까 격차를 좁혀주는 것이다.

   이것이 Batch_Normalization 하는 일이다.

<br/>

2. 네트워크의 각 레이어를 거칠 때마다 Input값의 Variance가 달라지는 현상 :: Distribution이 커진다

   Normalization을 한국어로 번역하면 '정규화' 이다.

   공식 :: X-mean / std

   ![image](https://user-images.githubusercontent.com/78403443/120996771-98235500-c7c1-11eb-8dda-dc0b6e934488.png)

   std에 스케일링이 들어간다.

   이 공식 알아둬야한다.

   <br/>

   Batch_Normalization

   ① X를 평균으로 빼고 → X-mean

   ② 분산으로 나눈다

   분산이 커진다는 얘기는 중요한 값과 중요하지 않은 값 이게 점점 차이가 커진다

   여기서 먼저 ①번이 진행된다.

   X의 평균만큼 뺀다.

   분산으로 나눈다는 얘기는 255로 나눈다는 얘기랑 같다.

   255만큼 분산으로 나누면 격자가 좁아진다

   그러면 그림이 분홍색 ②번과 그림과 같이 바뀐다

   ![image](https://user-images.githubusercontent.com/78403443/120996868-affad900-c7c1-11eb-9df1-3f839901238f.png)

   이게 Normalization이다.

   <br/>

   근데, 앞에 Batch가 붙는다. 

   그 이유는 뭐냐면... 만약에 1 Epoch에 batch_size = 100이라면 100개씩 로드할 것이다.

   네트워크에 들어가서 한 Layer만 거치면 Wx+b연산에 의해서 값의 Variance가 굉장히 커져버릴 것이다.

   Layer를 거쳐갈 때마다 더 커진다. 모든 Layer마다 Normalization을 하는 것이다.

   그래서, 값이 더 커지면 다시 줄여주고, 다시 값이 커지면 다시 줄여주고 이것을 계속해서 반복한다고해서

   마치 batch_size 로딩할 때마다 계속해서 바꾸기 때문에 batch가 붙었다. 

   레이어마다 해준다!!

   ![image](https://user-images.githubusercontent.com/78403443/120996988-c99c2080-c7c1-11eb-8499-08c24cda7f9c.png)

   <br/>

   이게 레이어 하나다... (아래)

   ![image](https://user-images.githubusercontent.com/78403443/120997055-dde01d80-c7c1-11eb-8ba1-bbdedf301053.png)

   여기에 BatchNormalize(32)해주면

   ![image](https://user-images.githubusercontent.com/78403443/120997130-ec2e3980-c7c1-11eb-8b4a-229bcf2d8580.png)

   Batch_size 마다마다 반복된다.

   스케일링은 당연히 해야된다. 당연히 하더라도 또다시 연산이 진행되니까 거기서 어쨋든

   값이 계속 차이가 나기 때문에 batch_normalization 해줘야 하는 것이다.

   ![image](https://user-images.githubusercontent.com/78403443/120997226-fc461900-c7c1-11eb-97a8-f215f620a4a5.png)

   분산율은 데이터가 퍼져있는 정도를 말한다.

   이때는 분산율이 0이다.

   아래는 분산율이 엄청 높은 경우

   분산율 크게 만들면 안된다는 얘기...

   분산을 줄여주는데 중심축 폭도 작게 (왼쪽으로)가져가는 것

<br/>

**Batch_normalization을 얼마로 넣어줄 때가 가장 좋은지에 대한 연구...**

Batch_normzalization은 16이상으로 하라는 얘기

2, 4, 8로 하면 데이터 평균내기에 부족하다는 얘기이다.

이렇게 작게하면 노이즈 값이 너무 크고, 너무 많이 하면 Computation cost가 높은 문제가 발생한다.

그렇기 때문에, Network에서 Batch_size 지정하는거나, Batch_normalization 잘하는건 중요하다.

<br/>

결론 :: Batch_normalization은 32 주는게 좋다

<br/>

모델설계는 주로 표로 하는데 hidden layer 개수, input, output 레이어, stride, max pooling... 이런거

다 직접 설계해야하는데, 잘 설계해야한다.

<br/>

(내용 pdf파일 저작권으로 인해 캡쳐와 함께 내용 생략)

...

<br/>

결론 ::

강사님이 말 안하신 upsampling method, 나중에 segmentation때 나온다

over-sampling ratio, 몰라도된다!

<br/>

각각 최적의 하이퍼 파라미터 옵션 값... 다시 이전 노트와 함께보기
