<img width="583" alt="u-net_fig_1" src="https://user-images.githubusercontent.com/78403443/121654693-f493b680-cad8-11eb-9f82-30e015e039c9.png">

U-Net 초창기 방식

(출처 : https://m.blog.naver.com/9709193/221979612209)

<br/>

![aug_and_mask](https://user-images.githubusercontent.com/78403443/121654750-0412ff80-cad9-11eb-897d-7d79592e5add.png)

(출처 : https://mxnet.apache.org/versions/1.2.1/tutorials/python/data_augmentation_with_masks.html)

<br/>

원본이미지를 답지에 해당 영역에 매핑하려고 하는데, 답지 사이즈가 원본과 동일하지 않다면?

답지 비율만큼 사이즈에 맞게 전체를 Resizing 시킨다!

보통 U-Net은 

1. 입력과 출력사이즈를 똑같이한다.
2. Zero padding 준다. 

그러나, 우리가 본 것은 Unet 초창기 모델이기 때문에 Zero padding 안줬다. (이건 잘못한 것)

하지만 1번에 대한 부분은 잘못한 게 아니라 어쩔 수 없는 것이었다.

<br/>

자율주행 쪽에서는 reshape해서 하는 일이 많다. (이미지로 인식해야되는 정보가 많기 때문에)

어쨋든, 입력 출력 사이즈가 안맞을 때는 그런 Resizing 의도가 있었다. 라는 얘기

<br/>

입력과 출력 사이즈를 동일하게 만드는 것이 

U-Net Segmentation의 동기, 모티브이다. 

![image](https://user-images.githubusercontent.com/78403443/121654845-1bea8380-cad9-11eb-9bd6-3915056b1cea.png)

(출처 : https://www.researchgate.net/figure/The-architecture-of-Unet_fig2_334287825)

2배수 꼴로 작아지고, 2배수 꼴로 커진다. 

이렇게 하는 이유가 네트워크와 상관이 있다.

(네트워크로 연결했을 때 좋은 점이 있기 때문에...)

<br/>

![u-net_fig_1](https://user-images.githubusercontent.com/78403443/121654927-2e64bd00-cad9-11eb-88c4-66132db45c72.png)

(출처 : https://m.blog.naver.com/9709193/221979612209)

여기서 출력결과가 두개라는 얘기는 뭔 얘기냐면?

이런 바이너리 문제...

![image](https://user-images.githubusercontent.com/78403443/121655007-3e7c9c80-cad9-11eb-93e6-6cd36a2bc81b.png)

Cell U-Net

(출처 : https://www.mdpi.com/2075-4418/10/2/110/htm)

binary 문제일 경우에 최종 출력결과는 하나로만 하거나 둘로 하거나 할 수 있다.

binary 문제일 경우에 하나로 하건 둘로 하건 정해야한다. 

사실, 마지막 출력갯수는 자유롭게 정할 수 있기 때문이다.

답이 2개 이상일 경우에는 softmax로 해주고 확률값으로 치환해서 높은 값을 뽑아낸다. 

그러나, 출력결과를 하나만 출력하고자 할 때는 sigmoid를 쓴다.

만약에 sigmoid가 쓰였다면 분명 출력값 최종적으로 뽑아내기 전에 쓰였을 것이다. 

이때 쓰이는 sigmoid는 binary문제에서 최종출력 갯수를 하나만 설정했을 때 sigmoid를 쓴다.

여기서 sigmoid는 (전에 다뤘던 것처럼) 활성화 함수가 아니라 1에 가까우냐 0에 가까우냐를 판별하기 위해 사용한다... 

만약 결과가 0.7이라고 가정하면 cell이고, 0.2가 아니면 cell이 아닐 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121655087-4e947c00-cad9-11eb-9469-ae1ab4d64ad3.png)

그저께 다뤘던 main.py 파일은 인공지능의 뼈대가 되는 코드이지만 현업용 코드는 아니다.

재사용성이 약하기 때문에... 

재사용성이 약하다는 얘기는 강사님이 만드신 CIFAR10 Custom Dataset에서만 돌아간다는 얘기다.

<br/>

오늘 볼 코드는 train.py 파일로 돌리는 현업용 Custom Dataset이다.

재사용성이 좋다. 그 말은 다양한 Model, 다양한 Dataset을 사용할 수 있다는 것이다.

그러나, 어렵다... 어렵다라는 얘기는 복잡하다는 얘기

그래서, 우리가 최상의 내 것으로 가져가기 위해서는 이 코드가 어떻게 구조적으로 만들어져 있는지 이해를 해야한다.

우리가 조금 보고, 그리고 강사님이 설명해주신다. 

(구글 개발자코드.. 구글이면 Tensorflow를 쓸텐데, Tensorflow가 아니라 Pytorch로 그저께 봤던 코드와 비슷한 스타일이다.)

<br/>

---

- **7.Segmentation.pdf 파일 보기**
- (※ PDF 저작권 문제로 PDF파일 캡쳐본은 업로드하지 않고 내용만 업로드합니다.)

Evaluation Matrix는 뭐냐?

Segmentation은 기존에 우리가 알고 있던 Accuracy 측정방법...CrossEntropyLoss 써도되는 경우가 있다.

라벨의 카테고리가 2개일 경우...

그러나 라벨의 카테고리가 많은 경우에는 Inersection Over Union(IoU) 를 써야한다.

IoU 설명...

<br/>

하나도 못맞춘 경우... 우리가 기존의 평가방법으로 하면 

Accuracy는 0%에 가깝게 나와야하지만 99%가 나온다. 

Segmentation은 평가가 위처럼 되면 안된다. 평가 방법이 달라야 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121655357-83083800-cad9-11eb-8203-1e9c6f89cc45.png)

그러면 Segmentation 평가는 어떻게 하냐?

원본이미지가 있다. 원본이미지에 사람과 자동차와 나무가 있다고 가정한다.

그리고 각각 픽셀의 영역을 위 그림과 같이 매핑했다고 가정하자.

이럴 때 IoU 방법으로 평가하는데... 

IoU 방법을 잠깐 PDF에서 보고와보도록 하자.

<br/>

IoU 공식에서 분자 부분에서 교집합이 되는 부분을 A라고 한다.

분모 쪽에 못맞춘부분까지 다 합친(합집합) 부분을 B라고 한다.

![image](https://user-images.githubusercontent.com/78403443/121655526-a337f700-cad9-11eb-8a11-4fede584ab5b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121655573-acc15f00-cad9-11eb-8b5b-940143b6532d.png)

Segmentation은 IoU가 70% 이상 나오면 Good이라고 한다. 

B는 전체 이미지(합집합) A는 맞춘 부분(교집합)... 

B분의 A를(A/B)(전체 합집합 분의 교집합(전체 교집합/전체 합집합) 한 것이 IoU이다.

![image](https://user-images.githubusercontent.com/78403443/121655622-b6e35d80-cad9-11eb-8000-9f32c6c4bc35.png)

Ground Truth == Target, Y (정답지이다.)

빨간색 네모박스 == 예측한 부분(Predicted)

이거의 평가는 IoU(전체 교집합/전체 합집합)로 하는데

이 IoU가 Segmentation의 평가방법이다.

<br/>

그림으로 다시 설명

![image](https://user-images.githubusercontent.com/78403443/121655692-c367b600-cad9-11eb-856f-ae63a6adcaab.png)

위 그림을 바탕으로 IoU가 나오고, 그것을 모두 더 한다. 

모두 더 한 것... (카테고리 개수가 10이라고 하면) 그것을 개수인 10으로 나눈다. 

이것이 mIoU 공식이다. (위 그림의 분수공식)

mIoU 공식은 일반적으로 Segmentation에서 가장 많이 사용하는 성능지표이다.

<br/>

mIoU를 쓰면 아까 제기했던 정확도 문제가 해결되는지? (못맞췄을 때 Accuracy는 0%에 가깝게 나와야하지만 99%가 나온다라는 문제)

(세포 사진같이)물체가 너무 작을 때 효율적인 계산이 안된다.

![image](https://user-images.githubusercontent.com/78403443/121655757-cfec0e80-cad9-11eb-8e7e-b73b3223746a.png)

(출처 : https://www.allencell.org/)

이런식으로 입자가 작은 것을 mIoU로 계산하려고 하면 계산이 잘 안된다.

<br/>

이럴 때는 Dice Coefficient 라는 계산 방법을 써야한다.

<br/>

예측하고자하는 물체가 작고 자주 등장하지 않는 경우에 Dice Coefficient 를 굉장히 많이 쓴다.

예측하는 물체가 다소 크고 자주 등장하는 경우에 mIoU를 많이 쓴다.

<br/>

Segmentation에서 평가함수를 결정할 때는 물체의 종류를 이렇게 두 종류로 구분해서 쓰는게 원칙이다.

<br/>

각각의 성능 수치는 0에서 1사이의 수치가 나오고, 1에 가까울수록 더 예측을 잘한 값이 되겠다.

![image](https://user-images.githubusercontent.com/78403443/121655905-edb97380-cad9-11eb-8198-44682ee30346.png)

그래서, 우리가 Loss 값을 구할 때 공식 :: 

1 - mIoU or Dice Coefficient(썼을 때 최종결과값) = 0에 가까운 수라면 Loss가 적은 것이다.

<br/>

정리 :: 

Segmentation에서의 평가함수 방법은 2가지가 있다. 

mIoU, Dice Coefficient

예측하고자하는 물체가 작고 자주 등장하지 않는 경우에 Dice Coefficient 를 굉장히 많이 쓴다.

예측하는 물체가 다소 크고 자주 등장하는 경우에 mIoU를 많이 쓴다.

<br/>

Segmentation 개념은 여기까지 정리하고, 코드로 들어간다!

<br/>

---

![image](https://user-images.githubusercontent.com/78403443/121655992-0033ad00-cada-11eb-8c5e-bad5cffebc34.png)

(사이트를 들어간다. https://www.isic-archive.com/#!/topWithHeader/wideContentTop/main)

딥러닝을 하려면 코드도 코드지만, 데이터셋 확보가 가장 중요하다.

데이터셋 확보에 가장 좋은 데이터가 Chellenges 대회 데이터이다. 

좋은 데이터를 가져오려면 이런데서 데이터를 확보해와야 함

<br/>

좋은 데이터 확보를 못해서 딥러닝을 못하는 경우가 가장 많다.

<br/>

갤러리를 들어가본다. (이런 데이터가 있다는 것을 볼 수 있다)

<br/>

Chellenges 탭에서 Chellenge 2020에 들어가보자

![image](https://user-images.githubusercontent.com/78403443/121656076-12ade680-cada-11eb-9acb-b4e55cd5676c.png)

여기서 데이터셋을 받는건데 데이터가 기가바이트 단위이다. 

우리는 지금은 여기서 다운받지 않고, 강사님이 여기서 다운받아서 정제하신 데이터로 진행한다.

(강사님이 개수, 종류 추림)

<br/>

우리가 잘 아는 Kaggle같은 곳에서도 무료로 데이터셋을 제공하기도 한다.

어떤 데이터는 무료로 하기도하고, 회원한테만 제공하기도 하고, 계약서 쓴 조건으로 제공하기도 한다.

분석으로 팀 단위로도 많이 진행한다.

<br/>

여기까지 우리가 Segmentation할 데이터의 출처를 보았다.

<br/>

이제, 구글 코랩을 연다. Dataset에 ISIC 폴더를 만든다.

![image](https://user-images.githubusercontent.com/78403443/121656135-23f6f300-cada-11eb-9d13-334388de9af0.png)

ISIC.zip 파일을 넣는다.

<br/>

압축을 풀어서 testset데이터를 확인해본다.

![image](https://user-images.githubusercontent.com/78403443/121656205-3a9d4a00-cada-11eb-803c-999605471592.png)

label과 image를 분류했다.

라벨이 이렇게 생겼다.

![image](https://user-images.githubusercontent.com/78403443/121656266-4557df00-cada-11eb-9daf-6e26a75460c1.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121656299-4e48b080-cada-11eb-9863-a9b6fb1ef40f.png)

구글 개발자가 만든 현업용 코드가 들어있는 폴더를 구글 드라이브에 넣었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121656352-5b659f80-cada-11eb-9719-36ed1a5b2332.png)

실제로 Segmentation에서 사용하는 모든 답지는 흑백이다. → 흑백이어야만 용량 문제가 해결되기 때문!

구글 검색해서 나오는 이미지 중에 컬러로 되어있는건 이미 후처리된 결과물이다.

<br/>

0~255 사이의 값으로 분류한 답지가 있다. 

근데 간혹가다가 0~50정도로 분류한 것도 있지만, 0~255 사이의 값으로 분류하는게 더 직관적이기에

0~255 사이의 값으로 분류

<br/>

흰색은 우리가 맞춰야 하는 부분이다. 

0에서 255 사이의 값을 0에서 1 사이로 표시하고 0~1 값을 확률값으로 사용한다.

0.3%으로 예측한 부분이 있고, 0.7%로 예측한 부분이 있다면 

0.7% 부분이 70% 확률로 암이라는 것을 예측할 수 있을 것이다. 이게 Binary 문제이다. 

![image](https://user-images.githubusercontent.com/78403443/121656416-6b7d7f00-cada-11eb-8a13-35d11202756b.png)

Binary 문제는 아래 2가지 모델로 설계 가능

1. 출력결과 2개로 뽑는 경우

   - 강아지냐? 고양이냐?
   - 강아지냐? 강아지가 아니냐?
   - output 결과가 2개
   - 2개에 대해서 각각 softmax 적용
   - 확률값

2. 출력결과 1개로 뽑는 경우

   - 0~1 사이 값으로 출력
   - output이 하나라면 0.6
     - 고양이인지, 고양이가 아닌지 어떻게 알까?
   - 0~1 사이에 기준값(Thresh Hold값, 역치값)이 필요하다

<br/>

단, Thresh Hold 값을 절대적인 값으로 설정해서는 안된다.

<br/>

ex1) 강아지를 예측하고 싶다. 데이터 확보... 헷갈릴 수 있는 강아지 사진이 많다.

"가능하면 '강아지'라고 예측하고 싶다."

그러면 Thresh Hold를 어떻게 잡아야 하나? 낮게 잡아야 할 것이다.

<br/>

결론 :: Thresh Hold 값은 자율적으로 정하는 것이다.

낮으면 가능성이 높을 것이고, 높으면 까다로울 것이다.

<br/>

하나만 더 예를 들어서,

ex2) 동일한 모델에서 질문만 "암인지 암이 아닌지" 바꿔 보자.

Thresh Hold를 높게 잡아야 할 것이다.

<br/>

Thresh Hold 값이 어마어마하게 중요한 값이고, 자율적인 값이라는 것을 알아두자!

<br/>

마지막에 다룰 코드 경우에는 Thresh hold 값이 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121656557-923bb580-cada-11eb-95de-5f5efb32a2b0.png)

Segmentation 모델이고, 출력값이 하나이다.

0에 가깝게 나오면 고양이, 1에 가깝게 나오면 강아지라고 가정한다.

이럴 때는 기준치를 균등하게 0.5로 잡으면 될 것 같다.

<br/>

만약에 1에 가깝게 나왔다.

그러면, 강아지로 잘 예측한 것일 것이다. (칭찬)

그럼 이때 sigmoid 함수를 그려보면 (출력결과에 sigmoid를 쓰는거니까)

![image](https://user-images.githubusercontent.com/78403443/121656613-9ff13b00-cada-11eb-9b8c-85cc85ff680f.png)

이런 그래프가 나올 것이다. 이게 강아지로 잘 예측 한 것...

강아지로 잘 예측했다는 얘기는 1일 때... 

Loss는 0에 가깝게 나와야 할 것이다.

![image](https://user-images.githubusercontent.com/78403443/121656638-a8e20c80-cada-11eb-8ccb-5078f5517339.png)

그래서 정리를 하면, 강아지가 1일때

Loss를 구하면 잘한거기 떄문에 Loss는 0에 가깝게 나온다.

<br/>

이게 Binary Cross Entropy에서 이렇게 나오는데...

여기까진 다들 알 것이다.

<br/>

고양이는 0값에 가깝게 나올 것이다. 

고양이는 0값에 가깝게 나왔다는 얘기는.. 

0에 가깝게 나오면 고양이도 칭찬을 받아야한다.

고양이로 정확하게 예측했을 때도 Loss가 0으로 나와야한다. 

근데, 위 Loss Function 하나만 가지고는 고양이로 예측했을 때 Loss가 무한대로 떨어진다.

<br/>

그럴때는 어떻게 되냐면 이 Loss가 똑같다.

그리고, 파형을 대칭으로 그린다.

![image](https://user-images.githubusercontent.com/78403443/121656708-bbf4dc80-cada-11eb-8f8e-accffe7bd9eb.png)

이렇게 되면 고양이가 0일 때 Loss도 0에 가까워진다. 라는 얘기가 된다.

결론 :: Loss Function을 대칭으로 그릴 줄 알아야 한다는 얘기...

<br/>

왜 값이 하나로 출력되는 이런 경우를 계속 설명하는가? Binary 문제...

아까 Thresh Hold를 정해야한다고 했다. 

Thresh Hold를 이용할 수 있는 이런 걸 많이 이용하기 때문에 계속 설명했던 것이다.

<br/>

코드로 들어간다.

(코드 출처 : https://github.com/meetps/pytorch-semseg)

![image](https://user-images.githubusercontent.com/78403443/121656775-cb742580-cada-11eb-8fa9-ce5121d472d5.png)

Train안에는 Train과 Validation Test 데이터에 대한게 있다.

여기서 Test는 Inference를 의미한다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/121656816-d7f87e00-cada-11eb-8017-e0fb60eda433.png)

구조를 파악한다. 특히 Config 폴더가 핵심이다. 

전체적으로 다 살펴라. 

대신, 코드를 한땀한땀 보지는 말라... 그냥 대략적 구조만 파악해라

<br/>

![image](https://user-images.githubusercontent.com/78403443/121656877-e3e44000-cada-11eb-92b0-3dbacce30c98.png)

![image](https://user-images.githubusercontent.com/78403443/121656956-f5c5e300-cada-11eb-9853-6fcc1fc6f5a5.png)

![image](https://user-images.githubusercontent.com/78403443/121657011-ff4f4b00-cada-11eb-8655-bb424ab77a17.png)

checkpoint안에는 Weight값들 저장

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657088-0d9d6700-cadb-11eb-9338-c9fccecb4a67.png)

results 폴더에는 예측값, 결과값 저장(html 수업 때 결과페이지 이동하게 했던거랑 같은 맥락)

<br/>

재사용성을 보여주는 곳이 config폴더이다.

![image](https://user-images.githubusercontent.com/78403443/121657131-1b52ec80-cadb-11eb-914e-c01fc339ef19.png)

설정문서 :: yaml(야믈)확장자로 되어있다.

Deep Learning이 실행되는데 있어서 필요한 파편적인 정보들을 모아놓은 파일

<br/>

재사용성이 높다는건 맨 오른쪽 파일만 바꿔주면 된다. 

추가하거나 수정하거나...

<br/>

isic.yaml 파일로 들어가본다. (Binary 문제)

다운로드를 받아서 Editplus나 워드패드로 열면 된다.

![image](https://user-images.githubusercontent.com/78403443/121657222-2c9bf900-cadb-11eb-8db9-a637a8080bdb.png)

![image](https://user-images.githubusercontent.com/78403443/121657249-34f43400-cadb-11eb-88f3-76bf001ae6fb.png)

카테고리 갯수 2... Binary 문제이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657304-3faec900-cadb-11eb-82e7-e87a2cd4a903.png)

Loss_function이다.

전에는 이런것들이 CODE에 하드코딩 되어져있었다.

하지만 코드는 변수처리하고 값을 외부에 모듈화를 시켜놓은 것이다.

그래서 isic.yaml를 수정해서만 쓰면 된다.

<br/>

dict = mIoU 

ce = crossentropy Loss

bce = biascrossentropy Loss

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657346-4b9a8b00-cadb-11eb-8093-ba777176e3e0.png)

Data Augmentation 관련

gpu가 0~3번까지 총 4개를 다 쓰겠다는 얘기

workers는 cpu worker를 얘기하는 것이다.

batch_size 16이상... 위 12는 16으로 바꿔주는게 좋을 것 같다.

ckpt_root는 checkpoint 경로.. 각각(isic, city 등) 다 돌릴 수 있는 재사용성이 가능한 코드이기 때문에 ckpt에서 하나 더 추가된 것임

weight 부분은 그저께 봤던 코드에서 resume과 같은 기능을 하는 부분... resume 할 폴더를 지정한다.

(사람마다 weight이라고 하는 사람이 있고 resume이라고 하는 사람이 있다)

<br/>

이런식으로 설정 문서들이 있다.

<br/>

cityscapes.yaml 파일을 본다 - 멀티카테고리 라벨(다수의 라벨 카테고리)

![image](https://user-images.githubusercontent.com/78403443/121657427-5c4b0100-cadb-11eb-87ed-83d7735e4942.png)

값 수정해서 쓸 수 있는 것이다. 

하지만, 이 패턴을 거의 유지한다고 보면 된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657501-6a008680-cadb-11eb-8852-4e91c156f153.png)

utils 안에 dataset_utils 파일이 있다. 

그 전에 utils.py 파일을 본다.

<br/>

출력 패턴은 데이터에 따라 정해져있다. 

보면 one hot encoding도 있고... 

데이터 마다 특화된 부분을 다루는게 아니다. (재사용성 있다)

모든 데이터가 공용으로 사용할 수 있는 util이 utils.py 파일에 있다.

![image](https://user-images.githubusercontent.com/78403443/121657562-784ea280-cadb-11eb-9552-5e4b405d7be2.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657607-843a6480-cadb-11eb-8fc7-4b1a1b58041d.png)

dataset_utils 폴더는 데이터셋에 특화된 부분

주로, 출력관련 부분, 후처리 관련 부분이다.

<br/>

Accuracy 출력, Loss 출력하는 부분은 어떤 데이터셋이든 다 똑같기 때문에 

아까 봤던 utils 폴더의 utils.py 파일에서 돌아간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657671-90bebd00-cadb-11eb-9ddf-90bb737d2511.png)

그저께 봤던 코드1 main.py는

① CIFAR10에서만 실행 가능하다.

② 모든 정보가 CODE에 일일히 기재되어있기 때문에 재사용성이 낮다!

<br/>

오늘 보고있는 코드2 train.py는

① 모든 데이터셋에서 사용할 수 있다.

② 하드코딩 되어져있지 않기 때문에 재사용성이 높다!

그러나, 범용적이지 않다.

<br/>

그 이유는?

① isic.yaml 을 수정하거나, 새로운 데이터... 만약 iris 데이터를 새로 돌린다면 iris.yaml 파일을 만들어야한다.

② utils/dataset_utils에 있는 파일들을 수정하거나 새로 만들어야한다.

<br/>

이런 구조를 처음부터 짜는 것을 스켈레톤 코드라고 한다.

뼈대부터 작성한다. 

우리나라에서는 인공지능 분야에서 뼈대부터 작성하는 사람의 실력자는 없다. 

아까 git에서 받아서 썼던 것처럼 git에서 이미 만들어져있는 스켈레톤 코드를 다운받아서 커스텀해서 쓴다.

<br/>

기업에서 인턴 시켜서 스켈레톤 코드 만들게 시키는 경우가 많다... 머리가 빨리 빨리 돌아가고 배운지 얼마 안됐기 때문

<br/>

여기까지가 전체적인 구조...

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657918-d3809500-cadb-11eb-8994-7e97c3d95b14.png)

Segmentation에서는 isic.yaml이 단순한 텍스트 기반으로 설정되는데

Object Detection에서는 설정문서가 xml, JSON 이런 형태로 나온다.

답안 형태가 JSON 형태로 나오는데... 1천만줄이 나온다. 

(어떻게 천만줄이 나오는지는 나중에 Object Detection할 때 설명)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121657996-e2674780-cadb-11eb-8aa9-b4c4fac61646.png)

utils 폴더의 dataset_utils 폴더 안에 있는 부분이 다루기 까다롭다. 

Data 특화된 부분이기 때문에 직접 작성해야하고, 

후처리 기법도 쉽지 않기 때문에 되게 까다로운 부분이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121658136-00cd4300-cadc-11eb-819c-501c1059d846.png)

(출처 : https://www.pennmedicine.org/departments-and-centers/department-of-radiology/radiology-research/labs-and-centers/biomedical-imaging-informatics/cbig-computational-biomarker-imaging-group/cbig-research/research-areas)

유방암 데이터이다.

<br/>

맨 왼쪽이 답지(Label)

후처리에는 Visualization이 들어간다. (우측 2번째 사진)

어쨋든, 이런것들은 아까 dataset_utils 같은 폴더에 들어가야한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121658200-0dea3200-cadc-11eb-8128-11eb71ed777a.png)

transform.py 파일은 Data Augmentation(데이터 변형) 관련 파일이다.

정확도를 올리는데 굉장히 중요한 부분...

파이토치에서는 특히, Segmentation 모델을 다루는데 있어서 Data Augmentation할 때는

파이토치 API상에 굉장한 문제가 있다. 그 부분을 설명한다.

![image](https://user-images.githubusercontent.com/78403443/121658243-193d5d80-cadc-11eb-9b53-4def8bb9b4dc.png)

Segmentation Model, Data Augmentation시 주의점!

컬러로 된 원본 이미지가 있다.

왼쪽이 이미지고 오른쪽이 라벨이다.

여기서 Augmentation을 시켜본다.

<br/>

1. Random crop(이미지 랜덤하게 자르기) 

   원본이랑 똑같이 crop 할 수 있지만, 랜덤으로 가장자리 같은 곳에 crop될 수도 있다.

   그래서 항상 같이 따라가도록 되어있다.

   Crop을 시킬 때는 이미지를 잘라준다. 이때 답지도 동일하게 자른다. 이게 Pair이다. 

2. Random Rotate(랜덤하게 회전시키기)

   상하, 좌우반전 동일하게 일어난다.
   
   ![image](https://user-images.githubusercontent.com/78403443/121658328-2c502d80-cadc-11eb-9602-2f85bd5bbdb0.png)

   회전 시

   만약 ①을 ②로 회전시키면 짜투리 영역이 남게된다. 이거 어떻게 처리할까?

   → 모두 0 값으로 채운다 → padding 영역 처리가 개발시 필요하다!

   <br/>

   우리가 생각하는 것보다 실무 작업이 굉장히 복잡한 작업이 진행된다는 것이다...

   <br/>

   우리가 말한 이런 부분이 파이토치 라이브러리로 전부 해결이 된다.

   (개발할 떄 반드시 알아야 하는 부분)

   <br/>

   그러나 문제는 어디서 발생하냐하면,

3. Random Brightness(랜덤하게 밝기변경) 부분
   ![image](https://user-images.githubusercontent.com/78403443/121658448-50137380-cadc-11eb-8f4e-24f67733d539.png)
   
   컬러이기 때문에 채널은 3이 될 것이다.

   이 것의 답지는 마찬가지로 흑백..

   여기서 밝기조절이 들어간다.

   만약, 컬러 이미지 밝기를 전체적으로 어둡게 하고싶다.

   전체 모든 픽셀에다가 0.5씩 곱하게 되면

   모든 전체 픽셀이 0.5만큼 작아진다.

   255→127 이렇게 되면 조금 어두워진다. 

   이런식으로 밝기 조절한다. 

   그러면, 라벨도 절반으로 똑같이 어두워져야한다. 

   이 때 문제가 생기는 것이다.

   <br/>

   답지가 훼손되는 문제가 생긴다. 밝기 조절이 들어가버리면

   Ground Truth 에서 문제가 생겨버리는 것이다.

   그래서, Brightness는 무조건 이미지와 답지가 Pair로 가면 안된다.

   (Segmentation에서의 Data Augmentation에서 가장 중요하게 생각해야되는 부분이다)

   ![image](https://user-images.githubusercontent.com/78403443/121658558-67eaf780-cadc-11eb-9a27-037ff49dbd79.png)
   <br/>

![image](https://user-images.githubusercontent.com/78403443/121658610-776a4080-cadc-11eb-84c9-b1a91adcf094.png)

transforms.py 파일을 보자

<br/>

원래는 있었는데 위에서 설명한 이러한 문제때문에 Random Brightness 부분은 지워버렸다.

<br/>

그 다음 utils를 보면 dice_loss.py파일이 있다.

![image](https://user-images.githubusercontent.com/78403443/121658783-9ec10d80-cadc-11eb-821f-fda7c5448bc6.png)

이거 왜 나왔을까?

dice_loss는 파이토치에서 제공하지 않는 Loss Function이다.

그런데, 아주 유명한 Loss Function이다.

굉장히 유명한 Loss Function이고, 굉장히 많이 쓴다. (Tensorflow에서도 제공 안한다)

<br/>

Tensorflow, PyTorch 프레임워크에 구현을 안해놓은 것이다.

이걸 어떻게 쓰느냐? 

(정말 좋은 기술인데 프레임워크에 구현 안해놓은 것들이 꽤 있다)

(최신 논문에서 꽤 많이 쓰는데 프레임워크에 구현 안해놓은 것들이 몇개 있는데 그 중 최고가 dice_loss라는 Loss Function이다)

github에 올려놓은걸 끌어다가 Code에 연결해서 쓰는 것이다.

<br/>

이 얘기를 왜 하냐면?

인공지능 개발하는 사람들도 레벨이 있을 것이다.

그 말은, 인공지능 개발에 있어서 코드 레벨이 있다. (암묵적으로)

- 1레벨, 진짜 초심자가 짜는 코드

- 2레벨, 아주 General한 인공지능 코드 (지금이 이정도 코드다)

  - train.py 코드
  - 여기서 코드가 jumping하려면 그게 3레벨이 되시겠다.

- 3레벨, 남들이 만든 좋은 모듈을 가져다가 자기 코드에 붙여쓴다.

  - 이게 퍼포먼스를 굉장히 증가시킨다. 
  - 우리가 그걸 끌어다 쓴 것이다. dice_loss같은 것
  - 이런 인공지능 개발자가 진짜 몸값이 높다. 실력이 있어야 한다는 얘기, 국가대표급이다!
  - 그러나, 실제로 들어가보면 코드 별거 아니다.
  - (코드 레벨을 느낄 수 있었으면 좋겠어서 넣으셨다고 한다)

![image](https://user-images.githubusercontent.com/78403443/121658868-b4363780-cadc-11eb-8554-6c38a5a0974e.png)

겁먹을 필요 없다.

<br/>

이 정도가 전체적인 구성이다.

전체적인 구성을 보는게 굉장히 중요하다.

<br/>

- train.ipynb 파일 보기

  - 맨 마지막 셀 코드...

![image](https://user-images.githubusercontent.com/78403443/121658966-cca65200-cadc-11eb-86b3-434209e92127.png)

이 코드는 무슨 뜻?

main() 만 있어도 실행되지만, if를 붙였다. if절이 필요한 이유!?

☞ main()이 train.py를 직접 호출할 때만 실행되도록 하는 문장...

직접 호출은 이 파일 직접 돌리는 것, python train.py 이게 직접 호출, 실행 파일  

if절을 쓸 때는 직접 호출 될 때만 이렇게 쓰겠다는 얘기임

실행 파일이 직접 호출하는 것 == 직접 호출

<br/>

그럼, 간접 호출은 뭘 말하나?

import 되는 경우이다. 이때는 내가 돌리지 않는데, 이거 돌리다보면 unet.py 이런거 돌린다.

이런게 간접적으로 돌린다. 이게 간접 호출

<br/>

- unet.ipynb 파일 보기

![image](https://user-images.githubusercontent.com/78403443/121659040-dfb92200-cadc-11eb-932e-4ab95095e0cf.png)

if문 :: 이 해당 파일(unet.ipynb)이 직접  호출

train.ipynb에서 실행 안하면 간접 호출 안된다. (import 안된다)

용도가 뭔가? 디버그이다.

<br/>

단위테스트 하려면 직접 호출 해야한다.

<br/>

train.ipynb에서 파일에서

이 부분 직접 확인해본다.

![image](https://user-images.githubusercontent.com/78403443/121659111-ee9fd480-cadc-11eb-94d9-cdaa4c8b6f06.png)

load_model에서 config에 있는 unet모델 준 것이다.

model이라고 치니까

![image](https://user-images.githubusercontent.com/78403443/121659206-0aa37600-cadd-11eb-8a7e-8fd39000f4a0.png)

이렇게 나오는 것을 확인했다.

<br/>

unet.ipynb 파일 설명

![image](https://user-images.githubusercontent.com/78403443/121659277-1a22bf00-cadd-11eb-8039-d53678abc7c9.png)

1. 메인 모델 클래스 정의해야한다. unet.py
2. unet에서 사용할 모듈을 다시 지정한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659344-2b6bcb80-cadd-11eb-885f-9bd597af0b70.png)

unet이 있고 DoubleConv, Down, Up 크게 이 세 구조가 있는 것이다. 

DoubleConv는 무슨 일을 하냐면 Convolution, BatchNormalization 두번 반복한 것, 그래서 DoubleConv

stride 1아니면 2만 쓰게 했다. 그렇게 안넣으면 에러나게 했다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659394-37f02400-cadd-11eb-8881-7def94786e06.png)

Down은 사이즈를 줄인다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659435-43dbe600-cadd-11eb-8050-2d07d7053800.png)

Up은 사이즈를 늘린다.

interpolate(보간법), Nearest Neighbor 사용한 것임

<br/>

그런 것들이 여기서 돌아가는 것이다.

<br/>

맨 마지막,

![image](https://user-images.githubusercontent.com/78403443/121659511-548c5c00-cadd-11eb-84df-c65ed9f5df53.png)

unet128은 그냥 강사님 마음대로 넣은 것이다. 

원래는 unet32가 돌아가는데 어차피 단위 테스트니까..

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659551-60781e00-cadd-11eb-86b1-9025808b1e6e.png)

어떻게 forward되는지 알려면 디버그 해보면 된다. 하나씩 찍어보면 되는 것이다.

이렇게...

![image](https://user-images.githubusercontent.com/78403443/121659594-6cfc7680-cadd-11eb-87da-e323c632015e.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659672-7dacec80-cadd-11eb-8377-8a31348d57e5.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659711-87ceeb00-cadd-11eb-8173-177fb51fcda0.png)

forward에 들어가기 전에 x1, x2 어떻게 되는지 확인했다.

![image](https://user-images.githubusercontent.com/78403443/121659746-90bfbc80-cadd-11eb-884f-12436e9a4abe.png)

거기에다가 interpolate(보간법) 한 것이다.

그러면 늘리면... 32, 32가 된다, 

![image](https://user-images.githubusercontent.com/78403443/121659799-9fa66f00-cadd-11eb-8b54-80cfb8fe4406.png)

확인했다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/121659956-c5337880-cadd-11eb-8db5-43cae9f3be4a.png)

dim=1 을 기준으로 concat 시키라는 얘기다.

이게 의미하는 게 뭔가?

![image](https://user-images.githubusercontent.com/78403443/121659988-ce244a00-cadd-11eb-90b7-865cc8a1a7e4.png)

unet에서 torch.cat([x2, x1], dim=1)

(x2가 이전꺼, x1 현재꺼)

여기서 dim=1은 채널을 기준으로 붙인다는 얘기다. 

dim은 항상 4차원으로 나온다. [100, 3, 28, 28]

width, height 뽑을 때는 [2:] 을 하지만

여기서 1은 채널 인덱싱 하는 것이다.

<br/>

위로도 옆으로도 붙일 수 있지만,

채널을 기준으로 붙이라는 얘기는 앞뒤로 붙이라는 얘기임(맨 우측과 같이)

그렇게 붙여야 하기 때문에 width와 height가 정확히 일치해야 한다는 얘기임. 

이렇게 이해하고, 코드로 반드시 이해를 해야한다.
