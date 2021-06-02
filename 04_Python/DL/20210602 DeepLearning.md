(※ PDF 캡쳐파일은 저작권 사유로 올리지 않고, 메모 내용만 올림)

<br/>

- **D:\encore_jwc\util\PDF\DL\4.Pytorch Framework.pdf 파일 보기**

<br/>

새로운 프레임워크를 쓸 때는 앞을 내다보고 선택... 

기술이 변해서 그런 것도 있지만 고생을 덜 하려고 선택

<br/>

Deep Learning 프레임워크 Power score를 보게 되면 

랭킹이 높은 Tensorflow나 Keras를 써야된다는 생각을 하게 된다.

단면만 보고서는 알 수 없다는 뜻... 

PyTorch는 훨씬 더 쉽고, 지금 엄청 각광받고 있음

<br/>

파이토치의 장점은 포럼활동이 되게 활발함 (답변 등)

반면에 Tensorflow는 이런 포럼활동이 활발하지 않음

<br/>

연산방식이 Tensorflow보다 PyTorch가 훌륭

<br/>

Github에서 star를 많이 받은 코드가 좋은 코드이다.

그런 코드들에서 PyTorch로 짠 코드가 많아지고 있음

<br/>

Keras는 전문가용이 아니다. 디버깅이 잘 안됨

대학생들이 Keras로 작업 많이함. 

깊이 있는 코드로 짜는게 아니라면 Keras도 훌륭하다.

전문가용으로는 텐서플로우와 파이토치를 꼽는다.

<br/>

---

---

- **3.Backpropagation.pdf 보기**

<br/>

(어제 내용 복습)

<br/>

기울기(값)이 Model 학습의 방향과 속도를 결정한다. 

음수면 방향이 왼쪽, 양수면 방향이 오른쪽

기울기가 클수록 값도 커지고 속도도 빨리 내려오게된다.(학습속도 빠르다)

기울기가 작으면 학습속도가 느리다. 꼼꼼하게 학습할 수 있다. 

마지막으로, 하산할수록(학습을 거듭할수록, Epoch을 늘릴수록)

기울기는 점점 완만해진다. 학습속도는 느려진다.

이때, 느려진다고 가만히 보고 있는게 아니라, Learning_rate 값도 함께 작게 줘야한다. (Learning_rate도 같이 느려져야)

<br/>

epoch에 대한 설명을 다시한다.

