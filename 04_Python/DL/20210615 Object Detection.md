(※ pdf 파일 슬라이드 캡쳐본은 업로드하지 않고, 메모내용만 업로드 함)

<br/>

**Object Detection**

**YOLO Ver.1**

- 이미 학습을 마친 Network를 가져다 사용

  (구글넷을 쓰던, VGG를 쓰던 어떤걸 쓰던 상관은 없다)

- 저장

- 파란박스 부분 == 실제 학습이 이뤄지는 부분

- 파란 박스 마지막에 5만개 정도의 채널이 나오지만, 연산이 많아지기 때문에 5만개쓰지 않고

  아무리 많아도 4096개 정도로 줄인다.

- 맨 마지막 7x7x30 부분에서 해석이 이루어진다.

- 가장 이해하기 어려운 지점 == 맨 마지막 부분...

  어떻게 해석을 이뤄내야하는지에 대해 가장 고달픈 부분

<br/>

두번째 부분을 Pre Training 혹은 Transfer Learning 부분이라고 한다.

이 부분에 대해 설명...

![image](https://user-images.githubusercontent.com/78403443/122006928-624e2400-cdf2-11eb-9787-635b49144f77.png)

앞에 만든 모델1을 재사용... cat_dog_model.ckpt 그대로 resume 해서(if args.weight) 로딩한다.

![image](https://user-images.githubusercontent.com/78403443/122006963-6d08b900-cdf2-11eb-895d-4cc6f4b8ce9f.png)

보통 resume 사용 안하면 Loss의 파형이 위와 같이 나온다. (빨간선)

(resume 사용 안했다는건 == Pre Training 안함)

<br/>

resume 사용 하면 낮은데 부터 Loss가 떨어진다. (하늘색 선)

(resume 사용 == Pre Training 사용)

<br/>

Loss값의 시작점이 달라진다.

연두색 화살표가 차이... 

많은 경우에 2~3일 차이를 보인다.

<br/>

이런 Pre Training, Transfer Learning이 학습방법 중의 한가지이다. 

학습방법이라고 하면 Weight값 크기 줄여서 효율적으로 값을 계산해주는 Regularization이라든지

Batch Normalization 이라든지, dropout이라든지 이런 것들이 굉장히 중요한 딥러닝의 학습방법인데,

그 그런 방법들 중에 하나라는 것이다.

기술이 복잡해질수록 Transfer Learning은 안 쓰일 수가 없다. ☞ 자유도가 높은 기술

<br/>

자유도가 높은 기술이란? (우리가 자주 사용했던 VGG 가지고 설명)

![image](https://user-images.githubusercontent.com/78403443/122007039-814cb600-cdf2-11eb-8e3c-827870976694.png)

VGG 모델은 CNN으로 쭉 갔다가 마지막에 Classification하기 위해, 쫙 펼쳐 FCN으로하는 방법

두 모델은 학습이 이미 끝난 상태, 모델 구조는 조금 달라지고, 데이터도 다르다. 

학습시작 전이다... 

Q. 위 그림처럼 Transfer Learning시 분류갯수가 4개로 늘어난다면 어떻게 할까

1. 옵션 (Strict = False) → Model 1의 2개까지 그대로 가져오고, 나머지는 그대로 진행. True는 Error (중요 ★)

2. 윗 부분을 잘라서 가져온다. 나머지 뒷부분은 알아서 학습진행한다.<br>(나머지 뒷부분 값은 다시 랜덤한 값으로 진행)

두 방법 모두 많이 쓴다.

![image](https://user-images.githubusercontent.com/78403443/122007078-8b6eb480-cdf2-11eb-9ccb-fb934e3471f5.png)

그대로 가져오는 것 뒷 부분에 Segmentation 모델도 연결가능 (앞뒤가 연결된 형태니깐)

가지고 오고 싶은 부분만 원하는 만큼 뜯어서 가져올 수도 있다.

<br/>

가장 많이쓰는 일반적인 형태는 맨 밑 그림 앞 부분

이미 학습한 부분을 뜯어오고, 뒷 부분은 랜덤하게 학습시키는 것이다.

<br/>

하지만, 다른 방법도 모두 가능하다. 그래서 자유도가 높다고 하는 것...

Transfer Learning 장점 되시겠다.

<br/>

PDF에선 구글에서 만든 GoogLeNet 가져온 것이다.

이 GoogLeNet 20 레이어를 가져왔다. 

GoogLeNet은 깊다고 하는데... 속도와 연관된다. 

그리고, GoogLeNet은 원래 1000개의 카테고리를 분류하는 이미지 네트워크이다.

1000개를 분류하기 때문에 깊이가 깊을 수 밖에 없다.

→ 결과론적으로 학습 속도가 빠르다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122007491-ef917880-cdf2-11eb-96ac-e07b95a8fb23.png)

Transfer Learning을 사용할 떄는

얼려서 사용하는 방법(Freeze)이 있고, 얼리지 않고 사용하는 방법이 있다.

<br/>

① 얼린다(Freeze 시킨다) == 고정만 시킨다는 얘기이다. == 아예 학습을 안함, 그대로 사용

② 얼리지 않는다 == 학습된 모델을 가지고 왔는데... 

다른 데이터이기 때문에 기존의 Weight값을 가지고 오고, 거기에 학습을 다시 진행하는 것

(안가져 왔을 떄보다는 속도가 높지만, ①보다는 속도가 안나온다)

<br/>

정리 :: 

Transfer Learning은 자유도가 높다. 

두 가지 방법이 있다. 얼리는 방법, 얼리지 않는 방법

<br/>

YOLO는 얼리는 방법을 사용했다.

<br/>

YOLO는 크게 네 부분으로 나눌 수 있다.

각각 정리를 하면

1. == Transfer Learning을 사용해서 각각 붙인 것인데, Freeze했기 때문에 학습이 전혀 안이루어지고

   학습을 전혀 안했기 때문에 속도가 빠르다

2. == 1번에서 나온(구글넷 20개의 레이어) 압축된 결과를 저장하고 있다.

3. == 2번의 압축된 결과를 가지고 우리가 원하는 사물의 위치좌표 그리고, 어떤 물체인지를

   식별할 수 있는 학습을 진행

4. 그리고 나서 결과로 7x7x30이라는 3D 직육면체를 만들어낸다.

   얘를 잘 분석(해석)하면, 사물의 위치Box가 나오고, 어떤 사물인지 결과를 알 수 있다는 것이다.

   (해석하는 과정이 엄청 어렵고 고통스러운 과정이다)

   그를 바탕으로 후처리(Output) 할 수 있다.

<br/>

Use new additional conv layers → better performance 를 잘 읽어봐야 할 것 같다.

<br/>

실제 학습이 일어나는 부분은 파란 박스부분...

총 4개의 레이어로 학습이 일어난다.

 Fully Connected Layer는 2개. 이걸 다 합해서 우리는 Fully Connected Network라고 하는데,

성능을 높이기 위해서 이 부분은 더 이상 늘리면 안된다.

이유는 Compution power가 너무 많이 들기 때문이다.

 Use new additional conv layers → better performance는

성능을 향상시키기 위해서라면 중간레이어 conv 부분을 늘리라는 얘기이다.

속도는 다소 떨어질 수 있지만 성능 향상에 보탬이 된다.

<br/>

여기까지 이해를 해야 다음을 이해할 수 있다.

<br/>

원본이미지 448x448x3을 7x7x30으로 전체비율은 유지하면서 줄였다고 보면 된다. 

중요하기 때문에 7x7x30 확대시켜 놓은 것이다.

![image](https://user-images.githubusercontent.com/78403443/122007971-79d9dc80-cdf3-11eb-8817-2eb81af346ef.png)

오른쪽이 원본이미지 448x448

원본이미지에 빨간 박스가 의미하는게 뭔지 설명한다.

이게 학습이 정말 잘 이루어지면 노란색 박스처럼 쳐질 것이다.

그 다음에 왼쪽 그림에 있는 작은 빨간 박스 표시가 오른쪽 빨간 박스 표시와 똑같다. (같은 이미지)

동일한 비율이다. 

빨간 박스가 뭐냐면 x의 중심점이다. 

전체이미지에서 7등분 되있으면 한 칸에 64일 것이다.

그러면 x, y좌표가 한칸에 64니까 x는 103정도가 될 것이고

y는  300이 될 것이다. 이것이 노란색 박스의 중심점 좌표이다. (x 103, y300)

노란색 박스의 width, height는 각각 200, 350 정도 될 것이다. 이렇게 하면 박스의 크기가 나올 것이다.

오른쪽 이미지 한칸 한칸을 grid cell이라고 하고, 뒤에 30개의 채널이 있을 것이다. depth가 30개...

<br/>

왼쪽 그림의 초록색 박스는 노란색 박스의 중심점의 grid cell을 잡은 것이다.

앞에 5개의 정보는 각각 x, y, h, w, c(가로좌표, 세로좌표, height, width, Confidence score) 그리고 나머지 뒤에 25개의 값이 있을 것이다.

c는 Confidence Score라는 값인데, 0~1사이로 Box안에 물체가 들어있는지 여부를 확률적으로 나타내는 수치이다.

<br/>

중심점이 grid cell에 들어가 있는 것뿐이지 물체를 Boundary하고 있는 B-box의 중심점을 얘기하는 것이다.

(전체의 중심점이 아니라 각 물체 그리드별 중심점이라는 얘기다)

그런게 7x7 = 49니까 49개의 grid cell이 나올 것이다. 그리고 이런게 총 3개 있는 것이다.(물체가 3개이므로)

<br/>

그런데, 실제로 이렇게 값이 들어가면 안된다. 

이유는? weight값이 어마어마하게 커지기 때문에... 

그래서 Normalization, 일종의 스케일링을 해줘야하는 것이다.

다시 말해서, 스케일링을 해야하는데 어떻게 스케일링 해야하는지가 정말 어렵다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122008109-9c6bf580-cdf3-11eb-9a9f-1d47bc5c1723.png)

왼쪽 이미지가 7x7이다.

그리고, 뒤에 30개의 depth가 있을 것이다.

쉽게 말하면, 원본이미지를 7x7로 grid한 것이다.(쪼갠 것이다)...①

그냥 쪼개는 것이기 때문에 13x13이든 20x20 으로도 쪼갤 수 있을 것이다.

7x7보다 많이 쪼갤수록 디테일하게 세세하게 쪼개는 것이다.

<br/>

학습이 잘되면 Boundary box(Bbox)가 최종적으로 3개 나와야한다.

결론적으로 물체가 3개면 3개의 Bbox가 나와야한다.

중심점은, Boundary box의 중심점이다.

<br/>

Grid cell 기준으로 x와 y좌표를 구하는 것이다.

(Grid cell의 전체 가로, 세로는 각각 1이다.)

오른쪽의 중심점은 Boundary Box의 중심점이다.

거기서 절반이니까 0.5, 0.5가 나온다

이런식으로 스케일링을 해야한다. 

5번째까지 굉장히 중요한데 

왼쪽은 전체이미지 기준으로 비율을 찾는다.

전체이미지 가로 세로를 1로 하고 노란색 Bbox 기준으로 하면 0.7, 0.4의 width, height가 구해질 것이다.

<br/>

위를 바탕으로 스케일링 한 값

최종 :: x 0.5, y 0.5, h 0.7, w 0.4, c 1이 나온다. (이것은 약속, 규칙이다)

<br/>

만약에 자동차 Boundary box 라면?

![image](https://user-images.githubusercontent.com/78403443/122008189-b4437980-cdf3-11eb-9b48-2b0ef65ff724.png)

이런식으로 나올 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122008227-c02f3b80-cdf3-11eb-8d10-d292d2e1b368.png)

주황색과 초록색 grid 둘 중에 누가 더 예측을 잘한걸까? 둘다 마찬가지 예측못한 것

IoU는 전체를 많이 포함할수록 높게 나오는데 초록색은 그 반대이므로 IoU가 낮다.

그러므로 Bbox 안그려진다. 주황색도 마찬가지이다.

사물이 들어있다고해서 박스가 그려지는게 아니라 IoU가 안나오면 박스가 안그려진다!

![image](https://user-images.githubusercontent.com/78403443/122008275-cd4c2a80-cdf3-11eb-877c-c3d78b1e5d89.png)

그럼, 여기서 하늘색 박스는 그려지고, 주황색 Bbox가 그려지지 않은 정확한 이유는?

주황색은 정답의 중심점이 들어있는 grid cell 밖에 중심점이 있기 때문에,

정답의 중심점이 들어있는 grid cell 안에 Boundary box의 중심점이 들어와있어야 정답이 된다.

그래서, 하늘색 박스는 개의 얼굴이 반 잘려있는데도 정답으로 그려진 것이다.

<br/>

x에 보면 grid cell size 앞에 wrt라는 표현이 붙어있다. 

많이 쓰는 표현인데 with regard to(~에 관하여)의 줄임말이다.

<br/>

x와 y는 grid cell 사이즈 비율에 대해서 0~1로 라는 뜻

w와 h는 전체 이미지 사이즈 비율에 대해서 0~1로

c 는 Confidence Score = P( 물체가 존재할 확률값) * IoU 값 

물체가 존재할 확률값에 IoU 값을 곱한 것이 전체 Confidence Score가 된다.

<br/>

IoU값은 전체 분의 교집합 (교집합/전체)

IoU는 0.7 이상이면 Good으로 본다고 전에 말씀해주심

<br/>

Confidence Score는 물체가 존재할 확률값과 IoU 값 둘다 높아야 높아진다.

Threshold값 적용했을 때

Threshold값 낮을수록 Box 많이 그려진다.

Threshold값 높을수록 Box 적게 그려진다.

<br/>

물체가 존재할 확률값 x IoU 값 == 여기에 Thresh hold값이 존재해야한다(존재한다)는 얘기

<br/>

P값이 안좋을 때 예시... 

![image](https://user-images.githubusercontent.com/78403443/122008466-0edcd580-cdf4-11eb-80d7-fb18da5013fb.png)

노란색(정답) 연두색(예측값) (강사님이 그려주신 그림 캡쳐를 못해서 그나마 비스무리한 그림으로 설명)

연두색 박스보니 예측을 꽤 잘했다... 

정답의 중심점이 들어있는 grid cell과 예측값의 중심점이 들어있는 grid cell의 위치가 다르다.

confidence score = P * IoU 라고 했다. 

예측값의 중심점이 들어있는 grid cell 위치가 정답의 중심점이 들어있는 grid cell과 위치가 다르면

P = 0이 되어 최종적인 값이 0이 되기 때문에 박스가 그려질 수 없다!

<br/>

정답을 제외한 나머지 grid cell 49 - 3 = 46

P값은 전부다 0값이 된다. 

박스가 살아남는 개수가 상당히 적다.

![image](https://user-images.githubusercontent.com/78403443/122008524-20be7880-cdf4-11eb-95e0-794d007c06a9.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122008556-2ae07700-cdf4-11eb-9ae3-349234ac492a.png)

이건 그려질까? 안그려진다.

P값은 높게 나오지만, IoU값이 적게 나오기 때문에, 종합적인 결과는 굉장히 작게 나와서 안그려진다.

그래서 둘다 높아야지만 Loss값은 적고, B-box는 정확하게 예측

<br/>

IoU값이 안좋은 예시임

<br/>

![image](https://user-images.githubusercontent.com/78403443/122008617-3af85680-cdf4-11eb-997a-f96d211530cf.png)

Confidence Score 값은 어느정도 물체가 포함되어있는지

물체가 들어있는지 여부를 종합적으로 판단한다.

<br/>

그래서 Confidence Score을 Box Quality라고 표현한다.

이것이 C값이다! (Box Quality 이 표현 굉장히 많이쓴다.)

<br/>

그 다음에는 굉장히 미묘한 얘기이다.

![image](https://user-images.githubusercontent.com/78403443/122008729-55cacb00-cdf4-11eb-9de0-7dab8feae3fb.png)

Cat이랑 Dog 분류할 때 Prediction이 큰 값일수록 Cat으로 예측해야한다고 했다.

하지만, C값은 높은게 좋은게 아니다.

무조건 0.7과 1중에서 예측값이 1이면 정답이랑 똑같이 맞춘 높은 예측값이라고 해서 좋은게 아니라는 얘기다.

퀄리티 값은 예측값.. 다시 말해, 이걸 얼마나 정확히 예측했는지의 값이다.

0.7로 나왔는데 1로 해버리면 정답이 이거여서 예측했다고 했기 때문에 x, y, w, h 값이

어그러지는 결과를 낳게 된다. (미묘한건데 굉장히 중요하다!)

예측을 잘한 0.7과 같은 값으로 해야 다음에 1에 가까운 값이 나올건데, 

완전 정답이랑 똑같은 1인 값으로 하면 다음 학습결과값이 어그러진다는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122008867-76932080-cdf4-11eb-96a2-33f664f60f15.png)

사람이 있다.

중심점은 한 가운데...

Image안에 물체가 1개 존재 

여기에 이렇게 예측했다. (초록색 박스)

그러면 중심점이 초록색 점 표시한 부분에 만들어진다.

<br/>

중심점이 저기 만들어진다는 얘기는 저 grid cell이 아니라는 것이다.

그러면 Box Quality가 0으로 나온다. 

결론적으로 Bbox가 안그려진다.

아슬아슬하게 비껴갔다.

<br/>

학습을 어느정도 진행했는데

아쉽게도 P값이 살짝 벗어나서 Boundary Box가 안나왔다.

하필 해당 Image에 물체가 딱 하나다!

이런 경우, 어떤 트릭이 마련되어야 한다!

<br/>

이런 경우를 조금 방지하기 위해서 하나의 grid cell당 이미지를 하나 더 그리도록 한다.

그러면 확률적으로 조금 줄어들 것이다.

<br/>

어떤 트릭이냐면 좀전의 상황을 어느정도 방지하기 위해서 Box를 cell당 하나 더 그려서 2개씩 그린다!

<br/>

2개씩 그린다는 얘기는 이게 하나 더 나온다는 얘기다

![image](https://user-images.githubusercontent.com/78403443/122009007-9b879380-cdf4-11eb-8a34-043cbf54c309.png)

이렇게...

그러면 뒤에 20개가 남을 것이다.

<br/>

박스를 하나 더 그린다.

grid cell 센터는 하나인데 그려진 Box는 2개씩 나온다.

→ 중요한건, 박스를 그리는 기회를 한번 더 준다는 것이다.

<br/>

grid cell은 총 49개이다.

최종적으로 그려지는 박스의 개수는 cell당 2개씩 그려지니까 98개의 박스가 그려진다. 

<br/>

![image](https://user-images.githubusercontent.com/78403443/122009245-d8ec2100-cdf4-11eb-9fab-e6acc38dafa5.png)

제대로 보면, 박스의 굵기가 다르다. 

박스의 굵기는 어떤 값과 연관이 있을까? C(Confidence Score, Box Quality)값과 연관이 있다.

C값이 크면 진하게, C값이 작으면 가늘게 그려지도록 후처리 한 것이다.

<br/>

나머지 20개는 카테고리에 대한 정보이다.

마지막의 도출결과가 7x7x30의 직육면체이다. 

우리가 이걸 가지고 해석해서 이 두개를 그린다고 했다. 

![image](https://user-images.githubusercontent.com/78403443/122009358-f8834980-cdf4-11eb-856e-b001ff32a8fa.png)

우선, 앞에 있는 10개의 정보를 가지고 98개의 박스를 그렸다. (상단)

여기서는 아직 박스가 표시한 것이 어떤 물체인지 모른다. 

아까 말한 20개의 카테고리로 해석해서 위 이미지 하단의 결과와 같이 물체의 종류를 해석하는 것이다. 

이 부분을 설명한다.

<br/>

YOLO 데이터셋 카테고리가 20개(→80개) 있다는 얘기이다.

인덱스가 0~19까지 있을 것이다.

예를 들어, 가장 큰 값을 가지고 있는 인덱스 3이 Dog이고 앞에 있는 5개의 Boundary 정보를 가지고

박스를 친다. 그리고 또 그 바로 뒤에 있는 5개의 Boundary 정보를 가지고 박스를 친다.

<br/>

정리 :: 

앞 10칸에서는 Box안에 들어갈 물체의 존재 여부에 대해서만 다루는 정보였다.

정작, Box안의 물체가 무엇인지는 아직까진 알 수가 없다.

Box안의 물체가 무엇인지에 대한 정보는 마지막 20개의 칸에 들어있는 정보를 통해서 알 수 있는데

20개의 값 중에서 가장 큰 확률값에 해당하는 인덱스가 Box안에 물체가 된다.

<br/>

YOLO Ver.1은 (장점)

1. 속도가 굉장히 빠른 네트워크이다.(45~155 fps)

   - 속도가 빠른 이유는 R-CNN과 비교해봤을 때 Forward를 단 한번만 하기 때문

2. 대신에, 성능은 다소 떨어짐... 다소 아쉬운 부분이 있을 수 있다.

   - 그래서 이런걸 LowAndModel이라고 한다.

3. 처음부터 끝까지 Training한다.

4. <br>

   ![image](https://user-images.githubusercontent.com/78403443/122009610-37b19a80-cdf5-11eb-8e84-2311365ca810.png)
   
   둘 중 어느모델이 좋은가?

   A는 후처리 필요, B는 학습을 좀 더 시켜야한다.

   <br/>

   정답이 없다. 

   둘다 Case by Case, Trade off관계

   완벽하게 Trade off 관계
   
   <br/>

   ① 보수적인 작업 할 때 → Model A

   ② 속도가 중요한 경우 "웬만한 것은 잡아내는데 종종 놓치는 것도 있다." → Model B (LowAndModel... YOLO)
   
   <br/>

   속도는 느리지만 성능을 중요시 할 때 R-CNN 종류를 쓴다.

   빠른속도가 중요할 때 YOLO 종류를 쓴다.

   YOLO는 Model B...
   
   <br/>

   정리 ::

   Model A 같은 것을 Precision이 낮은 모델이라고 한다. (정밀도 낮음)

   Model B 같은 것을 Recall이 낮다고 한다.
   
   <br/>

   결론 :: YOLO에 대한 설명이다.

<br/>

이렇게 YOLO를 살펴봤다.

7x7x30이 중요하다. 이 안에 다 들어있다.

<br/>

Loss Function으로 살핀다.

위치 x, y 격차만큼 차이(뺀 거)를 제곱해준다. 

c도 뺀걸 제곱한거가 Loss값에 해당이 되는데...

![image](https://user-images.githubusercontent.com/78403443/122009858-78a9af00-cdf5-11eb-96bb-98174e3fbfce.png)

예측값 (위)

Label은 직접 다 넣어줘야한다. (아래)

<br/>

각각의 차이를 뺸 것 만큼 제곱한다. 그리고, 이거 다 더하고 구한 평균값...

차이가 없다면 100% 정답률, Loss는 0이 될 것이다.

→ 각각 뺀 값이 최대한 0에 가까워지도록 학습 진행

→ 그건 x값이건, y, w, h값이건 다 동일하다

<br/>

이것이 각각의 Loss function이 작동되는 방법이다.

우리가 알고있는 것과 똑같다. 

각각을 빼고 제곱하는... 공식이 코드에 그대로 들어있다.

<br/>

YOLO Ver.1에 대한 디테일한 정리가 되어있다.

- GoogLeNet (20개 레이어로, 1000개의 이미지를 분류하는 네트워크이다)

- Object Detection에서 활성화함수로는 Leaky ReLU(리키 렐루)를 쓴다

- (★중요) 이미지 입력사이즈가 무조건 448x448x3 그리고 이걸 가지고 이미지 리사이즈를 했다.<br>
  근데, 자세히보면 224x224 학습 입력하고 test할 때 448x448로 한거다.

- mAP(성능 지표 종류이다)는 IoU랑 같이 쓴다.

- 파스칼은 이미지 분류개수가 20개밖에 안되서 일상생활 사물을 인지하기 위해서는 터무니없이 작은 개수이다<br>
  나중 버전에서는 늘린다.

- Batch size = 64 이다.

- Dropout = 0.5

- 데이터 변형...(어느걸 먼저 하느냐가 영향을 미친다)<br>
  센스있게 가야한다.<br> 
  어느걸 먼저해야 코드가 수월하게 작성되는지에 영향이 있다.<br>
  약간약간씩 변형하는 센스가 중요하다.<br> 
  (직접 경험해보지 않으면 알 수 없는 코드)<br>

<br/>

YOLO는 슈퍼맨이라고 부르는 Batch Normalization 안쓴다.

안쓰는 이유는? Batch Normalization 나오자마자 YOLO Ver.1이 나왔고 

넣을 겨를이 없었기 때문에 나중 버전에서 추가가 된다.

<br/>

YOLO기술은 IoU만으로 성능평가하기엔 굉장히 무리가 있다.

그래서, YOLO는 속도가 중요하니까 속도적인 측면하고, mAP라는 성능지표를 같이 보면서 조정을 한다.

YOLO 경우에는 속도가 0.45초 정도이다.

성능 확인하고... 

거의 비슷한데 Caltech이라는 데이터에서 속도가 조금 더 잘나온다.

어쨋든, 속도와 성능을 집중해서 봐야한다는 것...

<br/>

결론 :: 성능은 다소 떨어지지만 속도는 최고

<br/>

coco dataset을 보자

![image](https://user-images.githubusercontent.com/78403443/122010057-b27ab580-cdf5-11eb-9586-9421f250290d.png)

실제 YOLO ver.3에서 쓰는 데이터셋이 coco dataset이다.

coco dataset으로 정확도 측정했을 때 랭킹 순위

<br/>

AP값을 올리기가 굉장히 어렵다... 

Coco dataset 엄청 어려운 데이터셋이다.

Coco dataset은 해상도가 작고, Size가 크다.

데이터가 50만개가 있다... 따라서 50만개 중 58% 맞춘 AP값은 엄청 높은 것이다.

<br/>

구글 검색 : coco yolo v1

![image](https://user-images.githubusercontent.com/78403443/122010192-d63dfb80-cdf5-11eb-968a-a367bd0139f0.png)

보면 이런 사무실 집기류 데이터셋이 cocodata의 많은 비중을 차지한다.

<br/>

Retinanet face

![1_kCNF6Ti1tj-onoKI0IGqwg](https://user-images.githubusercontent.com/78403443/122010262-e8b83500-cdf5-11eb-9eb1-078e79b894c9.png)

(출처 : https://blog.usejournal.com/object-detection-object-detection-is-an-important-task-in-the-field-of-computer-vision-research-63fdcc006fb1?gi=b2c2060315c8)

이런걸 50% 이상 맞췄다는 것이다.

아마 YOLO를 쓰지 않고, R-CNN 알고리즘을 사용해서 50%나 되는 정확도가 나온 것인듯하다.

<br/>

YOLO Ver.1은 (단점)

1. 공간정보를 잃는다

   - 다시 3차원으로 reshape 하지 않는다!

2. anchor 사용 안한다. 

   - ver.2에선 사용한다. (ver.2에서 넘어야 할 산 중 하나)

3. 낮은 recall이 일어난다.

   - ver.2에선 7% 상승하는데, 그만큼 anchor가 막강하다

4. 정답 카테고리 20개밖에 안된다

<br/>

ver.2에선 다 해결이 된 부분이다.

ver.2는 ver.1 부족한 점 보완 + anchor

<br/>

---

**YOLO ver.2**

<br/>

- Better 

  - 성능 향상

  - Batch Normalization 적용

  - High resolution classifier

    - ver.1에서는 train과 test 해상도가 달랐다. → Acc 낮았다.
    - ver.2에서는 성능 향상을 위해서 사이즈를 똑같이 맞춰줬다. 448x448로 학습, 테스트때 동일한 사이즈로

  - anchor를 써서 성능이 높아졌다.

  - Multi-scaling training (굉장히 어렵고, 기술적인 부분)

- Faster

  - 속도 향상

  - Darknet-19

    - YOLO ver.1과 Darknet 프레임워크를 만든 조셉 레드몬이 만듬
    - Darknet이라는 프레임워크(PyTorch, Tensorflow 같은)로 만든 네트워크 모델
    - 똑같은 이미지넷 데이터셋으로 GoogLeNet에 비해 2% 상승한 74% 정확도 뽑아내고, 속도를 대폭 향상시킴

- Stronger

  - 카테고리 갯수를 늘렸다.

  - 원래 20개짜리를 9000개로

  - 실제로 이 부분은 해당이 안되고 ver.2에서 better, faster를 꼽을 수 있다.

  - 이 부분은 사연이 있다. 그 부분을 설명...<br>
    논문에는 한 가지 모델만 소개되는게 일반적인데,<br> 
    YOLO 2 논문에는 2가지 모델이 소개됨<br>

    - YOLO ver.2

    - YOLO 9000

      - 카테고리 개수를 무진장 늘린 모델, 9000개로

      - 성능이 30%가 안되게 나온다.<br>
        (시도는 굉장히 좋으나, 실생활에서 가져다 쓰기에 아쉽다는 얘기다, 이걸 극복하지 못함)

      - 아쉽게 포기

      - 정리 ::<br> 
        혁신적이기는 하지만 상용화 할 수 없는 모델<br>
        쓸모는 있지만 그닥 혁명적이진 않은 모델<br>

<br/>

마무리 짓고 YOLO 2를 만듬, 카테고리 개수는 20개 정도로 비슷하게 가져가고,

성능과 속도를 끌어올렸다. - 이게 정말 혁신적인 부분

<br/>

특히 anchor는 Faster R-CNN을 참고함

<br/>

![image](https://user-images.githubusercontent.com/78403443/122010556-2d43d080-cdf6-11eb-97de-72e7ae0de250.png)

앞 부분 :: Convolution 설명 생략

여기서는 unet에서 사용했던 concat기법이 사용된다.

26x26x256 → max pooling 해서 사이즈 줄임 → Convolution으로 채널 늘림

13x13x2048이랑 concat이 이루어짐, 여기서 하나 생략되있음... 13x13x1024로 늘려서 더하고) 13x13x2048이랑 concat

그래서 13x13x3072 만들어짐 (채널 1024 + 2048 = 3072)

그리고 13x13x125 만들어짐. 

원본이미지는 416x416

<br/>

YOLO 1에서는 7x7x30

YOLO 2 에서는 13x13x125 더 잘게 쪼겠다.

YOLO 2에서의 출력 사이즈 (13x13x125) 굉장히 중요하다.

<br/>

ver.1에서 문제였던 recall이 낮은 문제를 해결했다. 

7%나 향상

<br/>

---

anchor부터는 내일 제대로 다시 나간다.
