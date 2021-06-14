## 2021.06.14 Semantic Segmentation, Object Detection

**Semantic Segmentation**

<br/>

ISIC 데이터

![image](https://user-images.githubusercontent.com/78403443/121848409-f2be3300-cd24-11eb-9ffc-34e8561beb67.png)

![image](https://user-images.githubusercontent.com/78403443/121848440-fa7dd780-cd24-11eb-87e6-775b8ec58ef1.png)

image 폴더, label 폴더 있다.. 

~.txt 파일이 하나 더 존재(이번에 처음 나왔다)

위 이미지와 같이 500줄이 있다. 

![image](https://user-images.githubusercontent.com/78403443/121848470-06699980-cd25-11eb-8c2a-1e4bffbf75c5.png)

이미지 파일 정보 /이미지에 대한 라벨 정보

- ① 공백 앞 부분 = 이미지 파일 절대 경로
- ② 뒷 부분 = 답지의 절대경로

<br/>

⑴

이전 방식(txt 파일이 없었을 때)

(이런 코드가 있었다) → sort(os.listdir(image_root)) 이렇게 저장

마찬가지 라벨도 label_list = sort(os.listdir(label_root))

☞ 이렇게 해서 해당 경로에 있는 image / label을 load해옴

(폴더를 직접 찾는 방식, 자유도가 있다)

<br/>

⑵

지금 방식(txt 파일 있는 경우)

위와 같은 코드 없고, 다른 방법으로 한다. 

→ dataset.py 에서 다르게 작성 → txt파일 정보(txt파일 경로에서 찾아온다)

<br/>

현재 인공지능 개발자들이 하는 형식이 이와 지금 방식과 같은 형식이다. 더 선호!

왜?

image나 label이나 예를 들어 5만개 넣어야 한다고 하면 실수가 많이 발생한다.

(하나를 더 넣거나 덜 넣거나 하는 실수)

이렇게 되면 답지가 한 칸씩 싹 다 밀리게 된다.

이런 실수가 더 잦아지는 방법이 ⑵ 지금 방식의 방법이다.

그런데 왜 쓸까?

![image](https://user-images.githubusercontent.com/78403443/121848522-20a37780-cd25-11eb-9596-6a1ec24ce773.png)

이미 학습이 끝난 이미지, 조금 더 학습을 해야 하는 이미지가 있다고 하면

폴더를 두개로 나눠서 관리를 해야한다.

그렇게 되면 이미지가 바뀔 때마다 수정할 때 알고리즘을 변경하는 등의 번거로움이 생긴다.

⑵의 방식은 내가 필요한 것만 골라서 필요한 라인만 쓸 수 있기 때문에 효율적으로 관리가 가능하다.

훨씬 더 사용적인 측면에서 편리하다.

<br/>

- **train.ipynb 파일 보기**

딱 2군데 정도 언급을 해보도록 한다.

![image](https://user-images.githubusercontent.com/78403443/121848572-3153ed80-cd25-11eb-849a-a4d58222d823.png)

먼저, 위 이미지 빨간 네모 박스 표시한 부분 설명

구글 내부 개발자들이 이런식으로 쓴다.

Step Learning Rate

<br/>

먼저 어떤식으로 동작하는지 설명

![image](https://user-images.githubusercontent.com/78403443/121848603-3ca71900-cd25-11eb-8231-c8af0b097022.png)

Epoch수, 학습이 진행될수록 늘어남

Loss, 학습이 진행될수록 작아질 것임. 

보통 이런식으로 진행되어야 한다. 

학습이 진행될수록 Learning Rate도 조금씩 줄어들어야 한다. (빨간색 선)

Step Learning Rate는 가파르게 줄어든다. (주황색 선 같이)

반면에, (분홍색 선 같이) 천천히 줄어들 수도 있다.

학습의 진행되는 정도에 따라서 Learning Rate를 정교하고 디테일하게 줄일 수 있다는 말이다.

<br/>

어떻게 줄일 수 있는지 나와있는게 아까 네모 표시한 코드이다.

(출처 : https://pytorch.org/docs/stable/optim.html)

![image](https://user-images.githubusercontent.com/78403443/121848649-4af53500-cd25-11eb-90a6-6dc1a150b053.png)

![image](https://user-images.githubusercontent.com/78403443/121848671-52b4d980-cd25-11eb-861f-7c445c1e2a16.png)

요렇게 동작하는 것이다. Example부분과 함께 맨 위 CLASS 부분 참고

```python
'''
torch.optim.lr_scheduler.StepLR(   )

→ 학습을 진행함에 따라서 Learning Rate를 어떻게 줄여가야 하는지를
  정밀하게 설계하는 기능
'''

for i in range(num_epochs) : # num_epochs ex) 100이면
    if i < 20 : # 0~20번 학습 진행
        lr = 0.1
    elif 20 <= i < 40 : # 20~40번 학습 진행
        lr = 0.01
    elif 40 <= i < 60 : # 40~60번 학습 진행
        lr = 0.01

'''        
(제어문 사용해서) 코드로 작성한다면 이런식으로 길어진다...
이걸 다 담고 있는 것이 
torch.optim.lr_scheduler.StepLR(   ) 라는 것이다.
여기 안에 Step_size 라는 것이 있다. 위와 같이 하려면 어떻게?

step_size = 20, (학습을 20번 단위로 끊는 것이니까)

(gamma 는 learning rate를 얼마씩 곱해라~ 라고 하는 것)
gamma 0.1 하면 = 0.1씩 learning rate를 곱한다.

보폭과 속도를 조정하는 옵션 이렇게 썼다.
'''
```

![image](https://user-images.githubusercontent.com/78403443/121848984-c525b980-cd25-11eb-9b68-1a71f68cc538.png)

파이토치로 이런 것 쓴다는게... 

이런 부분이 그대로 현업에서 진행되고 있다는 것이다.

<br/>

이런식으로 학습의 보폭을 줄이는 것이 Step Learning Rate이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121849047-d373d580-cd25-11eb-979a-5e07f64807f0.png)

이 부분은 안돌아갈거다... 

그래서 config 폴더 ISIC.yaml 파일 보자.

![image](https://user-images.githubusercontent.com/78403443/121849107-e9819600-cd25-11eb-89d2-dc2b6d5ce774.png)

여기선 weight라고 썼지만 저번에 봤던 resume 기능과 동일하다. 

이 yaml파일에서 path가 없어서 False일 경우이면, 돌아가지 않는다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121849153-f56d5800-cd25-11eb-87cd-475f699675fd.png)

이번엔 strict = False 설명한다.

![image](https://user-images.githubusercontent.com/78403443/121849188-fef6c000-cd25-11eb-8d1b-96a105c464af.png)

```python
model.load_state_dict(Strict = False) # 의미를 알아본다. 
# load_state_dict는 weight값 받아오는 기능

'''
각각 다른 네트워크 A, B가 있다. A는 layer 10개...
Network A에서 각각이 블락 구분되는 이유는 Activation 처리가 되어져 있을것이기 때문...

반면에 Network B는 Layer가 총 11개짜리이다.
둘은 다르다. 
하지만 Dataset만 다르고 둘다 Classification을 하는 모델이다.

Network A가 학습을 진행하면 
load_state_dict에 의해서 계산된 weight값이 저장되어 있을 것이다. 

그리고 Network B에서 학습을 돌리는데, 처음부터 학습을 진행할 필요가 없다.
왜?
Network A에서 이미 학습한 weight값을 그대로 사용할 수가 있기 때문
그러면, 훨씬 학습이 빨리 효과적으로 이루어지게 된다.

그런데 이때
Strict = True로 하면 Error 떨어진다!
둘이 layer수가 다르게 때문에... 엄격한 것이다.
True로 하려면 layer수를 같게 해야한다.

너무 엄격하게 하지말라는 의미로 Strict = False로 주는 것이다.
'''
```

정리 :: 

Network A에서 이미 학습이 완료되었다면, 그 weight값을 받아와서

Network B를 학습시키는데 사용할 수 있다.

☞ 이렇게 되면 훨씬 학습효과도 좋고, 학습속도도 빠르다!

단, 두개의 Network가 동일하지 않기 때문에 Strict = False로 반드시 해줘야한다!

(안그러면 Error 떨어진다!)

(★ 굉장히 중요~! Object Detection에서 나온다!!!!!!!!)

<br/>

---

- **models 폴더 unet.ipynb 파일 보기**

![image](https://user-images.githubusercontent.com/78403443/121849392-3b2a2080-cd26-11eb-85ac-b584a634a916.png)

2번 module.py로 빼놓고 거기서 뽑아쓰는 방법...확인해본다

models 폴더 들어가자.

![image](https://user-images.githubusercontent.com/78403443/121849429-45e4b580-cd26-11eb-88b5-ed0a6bde0ad4.png)

이게 뭘까?

이게 모듈화... 빼놓은 거라는 얘기다.

module.py 파일 보자.

![image](https://user-images.githubusercontent.com/78403443/121849461-4ed58700-cd26-11eb-81b6-21a59b223473.png)

이거 그냥 호출해서 쓰라는 얘기다 (줄 표시)

![image](https://user-images.githubusercontent.com/78403443/121849480-585eef00-cd26-11eb-963c-aa1413c8c685.png)

이런식으로 모듈화 시켜놓고 뽑아 쓸 수 있다는 얘기다.

이런식으로 함수로 만들어놓고 함수로 호출해서 쓸 수도 있지만...

우리는 unet.ipynb 파일 보면 알지만... 직관적인 방법으로 만들었다. (선택사항)

<br/>

unet.ipynb 파일 보기

![image](https://user-images.githubusercontent.com/78403443/121849528-657bde00-cd26-11eb-89c4-10c0106081ec.png)

사이즈 늘리고, 붙이는 부분...

<br/>

![image](https://user-images.githubusercontent.com/78403443/121849614-804e5280-cd26-11eb-8307-73a21285e732.png)

여기서 기본 채널이 지정이 된다.

unet32로 지정하게 되면 가벼운 모델이다.

unet128은 무거운 모델이다. 위와 반대가 된다. 성능이 어느정도 보장...코드 작성하는 사람의 자율도

else문에 이 밖의 채널이 들어오면 에러나도록 작성함

<br/>

base_channel은 컴퓨터 파워와 연관이 있다.

base_channel은 뭐냐면 만약, 내 컴퓨터 파워가 감당이 되면

unet128로 가지만, 감당이 안되면 unet32로 돌린다. (unet32가 가벼우니까... 대신 성능은 비교적 낮다) 

base_channel은 코드 작성하는 사람의 자율이다.

<br/>

down4 까지가 downsampling(같은말 : Convolution, Encoding)이기 때문에 256에서 더 이상 안올라간다.

Encoding은 특징을 추출하는 것, 특징의 개수를 늘리는게 중요, 사이즈는 중요하지 않기 때문에 줄어든다.

채널은 2배수로 늘린다. (이건 무조건 이렇게 해야한다, 뭔진 모르겠지만 네트워크 전문가들이 2배수가 좋다고 한다)

<br/>

up1부터 upsampling, Decoding, Interpolate

down 마지막은 256이었는데, 왜 512로 시작되는가? 

upsampling은 사이즈가 늘어나는 대신에 채널이 줄어야한다.

256짜리가 concat이 되기 때문에 512가 되는 것이다. 그리고 128...

그리고 128짜리가 concat되서 두개가 되기 때문에 256이 되는 것이다.

<br/>

그리고 마지막은 32 → 2이렇게 출력되는게 Downsampling, Upsampling이다.

이와 같이 채널이 바뀌는 이유에 대해서 알아야한다... Concat!!

<br/>

---

---

---

(※ pdf 캡쳐파일은 저작권 문제로 인해 업로드 하지 않습니다) 

**Object Detection**

- 8.Object Detection.pdf 파일 보기 

<br/>

우리가 다루는 모델은 아니지만 Object Detection과 GAN이라는게 또 있다.

<br/>

중요한 모델들은 빨간색으로 표시를 해보았다.

2019년도까지 정리

Object Detection모델은 굉장히 많은데

여기서 눈 여겨볼게 있는게 Object Detection의 시초가 된 모델이 R-CNN이다.

<br/>

Object Detection 모델의 카테고리는

- ① R-CNN 류

  - 위 PDF 1), 2), 3), 4)번이 R-CNN류이다.

- ② YOLO류

  - 1,2,3 버전이 있는데 4는 2020년에 나옴
  - 이거 중에서도 YOLO3로 코드 돌리는 방법 알려줌(코드 돌릴 수는 없음)

<br/>

(Object Detection은 다른 방법으로 코드를 돌려야 하는데 그건 나중에 본다)

(위  2), 3), 4)번은 아예 보지 않는다, 쓰이지 않기 때문, YOLO와 완전이 다르다(구조가 완전 다르다))

그래서, YOLO로 바로 들어간다

그 전에 Object Detection의 시초인 1) R-CNN은 조금 보고 들어간다.

<br/>

매년 버전이 나왔다는 것은 해마다 따박따박 YOLO 관련한 논문이 나왔다는 얘기임

그리고 논문이 SSD는 한번만 발표하고 더 이상 발표되지 않음. 

그런 부분 눈여겨봐야한다.

<br/>

Object Detection은 2개의 파로 나뉜다. (구조가 다르다는 말)

하나가 R-CNN류, 또 하나 YOLO류

YOLOv4가 가장 최근에 나옴.

<br/>

구조가 다르기 때문에 YOLO를 이해하기 위해서 (R-CNN류를 다 보지 않지만)

R-CNN은 살펴볼 필요가 있다. 

순서는 R-CNN 살펴보고, 바로 YOLO로 들어갈 것이다.

YOLO는 1, 2, 3버전까지만 볼 것이다. (step by step)

<br/>

구조가 다르다는 얘기 ::

R-CNN은 Region Proposal 기반으로 작동한다.

YOLO는 Regression 기반으로 작동한다.

<br/>

YOLOv3가 나온뒤에 EfficientDet이 나왔다.(Det은 Detection을 의미한다)

EfficientDet은 말도 안되는 네트워크 모델이다... 그말은 가성비가 좋은 모델 (속도가 어마어마하게 빠르면서 성능이 좋게 나온다)

가성비가 좋은 모델을 하나 꼽으라면 EfficientDet

감히, YOLO4가 견줄 수 있다.

최근 논문의 양대산맥이라고 볼 수 있다.

<br/>

스타트업에서는 아직도 YOLO 1을 쓰고 있다.

국내 굴지의 대기업에서 EfficientDet과 YOLO4를 쓰고있다. 

(당연히 YOLO4 써야되지 않냐는 말 == 틀린 말)

<br/>

딥러닝을 할 때는 입력이 뭔지   |   출력이 뭔지

이것부터 구분을 하고 들어가야한다.

<br/>

이거를 네트워크에 입력해서 학습 시킨 결과가 밑줄과 같이 나온다는 얘기...

그 말은 감지할 수 있는 사물이 총 3개이기 때문에

bbox(boundary box)라고 하는데 이 결과가 총 3개가 나온다. 

이게 출력결과이다.

출력결과를 후처리(Visualization)한 결과가 output(이미지)이다.

![image](https://user-images.githubusercontent.com/78403443/121849916-f05cd880-cd26-11eb-8270-1c3fc82d1016.png)

x1, y1, h1, w1 무슨 값일까?

h, w는 박스의 중심점을 기점으로 가로,세로 사이즈

x는 박스 가로의 중심점 좌표

y는 박스 세로의 중심점 좌표

![image](https://user-images.githubusercontent.com/78403443/121849943-fe125e00-cd26-11eb-94f7-4b11fee6c281.png)

맨 마지막 값은 출력 카테고리 중에서 가장 큰 값으로 예측한 결과값

<br/>

입력과 출력이 뭐다 라고 충분히 이해하고 넘어가는 것이 중요하다!

<br/>

R-CNN은 2013년도 말, Segmentation 전에 나왔다.

이때까지의 CNN은 Classification(분류)밖에 못하는 네트워크였다.

<br/>

R-CNN은 총 4단계로 이루어진다. 

1. 이미지가 입력되는 단계

   - 여기서 개체로 감지해야되는데, 잘 감지하려면 위 경우는 사람과 말로 감지해야한다.
   - 그러기 위해서 이미지가 입력되는 단계

2. region proposal 단계

   - 뒤 페이지...

     - region을 제안해주는 단계

     - Selective Search Algorithm 이라는 알고리즘이 돌아간다.

       - 인공지능 알고리즘이 아니다! == 학습되는게 아니다

       - 단순한 알고리즘인데, 내부적으로는 상당히 복잡하다

       - 비슷한 색끼리, 비슷한 패턴끼리, 비슷한 질감끼리 묶어주는 알고리즘

       - 어떻게 돌아가는지 알 필요는 없다. 이정도 알면 충분하다

         - 색깔이나 질감이 조금만 달라도 세세하게 구분 ☞ 1단계
         - 조금 공통점 찾아서 구분 ☞ 2단계
         - 조금 더 공통점 찾아서 구분 ☞ 3단계
         - 너무 러프해짐 ☞ 4단계

       - 한 3단계 정도되면 구분을 너무 러프하게 하지도 않았고, 너무 디테일하게 하지도 않았고<br>
         어느정도 잘 구분됐다고 볼 수 있는 알고리즘이 Selective Search Algorithm!!!

       - Selective Search Algorithm은 색깔로 덩어리로 묶어주는 알고리즘이다.

     - Selective Search Algorithm만 생각하면 위 Input image를 한 덩어리로 묶어줄 수 있나 없나?<br>
       안묶일 가능성이 크다. 모자색상, 얼굴, 셔츠의 패턴이 다 다르기 때문<br>
       그래서, Selective Search Algorithm 만으로는 안 묶이는 것들이 굉장히 많다는 얘기다.<br>
       그래서, 어떤 대안책을 쓰냐?<br>
       box를 굉장히 많이 쳐주자는 것이다.<br>
       그러다보면, 사람과 말이 쳐지는 경우가 생길 것이라는 얘기다.<br>
       이런 제안을 평균 2000개 정도 한다. (1500개~2000개 내외)<br>
       이게 두번째 단계이다.<br>
       
     - 이미지는 1개인데, 네트워크 들어가는 단계에서는 이미지가 2000개가 들어가는 것이다.<br>
       (얼마전까지는, 이렇게 했다...!)<br>

3. 3단계 :: 동일한 사이즈로 압축해서 Network로 이미지를 집어넣는다. 

     - 똑같은 사이즈만 Network안에 들어갈 수 있다!

     - 2000개 정도의 Region Proposal로 제안된 모든 이미지들을 일정한 사이즈로 압축시킨다.

     - 그럼 한 이미지당 2000개 정도의 압축한 이미지들이 나온다.

     - 동일한 사이즈의 이미지가 들어가야한다!

     - 뒷 페이지에 자세하게 나와있다.

       - 우리는 이미지를 같게 하기 위해서 그동안에는 import cv2, cv2.resizing(240,240) 하거나<br>
         torch.reshape(240,240)으로 사이즈를 조절했다.<br>

       - 2천개 전부다 압축하기 때문에 (2천개 전부다 Network를 통과해야하기 때문에)<br>
         Computation Cost가 엄청나다 → R-CNN의 최대 단점이다.<br>

       - 이미지를 넣는데 시간이 얼마나 소요되나..?<br>
         이미지 한장 처리하는데 1분정도 소요되므로 꽤 오랜시간이 걸릴것이다.<br>

       - 학습은? 특징 압축때 학습이 진행<br>

4. 4단계 :: 압축된 이미지 2천개가 네트워크를 거쳐서 2천개 하나하나에 대한 분류작업 진행 (사람이냐, 말이냐 등...)

      - SVM

      - 그림으로 설명
        ![image](https://user-images.githubusercontent.com/78403443/121850324-914b9380-cd27-11eb-8d57-283200b76024.png)

      - FCL로 쫙 펼쳐서 4096개로 만든다.

      - 독특한건, 여기서 copy해서 똑같은 4096개 들어있는 Vector를 또 만든다.

      - 그리고, 여기서 SVM을 진행한다.

      - 이쪽과 이쪽을 구분하는 이진분류를 진행하는데, 물체가 있는지 없는지 구분...<br>
        이 구분을 SVM으로 한다!<br>

      - 여기서 1에 가깝게 나오면 물체이고, 0에 가깝게 나오면 물체가 아니다.

      - 이때, Thresh hold값은 0.9로 준다.(굉장히 높게 준다)<br>
        그 얘긴, 정말 확실한 값만 물체로 취급한다는 얘기<br>

      - 그리고, argmax로 10개의 최종출력값(라벨)과 연결

      - 실질적인 Classification 한다.

      - 왜 SVM을 썼냐?<br>
        AlexNet이 나온지 얼마 안된 시점<br>
        SVM은 머신러닝 쪽에서 성능이 꽤 잘 나온다(딥러닝측에서는 잘 안쓰지만...)<br>

<br/>

이것이 R-CNN 방법이다!

그래서 마무리하면, Threshold값이 0.9이상인 추출결과에 대해서만 Classification을 진행했다. 라고 정리!

<br/>

R-CNN의 문제점

<br/>

치명적 단점이다...

1. 시간이 너무 오래 걸린다. Computation Cost도 너무 많이 들어간다.

2. Selective Search Algorithm / SVM 둘다 인공지능 알고리즘이 아니다 == 학습이 되는 알고리즘이 아니다.

   학습되지 않는 알고리즘이다.

<br/>

그래서, Fast-R-CNN이 나중에 나온다. 

그래도 부족해서 시간을 더 줄인다. Faster-R-CNN이 나옴

이렇게 진행되는게 Region Proposal Base 방식의 Object Detection 구조이다.

<br/>

이건 Object Detection의 시조격이기 때문에 정성들여 살펴봤지만 같은 방식의 이후 버전에 대해서는 더이상은 살피지 않는다.

<br/>

YOLO로 들어가기 전에 잠깐 더 살펴본다...

<br/>

R-CNN과 Fast R-CNN간의 학습과 테스트하는데 걸리는 시간 비교

<br/>

YOLO는 You Only Look Once의 약자이다.

딱 한번만 본다. 

딱 한번만 Forward 진행한다는 뜻이다.

아까 확인했듯이 R-CNN은 2000번 Forward 하는 반면 YOLO는 딱 한번

참고로, YOLO가 모델 Paper 제목이 아니다.

<br/>

YOLO는 속도가 매우 빠르고 그에 대비해서 mIoU(성능 평가 지수)는 조금 떨어지는 LowAndModel

R-CNN은 이미지 한장 처리하는데 49초 걸린다.

YOLO는 0.04초 걸린다.

Q. 1초에 이미지 몇장처리?

1/0.04 = 25개 처리 가능 (25 * 0.04 = 1)

FPS(초당 처리하는 Frame 갯수)가 결과적으로 25가 되는 것이다.

인간이 자연스러운 동작을 보는데 FPS 10... FPS = 25라는건 어마어마하게 빨리 처리하는 것임

<br/>

mAP(성능 지수)는 Accuracy랑 똑같다고 생각하면 된다.

오른쪽 그래프를 보면 왼쪽에선 FPS가 결과적으로 25라고 나왔는데, 오른쪽에선 45다. 

이렇게 FPS가 다르게 기재되는 이유가 뭔가?

☆ YOLO는 실행되는 Computer power(컴퓨터 사양)에 따라서 차이가 있다.

100만원짜리 컴퓨터 vs 5천만원짜리 컴퓨터에서 돌리는 차이가 클 수 있다는 얘기

논문에 성능평가시에는 반드시, 무슨 GPU를 사용했는지 디테일하게, 정확하게 기재해야 한다. (☆ 중요한 항목임)

이렇게 차이가 많이난다.

<br/>

그리고 그 옆 SSD를 보면 YOLO에 비해서 FPS와 성능 지수 둘다 높다. 

언뜻보면 SSD를 배워야할 것 같지만, SSD는 후속논문이 없다.

YOLO는 version 1 대비해서 성능을 나타낸 것이다. 

이후에도 2, 3 최근에는 4도 나왔기 때문에 이런 것으로 비춰봤을 때 후속논문이 있는

YOLO를 배우는게 더 낫다고 볼 수 있다.

<br/>

그래서 우리는 계속 YOLO로 나아갈 것이다.

<br/>

조셉 레드몬이라는 저자이다.

조셉 레드몬의 이력서가 맨 오른쪽

이것만 봐도 틀에 얽매이지 않는 독특한 사람이라는 것을 알 수 있다.

전 세계의 인공지능의 아주 많은 천재들을 좌절에 빠트린 천재 중의 천재

Ver.3을 끝으로 업계를 떠났다.

왜 떠났을까?

Object Detection이 군사용, 대량 살상 무기로 많이 활용되고있고, 이 사람의 기술이 많이 쓰였다.

자기의 논문이 많은 사람들을 죽이는데 쓰여서 자괴감이 들어서 더 이상 안하고 그만하기로 결정했다고 함...

하나의 라이브러리를 뚝딱 만들 정도로 굉장히 천부적인 천재 of 천재인 사람

이 사람이 떠난 것은 인공지능의 부모를 잃은 것과 마찬가지

![image](https://user-images.githubusercontent.com/78403443/121850773-3a928980-cd28-11eb-9777-4093371158de.png)

드문 케이스인데 이런 케이스가 또 있다.

<br/>

얀 르쿤의 스승 제프리 힌튼 교수

원래 영국인인데 영국에서 자기 기술을 군사적 목적으로 사용해서 

그게 마음에 안들어서 캐나다로 이민

<br/>

여기서 C.R은 C 콤마 R이다. (Convolution + ReLU)

우리가 배웠던 Network하고 다른 지점이 위 연두색 동그라미로 표시한 부분

입력 이미지(448x448x3)를 GoogLeNet에 넣는다.

(꼭 구글넷을 넣어야 하는 것은 아니고, VGG... 등도 상관없다

이때 당시는 VGG도 없었고, 제일 좋은게 구글넷밖에 없어서 그것밖에 못쓴것)

어쨋든 저 부분을 VGG라고 생각해도 좋다.

그림에서 모양이 마름모꼴로 생긴 이유?

![image](https://user-images.githubusercontent.com/78403443/121850834-50a04a00-cd28-11eb-8552-2cf9174875ad.png)

FCN... vector로 펼쳐서 Classification하는데, 

그 전에 이미지를 줄여서 특징 추출... 그만큼 잘라서 붙인 것

레이어를 끝까지 쓰지 않고, 중간에 잘랐다.

어디? 딱 1x1x4096쪽 앞에서 자른 것... 

그러면 그 전 부분... 그 전 부분에서 원본 입력 이미지를 인코딩한 부분이라고 딱 한마디로 얘기할 수 있다.

인코딩은 다른 말로 얘기하면 "특징을 추출" 하는 부분이다.

그 당시에 구글넷을 사용

지금처럼 VGG를 사용해도 전혀 문제 없다. (오히려 더 좋을 것임)

<br/>

어쨋든 이런 마름모꼴이 나왔다는 것을 기억하면 된다.

바로 그 부분임...

<br/>

왼쪽에서 세번째인 그 다음부분은... 

Classification 한게 아니라 앞에서 Encoding한 이미지의 특징을 그대로 저장만 하고 있는 것이다.

<br/>

마름모부분은 작게 나타난 것 같이 보이지만 실제로 20개나되는 레이어를 가지고 있다. 

기존에 학습한 부분을 그대로 가지고 있는 것이다. 

그러면 여기서 새로 레이어를 돌리는게 아니라 그 다음에서 학습해놓은 모델을 그대로 갖다 쓰는 것이다.

그래서 속도가 빠를 수 밖에 없다.

<br/>

그리고 실제로 학습하는 부분은 이 파란박스 부분 밖에 없다.

<br/>

다시 과정을 보자면... 

세번째 부분을 보면 14x14로 줄였고 채널은 1024로 늘렸다. 거기에 압축된 특징을 저장하고 있다.

그 다음에 (네번째 부분) Convolutation을 진행하고 있다. 

사이즈 안 변한 것을 알 수 있다. 그렇기 때문에 stride = 1, filter size = 3x3, Filter갯수 1024개, 이때의 filter 채널 = 1024

그 다음 다섯번째 부분 :: stride 1, 3x3, 1024개, 1024

그 다음 여섯번째 부분 :: 사이즈 줄었다. 그러므로, stride = 2, 나머진 똑같다.

그 다음 일곱번째 부분 :: stride = 1, filter size = 3x3, Filter갯수 1024개, 이때의 filter 채널 = 1024

이렇게 진행되면서 vector로 펼친 부분보면 그 전 값들 다 곱하면 다른 값 나온다. 

7x7x1024 = 50,176 나오니까...

여기서 채널사이즈가 5만이 넘어가는 경우는 거의 없다.

5만을 넘기고 나서 그걸 vector로 바꾸면 연산량이 너무 많아진다. 

Fully Connected 에서 4천이 거의 한계이다.

그래서 여기서 뭐가 생략되있냐면 채널을 조금 줄이고 Fully Connected Layer가 적용된다.

이런 것들 생략되어있다.

<br/>

그 다음에 그리고나서 다시 한번 1470으로 줄이고, 그리고 그걸 reshape해서 7x7x30으로 만들었는데

이거 다 곱하면 1470된다. 

이게 무슨 꼬라지랑 같냐면 처음 넣었던 원본 이미지와 동일한 형태(꼬라지)로 넣은 것이다.

원본이미지에서 7x7로 그대로 줄였다고 보면 된다. 

줄이긴 줄였는데 채널은 30으로 늘렸다고 보면 된다. 

그래서 맨 마지막 부분과 원본이미지와 밀접한 연관이 있다고 보면 된다.

<br/>

여기서 정리할 것 :: 

1. Max Pooling 사용 안했다.
2. FCR 가기전 50,176을 4096으로 줄여서 갔다.
3. 1470x1 사이즈를 7x7x30으로 reshape 했다.
4. 기존 Network를 맨 앞에다 붙였다는 것

여기까지 잘 봐둘 필요가 있다.

<br/>

---

나머지 진도는 내일...