![image](https://user-images.githubusercontent.com/78403443/120445448-96bdeb00-c3c3-11eb-80dc-49ed6efd6faf.png)

Validation Data가 1만개 있을 때는 Cross Validation 안해도 된다. 

이미 데이터가 충분하기 때문에

Cross Validation은 데이터가 턱없이 부족할 때 쓰는 기법이다.

![image](https://user-images.githubusercontent.com/78403443/120445495-a0dfe980-c3c3-11eb-9eeb-1190c4e3d59f.png)

여기서는 5만번의 문제집 풀고 1만번의 모의고사를 풀고 끝나는게 1회로... 1 Epoch이다.

위와 똑같은 과정이 한번 더 반복하면 2 Epoch

세번째 반복 3 Epoch

...

열번째 반복 10 Epoch

여기까지가 Training이 끝나는 것

그리고 나서 맨 마지막에 딱 한번 테스트를 본다, 이게 수능시험

<br/>

Epoch은 학습을 총 10번하는게 Epoch이다. 

이게 모델에서 진행되는 학습이다.

<br/>

기계라면 학습이 거듭될수록 외워버리게 될 것 같다.

이런 문제가 생긴다면 어떻게 해야할까?

<br/>

Epoch을 거듭할수록 

문제집 풀고 데이터를 변형해서 문제 풀어야한다.

(Data Augmentation(데이터 변형) + Shuffle(순서섞기)

데이터 변형은 밝기를 달리하거나, crop하거나 하는 등의 방법으로...

<br/>

---

- **3.Backpropagation.pdf 이어서 보기**

![image](https://user-images.githubusercontent.com/78403443/120445615-bfde7b80-c3c3-11eb-8406-c7995d7ed5a7.png)

여기서 Hidden layer는 몇개?

<br/>

위와 같은 선을 Weight Edge라고 한다.

Weight Edge가 많다고하면 연산량이 엄청나다.

<br/>

이 그림에서는 hidden layer가 없다.

그냥 연산만 된 것

<br/>

어쨋든 최종 연산된 값을 바탕으로 loss값...

loss값 바탕으로 W에 대한 보정이 일어난다. 

그게 Back.. 

<br/>

이 과정을 통틀어서 **Fully Connected Network(FCN)**라고 한다.

<br/>

**Neural Network**

![image](https://user-images.githubusercontent.com/78403443/120445755-e69cb200-c3c3-11eb-8eb1-9467afbe1176.png)

(출처 : https://dic.kumsung.co.kr/web/smart/detail.do?headwordId=1404&pg=6&findCategory=B002004&findBookId=25&findPhoneme=)

인간 신경망을 본따서 만든 방법으로 학습을 하는게 딥러닝이다!

<br/>

머신러닝과 딥러닝의 차이는

머신러닝은 학습의 지도방법에 따라서 지도학습, 비지도학습을 하는거지만 

딥러닝은 뉴런을 본따서 만든 뉴럴 네트워크로 학습한다는 점에서 차이

<br/>

Activation 함수를 쓰는 이유?

1. Neural Net은 인간 신경망을 본따서 나온 학습법

   그렇기 때문에 인간의 반응과 유사하도록 만들어졌다.

   즉, 신경전달 자극값이 미세하면 무시

   신경전달 자극값이 크면 출력을 위해서 전달된다.

2. 수학적으로, Activation 함수가 필요한 이유가 있다!

![image](https://user-images.githubusercontent.com/78403443/120445924-0e8c1580-c3c4-11eb-94cc-8edc6e9b2a6b.png)

수학적인 한계점... 

선형의 문제점, 블럭을 100개 쌓더라도 1개의 선형을 못벗어남

<br/>

비선형은 각각의 블럭의 독립적인 값을 유지하고 풍부한 내용을 사용

좋은 결과를 도출해내려면 비선형이 필요하다.

Activation 함수는 비선형이기 때문에 Activation 함수써야

<br/>

그리고, Activation 함수 중에 어떤 함수를 기억하면 되느냐! 렐루!! ReLU

<br/>

---

**코드로 실습**

<br/>

- **구글 드라이브 1. Pytorch, Keras Tutorial 폴더, 03_Deep_FCN_cifar10.ipynb 파일 보기**

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446088-35e2e280-c3c4-11eb-8bf3-53662d97a11e.png)

CIFAR-10 데이터에 대한 정보

(출처 : https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=qbxlvnf11&logNo=221295867121)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446169-42ffd180-c3c4-11eb-9283-73acfcc95ac0.png)

이미지 데이터셋에 쓸 수 있는 여러 가지 (데이터 변환에 대한)변환 필터를 담고 있는 모듈로,

 텐서로 변환, 크기 조절(resize), 크롭crop)으로 이미지 수정, 밝기(brightness), 대비(contrast) 조절 등으로 쓰인다.

<br/>

**CIFAR10 DataSet Loading and Show Image**

![image](https://user-images.githubusercontent.com/78403443/120446230-4eeb9380-c3c4-11eb-85b8-25da7a8dd379.png)

download = True 하면 train 데이터셋만 다운로드 하겠다는 뜻이다. (download = True하면 다운로드가 root에 진행되기 때문)

![image](https://user-images.githubusercontent.com/78403443/120446296-6165cd00-c3c4-11eb-8e3f-5b036fae90b9.png)

압축된 형태로 제공된다는 것 확인

(다운로드 된 것이다)

<br/>

다운로드 된 이미지 중 한장만 찍어본다

![image](https://user-images.githubusercontent.com/78403443/120446350-6e82bc00-c3c4-11eb-8bd5-0e33ed7c6fac.png)

![image](https://user-images.githubusercontent.com/78403443/120446385-75a9ca00-c3c4-11eb-9e54-e3cdf8143cce.png)

Frog 이미지 한 장에 대한 값이 나왔다. 

Frog 이미지에 대한 32x32x3의 픽셀값 3072개

6번 Label == Frog 알 수 있다

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446432-835f4f80-c3c4-11eb-850a-1a7f6ee61211.png)

![image](https://user-images.githubusercontent.com/78403443/120446462-8a865d80-c3c4-11eb-9853-a24853bd1d13.png)

ToTensor() 때문에 컬러에 대한 채널값(3)이 앞에 오게 된다. 

이걸 반드시 명심하고, 나중에 채널을 뒤로 보내줘야한다 (채널을 못보기 때문에)

<br/>

**Image 변환하기**

Torch 타입을 Numpy 로 일단 변경부터 시켜야 한다

![image](https://user-images.githubusercontent.com/78403443/120446516-9bcf6a00-c3c4-11eb-832f-bc737ab1b377.png)

moveaxis하면 축을 바꿔주는 것임... 

아무튼 moveaxis함수를 이용해서 0인덱스에 있는 걸(여기선 3을) 맨 뒤인 -1인덱스로 보낸다

<br/>

이미지는 출력 안됨(kernel 죽어서)

구글 코랩으로 옮겨서 다시 실행, 출력

![image](https://user-images.githubusercontent.com/78403443/120446612-adb10d00-c3c4-11eb-9ae4-eec1ed6b4685.png)

잘 나왔다. 

해상도가 낮은데 왜 낮을까? Toy Dataset이기 때문에 해상도가 낮다

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446667-ba356580-c3c4-11eb-8979-f75e2d13896b.png)

<br/>

데이터셋 로딩은 2번 한다. 

첫번째 로더는

![image](https://user-images.githubusercontent.com/78403443/120446711-c9b4ae80-c3c4-11eb-9224-4dec13aca387.png)

실질적인 DataSet을 물리적인 위치로 다운로딩, 이때 Training 데이터와 테스트 데이터 분리되어야 한다.

지금은 Training 데이터만 받았다.

<br/>

그리고 두번째 과정을 거쳐야 하는데,

![image](https://user-images.githubusercontent.com/78403443/120446756-d6d19d80-c3c4-11eb-92d4-e54593aed552.png)

이것이 두번째이다. 

기존에 저장되있는 데이터셋을 가져온다.

가지고와서 batch_size를 준다. 

왜? 5만개의 데이터를 한꺼번에 못주기 때문에... (연산량이 많아서 멈출 수 있기 때문에)

그래서 5만개를 다 다운받아서 쪼개서 학습시켜야 하는데

만약 batch_size를 100으로 주면 500번 로딩이 계속 진행된다. 

(5만개의 데이터를 100개씩 쪼개서 넣어주는거니까 총 500번)

<br/>

결론 :: batch_size는 데이터를 쪼개는 옵션 (데이터를 조각내어서 학습시키는 옵션)

<br/>

위에서는 batch_size를 64를 줬으니, 5만개의 데이터를 64개씩 묶어서 쪼개라는 구문이다.

![image](https://user-images.githubusercontent.com/78403443/120446802-e5b85000-c3c4-11eb-92c7-45fe8374d476.png)

총 781번 정도 로딩이 진행될 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446882-f23ca880-c3c4-11eb-8fa1-36059e757289.png)

782 라는 것을 알 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446919-fe286a80-c3c4-11eb-90ba-544df5facb33.png)

(출처 : https://pytorch.org/docs/stable/data.html)

drop_last = False 여서 782로 출력된 것이라는 것을 알 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120446974-0d0f1d00-c3c5-11eb-9f82-6ab1386bb715.png)

shuffle = True는 학습의 효율성을 위해 shuffle해준 것이다.

결론적으로, 위 코드는 Stochastic Gradient Descent 한 것이다.

<br/>

---

- **04_Deep_FCN_mnist.ipynb 파일 보기**

<br/>

**딥러닝코드는 github에 올라와있다. (좋은 코드를 찾는 것도 github로 찾는다, star수 기반해서)**

(pytorch-tutorial 코드: https://github.com/yunjey/pytorch-tutorial/blob/master/tutorials/01-basics/pytorch_basics/main.py)

한국인이 만들었음, 네이버에서 일하는 인공지능 개발자

가장 베이직한 코드

이것도 보기...

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448044-206eb800-c3c6-11eb-8101-850643dee2e4.png)

우리가 쓰는 컴퓨터에서 현재 gpu를 쓰고 있다면 cuda가 출력되게 한다.

<br/>

MNIST 데이터

![image](https://user-images.githubusercontent.com/78403443/120448099-2f556a80-c3c6-11eb-9414-f51473c313a2.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448149-3aa89600-c3c6-11eb-8b9e-48e77a0f3a60.png)

모델 설계할 때 batch_size를 딱 떨어지도록 주는게 중요하다. 

(딱 떨어지게 못줘서 데이터가 남으면 오류가 생기기 때문)

<br/>

MNIST 데이터는 28x28x1 이기 때문에 input_size는 784개가 나온다. (1인 이유는 흑백이라서) 

num_classes = 10 은 라벨의 갯수 (라벨은 0~9)

hidden_size = 500 이 의미하는건 hidden layer의 unit수를 의미 

(hidden layer가 중간에 하나 있고 unit의 개수는 500개 라는 얘기)

그래서 최종 결과출력 직전에 W는 500x10이 나오게 된다 (압축해줬기 때문 그리고 10개의 라벨이기 때문)

그리고 ReLU() 함수를 예측값 나오기 전에 써줘야한다. 

언제? Hidden layer에서 결과출력하기 직전에 써준다.

<br/>

최종 예측값 출력 직전에는 activation(ReLU() 함수)을 또 주는게 아니라 softmax를 쓴다. 

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448214-4f852980-c3c6-11eb-84d6-47434d41e84a.png)

train = True는 트레이닝 데이터셋을 다운받겠다는 뜻 (테스트 데이터셋은 아니다)

test_dataset에는 download 옵션 빼준다. 

이것이 1단계

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448267-5b70eb80-c3c6-11eb-9e2a-73f8307cb98e.png)

DataLoader 함수 자체는 C#으로 만들어져있어서 상당히 복잡함... 해석 어렵다. 

(우리는 그냥 쓰는 것.. 쓰는 입장은 그냥 쉽다)

batch_size를 이용해서 잘라서 로딩시키고, 

shuffle은 학습할 때만 섞어준다.

<br/>

**Model 생성하기**

![image](https://user-images.githubusercontent.com/78403443/120448305-66c41700-c3c6-11eb-9e2d-df4fc400f7ad.png)

hidden layer 전 위치에서 activation 해줘야하고(ReLU함수 적용)

최종출력 전에는 softmax 함수 써줘야한다. 

![image](https://user-images.githubusercontent.com/78403443/120448341-717eac00-c3c6-11eb-8df3-95155e02363b.png)

적용하였다. 

위와 같이 정의한 클래스를 인스턴스화 시켜주면 모델이 되는 것이다.

![image](https://user-images.githubusercontent.com/78403443/120448393-7e030480-c3c6-11eb-9d44-53b25fa99255.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448448-89eec680-c3c6-11eb-870a-6c97ead2edd6.png)

CrossEntropyLoss() 함수 가장 많이 쓴다.

이렇게 loss와 optimizer 선정의했다

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448509-9541f200-c3c6-11eb-86a8-311b6cc97407.png)

total_step 몇개 나오나?

train_dataset은 6만개 (MNIST 데이터셋이니까)

batch_size = 100 이므로 600번 로딩되어야 하기 때문에

total_step은 600이 나와야한다.

![image](https://user-images.githubusercontent.com/78403443/120448544-9f63f080-c3c6-11eb-9086-6308877856f5.png)

첫번째 for문에서 총 epoch횟수는 5번만 돌린다. (시간관계상... 시간이 너무 오래걸려서...)

두번째 for문에서는 1회에 600번 돈다. 한번에 100개씩 덩어리가 600번 들어가는 것이기 때문에...

우리는 epoch 횟수를 5로 설정했으므로 600번 도는게 총 5번 도는 것이다.

<br/>

images.reshape()함수에서 -1은 28*28 제외한 나머지를 말함. 채널을 말하는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448593-adb20c80-c3c6-11eb-8538-5d4580f92fb7.png)

backward하기전에 optimizer를 초기화 시키고, 

backward를 한다. 

그리고 학습을 진행한다

![image](https://user-images.githubusercontent.com/78403443/120448667-befb1900-c3c6-11eb-86e6-d3c1ca5b7f70.png)

<br/>

**전체코드**

![image](https://user-images.githubusercontent.com/78403443/120448714-ca4e4480-c3c6-11eb-8500-38c3f20cc9c2.png)

**출력결과**

![image](https://user-images.githubusercontent.com/78403443/120448753-d508d980-c3c6-11eb-86cd-6ebc58378254.png)

<br/>

**Test**

![image](https://user-images.githubusercontent.com/78403443/120448797-e18d3200-c3c6-11eb-9c97-035d10fceb0d.png)

빨간 네모 표시한 부분에 대해서 설명...

![image](https://user-images.githubusercontent.com/78403443/120448849-eb169a00-c3c6-11eb-816f-4729ff456404.png)

중요한 부분

torch.max에 예측결과, 1 넣어줌

1이 매우 중요한 부분...

max는 기본적으로 리턴되는 값이 2개다.

하나, 결과에 해당하는 값이 리턴

두번째, 값에 해당하는 인덱스가 리턴

<br/>

파이썬에서는 언더바 같은게 쓰인다. 

언더바로 변수를 받을 때는 리턴은 받겠지만, 값을 저장하지는 않겠다는 뜻이다.

왜? 필요 없기 때문에

그럼 값이 왜 필요없는지...?

<br/>

예측값이 100개씩 로딩됐다. 

그러면 정답도 100개 나온다.

<br/>

batch_size가 왜 중요한지 알아야한다.

<br/>

어쨋든 100행 10열이 나온다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/120448970-0bdeef80-c3c7-11eb-8447-1f8eb02a2506.png)

어쨋든 1이 뜻하는건... outputs 열을 기준으로 값을 찾는다는 얘기

(행 인덱스가 [0] 이고, 열 인덱스는 [1]이기 때문에)

<br/>

이 코드가 Basic of Basic...
