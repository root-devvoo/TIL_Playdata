1. Paperswithcode(사이트)

   - 정확도↑, 모델
   - 오픈된 DataSet에 대한 Accuracy(정확도) 정보 제공해주는 사이트

2. 업계용어

   - 학사 :: (잘 나올 때) Accuracy 92%
   - 석사 95%
   - 박사 97%
   - 특히, 석사에서 박사 정도의 정확도 올리기 굉장히 어렵다.
   - 방법을 점점 달리해서 정확도를 올림
   - 앞으로 일반인 관점에서 Accuracy 보면 안된다. (정확도 1%, 2% 올리는건 큰 차이... 방법론 등등)
   - 80% 정확도 나오는거 당연한거 아니다 (고도의 기술과 지식을 필요로 한다는 얘기)

<br/>

---

- **2.Linear_Classification.pdf 파일 보기**

<br/>

**Linear Classification**

<br/>

행렬연산

![image](https://user-images.githubusercontent.com/78403443/120293461-429e0280-c300-11eb-80a4-5d40869e940b.png)

위 행렬연산 설명 예시를 보자.

입력되는 입력값 x의 데이터는 3072x1

최종출력값(y 혹은f(x,W)) 은 10x1 (입력값(x)과 출력값(y 혹은 f(x,W))은 우리가 먼저 알 수 있다, 지정되있으니까)

그러면 W(Weight, 중요도)값은 10x3072가 나와야한다.

모든 3072개 속성 다 더한 가중치 + bias 값을 10x1 출력값으로 나타냄

그러면 b(bias)는 10x1, 출력값이 10x1이니까

최종적으로 출력된 10x1 에서 제일 높은 값을 가지는 인덱스의 데이터 가중치가 최종 예측한 결과가 된다.

<br/>

극대화... 학습에 있어서 굉장히 중요하다

(명확한 예측결과값이 나와야 한다)

<br/>

예측값은 Normalization + Exponential로 만들어야 한다. 

(Normalization :: 확률값인 %(퍼센트)로 나타낼 수 있어야한다.

Exponential :: 극대화... 애매하지 않은... 명확한 예측값이 나와야한다.)

<br/>

**Classification Loss Function**

Loss Fuction은 Cost Fuction이라고도 불리는데

해당 모델이 얼마나 예측을 잘했는지를 정량적으로 나타내는 함수

값이 0에 가까울수록 예측을 잘한 모델

밥그릇 함수로 주로 표현

<br/>

Softmax Loss

Regularization 이 두개는 많이 쓰이지만

Hinge Loss는 많이 쓰이지 않는다.

<br/>

Hinge Fuction의 문제점

잘한 건 잘했다. 못한 것은 못했다는 걸 나타내지 못한다.

(Normalization + Exponential 안됨)

<br/>

Hinge Function의 문제를 보완한 것이 Softmax Function이다. 

Softmax Function 어떻게 돌아가는지 보도록 한다.

(Hinge Function의 문제점을 보완한 것)

<br/>

Softmax Function 설명

![image](https://user-images.githubusercontent.com/78403443/120294107-d7086500-c300-11eb-92f1-44a9309b53c4.png)

y=2.7^x 그래프 (구글 검색)

![image](https://user-images.githubusercontent.com/78403443/120294144-e091cd00-c300-11eb-8e71-7dcac776a038.png)

그래프는 파형을 보는게 중요하다. (외우기)

값의 간극을 늘리는(극대화하는) 트릭을 준다는 것을 알 수 있다.

![image](https://user-images.githubusercontent.com/78403443/120294191-edaebc00-c300-11eb-881b-6f2771f8e93b.png)

간극을 늘려주는 e라는 것을 쓴다는 것을 알면 된다.

값의 간극을 늘려준 것에 Normalization 해주는 것...

<br/>

간극도 벌렸고, Normalization도 취했다. 

애매하게 40, 30, 30%로 결과 나온 것이 58%, 26%, 26%로 나왔다.

이것이 Softmax Function이다! (공식은 위 이미지 상단제목 우측에 있음)

<br/>

그림으로 Regularization 설명...

![image](https://user-images.githubusercontent.com/78403443/120294482-30709400-c301-11eb-94f2-0bb50ced1bc2.png)

위 그림으로 설명하면...

딥러닝 모델에 의한 전체 Loss값인 0.3에

Regularization 결과까지 추가한 것이 Full Loss이다.

<br/>

---

**코드로 실습**

- **D:\encore_jwc\py_workspace\04_DeepLearning 폴더 01_Deep_NN.ipynb 파일 보기**

<br/>

![image](https://user-images.githubusercontent.com/78403443/120294634-5a29bb00-c301-11eb-9b76-5a6dc0bc9f9a.png)

![image](https://user-images.githubusercontent.com/78403443/120294662-631a8c80-c301-11eb-937a-77be769b2a3d.png)

빨간색 사각형 표시된 부분 처럼 하면 값을 지정해서 텐서를 하나 생성하는 것

윗 부분은 랜덤한 값으로 넣는 것

![image](https://user-images.githubusercontent.com/78403443/120294701-6ca3f480-c301-11eb-886e-ee60364fce21.png)

간단하게 살펴보기 위해 예측값을 그냥 준 것... (학습 시킨게 아님)

<br/>

예측값에서 정답을 뺀게 Loss

<br/>

![image](https://user-images.githubusercontent.com/78403443/120294750-7b8aa700-c301-11eb-9174-457e69d459e1.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120294799-86453c00-c301-11eb-9c82-001d90b88797.png)

loss에 backward() 하면 책임을 묻는 것이다

BackPropagation 경사하강한다. 

![image](https://user-images.githubusercontent.com/78403443/120294837-90673a80-c301-11eb-92dc-6f0ba368d27d.png)

x는 미분적용 된 것이지만 예측값은 미분적용이 안되서 None이 나옴

<br/>

**Create Tensor ....Using NeuralNet**

![image](https://user-images.githubusercontent.com/78403443/120294893-9d842980-c301-11eb-872a-2999c0957a82.png)

w는 3행 2열 나와야하고, b(bias)는 10행 2열 나와야한다.

<br/>

3, 2해야 결과가 제대로 나올 것이다.

<br/>

weight과 bias가 출력되었다.

![image](https://user-images.githubusercontent.com/78403443/120294961-ab39af00-c301-11eb-90e9-fa20db371afd.png)

그러나 원래 나와야 할 형태와 다른 형태로 나왔다. 

w는 3x2로 나와야할게 2x3으로 나왔고

b는 10x2로 나와야할게 1x2로 나왔다

<br/>

![image](https://user-images.githubusercontent.com/78403443/120295016-b68cda80-c301-11eb-88dc-75e97caf452d.png)

나중에 모델학습할 때 얘(parameters()함수)를 쓸거다. 알아두기...

객체가 출력됨;;

![image](https://user-images.githubusercontent.com/78403443/120295057-c0164280-c301-11eb-8863-e2d58fb71808.png)

SGD는 Stochastic Gradient Descent

lr은 learning rate

<br/>

여기서 미분을 적용해서 기울기를 조금 수정해주면 loss가 조금 줄어둔다.

이렇게 기울기를 줄여주는게 BackPropagation 이라는 것이다.

<br/>

기울기를 줄인다는건 Backward를 한다는 얘기고

Backward하면 loss값이 줄어든다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120295106-cdcbc800-c301-11eb-876b-4f1bd0e24215.png)

위 출력된 값을 사용해서 기울기를 적용한다.

<br/>

BackPropagation을 진행한 뒤...

![image](https://user-images.githubusercontent.com/78403443/120295157-d91ef380-c301-11eb-9e39-aea13ac745e8.png)

줄어들었다. (조금 줄은거라고 생각하면 안된다!)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120295196-e4721f00-c301-11eb-8f6d-755a36fec274.png)

W(weight) 값은 랜덤하게 주어진다.

랜덤하게 주는게 학습효과도 높기 때문에(학자들의 연구결과)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120295291-f94eb280-c301-11eb-8c24-9590d952206b.png)

책임을 물을 때는 미분에 대한 공식을 적용해서 기울기를 조정, 적용하는게

책임을 묻는 것이다.

이걸 계속 반복하게 되면 전체적으로는 loss가 하강하면서 0에 가깝게 된다는 것!

<br/>

---

---

- **DL/3.Backpropagation.pdf 파일 보기**

이 4개에 대한 용어정리 명확하게 해야한다. 

Neural Network의 가장 기본적인 전제가 되는 개념, 용어

1. Optimization
2. Gradient Descent
3. Backpropagation
4. Loss Function

<br/>

Neural Network 

(Hidden Layer는 입력과 출력 사이에 있는 보이지 않는 Layer)

    ① RNN

      CNN : Convolution

      DNN : 

      ANN : Hidden Layer가 하나있으면 ANN

<br/>

    ② FCN : Fully Connected Layer

<br/>

Neural Network(N.N)는 크게 두개로 나뉜다.

<br/>

Optimization은 어떻게 하산할지를 정하는 것 (하산하는 방법을 정하는 것)

<br/>

고도는 Cost, Loss를 의미

위치는 어디가 되던지 간에 각자의 방향으로 내려와야한다.

(방향이 달라진다, 뭐에 따라서 방향이 달라지는지는 나중에 볼 것임)

잘못내려오면 약간 파여있는 완만한 곳을 평지로 착각할 수 있다.

그런 곳을 Local Minimum이라고 한다.

0자리인 평지는 Global Minimum이라고 한다.

<br/>

Local Minimum에 빠지지 않고, Global Minimum까지 잘 내려오도록 

Optimization 하는 것은 그리 쉽지 않다. 

내부적으로 수학적인 알고리즘이 복잡하게 돌아가기 때문

<br/>

아까 코드로 실습하면서 쓴 SGD 방법은 Gradient Descent 방법으로 한 것이다. 

(자세히는 나중에 설명)

SGD 방법은 Optimization의 한 방법이다. 하강하는 많은 방법들 중에 하나다.

<br/>

세타0, 세타1

두 가지의 Linear가 돌고있다. (Linear 2개라는 뜻은 블럭을 2개 쌓았다는 뜻)

Linear의 공식 W1 * x+b1 = 세타0 으로 표현함

세타1은 x가 세타0이 되기 때문에, W2(W1 * x+b1)+b2 = 쎄타1이 된다.

<br/>

연산을 쌓고 쌓고 쌓고 하다보면 세타값이 올라가면서 굉장히 깊은 Linear가 된다.

쎄타는 레고블럭을 하나씩 쌓는다고 생각하면 된다.

여기서 질문... 중요한 지점

<br/>

W4 x + b4 랑 세타3에서 +b4를 뺀 나머지랑 같은 이유가 뭔가?

동일한 Block 하나라는 한계점...

그것은 선형의 한계를 말함!, 디테일하게 데이터를 표현할 수가 없다는 얘기

직선의 한계...

<br/>

데이터를 다양하게 풍부하게 표현하려면 비선형이 나와야한다.

곡선의 중요성...

(나중에 다시 나온다)

어쨋든, SGD방법으로 하산을 한 것이다.

<br/>

<br/>

하산하는 방법이 Optimization인데 

Optimization에는 크게 3가지 방법이 있다.

<br/>

(1) Random Search

눈을 가리고 끝까지 내려가본다, 수천번 반복, 그리고 그 중에서 가장 잘 내려간 방법을 선택

(무식한 방법)

'눈을 가렸다'를 딥러닝 표현으로 바꾸면 'Weight에 무작위 값을 넣었다'는 뜻

Loss 최소값 선택...

<br/>

굉장히 많이 내려가봐야하고, 수천번 반복해야된다는 점에서 무식한 방법이다.

<br/>

(2) Random Local Search

내려가려고 발을 살짝 내딛어봤을 때 진행방향이 고도가 더 낮은 방향일수도 있고, 반대로 높은 방향일 수도 있다.

이때, 진행방향을 봤을 때 고도가 내려가는 방향이면 진행하고, 

고도가 내려가는 방향이 아니면 거기서 멈춘다.

그리고 발을 다시 살짝 다른 방향으로 내딛어서 진행방향을 살피는 것

<br/>

Weight를 무작위로 추출했을 때 여러번 돌려서 내려가는 진행방향이 맞을 때 내려간다.

하산의 방향을 따라간다

<br/>

(3) Gradient Descent

핵심은 가장 가파르게 Loss를 감소하는 W 방향을 수학적으로 계산 한 뒤, 해당 방향으로 이동한다는 것

<br/>

만약 내가 서 있다. 방향이 있다. 쭉 둘러봤을 때 경사가 가장 가파른 방향을 계산한다.

경사가 가장 가파른 곳으로 내려간다.

<br/>

Random Local Search와 큰 차이가 어디서 발생하는가?

- 하산 방향뿐만 아니라 최적의 고도를 찾는 계산법이 있다는 점 (최적의 고도 == 가장 가파르다)

- - 하산은 가장 가파르게 해야한다.

<br/>

하산법으로 설명하게 되면 Gradient Descent는 가장 가파른 경사를 찾아서 내려가는 Optimization 방법

딥러닝 적으로 표현하면 핵심은 가장 가파르게 Loss를 감소하는 W 방향을 수학적으로 계산 한 뒤, 해당 방향으로 이동

수학적으로 계산이라는 얘기는

미분 (W → 1개)

편미분 (W → 多)

그리고, 이게 BackPropagation 계산이 편미분...

backward() 함수를 이용

<br/>

결론 :: BackPropagation은 Gradient Descent 방법 중에 하나로 편미분이 적용된다.

BackPropagation : 가장 가파르게 loss(고도)를 감소하는 W 값을 찾아내는 계산법 → 편미분 적용

<br/>

Random Search

Random Local Search에 비해서 Trial Error가 없다!

<br/>

[아래 이미지 출처 https://nittaku.tistory.com/271]

![9977E1365B627B470F](https://user-images.githubusercontent.com/78403443/120295920-93165f80-c302-11eb-9785-1d74ea712035.gif)

(빨간색)SGD : 느리다. 평지 근처에 와서도 정확하게 별을 찾는다

(파란색)Adagrad : 굉장히 빠르다. 빠르게 하산, 별의 정확한 지점 노이즈가 많이 발생(심하게 흔들리는걸 보면 알 수 있다)

<br/>

아무거나 써도 되긴하지만...

Epoch(학습 횟수) 앞부분의 optimization과 뒷부분의 optimization때 섞어서 쓸 수 있다.

학습의 전반부는 빠르니까 Adagrad쓰고, 뒤에는 꼼꼼하고 정확하게 할 수 있는 SGD를 쓰는 식으로

<br/>

![image](https://user-images.githubusercontent.com/78403443/120296010-a9bcb680-c302-11eb-8ed7-e54f010744b4.png)

dy/dx :: y를 x로 미분한 값을 이렇게 표시한다.

y를 x로 미분했다, 이게 내포하는 의미?

x가 변함에 따라서 y가 얼마나 변하는가를 내포

<br/>

Loss가 크다 → Weight의 책임이 많다(크다) → 체벌(Punish)을 가해야한다 코드로 ::  Weight 값 변경이 大

Loss가 작다 → Weight의 책임이 적다 → 칭찬을 해야한다 코드로 ::   Weight 값 변경이 작다

결국 값 수정 해야된다는 얘기

<br/>

보정이 작다는 얘기, 값의 변화가 작다

보정이 크다, 값의 변화가 크다(?)

<br/>

<br/>

Learning Rate와 미분 간의 어떤 관계가 있는지 설명

![image](https://user-images.githubusercontent.com/78403443/120296077-ba6d2c80-c302-11eb-872f-603c825bb78f.png)

기울기가 양수면 왼쪽으로 움직인다.

음수면 오른쪽

<br/>

기울기 값에 따라서 

① 하산하는 방향이 결정된다.

<br/>

기울기가 작으면 천천히 내려온다.

기울기가 값이 크게 되면 가파르게 내려온다.

Learning Rate와 상관없이 기울기가 가지고 있는 자체의 값에 따라서

② 하산하는 속도가 달라진다.

기울기가 완만하면 속도가 느려진다. 이와 동시에 Learning Rate도 같이 줘야한다.

그래야 꼼꼼하게 0지점을 찾을 수 있다.

<br/>

속도가 느려진다는거는 평지지점에 거의 왔다는 얘긴데 이때 Learning Rate도 같이 속도를 줄여줘야한다.

<br/>

100% 아니지만 일반적으로 관례상 연구결과에 따라 권장하는 값이 이와 같다...

SGD의 경우 1e-2 (=0.1)

Adam의 경우 1e-4 (=0.001)

Learning rate 1/2 decay / n epoch

<br/>

(p - y) * (x) 에 대한 설명 그림으로...

![image](https://user-images.githubusercontent.com/78403443/120296472-1e8ff080-c303-11eb-8a90-4b14944de210.png)

다 같은 의미이다.

![image](https://user-images.githubusercontent.com/78403443/120296502-28195880-c303-11eb-9a31-d7fe97f4539c.png)

고양이 사진이 있다고 가정

 4082개의 픽셀값(X)이 속성이 된다.

그리고, W1 * X + b1 연산에 의해서 Y1 예측값이 2086개 나온다

W2 * Y1 +b2 연산에 의해서 Y2가 나온다. 

그리고 Output(예측값)이 나온다.  예측값은 카테고리별로 나온다. 

만약에 카테고리가 3개라면 예측값은 3개가 나와야한다.

그런데 그 전에 무슨 함수를 써야하나?

Exponential e에 32승 곱하고

e 25승 곱하고

Normalization 한다. 

이게 Softmax 함수!!! Softmax 함수 써야한다!

<br/>

여기까지 해야 딥러닝을 통한 최종 예측결과 나오는 것

<br/>

예측값이 나온 다음에 어떤 작업이 진행되는가?

오차보정...

방법은 여러가지 있다. 

- -log(예측결과값) (여기 경우엔 0.8...)

<br/>

Forward Propagation에서는

1. 입력
2. Model실행, Linear Regression(W * b)으로 학습 시킴
3. 예측값 → Softmax 실행시켜서 확률갑승로 바꿔준다
4. Loss를 구함

이것이 Forward 과정의 끝이다! 

그렇다면, Propagation에서 Loss 결과가 도출된다!!!

이것이 Forward 방향에서 진행되는 핵심적인 과정

Forward의 결론은 Loss!

<br/>

Forward는 미분의 ''미'' 자도 상관없다

![image](https://user-images.githubusercontent.com/78403443/120296649-4da66200-c303-11eb-92a9-2cd43d504130.png)

이것은 Back Propagation, 미분.. Forward랑은 상관없다

따라서, 미분이 적용된다는 것은 Forward에서 나온 Loss값을 보고 Weight 값을 보정한다는 얘기(두번째부터)

이걸 반복(아래 그림 과정 반복)

![image](https://user-images.githubusercontent.com/78403443/120296693-572fca00-c303-11eb-92d2-1d5284b0708f.png)

학습이 진행되는 방향은? backward에서 진행된다!

<br/>

---

**코드로 실습**

<br/>

- **02_Deep_NN.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/120296797-729ad500-c303-11eb-9727-c58ab071caa1.png)

![image](https://user-images.githubusercontent.com/78403443/120296823-7b8ba680-c303-11eb-80a4-3172782128ac.png)

임의로 데이터 세팅

<br/>

![image](https://user-images.githubusercontent.com/78403443/120296921-91996700-c303-11eb-8131-f42ffa1a5061.png)

5번 Loss에 대한 책임을 W에게 묻는다는건 델타wL 적용, 즉, 미분을 적용한다는 얘기

![image](https://user-images.githubusercontent.com/78403443/120296969-9d852900-c303-11eb-8ccb-9153321d3e37.png)

최종

<br/>

![image](https://user-images.githubusercontent.com/78403443/120297047-ac6bdb80-c303-11eb-88f2-9583ac31dc2b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120297074-b55cad00-c303-11eb-9aa7-3f3254c72cb1.png)

<br/>

**Train Model**

![image](https://user-images.githubusercontent.com/78403443/120297138-c5748c80-c303-11eb-8df3-ca2396223238.png)

Forwarding에 있어서 loss가 나오면 Forwarding이 끝난것이다. 

나온 loss값을 바탕으로 backward 진행해야한다.

<br/>

optimization을 반드시 초기화 하고 Backward해줘야한다.

<br/>

item써주면 값만 이쁘게 뽑힌다.

<br/>

**Plot the Graph**

![image](https://user-images.githubusercontent.com/78403443/120297199-d4f3d580-c303-11eb-8935-9e654fea122e.png)

여기서 나온 weight값을 저장하려면 save함수쓰고 state_dict()해줘야한다.

ckpt는 체크포인트를 의미한다.

![image](https://user-images.githubusercontent.com/78403443/120297229-df15d400-c303-11eb-8b10-57f8ebf93cb3.png)

위와 같이 시각화되었다.

<br/>

---

(※ 참고 :: 특히, 2번째 코드로 실습할 때 랜덤한 값으로... 셀을 새로 실행할 때마다 값이 바뀌었기 때문에 실제 코드 내용과 차이가 있을 수 있음)

(※ 참고 :: 저작권 문제로 pdf 캡쳐파일 업로드 못하고 메모한 내용만 올렸음)
