오늘 할 내용

![image](https://user-images.githubusercontent.com/78403443/121324640-df3d5180-c94b-11eb-8637-bf41826c3722.png)

custom dataset 어떻게 만들고 구성하고, 로드하는지, 라벨링을 어떻게 하는지 본다.

![image](https://user-images.githubusercontent.com/78403443/121325043-3e02cb00-c94c-11eb-8bed-a28066ffdf94.png)

구글 코랩은 구글 드라이브랑 연결되있음

google에서 제공하는 무료 GPU 서버 + Jupyter Notebook

그렇기 때문에 Data는 Cloud기반 

데이터를 드라이브에 copy해서 써야한다. 

그 얘기는 뭐냐면 코랩에 Mount를 해줘야한다.

<br/>

구글 드라이브와 코랩 연동과정을 설명하면서

코랩으로 어떻게 마운트하고, 로드하고, 압축을 푸는지 설명한다.

(강사님도 예전에 하루종일 삽질하심...ㅠ)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121325120-4f4bd780-c94c-11eb-859d-c2ec12eb98af.png)

그리고, 오늘부터 진짜 코드가 나온다.

Computer vision 기반 

1. Sementic Segmentation 

2. Object Detection

   - 수학적 난이도 40%
   - 단계가 많고, 한 단계, 한 단계를 이해하지 못하면 그 다음으로 못 들어간다.
   - 처음부터 끝까지 Perfect하게 알아야 한다.
   - 코드로 재현해본다.
   - 어렵다.

3. GAN

   - 수학적 난이도 80%
   - 그러나, 실제 코드는 더 쉬움, 그냥 가져다 쓰면 됨(네 단계를 다 이해하면...)

<br/>

자연적인 파트에서는 1, 2번을 많이 쓴다.

Object Detection은 아카데믹 적 부분, 프로그램적인 부분 둘 다 알아야 잘하기 때문에

아직까지 현업에서 Object Detection을 잘하는 사람은 많지 않다.

그만큼 어렵다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121325214-612d7a80-c94c-11eb-8e5b-73d1dbfa4fb5.png)

정리

1. Custom Dataset Load + (Colab + Google Drive (Mount))

   - 여기서 코드 하나 나옴! 모든 인공지능의 뼈대가 되는 코드, 간단한 코드
   - 해독을 먼저 해본다.

2. Sementic Segmentation

   - 코드 제공! 재사용성 보장되는 코드, 현업용

3. Object Detection

   - 코드 제공! 재사용성 가장 높다, 현업용, 어렵다, 구조만 파악해도 충분
   - 한땀 한땀 알고리즘 공부하는 것처럼 해야함

<br/>

좋은 수업은 스토리라인이 잘 짜여져있는 수업,

좋은 강사는 그거에 매진한다.

<br/>

---

**(※ 오늘부턴 GPU사용량 초과 문제로, 구글 코랩, 학교계정으로 새로 한다.)**

<br/>

**실제 개발시 우리만의 데이터셋 가지고 작업**

