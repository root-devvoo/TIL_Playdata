(pdf 파일 캡쳐파일은 저작권 사유로 업로드하지 않고, 내용만 입력)

learning rate는

가이드가 따로 없다. 데이터, 문제양상에 따라 천차만별이다.

따로 해결법이 정해져 있지 않다.

<br/>

논외로, GridSearch 6~10개 돌린다. 

실제로 하이퍼 파라미터는 100종류가 넘는다.

알고리즘을 교차검증해서 Best조합의 파라미터 값을 찾아야한다.

시간이 많이 듬, 노가다

<br/>

딥러닝 개발자가 왜 몸값이 높은지 알 수 있다.

노하우에 따라서 다르기 때문에...

<br/>

100~500가지 넘는 하이퍼 파라미터...

모든 것들 조금씩 값을 변경해보아야 한다. → 성능이 달라진다

추천값, Recommand값을 알아야한다.

<br/>

Initial learning rate : 0.01 ~ 0.04

batch size : 100

(batch normalization : 16이상... 32)

Epoch : 100

kernel size : 3x3

activation function : ReLU

optimizer : SGD, ADAM... ADAM 많이 쓴다

<br/>

딥러닝 코드는 모든 코드가 거의 똑같다

![image](https://user-images.githubusercontent.com/78403443/121163163-86a58000-c889-11eb-84a3-ecd6d026a723.png)

이런 순서로 가면 된다. 

우리는 인공지능 학부생, 석사생 코드라고 생각하면 된다. (재사용성 x)

<br/>

인공지능 코드... 좋은 코드 설계 성공을 위해서 수학적 증명을 하려고 하는데

수학적으로 접근해서 되지 않는다. 하이퍼 파라미터 값은 수학적으로 찾아낸게 아니라 

경험적으로 찾아낸 것이기 때문

<br/>

오늘 dropout도 들어간다.

keras도...

<br/>

Normalization은 정규화라고 생각하면 된다. 

수학적으로...

<br/>

---

---

**keras 기본적인 것부터 다뤄본다**

<br/>

- **06_NN_keras.ipynb 파일 (Jupyter Notebook)**

![image](https://user-images.githubusercontent.com/78403443/121163350-a9d02f80-c889-11eb-8766-4eb3fc20cd1d.png)

![image](https://user-images.githubusercontent.com/78403443/121163379-b05ea700-c889-11eb-98f1-286988f70969.png)

입력이 하나라는 얘기는 속성의 개수가 하나라는 얘기

<br/>

Sequential() 왜 나왔나?

Sequential 사전적 의미는 연속적이다. 라는 의미

입력과 출력 사이에 중간 출력(hidden layer)이 나올 것임

일직선상에 연속적으로... 라는 의미에서

Sequential은

![image](https://user-images.githubusercontent.com/78403443/121163437-bd7b9600-c889-11eb-996d-ea0bcf24dbd8.png)

위와 같은 모델을 만든다는 얘기

Dense() 함수는 FCN, Fully Connected Network를 만들 때 사용

Fully Connected Layer를 의미

keras 입력은 input_shape 뒤에 튜플 형태로 하나 출력한다고 쓴다.

![image](https://user-images.githubusercontent.com/78403443/121163547-d97f3780-c889-11eb-9b94-de92111c81af.png)

모델 다 만들었다.

![image](https://user-images.githubusercontent.com/78403443/121163594-e3a13600-c889-11eb-809e-79476daa5e0b.png)

![image](https://user-images.githubusercontent.com/78403443/121163631-eac84400-c889-11eb-8528-65a473a94921.png)

참고! input_shape만 처음에 들어가고 안들어간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121163692-f7e53300-c889-11eb-9ab6-62a8ac2ca5d2.png)

SGD 괄호 안에 0.01은 SGD로 Learning rate 0.01 설정한다는 얘기

![image](https://user-images.githubusercontent.com/78403443/121163750-029fc800-c88a-11eb-9422-1023ab1050e9.png)

어떻게 학습 하는지 compile안에 다 떄려넣는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121163978-324ed000-c88a-11eb-859f-ba5e2332dc77.png)

트레이닝 테스트를 4분의 1로 나눠서 쓰도록 하겠다.

![image](https://user-images.githubusercontent.com/78403443/121165428-392a1280-c88b-11eb-813e-45a337e6bc33.png)

keras에선 학습할 때 학습된 결과의 설명하는 걸 안본다 하면 verbose = 0

1이면 설명 많이 있고, 2면 설명 간략하게

<br/>

![image](https://user-images.githubusercontent.com/78403443/121165684-6676c080-c88b-11eb-8594-52e8ea2d12a4.png)

flatten() 함수를 쓰면 출력값을 1차원으로 펼친다. (직관적이라 비교하기 쉬움)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121165746-72628280-c88b-11eb-828a-ab19112f93fb.png)

evaluate안에 예측하고자 하는 값 넣고, 뒤에는 정답 넣는다. 

그 값을 가지고 predict(예측)하고 evaluate 한다는 얘기이다. 

evaluate() 함수는 독특한 함수인데

![image](https://user-images.githubusercontent.com/78403443/121165846-873f1600-c88b-11eb-8f01-370aa7221275.png)

(값이 좀 이상하게 나오긴 했는데...)

evaluate 함수는 이렇게 두개의 값을 내포하고 있다. 

왼쪽은 Loss 값이고, 오른쪽은 Accuracy 값

<br/>

두개의 값을 내포하고 있긴 하지만

값을 따로따로 출력해주는게 아니기 때문에

![image](https://user-images.githubusercontent.com/78403443/121165891-932ad800-c88b-11eb-98f8-788bb0497537.png)

이렇게 포매팅 해줘야한다.

<br/>

(데이터가 워낙 적기 때문에 accuracy는 이상하게 나왔다...)

어쨋든 간에 이 파이프라인을 익힐 것...

![image](https://user-images.githubusercontent.com/78403443/121165956-a047c700-c88b-11eb-9b0b-5cc737e80473.png)

<br/>

구글 코랩으로... keras이용해서 mnist데이터셋 가지고 ANN 모델 만들어서 출력해본다

<br/>

- **(구글 코랩) 07_ANN_MNIST_keras.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/121166041-b3f32d80-c88b-11eb-8459-cadcd306a348.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121166092-be152c00-c88b-11eb-8a2e-3dd584bf2ca6.png)

이 값들이 0~255 사이인 것을 알 수 있다.

스케일링이 안된 상태인 이 값에다가 w가 곱해진다는 것을 생각해보자

<br/>

시퀀스 모델 생성하기 전에 데이터 전처리 과정해줘야한다.

우리는 지금 ANN을 하고있다.

① 1~255 스케일링

② 일직선으로 펼쳐줘야한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121166675-3f6cbe80-c88c-11eb-8fdd-5210a66547c1.png)

shape을 찍어보니 채널이 없다. 

왜? keras에서는 채널 = 1인 흑백 데이터이기 때문에 빠진 것

<br/>

![image](https://user-images.githubusercontent.com/78403443/121166738-4b588080-c88c-11eb-9d85-b175e081f00d.png)

<br/>

3) y값 전처리하기...One Hot Encoding

One Hot은 하나만 Hot게 한다는 뜻

PyTorch에서는 확률값으로 제일 높은값을 뽑아냈지만

Keras에서는 One Hot Encoding을 해줘서 다 0으로 바꾸고 제일 높은 값만 1로 표현

<br/>

One Hot Encoding은 from keras.utils import np_utils 에서 제공

![image](https://user-images.githubusercontent.com/78403443/121166826-5c08f680-c88c-11eb-99f6-d2d8ba46444c.png)

One Hot Encoding 해서 값이 위와 같이 나왔다

<br/>

하이퍼 파라미터 지정한 후 모델 생성

![image](https://user-images.githubusercontent.com/78403443/121166881-688d4f00-c88c-11eb-9e9b-16778a14f4c4.png)

![image](https://user-images.githubusercontent.com/78403443/121166912-6f1bc680-c88c-11eb-8854-6a9bb098e143.png)

Dense함수 안에 unit을 먼저 넣어주고, input_shape= 튜플 형식으로 넣어준다

<br/>

activation함수는 소문자로 넣어준다. unit과 input_shape 사이에

softmax는 numclasses 다음에 activation = 'softmax' 이렇게 넣어준다

모델 생성 끝..

<br/>

compile

![image](https://user-images.githubusercontent.com/78403443/121166969-7cd14c00-c88c-11eb-8140-e05f3dcbd38a.png)

맨 왼쪽에 optimization 방법... 

categorical_crossentropy... 이게 Loss함수와 같은 것이다

<br/>

fit

![image](https://user-images.githubusercontent.com/78403443/121167032-88bd0e00-c88c-11eb-96c7-9a90f6e2ac52.png)

validation_split= validation_data 대신 사용할 수 있습니다. 검증 데이터를 사용하는 것은 동일하지만, 별도로 존재하는 검증 데이터를 주는 것이 아니라 X_train과 y_train에서 일정 비율을 분리하여 이를 검증 데이터로 사용합니다. 역시나 훈련 자체에는 반영되지 않고 훈련 과정을 지켜보기 위한 용도로 사용됩니다.

(출처 : https://wikidocs.net/32105)

<br/>

0.2는 20%를 의미

<br/>

![image](https://user-images.githubusercontent.com/78403443/121167149-a0949200-c88c-11eb-9396-a8d9af295568.png)

<br/>

Evaluation

![image](https://user-images.githubusercontent.com/78403443/121167186-ab4f2700-c88c-11eb-9fc6-77e7b15b00cc.png)

Loss값, Accuracy 값 뽑았다.

아까 전에 전처리 3개 추가된 것말고 흐름은 keras 맨 처음에 한거랑 똑같다.

![image](https://user-images.githubusercontent.com/78403443/121167222-b3a76200-c88c-11eb-9372-542545df0727.png)

keras의 evaluate() 함수는 loss, acc 값 2개를 포함한 객체를 리턴

<br/>

*model_performance :: model_performance 안의 모든 정보를 반환한다는 뜻

Loss, Acc 값을 꺼내오는 역할

<br/>

**시각화**

history 정의

![image](https://user-images.githubusercontent.com/78403443/121167362-d5a0e480-c88c-11eb-8642-106ee37322b8.png)

확실하게 시각화하기 위해서 epochs는 50을 설정함

<br/>

시각화함수 정의

![image](https://user-images.githubusercontent.com/78403443/121167408-e05b7980-c88c-11eb-9b8f-7fede91acaa1.png)

history는 딕셔너리 형태

history안에 한번 더 들어가야지만 딕셔너리를 받아올 수 있다.

loss라고 하면 loss정보 받아온다

val_loss는 validation loss이다.

![image](https://user-images.githubusercontent.com/78403443/121167453-e94c4b00-c88c-11eb-931e-aa9cde3cc3e5.png)

<br/>

시각화할 때 괄호안에 history 찍어들어가줘야한다.

![image](https://user-images.githubusercontent.com/78403443/121167511-f406e000-c88c-11eb-9118-cdc2f97e98ac.png)

잘 나왔다.

<br/>

---

keras로 DNN, CNN 다뤄본다

<br/>

- **(구글 코랩) 08_DNN_FashionMnist_keras.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/121167587-07b24680-c88d-11eb-89e6-035170a1c506.png)

![image](https://user-images.githubusercontent.com/78403443/121167621-10a31800-c88d-11eb-87ab-0f5ff6b79fa1.png)

28x28이고, train data 6만개, test data 1만개, 흑백

신발모양... (숫자데이터로 나온 값 모양과 plt로 찍어서 볼 수 있다)

![image](https://user-images.githubusercontent.com/78403443/121167655-1a2c8000-c88d-11eb-90b4-ba5cedb91e9e.png)

<br/>

숫자 1, 3을 구분하는 것보다는 바지와 신발을 구분하는 것이 더 복잡할 수 있다.

어제 작업을 바탕으로 오늘은 이미지 정확도 결과를 97% 이상으로 끌어올리는 것을 목표로 잡자.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121167711-287a9c00-c88d-11eb-8f14-ad70cc4b0ceb.png)

잘 reshape 되었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121167841-4516d400-c88d-11eb-8746-d6744c8a06c3.png)

스케일링과 One Hot Encoding 잘되었다. 

전처리 끝

<br/>

모델 생성...히든 레이어를 2개 생성

![image](https://user-images.githubusercontent.com/78403443/121167889-5233c300-c88d-11eb-90d9-f43e6ae57a06.png)

DNN이든 ANN이든 Fully Connected Layer기 때문에 Sequential하게 만들면 된다.

input_shape는 무조건 튜플로 들어가야하기 떄문에 하나라도 위와 같이 넣어야한다.

맨 처음에만 넣어주면 된다.

![image](https://user-images.githubusercontent.com/78403443/121167913-5bbd2b00-c88d-11eb-848b-250b37388568.png)

오른쪽 그림을 그대로 코드로 구현했다

<br/>

![image](https://user-images.githubusercontent.com/78403443/121167974-6972b080-c88d-11eb-892f-8455ec695699.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168007-755e7280-c88d-11eb-870b-f3c474375363.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168050-80190780-c88d-11eb-83f1-5fa65527078b.png)

결과를 보니 나쁘지 않게 loss값과 accuracy값이 나왔다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168086-8ad39c80-c88d-11eb-8bd9-3e46500deb6b.png)

이렇게 중간중간 선들을 잘라 추상성을 높이는게 결정 트리에서는 pruning(가지치기)기법이었다. 

keras에서는 dropout() 함수를 사용해서 잘라서 추상성을 높여준다.

<br/>

dropout() 함수 써본다

![image](https://user-images.githubusercontent.com/78403443/121168136-9757f500-c88d-11eb-82f3-fa63f1ec3805.png)

똑같이 add에서 Dropout 함수 써주는 것이다. 

0.4는 40% 가지치기 한다는 얘기이다.

![image](https://user-images.githubusercontent.com/78403443/121168165-a048c680-c88d-11eb-8508-652977a70470.png)

0.25는 25% 가지치기 한다는 얘기

가지치기 하면 Accuracy올라간다.

<br/>

MNIST와 Fashion MNIST의 차이를 알 수 있다. 

Fashion MNIST가 복잡하고 더 어렵다는 걸...

<br/>

시각화 함수 정의

![image](https://user-images.githubusercontent.com/78403443/121168221-ae96e280-c88d-11eb-8d13-3ee38a305cbc.png)

시각화

![image](https://user-images.githubusercontent.com/78403443/121168261-b8204a80-c88d-11eb-89b2-deab4f609735.png)

간극이 좀 있다... Epoch을 더 많이줘서 돌리면 결과값이 더 잘 나올 것 같다.

<br/>

여기까지 DNN...

<br/>

다시 이미지 데이터 Plotting 시켜놓기

![image](https://user-images.githubusercontent.com/78403443/121168338-cbcbb100-c88d-11eb-9d0d-e0c0a8e063e9.png)

아까 위에서 찍었는데 왜 에러나나? 1차원으로 펼쳐놔서 안되는 것

1차원으로 펼친 데이터를 다시 2차원으로 만들어 놓아야 한다.

![image](https://user-images.githubusercontent.com/78403443/121168380-d6864600-c88d-11eb-886f-7936b64b7b86.png)

reshape(28, 28) 하는건 다시 2차원으로 만드는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168415-e30a9e80-c88d-11eb-8d9c-a6d0ea9af237.png)

하나씩 뽑아볼 수 있다.

<br/>

(뭐 확인하는거 빠짐- 확인하고 추가해야됨)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168455-f0278d80-c88d-11eb-8406-b94a763fa7b3.png)

model.summary() 하면 모델 정보가 위와 같이 나온다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168491-fb7ab900-c88d-11eb-853f-60a84892f91c.png)

저장은 클라우드 기반이라 복잡... 나중에 다시 설명한다.

<br/>

여기까지 하고 Keras로 CNN 들어간다

<br/>

---

- **09_CNN_MNIST_Keras.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/121168626-21a05900-c88e-11eb-9e5a-f31b05f89065.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168667-2bc25780-c88e-11eb-9723-c263ac47709d.png)

채널이 안나왔다는 사실을 주의깊게 봐야한다.

4차원이 아니라 3차원으로 나왔다는 것은 채널이 빠졌다는 것... 흑백이라서... 

채널 정보를 파악하는게 굉장히 중요하기 때문에 잘 짚고 넘어가자.

28, 28 부분이 height(rows), width(cols) 되겠다.

![image](https://user-images.githubusercontent.com/78403443/121168696-35e45600-c88e-11eb-819b-8483f7568be6.png)

height, width 값만 뽑으려면 Shape[1:] 해줘야 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168745-4268ae80-c88e-11eb-9b08-5c87f6e2c32d.png)

파이토치는 ToTensor()로 뒤로 보내지만

파이토치와 다르게 keras에서는 채널 위치를 확인해야한다.

위 경우 backend.image_data_format() 함수 찍어서 channel_last로 동작한다는 것을 잘 파악하고 알고 있어야한다.

![image](https://user-images.githubusercontent.com/78403443/121168788-4c8aad00-c88e-11eb-9ffd-c18a38ab068d.png)

CNN은 채널이 필요하기 때문에 채널 정보를 잘 알아야 하는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168839-57ddd880-c88e-11eb-9401-fc929c6a40b8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121168886-64fac780-c88e-11eb-9468-a4fbb265c175.png)

<br/>

3.모델 생성하기

![image](https://user-images.githubusercontent.com/78403443/121168924-70e68980-c88e-11eb-8546-6affc1ea0e77.png)

Dense는 FCN 할 때 하는 것이므로 Conv2D써야한다.

keras에서 처음 입력만 input_shape 들어간다!!! (꼭 명심!)

<br/>

stride와 padding 따로 지정안하면 stride 는 기본값이 1이고, padding = 0이다. 

padding을 안줬기 때문에 특징은 늘고 사이즈는 줄 것이다.

![image](https://user-images.githubusercontent.com/78403443/121169006-865bb380-c88e-11eb-98ce-fad8b294bbc2.png)

이런식으로 만든 것이다. 이쁘게 안 만든 것..

<br/>

CNN(Convolution, max pooling, dropout)으로 특징 추출하고, FCN... 1차원으로 모든 데이터 분류해줘야한다.

![image](https://user-images.githubusercontent.com/78403443/121169053-9378a280-c88e-11eb-8633-b02a7c8a4db6.png)

Flatten으로 펼쳐준다.

![image](https://user-images.githubusercontent.com/78403443/121169105-9f646480-c88e-11eb-87ac-b8e0b89b238d.png)

Dense()함수로 Fully Connected Layer 만들어준다.

relu를 쓴다는건 Fully Connected Layer 한번 더 써서 특징 늘려준다는 것

<br/>

학습방법 지정 == compile()

![image](https://user-images.githubusercontent.com/78403443/121169153-ab502680-c88e-11eb-9255-b9fefc00a6e0.png)

<br/>

fit() (학습) + 시각화 함수 정의 및 시각화

![image](https://user-images.githubusercontent.com/78403443/121169193-b905ac00-c88e-11eb-8ef9-64edd08b85ca.png)

![image](https://user-images.githubusercontent.com/78403443/121169230-c0c55080-c88e-11eb-961e-a3a801948826.png)

<br/>

---

내일은 Custom Dataset 어떻게 만드는지 + 구글 코랩 어떻게 쓰는지(마운트 시키는 방법) 수업 나감