![image](https://user-images.githubusercontent.com/78403443/121325329-7904fe80-c94c-11eb-8a93-22677f959555.png)

1. Custom Dataset 만드는 방법
2. Google drive 로딩, 코랩에 마운트 시키는 방법
3. 인공지능 코드로 CustomDataset을 로드해오는 방법

<br/>

구글 드라이브 무료 용량 15GB - 일단 작업하기 충분한 용량

![image](https://user-images.githubusercontent.com/78403443/121325430-8f12bf00-c94c-11eb-815c-24c3766f919b.png)

작업하기 위한 와꾸는 만들었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121325481-9b971780-c94c-11eb-9871-2ecb15c1dc9b.png)

외국 개발자의 github...

![image](https://user-images.githubusercontent.com/78403443/121325535-a651ac80-c94c-11eb-9965-541cc4d4a0f5.png)

이 모델 중에서 가장 가볍고 좋은 모델이 MobileNetV2

<br/>

zip으로 다운

![image](https://user-images.githubusercontent.com/78403443/121325622-b6698c00-c94c-11eb-8bec-5134fa6f83a3.png)

압축된 상태로 다운, 

압축을 푼 얘를 코랩에 올려서 써본다

(D:\encore_jwc\util\ai_util\pytorch-cifar 폴더)

폴더를 업로드 하였다.

![image](https://user-images.githubusercontent.com/78403443/121325680-c5e8d500-c94c-11eb-9ac9-4334c9e96b8a.png)

코드 배포 끝...

<br/>

main.py를 돌리면 test.java와 같이 하나로 다 돌린다는 얘기.

근데 코랩에서 못돌린다.

왜냐하면, 코랩은 GPU서버 + Jupyter notebook이기 때문에

그래서 ipynb 확장자로 바꿔서 돌려야한다.

그리고, 우리는 CIFAR10을 커스텀한 데이터로 쓸거기 때문에 그것도 바꿔서 적용해야한다.

![image](https://user-images.githubusercontent.com/78403443/121325744-d39e5a80-c94c-11eb-9e4f-cf7c6e2c3f32.png)

데이터는 이곳에 박아넣을 것이다.

<br/>

**앞으로 사용하게 될 Dataset 유형들**

지금까지 사용한 Dataset 유형

1. Open Dataset → cifar10 : 압축파일로 묶여져서 제공

   ![image](https://user-images.githubusercontent.com/78403443/121325836-eca70b80-c94c-11eb-8901-d35b6543d17a.png)

   Jupyter notebook으로 쓸 때 오픈데이터셋 물리적으로 저장된 장소

   들어가보면...

   ![image](https://user-images.githubusercontent.com/78403443/121325905-faf52780-c94c-11eb-8a33-9a85f6c21531.png)

   이게 오픈데이터셋의 모습이다. 

   CIFAR10 데이터는 총 6만개 데이터가 들어있다.(training 5만개, test 1만개)

   <br/>

   첫번째 data_batch_1 이면 1~10000.jpg

   2는 10001~20000.jpg

   ...

   5는 40001~50000.jpg

   ☞ 파이토치에서는 Loading 함수 할 수 있는 문법으로 Load

   torchvision.datasets.CIFAR10( root = " ", transform = " ", ToTensor())

   이런식으로 제공된다.

![image](https://user-images.githubusercontent.com/78403443/121325967-0ba59d80-c94d-11eb-950f-7fea248097d1.png)

그런데 개발 시에는 이렇게 사용하는게 불가능하다.

① 위의 1만개 데이터 압축해서 Load 가능한건 → 워낙 이미지가 작고 가볍기 떄문(Toy Dataset이라서)

② 위처럼 압축하게 되면 시간이 너무 많이 소요됨

※ 저렇게 압축 불가능, CIFAR10() 함수 사용불가, Custom 함수 정의해야 함★

파이토치에서 torchvision으로 쓰던 문법 다 바꿔야한다.

<br/>

그래서, 

2. Custom Dataset 사용할건데, 자료모으긴 힘드니까...

   CIFAR10인데, 압축 파일로 묶여져 있지 않은 데이터면 CIFAR10을 커스텀으로 사용할 수 있음

   (오늘은 이걸로 학습)

   오늘은 이 데이터를 가지고 Custom Dataset을 어떻게 직관적으로 구성시킬 수 있을까를 먼저 확인 (이게 굉장히 중요★)

   ![image](https://user-images.githubusercontent.com/78403443/121326447-8a9ad600-c94d-11eb-9c78-4deb62a9b899.png)

   Training Data는 이미지(X), 정답(y) 두 가지가 같이 제공되어야 함, 

   이걸 어떻게 해야지만 직관적인 데이터로 만들 수 있는가를 고민해야 함

   직관적인 Data 형태란?

   train 데이터 폴더, test 데이터 폴더가 잘 이어져있어야

   CIFAR10의 카테고리는 10개니까 이걸 어떻게 구성할 수 있냐면

   train data 폴더 안에 dog, cat, frog...ship 이런식으로 개별 폴더를 만들어서 거기에 각각의 jpg파일을 넣어준다

   <br/>

   그럴 때, 중요한 얘기...

   폴더는 label이고, 각 파일들은 image가 된다. 

   폴더명을 label로 바꿔야하고, 알고리즘을 만들어야한다. 그리고 그 안에 있는건뭔지..

   이렇게 하는 것이 직관적으로 만드는 것이다.

   <br/>

   이걸 지금은 내가 데이터셋을 만들었다고 생각하고 바로 갖다 쓰면 되는 것이다.

   <br/>

   torchvision.datasets.CIFAR10( root = " ", transform = " ", ToTensor()) 이런 문법은 오픈 데이터셋일때만 쓸 수 있다!!! 

   커스텀 데이터셋은 안된다!!!

   <br/>

3. 다 설명했고, (몇백개로 알맞게 추린) 개발용 Custom dataset은 강사님이 제공해주신다.

<br/>

데이터는 https://pjreddie.com/projects/cifar-10-dataset-mirror/

이 사이트에서 받았다. (cifar.tgz 파일)

압축을 풀고 보니 아래와 같이 나온다.

![image](https://user-images.githubusercontent.com/78403443/121326660-bae27480-c94d-11eb-904a-96d0d095cdee.png)

데쉬 뒤에를 라벨로 떼야한다. 

이미지는 1, 2, 3 ... 60000 번호로

![image](https://user-images.githubusercontent.com/78403443/121326803-d8174300-c94d-11eb-9ae4-a83177cf72a0.png)

구글 드라이브 dataset\CIFAR10 폴더에 압축파일을 넣어야한다.

풀어서 개수대로 못넣는다.

구글 드라이브가 6만개 데이터를 한꺼번에 로딩을 못한다.

(각각 파일을 10개, 100개 해도 오래걸린다) 

이건, 메커니즘이 용량이 아니라 갯수제한으로 가는 것이다.

그래서 압축으로 넣음 (강사님께서 이런 우여곡절 과정을 거쳐서 이렇게 했음)

<br/>

Custom Dataset은 직관적으로 만들어져야한다. 

직관적으로 만든다는 얘기는 Label과 Image를 분리시킬 수 있는 구조로 가야하는 것이다.

통으로 압축이 되어있어서 압축된 것 통으로 올렸지만, 안에서는 압축이 되어있는 상태면 안된다.

그래서 리눅스 명령어로 압축을 풀 것이다.

<br/>

그 전에,

![image](https://user-images.githubusercontent.com/78403443/121326879-e9604f80-c94d-11eb-869c-55fdc7709586.png)먼저 main.py 파일을 ipynb로 수정해야한다.

![image](https://user-images.githubusercontent.com/78403443/121327002-03019700-c94e-11eb-9551-4d75c1cf08cd.png)

![image](https://user-images.githubusercontent.com/78403443/121327024-0a28a500-c94e-11eb-8fd5-bb1544129b95.png)

변경된 파일을 구글 드라이브에 업로드

<br/>

Custom Dataset, 구글 드라이브라는 cloud 환경에 load된 데이터셋...

![image](https://user-images.githubusercontent.com/78403443/121327087-17de2a80-c94e-11eb-8ae1-5e8e30941d67.png)

어떻게 코랩에다가 로드시키는가? 본다.

![image](https://user-images.githubusercontent.com/78403443/121327217-3512f900-c94e-11eb-8199-7fb29d6b1be5.png)

코랩이기 때문에 main.ipynb 열어서 돌린다.

![image](https://user-images.githubusercontent.com/78403443/121327263-40662480-c94e-11eb-8292-8ead7244f5bf.png)

로드시키고, 압축까지 푼 과정의 코드

<br/>

![image](https://user-images.githubusercontent.com/78403443/121327326-4fe56d80-c94e-11eb-8643-b6932f8d12b9.png)

파이토치에서 쓰던 맨 첫번째줄 구문 두 줄을 한줄로 바꾼 것

<br/>

![image](https://user-images.githubusercontent.com/78403443/121327610-8de29180-c94e-11eb-8591-45b3504a80a9.png)

인증코드를 입력해야한다. 

링크를 누르고, 창이 뜨면 사용할 구글 계정을 누르고, 허용을 누르고

![image](https://user-images.githubusercontent.com/78403443/121327449-6a1f4b80-c94e-11eb-9086-b37efbe32984.png)

코드를 복사해서 아까 빈칸에 넣는다.

![image](https://user-images.githubusercontent.com/78403443/121327793-bbc7d600-c94e-11eb-94d1-11e5a11974d2.png)

![image](https://user-images.githubusercontent.com/78403443/121327819-c2eee400-c94e-11eb-9de3-22582d9fe2c4.png)

결과를 확인해보았다. 잘 되었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121327893-d13d0000-c94e-11eb-9d98-069c69615342.png)

Epoch를 20으로 바꿔서 다시 돌린다.

<br/>

**Colab과 Google Drive 연결하기**

**main.ipynb파일 코드 설명**

![image](https://user-images.githubusercontent.com/78403443/121327961-e023b280-c94e-11eb-9102-2bd0b3574efd.png)

왼쪽이 구글 드라이브, 오른쪽이 코랩

<br/>

①

CIFAR10.tgz 압축파일이 cloud환경에 로드되어있는 상황이다. (압축형태로 로드되었다)

원래는, image 여러개를(하나당 3kb) 로드하려고 했는데 속도가 너무 안나와서 어려웠다.

그래서, 압축형태로 파일 하나를 올렸다.

<br/>

②

이 데이터를 코랩에서 사용해야한다.

먼저, 코랩이 구글 드라이브를 import 해야한다.

from google.colab import drive 구문을 반드시 적용해야한다.

<br/>

③

그리고 그 데이터를 붙인다고 하는데...

그 뜻 :: 데이터 mount를 해온다. 

drive.mount('colab의 home 밑으로 경로 지정' 해주면 된다)

이때 colab의 밑이 content 라는 곳인데 거기에 있다.

<br/>

정리 :: 

1. Cloud 기반의 Dataset을 압축 파일 형태로 코딩

2. 1번의 데이터를 Colab에서 사용하려면

   - ① 구글 드라이브 import
   - ② Colab 홈 밑의 경로에 mount(붙인다)

<br/>

이것이 크게 봤을 때 세가지 과정이다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/121328113-03e6f880-c94f-11eb-8e41-15ae7b89f70b.png)

(첫번째, 두번째 문단) 

코랩 경로 잡아주고, 디렉토리 경로 잡아줘야한다.

(세번째 문단)

import는 파이썬만 가능하다. 

ipynb 파일을 import할 수 있는 모듈을 설치한 것이다.

ipynb 모듈이 content 경로에 있을때만 import가 된다.

<br/>

(코드 첫번째 + 두번째 문단 자세히 설명)

![image](https://user-images.githubusercontent.com/78403443/121328183-12351480-c94f-11eb-9c2a-1db9e46a57ea.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121328236-1bbe7c80-c94f-11eb-9528-e5938fe2b9d4.png)

이렇게 content\drive\MyDrive\Colab Notebooks\2. Classification\pytorch-cifar 안에 Mount하겠다는 것, 코드 두번째 문단

<br/>

![image](https://user-images.githubusercontent.com/78403443/121328288-2a0c9880-c94f-11eb-9f74-f085e7ebddfa.png)

Network로 코랩에서 로딩할 때

- 속도 오래걸린다.
- 네트워크 갯수 제한

결론 :: 압축파일을 copy해서 전송

<br/>

코랩 로컬에서 압축파일 해제하는 건 속도가 괜찮다.

이렇게 만들어 놓으면 계속 이렇게 쓰면 된다. (강사님이 힘들게 만드셨다)

<br/>

다시 코드를 본다.

![image](https://user-images.githubusercontent.com/78403443/121328355-37c21e00-c94f-11eb-96e0-d92d3fb32671.png)

%cp 명령어가 뭐냐면 구글 드라이브에 있는 cifar.tgz 압축파일을 카피해서 코랩로컬(content\sample_data) 이 안으로 저장해오겠다. 라는 뜻

'/content/sample_data' 이 부분은 코랩의 로컬이다.

(에러 때문에 상대경로가 아닌 절대경로로 잡은 것이다)

<br/>

구글 드라이브 영역에서 copy해서 colab 로컬에다 저장한 것이다.

압축을 풀어 drive 밑에 들어가면 코랩이랑 연결된다.

![image](https://user-images.githubusercontent.com/78403443/121328425-46a8d080-c94f-11eb-96d3-6fc211560ae8.png)

sample_data는 colab의 로컬 폴더이다.

<br/>

로컬에선 제한영향을 안받는다.

그래서 로컬 위치에서 압축을 풀었다.

현재의 작업 디렉토리는 무조건 content로 잡히기 때문

![image](https://user-images.githubusercontent.com/78403443/121328489-545e5600-c94f-11eb-8f9c-42141719f86e.png)

<br/>

지금까지 했던 얘기들을 주석으로 다시 설명 (main.ipynb 파일 참고)

<br/>

코랩과 구글 드라이브 연동의

중요한 지점 = 압축한걸 구글 드라이브에 업로드하고, 압축을 colab의 로컬에서 풀면 제한이 안걸린다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/121328579-67712600-c94f-11eb-9c67-3c22d33582d5.png)

체크한 부분은 코랩 로컬, checkpoint는 주피터 노트북의 checkpoint와 같다.

drive에는 모든 코드가 저장된다. -- 구글 드라이브

<br/>

이 코드가 인공지능의 뼈대가 되는 코드

이거 이해 못하면 앞으로의 내용 이해 못한다.

계속 쓰면 된다.

<br/>

두번째 코드 설명

![image](https://user-images.githubusercontent.com/78403443/121328655-78ba3280-c94f-11eb-8b1f-1b41186716cd.png)

drop_last는 마지막 배치를 버릴 것인지를 의미

실제 네트워크에 로드할 때는 drop_last = True 해야된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121328886-ab642b00-c94f-11eb-83ee-226f08521b80.png)

models 패키지에 있는 모든걸 다 가져와라 라는 뜻 

models 안으로 들어가면 여러개의 파일이 있다.

![image](https://user-images.githubusercontent.com/78403443/121328988-c33baf00-c94f-11eb-8e92-b701215b5ca6.png)

![image](https://user-images.githubusercontent.com/78403443/121329053-d0f13480-c94f-11eb-936e-a4219a19e787.png)

이게 먼저 import 된다는 얘기

이 안으로 들어가면

![image](https://user-images.githubusercontent.com/78403443/121329103-de0e2380-c94f-11eb-9bb8-61d91597b3e0.png)

우리가 선택해서 사용할 수 있는 여러 모델들이 다 나와있다.

<br/>

나머지 코드들 설명

(실제 코드에 조금 가까운 코드지 완전 완벽한건 아님, 이것도 약한 코드라는 얘기)

첫번째 셀

![image](https://user-images.githubusercontent.com/78403443/121329166-ec5c3f80-c94f-11eb-9780-1e9f9781ffda.png)

Calling 해야 work한다.

<br/>

두번째 셀

![image](https://user-images.githubusercontent.com/78403443/121329226-f8e09800-c94f-11eb-92df-61e6fba7c3aa.png)

데이터 로딩하는 부분

<br/>

![image](https://user-images.githubusercontent.com/78403443/121329264-05fd8700-c950-11eb-9d6a-9ec08f29f750.png)

![image](https://user-images.githubusercontent.com/78403443/121329293-0c8bfe80-c950-11eb-9edf-4ad3eb7b9cfe.png)

![image](https://user-images.githubusercontent.com/78403443/121329320-131a7600-c950-11eb-982c-ebabce8ab17d.png)

train이 먼저 동작하고, 그 다음 test가 동작

<br/>

![image](https://user-images.githubusercontent.com/78403443/121329379-20cffb80-c950-11eb-98bc-59598d004e1a.png)

![image](https://user-images.githubusercontent.com/78403443/121329416-27f70980-c950-11eb-8857-4750dee135d7.png)

main.ipynb에서 세개의 코드가 다 도는 것이다.

import 한거 보면 짚고 넘어갔어야 하는 부분...

<br/>

![image](https://user-images.githubusercontent.com/78403443/121329526-41985100-c950-11eb-9934-2d2b807d8f6f.png)

padding 4를 주고 crop하게 되면

주변 변두리가 까맣게 됨... 까맣게 된 부분 제외하고(셰도우 처리하고), 진한 노란부분만 건지는 것이다.

이렇게 되면 두가지가 됨

1. 변형

   - darkness
   - 자르고

이게 영리한 Augmentation 기법

<br/>

초록부분은 그럼 어떻게?

horizental flip, 좌우반전 시킴

그리고 마지막에 ToTensor() 써서 tensor type로 바꾸고, channel 앞으로하고,

0~1 스케일링

<br/>

현업에서 이런 방법 많이 쓴다.

<br/>

우리가 오늘 발표하면서 CIFAR10 제일 높은 Accuracy가 85%였는데, 굉장히 높게 나온 것이다.

왜 우리는 낮게 나왔을까? Data Augmentation(데이터 변형)적용 안하고 85% 나온건 엄청 높게 나온 것.

Data Augmentation(데이터 변형)적용하면 93% 이상 나온다.

근데... 지금까지 안가르쳐준건 

Data Augmentation은 코드로 구현되기 굉장히 복잡하다. 

그래서 영리하게 해야한다. 어떤 순서로 작업해야하는지 중요!

이 작업을 경험하고 아는 사람은 Data Augmentation할 때 어떤 순서로 작업해야하는지 중요하게 생각하고 진행함

<br/>

![image](https://user-images.githubusercontent.com/78403443/121329644-5aa10200-c950-11eb-918d-46aea59a0664.png)

위는 원래 문법... 

실제로 실행한 코드는 강사님이 직접 만드신 데이터 load하는 모듈

이런거 직접 자기가 모듈 만들어서 써야한다.

<br/>

**dataset.ipynb 파일보기**

![image](https://user-images.githubusercontent.com/78403443/121330061-b1a6d700-c950-11eb-9400-19bca292beb4.png)

라벨 (함수)정의

![image](https://user-images.githubusercontent.com/78403443/121330134-bd929900-c950-11eb-8a7d-44901ae383ac.png)

![image](https://user-images.githubusercontent.com/78403443/121330413-f599dc00-c950-11eb-80dc-cd820a7fc5d6.png)

<br/>

main.ipynb에서 (다시 main.ipynb로)

![image](https://user-images.githubusercontent.com/78403443/121330482-05b1bb80-c951-11eb-9d46-342145a37499.png)

이 함수로 가져다 쓴 것

<br/>

![image](https://user-images.githubusercontent.com/78403443/121330535-119d7d80-c951-11eb-9e75-b6d36cc134df.png)

이 부분은 첫번째 셀에서 False로 줬기 때문에 돌아가지 않는다.

Epoch를 한번만 실행하게 되면 True로 바뀌게...

![image](https://user-images.githubusercontent.com/78403443/121330624-2417b700-c951-11eb-99d5-8140278f7686.png)

첫번째 셀에서 resume = False로 해서 checkpoint를 생성하게 한다. 

(최초 실행시, 그래서 아까 1 epoch 주고 먼저 실행시킨 것임)

(1 epoch 돌려놔야 checkpoint 폴더가 생긴다)

(그러면, checkpoint 생성 뒤의 실행 때는 true로 바꿔서 실행시켜야 함)

저장하고 나서 validation test로 넘어가고, 

돌 때마다 더 accuracy 가장 높은 것, Loss는 가장 낮은 것을 다시 또 checkpoint에 저장한다.

<br/>

weight 값, epoch, accuracy 맵 형태로 저장되는 것임

<br/>

이렇게 되면 처음부터 학습할 필요가 없고, 체크포인트 저장 위치부터 이어서 하는 것임

<br/>

![image](https://user-images.githubusercontent.com/78403443/121330708-3a257780-c951-11eb-8dc3-fe023be07140.png)

표시한 이 부분 설명

![image](https://user-images.githubusercontent.com/78403443/121330756-43aedf80-c951-11eb-9c81-69b26f90bfec.png)

testloader(5만개)데이터가 image, label이 100개씩 압축되어져서 할당

아까 dataset.ipynb의 getitem() 함수가 100번 호출된다. (getitem() 함수는 강사님이 만들었다)

그럼 image 100개 label 100개 나올 것이다. 이거를 압축하고,

그걸 각각 이미지, 라벨로 넣는다.

<br/>

getitem() 함수 호출은 DataLoader가 해주는 역할

여기 설명에는 기술적인 Jumping이 있다.

DataLoader는 굉장히 복잡하기 때문에 그냥 그렇게 되있다고만 알고 넘어간다.

<br/>

어쨋든 100개이기 때문에 총 500번 반복되어 500이 출력 뜰 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121330838-53c6bf00-c951-11eb-89f1-95519afcce2c.png)

표시한 부분은 후처리부분이다. 

utils.py 파일에 있는거 따라서 넣어준것이다. 이거는 그냥 관례이다. (뜯어보면 복잡하므로 그렇게 알고 넘어간다)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121330975-70fb8d80-c951-11eb-86bf-7f4549ec5604.png)

이게 validation test... 

(하지만, 위처럼 코드에는 따로 쓰지 않는다. 딱 보고 validation 이라는 거 알아야 함)

최저의 Loss가 낮은 것만을 저장한다.

Accuracy는 높은 것만을 저장한다.

<br/>

train에서 돌고, test 돈 후에 test에서 저장한다.

<br/>

**vgg모델 확인**

models폴더 vgg.py 파일 본다.

![image](https://user-images.githubusercontent.com/78403443/121331070-8375c700-c951-11eb-96f7-465f47ab620e.png)

맨 위 cfg 부분 :: 리스트를 채널과 pooling값들을 묶어놓고 가져다 쓰도록 한 것이다.

<br/>

그 다음 부분 :: (우리가 그동안 썼던 방법이었음)

class 정의 부분은 하나하나 지정해주는 방법이다.

밑줄은 레이어를 어떻게 구성할건지 정의해준 것이다.

(추가설명 - 아래 이미지)

![image](https://user-images.githubusercontent.com/78403443/121331165-95576a00-c951-11eb-82d9-2f5f67c1681c.png)
