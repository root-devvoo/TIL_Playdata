(※ 저작권 문제로 인해 pdf 파일 슬라이드 캡쳐본은 업로드하지 않습니다)

<br/>

**YOLO 2**

<br/>

YOLO 기술의 핵심은 버전1, 버전2에 다 녹아들어있다.

오늘은 YOLO 2의 가장 혁신적인 기술이라고 할 수 있는 anchor 에 대해서 설명한다.

<br/>

Remove Fully Connected layers 라고 되어있는 부분은 Multi Scaling 부분과 연결된다.

<br/>

Modified input size in the detector 

448x448로 트레이닝하고 테스트하는데, 사실 여기 트릭이 있다.

448x448 대신 416x416으로 학습하고 테스트하기도 한다.

<br/>

anchor 들어간다.

<br/>

사실 7% 향상시켰는데, anchor는 레드몬이 발명한게 아니다.

Fast R-CNN에서 더 속도를 향상시킨 Faster R-CNN... 

여기서 anchor라는 아이디어가 나온다!

<br/>

버전 1에서의 답지의 형태 (좌측)

버전 2에서의 답지의 형태 (우측)

답지의 형태는 그림 표시가 아니라 어떤거나 위와 같음...

그림으로 박스가 그려진건 답지가 아니라 후처리한 결과임

<br/>

YOLO 1에서는 BBox 1, 2가 2개 있다는건 한 이미지 안에 물체가 두개 있다는 얘기임

하지만 YOLO 2에서는 비슷하게 나오는데 똑같아보이는게 몇개씩 있다. 

anchor의 개념을 이해하면 이해가 될 부분이다. 

<br/>

anchor

<br/>

anchor는 cheating(속임수)이다. 그런데, 납득할만한 Cheating이다.

<br/>

예를 들어, 우리가 모의고사를 본다. 

근데, 교무실에 몰래 들어가서 답안을 훔쳐간다. 

그러고 모의고사를 보면 성적이 잘 나온다. 흔히 이런걸 우리는 cheating이라고 한다.

근데, 수능해서는 이렇게 cheating을 못한다.

<br/>

anchor가 납득할만한 Cheating이라는건 

조금 야비하기는 하지만 실제 Inference에서 성능감소가 일어나지 않는다.

그래서, cheating(Anchor) 해도 된다.

<br/>

설명 ::

anchor는 이미지에 사물이 있다. 

데이터셋(답안)을 미리 컨닝하는 것이다. 

(컨닝)훓어보고 나서 자기랑 맞는 좋은 형태의 답지 몇개를 찾아서 

grid cell당 찾아낸 박스를 무조건 대입하는 것이다.

그리고 갖다 쓰는 것이다. 그리고 정답과의 격차만큼 보정해 나가는 것이다.

<br/>

다시 한번 천천히 설명 ::

답지를 먼저 보고 거기서 B-boundary로 좋은 형태를 찾아나가는 것이다.

미리 내가 Inference 하게 될 데이터셋 답지를 보고 거기서 몇개씩 찾는 것이다.

<br/>

Object Detection에서 가장 많이 사용하는 데이터셋이 CoCo Dataset이다.

CoCo Dataset은 사람들의 일상을 다루는 데이터셋이다.

(실제 존재하는 데이터들이 모두 들어있다는 것에서 굉장히 중요한 의미를 가진다)

현실(real world) 데이터이기 때문에 컨닝하기가 쉽다.

<br/>

(참고 :: 사진 공유 커뮤니티 사이트 : https://www.flickr.com/)

이 사이트에 일상의 이미지가 담겨져있다. 일상의 이미지는 real world를 의미한다.

이 곳 사진을 긁어다 모은 데이터가 CoCo Dataset이다.

CoCo Dataset을 보다보면 전체적으로 많이 등장하는 이미지의 사이즈가 있을 것이다.

그 박스모양을 cheating 하는 것이다. (답안을 커닝하듯이)

![image](https://user-images.githubusercontent.com/78403443/122184770-862f6980-cec7-11eb-9d07-aa30f63cec18.png)

이런 모양이 Cheating이 된 결과이다. 

이런게 많이 나올 수도 있다 하지만, 대략 5개정도로 추출한 것이다.

왜? 정교하기는 하겠지만 Computation cost가 많이 들어서...

그래서 5개 정도가 좋더라~

![image](https://user-images.githubusercontent.com/78403443/122184812-8fb8d180-cec7-11eb-963c-8c6516fea9ad.png)

이 정도대(5개 정도가) 성능이 좋더라라는걸 보여주는 그래프임

<br/>

맨 땅에 헤딩하는 것보다 가안을 가지고 정답을 향해서 수정해나가는 방식을 취하면

훨씬 더 Performance가 올라간다는 얘기(잘 찾는다는 얘기)

<br/>

조금 답안을 미리 본다는 점, 실제 Inference에서 성능감소가 일어나지 않는다는 점에서

조금 야비하기는 하지만 성능을 올리기 위해서 anchor를 쓴다(써야한다)는 얘기임

<br/>

![image](https://user-images.githubusercontent.com/78403443/122184883-9fd0b100-cec7-11eb-9f06-f59dfc789aa2.png)

YOLO ver.1에선 박스가 98개 쳐진다고 했는데,

YOLO ver.2에선 박스가 몇개 쳐질까?

셀 당 가안의 박스가 5개씩 쳐진 것이다.

<br/>

ver.1은 49*2 = 98

anchor를 5개 쓴다고 했으니까...

ver.2는 49*5 = 245

![image](https://user-images.githubusercontent.com/78403443/122184951-af4ffa00-cec7-11eb-95a5-74b6a93cefd8.png)

13은 원본이미지를 13등분 한다는 얘기니까,

더 촘촘하게 그리드셀이 나온다는 얘기이다.

최종적인 박스는 13x3x5 = 845

<br/>

![image](https://user-images.githubusercontent.com/78403443/122185251-e7efd380-cec7-11eb-9719-6be0943e9732.png)

모든 grid cell에서 좌상단을 기준으로 anchor를 가지고 온다. (x표시)

<br/>

이 상태에서 내가 가안으로 가지고 온 이 박스를

얼마나 수정해서 Loss가 0에 가깝게 예측을 하는가가 관건이다.

여기서 만약 학습을 통해 나오는 박스정보가 X, Y, W, H, C(0.5, 0.5, 0.5, 0.5, 제외)라면

<br/>

① x, y축으로 cell 기준으로 이동

파란색x... 원래는 하얀색 x였는데 X, Y값 기준으로 이동하는 것

수정된 파란색x(중심점) 기준으로 새로운 박스(노란색 박스)가 그려질 것임

(셀 안에서 중심 좌표가 이동)

<br/>

② y = ex 공식이 쓰임 (오른쪽 그래프)

w(가로), h(세로) 1.2배 키운다.

그러면 노란색 박스의 가로와 세로가 조금씩 길어진다

<br/>

①+② 합친 것으로 최종 수정된다. (연두색 박스)

정리 ::

학습에 있어서 1차 가안(Anchor)을 먼저 제공

그걸 수정하는 방향으로 학습진행

☞ Recall이 7%나 향상되는 결과를 얻었다

<br/>

![image](https://user-images.githubusercontent.com/78403443/122185356-00f88480-cec8-11eb-8d8c-4b0204e788a1.png)

이제, 이 공식 설명

버전 2는 최종출력값이 어떻게 나오냐하면

![image](https://user-images.githubusercontent.com/78403443/122185483-18377200-cec8-11eb-86cf-59bdb152e0df.png)

13x13

이거의 의미는 grid cell이 쪼개지는 정도(촘촘한 정도)

그런데 채널이 125가 나온다.

이건 어떻게 나왔냐? anchor를 5개 쓰는 것으로 정해놨다.

anchor를 5개 쓴다는 것은 grid cell당 5개의 boundary box가 쳐진다는 얘기임

BBOX 1 {x, y, w, h, c} 

BBOX 2 {x, y, w, h, c}

BBOX 3 {x, y, w, h, c}

BBOX 4 {x, y, w, h, c}

BBOX 5 {x, y, w, h, c}

이 정보가 각각 들어있을 것임

5칸이 Box의 정보를 가지고 있는 칸 (x, y, w, h, c} 

그리고 그 뒤에 20칸 == 카테고리 정보가 들어있는 칸

이게 각각 5개 있음, 그러므로 125칸이 나오는 것임

(25 * 5 = 125)

anchor가 5개이기 때문에 Box가 5개 그려지는 것이다.

<br/>

버전 1하고 원리는 똑같은데 버전 2에선 anchor 5개를 줘서 더 많이 촘촘하게 쪼갠다는 것이다.

<br/>

multi scaling (멀티 스케일링)

<br/>

멀티 스케일링은 네트워크에 입력되는 이미지 사이즈를 Multiple하게 가져간다는 의미

다시 말해서, 이미지 사이즈가 320 혹은 352x352 혹은 448x448... 608x608까지 다 다르게 들어갈 수 있다는 의미

네트워크를 통해서 학습하기 위해서 우리가 이미지를 넣을 때, 

512x512 원본 사이즈를 조금씩 줄여나가고 필터는 늘려가면서 특징을 늘려나갔었는데...

얘는 이걸 다 가져간다는 얘기임, 이게 multi scaling

<br/>

사이즈는 총 10개 중에 랜덤하게 들어간다. (그렇게 만들어놨다)

랜덤하게 들어가는 가장 작은 사이즈가 320으로 시작하고, 제일 큰게 608로 들어간다는 얘기

(320, 352, 416, 448, 480 ... 608)

<br/>

multi scaling 다시 설명...

![image](https://user-images.githubusercontent.com/78403443/122185709-474de380-cec8-11eb-8154-0b41fd9c5d6d.png)

⑴ 우리가 이미지 데이터셋 가져올 때 크롤링해서 많이 가져온다.

크롤링으로 가져오게 되면 정사각형 형태로 가져와지지 않는다.

(width, height 동일한 형태로 가져와지지 않는다)

<br/>

우리가 말하는 원본이미지는 위와 같은 사이즈를 말한다. 

(1024x890) 이렇게 긁어와진다. 

우리가 이걸 reshape 하게 되면 비율이 망가진다. 

☞ 비율은 그대로 유지한 채로 448x448로 (결론적으로) 만들어야 한다.

<br/>

이걸 어떻게 하느냐?

① 비율은 그대로 유지한 채로 하기 위해서 Random Crop을 사용한다.

가로, 세로 사이즈 중에서 Minimum한 값으로 Crop한다.

그러면 이런식으로 된다.

![image](https://user-images.githubusercontent.com/78403443/122185790-59c81d00-cec8-11eb-919c-9ee1da4f3733.png)

그러면 나머지 부분은 포기하는 것이다.

근데, minimum한 값으로 랜덤으로 crop하기 때문에 어떻게 잘릴지는 모른다.

일단 crop시킨다는 것, minimum한 값으로 crop한다는게 중요하다.

그러면 890x890이 될 것이고

<br/>

② 890x890을 448x448로 resize 한다. 

(이걸 꼭 알고 있어야 한다)

<br/>

그리고,

③ Random crip하고 resize한 ②를 모델에 넣고 학습 진행

이때, 사이즈가 448x448 로도 들어갈 수 있고, 416x416, 320x320, 608x608로도 넣을 수 있는데

이게 총 10개 중에 하나의 size를 랜덤하게 선택해서 학습을 진행하는게

multiple scaling이다.

<br/>

YOLO 버전 1에서는 224x224로 학습하고 test할 때만 448x448을 썼다.

버전 2에서는 448x448로 학습하고, 448x448로 test한다고 했지만

10개 사이즈 중 하나로 Multiple 하게 할 수 있다는 얘기

그래서 아~까 전에 416x416으로 학습하기도 한다는 점을 중요하다는 얘기를 한 것임

<br/>

multiple scaling 할 때 랜덤으로 나오는 사이즈가 총 10개라고 했는데, 왜 10개의 사이즈가 나왔는지 설명

![image](https://user-images.githubusercontent.com/78403443/122185916-75332800-cec8-11eb-8482-5816e06ef905.png)

여기서 사이즈 변화만 보기

416 → 208 → 104 → 52 → 26 → 13

<br/>

416으로 시작해서 13 출력결과를 만들어나가는 과정을 그린건데

2배씩 5번 줄여나갔다.

그렇게 되면, 총 25 이 줄여진다.

25 == 1/32배 줄여진 것임

여기서 32배라는 숫자가 나오게 되었고,

320은 32 * 10이다.

352는 32 * 11이다.

384는 32 * 12

416은 32 * 13

448은 32 * 14

480은 32 * 15

512는 32 * 16

544는 32 * 17

576은 32 * 18

608은 32 * 19이다.

<br/>

320, 352, 384, 416, 448, 480, 512, 544, 576, 608

이렇게 10개 중에 랜덤하게 입력을 하겠다는 얘기이다.

이게 multi scaling 이다. 

두번째 문단에 다 안나왔지만... 320, 352, 384, 416, 448, 480, 512, 544, 576, 608 이 10개가 들어감

<br/>

설명 ::

![image](https://user-images.githubusercontent.com/78403443/122186035-9431ba00-cec8-11eb-8df5-14b6f3b6f189.png)

원본이미지 넣으면 오른쪽과 같이 출력 (608x608 경우 19x19 출력)

<br/>

남는 최종적인 결과가 이렇게 된다는 얘기는

이미지를 크게 넣을수록 더 촘촘하게 grid cell이 나온다는 얘기임

![image](https://user-images.githubusercontent.com/78403443/122186082-a1e73f80-cec8-11eb-841f-658c0a976c57.png)

version 1은 98개 어떻게 나왔나... 7x7로 쪼갰고 한번 더 그렸기 때문에 98개의 boundary box가 그려진다.

version 2는 13x13x5 = 845, 

그럼 multi scaling을 한다는 얘기는 416x416 넣었을 때 Boundary box가 총 845개 쳐진다.

448x448 넣을 경우 :: 14x14x5 = 980,

320x320 넣을 경우 :: 10x10x5 = 500

<br/>

![image](https://user-images.githubusercontent.com/78403443/122186131-add30180-cec8-11eb-98c6-62175e83f053.png)

입력사이즈가 달라지면 네트워크 출력결과가 달라질 것이고,

우리가 하는건 Detection...

출력결과가 달라지면 사물의 중심 포인트가 있을 것이고

이 중심포인트를 알면 width, height를 구할 수 있는데...

이 Boundary Box의 center가 size에 영향을 미치지 않을까? 이런 우려를 하게된다.

그런데, 오해이다. 

CNN에서 네트워크는 사실 입력 이미지를 가지고 있는게 아니라 

(지금의 경우에는) 3x3x3이라는 정육면체... 이게 통과 되는 것이다.

(물론 이걸 여러개 사용하기는 하지만...)

무슨말이냐면, 내가 448x448 이미지에 3x3x3 필터를 통과시켜서

418x418 그대로 나오게 할 수 있다.

어떻게? padding = 1, stride = 1 주고 filter size 1x1 쓰면 똑같이 나올 수 있다.

마찬가지로 448x448에도... 사이즈는 중요하지 않다.

<br/>

그 다음에, 

만약 448x448을 원본이미지에 넣고, 3x3 필터를 통해서 사이즈를 최종적으로 줄여나가게 되면

14x14로 출력이 된다.

만약에 416x416 원본이미지를 넣고 3x3 필터로 네트워크를 통과시키면

최종 출력결과가 13x13이 된다는 얘기는

이 비율을 위는 가로 세로 14개로 나눈거고

아래는 13개로 나눈 것... 

더 촘촘하고 덜 촘촘한 것의 그것만 차이지 센터 지점이 바뀌는 것이 아니다.

<br/>

다시 말해, 출력 결과가 달라져도 center 지점하고, Boundary box의 size에는 영향을 미치지 않는다는 얘기

결국, 우리가 알고 있는 결과에서 달라지지 않는다는 얘기이다.

<br/>

정리 :: 

![image](https://user-images.githubusercontent.com/78403443/122186203-c216fe80-cec8-11eb-9fe8-32b8470bdfd7.png)

YOLO 1에서는 7x7x(결과)2 = 98개의 박스가 그려진다

YOLO 2에서는 n * n * (anchor의 갯수)5 = 500 (320x320 size) ~ 1805 (608x608 size)

multi scaling : 1/32 감소 → 320/10, 608/19... 10~19 grid cell이 그려졌다는 것을 알았다.

그리고 출력결과의 center가 box size에 영향을 주지 않는 것도 알았다. 

그러면 왜 multi size로 했나? 를 알아야한다. 

왜 했나?

설명...

![image](https://user-images.githubusercontent.com/78403443/122186228-cc38fd00-cec8-11eb-9c2d-29b63e7a5a68.png)

가로 2000 세로 1000의 아주 큰 이미지가 있다.

비율을 유지한 채로 정사각형으로 만들어야 된다는 것을 기억하고 있을 것이다.

<br/>

① 두 이미지 다 비율을 유지한 채로 정사각형을 만들어야 한다.

② 그리고나서, resize를 해야한다.

<br/>

Multi scaling이다. 

그러면 왼쪽과 같은 이런 이미지도 입력되고 오른쪽과 같은 이런 이미지도 입력이 될 것이다.

grid를 가장 촘촘하게 자르는게 608x608 이었으니까... 608로 만들어야한다.

그럼 오른쪽 주황색 박스는 500x500 왼쪽 주황색 박스는 1000x1000 상태에서

608x608이 되어야한다.

그러면 왼쪽은 원본대비 0.6배 감소한 것이다. (저해상도)

오른쪽은 원본대비 대충 1.2배 증가한 것이다. (고해상도)

<br/>

Multi Scale Training(Multi Scale Training은 입력 이미지 사이즈를 다르게 하는 것)

한 진짜 이유는 Resolution(해상도)과 상관이 있는데, 

Resolution과 무관하게 모델 학습을 진행할 수 있도록 하기 위함이다.

<br/>

다시 말해서, 고해상도, 저해상도 같은 이미지 상관없이 학습을 진행시키고,

그 결과로 예측력을 높이려고 한 것이다.

<br/>

그래서 이것을 Training 할 때는 448, 320, 608, 516... 등등 다양하게 하지만...

Test할 때는 하나로만 하면 되는데, 이때 사이즈는 반드시 416x416으로 한다.

Test는 굳이 multiple 하게 할 필요가 없으니까

<br/>

![image](https://user-images.githubusercontent.com/78403443/122186336-e70b7180-cec8-11eb-90cb-7e0188c3428a.png)

448에서 32로 나눠서 14로 사이즈를 나오게 했다는 얘기는

grid cell을 촘촘하게 나눴다는 얘기

<br/>

224에서 32로 나눠서 7로 사이즈를 나오게 한다는 얘기는

덜 촘촘하게 나눴다는 얘기

<br/>

박스가 많이 만들어지건 적게 만들어지건 정말 중요한건

Confidence Score가 높은 값을 추리기만 한다.

<br/>

Code 어렵다.

그래서 Object Detection은 진짜 전문가만 할 수 있다.

이 힘든 부분만 넘으면 진짜 딥러닝 전문가라고 얘기할 수 있다.

<br/>

솔직히 말하면 스켈레톤 코드 못짜고 (우리나라 굴지의 대기업도 못짠다, 손도 못댐)

Customizing 하는 정도면 충분한데, Customizing 하려면 이 내용들을 알아야한다.

<br/>

돌리는 것만 하고 입으로 딥러닝 전문가라고 하는 사람 되게 많다.

하지만, 이 공부를 시작해보면 이해한다. 공부하다보면 포기하게 된다(그만큼 정말 턱턱 막힐정도로 어렵다는 얘기)

<br/>

네트워크 설계할 때 잠깐 도움이 될 수 있는 지점 설명...

![image](https://user-images.githubusercontent.com/78403443/122186433-00acb900-cec9-11eb-8da4-53950dc9178d.png)

사이즈를 608.... 448, 416, 320

32로 나누는게 되게 중요한 의미 설명...

이미지 사이즈 420은 왜 안되냐?

420 → 210 → 105 → 그 다음은?... 2로 안나눠진다.

원래는, 52로 만들 수는 있다. zero padding으로 장난질하면 된다.

하지만 이건 정법이 아니다. 그냥 에러 안나게 하려고 하는 것...

(줄일 수는 있으나 줄이지 말라는 얘기)

<br/>

그래서 결론 :: 32배수를 쓰면 이런 일이 안벌어진다는 얘기

왜? 

2로 줄여나가는 경우보다 32로 줄여나갈 때 딱 떨어지게 확실하게 줄임

![image](https://user-images.githubusercontent.com/78403443/122186504-102c0200-cec9-11eb-8e22-5d6f593df823.png)

필터 갯수 → 2의 배수로 늘려나가면 되고

이미지 사이즈 → 32배수로 줄여나가면 된다.

<br/>

그리고 CNN이 기본이라는 얘기는 어떤 것이든 CNN형식으로 돌아가기 때문

모든 모델의 근간이라는 얘기! 

그래서 CNN부터 들어가는 것

<br/>

416인 이유에 대해서 설명

<br/>

448x448 에서 320(10)~608(19) 10개의 다양한 사이즈를 입력해서 학습

10x10x5 ~ 19x19x5 까지 다양하게 나온다.

<br/>

학습데이터 size와 Test 데이터 사이즈는 같다는 얘기다.

<br/>

하지만 Detector는 Inference할 때를 말하는 것이다.

448 대신 416x416을 써서 Accuracy를 올린다.

<br/>

성능을 올리는 가장 중요한 기법인데, 이 부분에 대해서 설명을 하겠다는 얘기

![image](https://user-images.githubusercontent.com/78403443/122186636-30f45780-cec9-11eb-9c74-a008e1949455.png)

YOLO 2 뿐만 아니라 YOLO 3에서도 중요한 부분이다.

YOLO 2 에서는 train 에서는 다양한 이미지로 학습

test에서는 한 size로 하면 된다.

(448x448 대신 416x416을 사실 쓰고 있다)

<br/>

사이즈는 320 ~ 416, 448 ~ 608 까지의 사이즈가 있다.

320 == 1/32로 나눌 때 = 10

416 = 13

448 = 14

608 = 19

그런데, test 608로 했더니 성능이 좋았다...는 평가도 있다. (디테일 하게 쪼갰으니까 당연히 좋을 수밖에 없다)

그러나, Network는 너무 무겁다. 

그래서 반드시 Computation cost 대비로 평가가 필요하다.

그래서 이런 말도 쓴다. Computation Effective한 size를 찾는다.

이때, 여기서 중요한건 448(14)을 안쓰고 416(13)을 써야한다는 점 (Accuracy에서 차이를 보인다)

이 둘의 차이는 뭘까? 416의 최종 출력결과가 13...홀수라는 점

Object Detection에서 홀수가 왜 중요하냐? 설명...

![image](https://user-images.githubusercontent.com/78403443/122186693-3fdb0a00-cec9-11eb-90ff-e28a7be20874.png)

이때 홀수로 하게 되면 가로, 세로 바로 정중앙에 Center가 찍히게 된다.

짝수로 하게 되면 grid cell이 겹쳐지는 부분이 정중앙이 된다.

→ Object Detection에서는 물체가 정중앙에 위치하는 경우가 많다

<br/>

14로 하면 센터점을 구분하는데 머신이 헷갈려한다.

반면에 13은 정중앙이 직관적으로 나온다, 그렇기 때문에 학습이 더 잘 이뤄진다.

(수학적으로도 그렇고, 결과로도 두드러지게 나온다)

정중앙에 중심점이 딱 1개 찍혀야 더 좋은 예측결과가 나온다!

<br/>

논문에 딱 두 줄 나올 정도로 마이너한 부분이지만

95% 에서 97, 98%로 올리는데 중요한 역할을 하는 부분이고, 

많은 사람들이 놓치고 있는 부분이다. 

코드를 제대로 돌려본 사람이면 절대 놓치지 않고, 중요하게 여기는 부분이다.

<br/>

---

**YOLO ver.3**

논문임에도 불구하고 상당히 장난스럽고, 진중하지 않은 모습

맨 마지막 보면 twitter 끊었다고 언급하고 있음. (논문인데 ㅋㅋ 독특)

<br/>

두번째 줄 :: YOLO 3에서는 조금밖에 바뀐게 없다고 언급 (사실... 보통 논문에서는 과장하는데 ㅎㅎ)

<br/>

YOLO 3에서 핵심적인 내용

Predictions Across Scales 짧게 설명한다.. (나머지는 다 아는 내용... 여기선 패턴을 바꾸기만 함)

<br/>

갈수록 Grid cell이 점점점 촘촘해진다.

예측을 한번만 해야되는데 또 하고, 또 했다. (전과 별 새로운 내용이 없다)

여기서는 LowAndModel임에도 불구하고 성능 부분을 조금 더 신경썼다고 보면 된다.

<br/>

버전 2에서 사용된 anchor는 똑같이 연결된다.

v2에서는 anchor를 5개 썼다면

v3에서는 anchor를 9개로 늘림 (아래)

![image](https://user-images.githubusercontent.com/78403443/122186888-744ec600-cec9-11eb-8aea-3934ed41669f.png)

Accuracy Scale을 3번 했다.

<br/>

YOLO 1, 2와 공식도 똑같고, Loss 구하는 방법 등등 다 똑같다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122187076-a7915500-cec9-11eb-87fc-a62eda65987a.png)

뭐가 9개 있는건가?

anchor의 사이즈들이다.

9개의 anchor들 점점 크기가 큰 것을 볼 수 있다.

config에 다 지정이 되어있다.

보면 이해된다.

<br/>

v1에선 박스가 98개 그려지고

v2에선 N * N * 5, 416x416 == 출력 13x13일때 845개 박스 나옴

v3에선 1만개 정도의 박스가 나옴, v2에 비해 10배 가까이됨, 

그러나 1, 2개 살아남기 힘들다. 그렇게 Loss Fuction 진행됨

<br/>

표시된 이 부분은 별도학습 진행된다. (Pre Training, Trasfer Learning 부분)

다크넷 사용했다. 

YOLO에서는 Pre Training... 얼려서 뜯어온다. (속도 문제 떄문에) 

Pre Training은 뜯어오는데 얼려서 뜯어오거나 그냥 뜯어온다고 저번에 말함

내가 어떻게 하냐에 따라서 달라짐

<br/>

설명하려는 부분은 표시된 부분에 동그라미+ 기호로 되어있는 곳이다.

표시된 부분은 뭐냐면 Residual Block이다.

![image](https://user-images.githubusercontent.com/78403443/122187248-d60f3000-cec9-11eb-9fbc-10f5b2302b24.png)

논문 중 :: 이게 최고로 많이 인용된 논문임

인용횟수를 볼 때 20000회만 넘어도 굉장히 대단한 논문임

<br/>

이걸 왜 보여줬냐면 Residual이 Resnet에서 새로운 지평이 된 부분이기 때문이다.

그래서,

1. Residual이 어떻게 작동하는지 작동 (원리)메커니즘을 먼저 본다.
2. 이걸 사용해야 하는 이유로 결론을 내릴 것이다.

<br/>

출처

![image](https://user-images.githubusercontent.com/78403443/122187530-12db2700-ceca-11eb-9fa5-3cfb1cb9663c.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122187578-1cfd2580-ceca-11eb-8b5a-1876875e5cef.png)

X == 입력값 (원본이미지로 보면 안되고 이전 레이어의 출력값임)

이전 레이어에서 출력된 것이 들어와서 Convolution 연산을 하는 것 

(weight 곱하고, bias 더하고) 그리고, ReLU

그리고, 또 Convolution 연산 진행

그러면 어떤 값이 출력이 될 것이다. 

그런데 여기서는 ReLU를 안쓰고 출력된 값(F(x))에다가 처음 X값을 더한다. 

그리고 그 값에다가 ReLU를 적용한다.

이게 Residual Block이다.

<br/>

조금 더 쉽게 다시 그림으로 설명

![image](https://user-images.githubusercontent.com/78403443/122187644-2e463200-ceca-11eb-8ab8-e9921c6bb8a5.png)

X == 입력값이다

입력값에다가 Convolution 연산하고, ReLU썼다. 그 결과로 출력값 하나 나왔다.

그리고 다시 Convolution 연산을 해서 출력값이 나왔는데

이거를 아까 사진 밑에서 F(x)라고 표현한 것이다.

그리고 F(x)와 맨처음 입력값(X)를 더했다. (F(x) + X)

그리고 여기에 ReLU를 적용했다.

![image](https://user-images.githubusercontent.com/78403443/122187673-37370380-ceca-11eb-9f47-bf7dd5129910.png)

수평적으로 copy 표시만 넣어서 그림을 다시 그렸다, 

이게 아래 그림과 똑같은 그림이다.

이게 Residual Block 메커니즘이다.

<br/>

우리는 unet에서 Concatenation 시키는 것 봤었다.

unet에서 concat은 이거였다. (아래)

![image](https://user-images.githubusercontent.com/78403443/122187721-43bb5c00-ceca-11eb-93df-3e5955c14995.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122187751-4d44c400-ceca-11eb-8c87-2178c3bbcd13.png)

하지만 Residual Block에서 더한다(동그라미+)의 의미를 정리하면

X + F(x) = F(x) + X

만약 둘다 각각 32x32x256 면 이걸 더한다. 

그러면 32x32x256이 되고, 여기에다가 ReLU를 적용하는 것이다.

<br/>

이런 방법으로 더해지는 것을 원소끼리 더한다는 의미로

Element wise라고 한다.

Residual Block에서 더하기가 나온다는 부분은 unet에서 concat과 완전 다른데

unet에서 봤던 concat과 어느 지점이 다른가?

사이즈는 동일해야한다, 채널도 동일해야한다.그래야 Element wise가 일어난다.

그리고 더한 값들이 채워지는 것이다.

<br/>

보통 성능을 높이면 Computation cost가 높아지는데,

이 Residual Block은 비용을 많이 들이지 않고도 성능을 높이는 최고의 방법이라고 할 수 있다.

Resnet 논문에서 처음 나온 획기적인 부분이 이 Residual Block부분이다.

<br/>

여기까지 메커니즘이고, 

이걸 왜 사용하는지 지금부터 설명한다.

![image](https://user-images.githubusercontent.com/78403443/122188023-89782480-ceca-11eb-87b1-a09b31f272f7.png)

Resnet 논문이 획기적일 수 밖에 없는 이유?

이전에는 레이어를 여러개 쌓으면 학습이 잘 이뤄지지 않았다.

그 설명을 하려고 한다.

<br/>

Forward :: 입력이 있고, 굉장히 많은 레이어를 거쳐서 예측 결과값이 나올 것이다.

그리고 Full Loss가 계산이 된다. Loss를 가지고 학습을 진행하는 방향이 Backward 방향이다.

레이어 사이에 Batch Normalization적용, 그리고 w값을 고르게 해주기 위해서 Regularization 하는 것도 우리는 알고 있다.

그럼에도 불구하고 이 Backward를 진행하게 되면 어느정도까지는 학습이 잘 이루어지는데

레이어가 길면 길수록 값이 점점점 사그라지는 현상을 보인다.

그래서 한 중간이상 오면 값이 0값에 수렴되는 현상이 계속 발생한다.

사실 Layer가 서너단계만 지나면 그 뒤쪽 단계는 진행되지 못한다.

레이어가 4,5개만 길어져도 수압이 가다가 약해지고 결국에는 끊어져서

앞 부분(전방부)에서는 학습이 거의 진행되지 못한다.

이런 현상을 해결할 수 없었는데, 이 현상을 해결한게 Resnet 논문이면서 그 안에 Residual Block이라는 방법이

그 부분을 해결하는데 중요한 방법이 된 것이다.

weight값을 판단하는 것이 Gradient값인데 weight값을 0으로 수렴하게된다는 얘기이다.

(아무리 Batch Normalization이 되더라도 depth가 깊어지면 0으로 수렴된다)

정교한 학습을 못한다는 얘기...

![image](https://user-images.githubusercontent.com/78403443/122188118-9d238b00-ceca-11eb-9ebc-33a2c1b04c04.png)

이 지점(오른쪽)에 있는 수압을 copy해서 전방부에 약해진 쪽으로 현재 수압을 copy해서

쏴버리는 것이다. 어디로? 맨 앞 X로!

동일한 강도로 학습이 진행되도록 할 수 있게...

<br/>

이걸 한마디로 얘기할 수 있어야한다.

"Gradient Banishing" 현상을 막아준다!

Gradient Banishing 현상이 뭐냐? 학습이 끝까지 진행되지 않는 것을 말한다. (★중요)

레이어 안에서 weight값이 0에 수렴되기 때문에!

<br/>

이게 Residual Block의 매커니즘과, 왜 Residual Block 사용하는지 이유인데,

Gradient Banishing 이라는 중요한 단어가 나왔다!

<br/>

![image](https://user-images.githubusercontent.com/78403443/122188184-af052e00-ceca-11eb-9b5d-61d9340bfdfe.png)

아무튼 Residual Block 매커니즘을 써서 결과를 또 뽑고, 또 뽑고, 또 뽑았다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122188244-bd534a00-ceca-11eb-8d34-0e36b46befcc.png)

(동그라미*) 부분은 Comcatenation...

concat을 해야하는 경우는 어떤 경우?

올라오면서 기존의 정보가 상실 됐으니까

제대로 정보를 찾으려면 날 것이 필요하다. 그래서 Concat을 한다.

그것을 똑같이 뒤에서 또 반복한 것이다.

<br/>

32x32라고 가정...

초록색 부분에서 Upsampling이 이루어진다.

16을 Interpolation한 방법으로 Upsampling... 32x32이 되었다.

그리고 얘가 32x32로 concat됐다는 얘기이다.

<br/>

그 다음 32x32.. Upsampling... 64x64 되었다.

그리고 걔가 그 뒤로 가기 위해서 64x64 그리고 거기서 작용되는 것?

채널을 중심으로 64x64 짜리랑 앞에 32x32랑 붙이려고 하는데

사이즈가 맞지 않아서 못 맞춘다.

그러면 어떻게 사이즈를 맞출까? 앞 이미지를 Upsampling을 해서 사이즈를 64x64로 늘려준다.

<br/>

①의 경우 :: 32x32 이미지를 16x16 이미지에 concat하려고 한다.

stride = 2를 주거나 Max Pooling을 해서 사이즈를 줄인다.

<br/>

②의 경우 :: Resize (Upsampling 하면 된다)

<br/>

기존에 배운거 다 떼려박았다. 새로운건 scaling을 여러번 하는거 말고는 없다.

<br/>

Retinanet은 속도는 빠른데 성능이 좋지 않다. 

YOLO는 속도와 성능 둘다 잡았다.

<br/>

---

**구글 코랩 4. Object Detection 폴더 final_detection.ipynb 파일보기**

<br/>

코랩에서final_detection.ipynb 전체코드를 돌리면 마지막에 에러가 뜬다.

그래서... 그림대로 경로에 들어가서

![image](https://user-images.githubusercontent.com/78403443/122188529-00adb880-cecb-11eb-9a48-ce8d101a7fdc.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122188574-0c00e400-cecb-11eb-9721-5396e63d5b3b.png)

![image](https://user-images.githubusercontent.com/78403443/122188597-1327f200-cecb-11eb-9db3-740f4c6f7195.png)

![image](https://user-images.githubusercontent.com/78403443/122188626-1c18c380-cecb-11eb-9bba-c185e378945a.png)

detect.py 파일, models.py 코드를 위와 같이 수정해준다.

<br/>

그리고 final_detection.ipynb파일의 마지막 셀을 다시 실행시킨다.

그러면 PyTorch-YOLOv3라는 폴더가 생기고

![image](https://user-images.githubusercontent.com/78403443/122190536-dceb7200-cecc-11eb-8d55-af78f8fb62dd.png)

그 안에 data/samples 폴더에는 Inference Test할 sample이미지 파일들이 들어있다.

(새로운 데이터로 학습 및 validation test 시킬 때는 data/custom 폴더에 학습 시킬 train이미지와 label 이미지를 넣어줘야한다)

(그리고, 설정도 해줘야한다)

<br/>

samples 폴더 안에 내가 찍은 사진 이미지 파일을 넣고

마지막 셀 코드를 다시 돌려주었다.

테스트 결과는 output 폴더에 있다. 확인해보았더니 아래와 같이 결과가 나왔다.

![image](https://user-images.githubusercontent.com/78403443/122190666-fe4c5e00-cecc-11eb-8b4b-8eb328f2fdc1.png)

나빼고는 인식을 못했지만, 그래도 이정도면 결과가 꽤 잘나온 것!

<br/>

---

https://www.immersivelimit.com/tutorials/create-coco-annotations-from-scratch 사이트 보기

coco dataset 답지... JSON형식의 답지이다.

JSON형식의 답지를 알아야한다.

알아보자.

<br/>

JSON 답지에서는 images 하고, Annotation이 제일 중요하다 (잘 봐야한다)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122190926-3ce21880-cecd-11eb-9c97-b75716ec5db2.png)

이런 JSON형식으로 되어있다.

<br/>

info == 정보

![image](https://user-images.githubusercontent.com/78403443/122190974-479cad80-cecd-11eb-8c1b-2bf384006097.png)

<br/>

images == 이미지 정보

![image](https://user-images.githubusercontent.com/78403443/122191016-52574280-cecd-11eb-86b3-c98a4e1d8b55.png)

flickr_url :: 이미지 다운받을 수 있는 주소

id가 진짜 중요한데, 이 값은 file_name에서 앞에 0을 지운 숫자

이렇게 id를 지정하는데 일종의 pk값이다

<br/>

JSON 한 블럭이 하나의 이미지 정보이다.

이런게 Coco dataset에는 6만개가 있다.

<br/>

Categories에는

![image](https://user-images.githubusercontent.com/78403443/122191090-613df500-cecd-11eb-8dc9-bb65dbb55b5b.png)

라벨 카테고리가 들어있다. 총 90개임...

<br/>

JSON 답지에서 images 하고, Annotation이 제일 중요하다고 했다.

그중에서도 Annotation을 꼭 알아야한다.

<br/>

Annotation은 박스 그리는 정보가 있다.

![image](https://user-images.githubusercontent.com/78403443/122191174-73b82e80-cecd-11eb-8546-d68aab79e446.png)

이게 이미지라고 하면 여기서 박스쳐야 하는 정보들...

이렇게 있을 것이다.(하얗게 체크한 것들) 얘네들 지금 7개의 이미지가 하나의 이미지에 들어있다.

(밑에꺼 3개는 없다고 친다)

다시 말해서 이 이미지에 물체가 7개있다.

<br/>

이걸 원본이미지라고 생각하고

이 안에 물체가 하나일 수도 있지만, 물체가 여러개 있을 수도 있다.

여기서 물체는 이미지이다. 

이걸 답지에서 어떻게 다루는지가 핵심이다. 

![image](https://user-images.githubusercontent.com/78403443/122191226-816db400-cecd-11eb-9809-32eff14e8e3c.png)

원본이미지기 때문에 당연히 박스는 안그려져있다.

이 파일이 1.jpg라고 하면

images 폴더에 이미지들이 들어 있을 것이다.

그리고 1.jpg가 이렇게 있을 것이다.

이렇게 되면 박스가 7개 쳐져야하니까 

bbox 1, bbox 2, bbox 3, bbox 4, bbox 5, bbox 6, bbox 7이 나올 것이고,

<br/>

bbox1(x, y, w, h, c)

bbox2(x, y, w, h, c)

bbox3(x, y, w, h, c)

...

bbox7(x, y, w, h, c)

이렇게 있을 것이다.

문제는 1.jpg에 하나로 묶여져 있지 않다는 점이다.

각각 다른 줄에 다 흩어져있다.

<br/>

그래서 이 boundary box 뒤에는 이 5가지 정보 외에 다른 정보가 필요하다.

bbox1(x, y, w, h, c), 1.jpg 

bbox2(x, y, w, h, c), 1.jpg 이런식으로...

<br/>

그리고 1.jpg 이미지를 로드해서 가져와야한다.

→ 1.jpg의 정보 다 가져와! 라는 알고리즘이 돌아가야 bbox 정보들이 다 불러와진다.

이렇게 묶어지는 형태이다.

<br/>

이게 무슨 값이냐면... Annotation

![image](https://user-images.githubusercontent.com/78403443/122192326-854e0600-cece-11eb-9c48-6d58152d63d9.png)

(여기서 마지막 c(confidence score)는 생략되었다)

images에선 이게 파일 이름이었는데, 

Annotation에서는 위와 같이 파일 이름이 image_id가 되는 것이다.

만약에 1.jpg면

1.jpg 이미지에서 정보들을 다 불러오는 것이다.

<br/>

그럼 다시 Annotation의 입장으로 보면

원본이미지 image_id가 되는 것이고

그 안에 각각의 물체이미지 정보가 있게 되는 것이다. 

그 bbox 정보가 위의 bbox에 있다.

그리고 category_id가 박스 안의 정보(라벨) id가 된다. 

이런 형식이 계속 반복되어 나타나게 되는 것이다.

<br/>

area는 면적이 되겠다. (w * h = 면적)

<br/>

어쨋든,

그래서 image_id 안에

이미지가 되게 여러개 들어가 있을 수 있고

이게 각각 흩어져있기 때문에 image_id 로 한번에 불러와서

로딩해서 알고리즘을 짜야된다. 그런 얘기다.

<br/>

나머지는 몰라도 짜는데 지장없다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122192390-9434b880-cece-11eb-9ede-d46cb5ab6775.png)

어쨋든... 그래서, 6만개 데이터를 위와 같은 JSON형식으로 만들어놓은 것이다. (왼쪽 부분)

근데 이것은 1차 관문이고

오른쪽과 같이 왼쪽에 있는 것을 이런식으로 수정해서 

하나의 답지에 있던 것들을 다 때려 뭉쳐서 하나의 Bbox를 각각 다 만들어놓는다. (맨 오른쪽 부분)

이게 2차 관문이다.

![image](https://user-images.githubusercontent.com/78403443/122192440-a0207a80-cece-11eb-9b81-43921d893c56.png)

2차 관문은 어떤 이미지안에 있던 물체인가를 다 이런식으로...

bbox를 txt파일에 한번에 명시해주는 것임 (우측)

이게 훨씬 간편하다. (1차 관문보다 간편하다)

![image](https://user-images.githubusercontent.com/78403443/122192480-a9114c00-cece-11eb-9273-1858fadb0c06.png)

289343이라는 제목의 jpg이미지 파일이 있다고 가정하면...

image 폴더 안에 289343.jpg 이렇게 들어갈 것이다.

그럼 labels 밑에는 289343.txt파일이 들어간다.

그리고 그 txt파일 안에 bbox정보...

bbox1 (473.07, 395.93, 38.65, 28.67, 18)

이런식으로 들어간다. 

만약에 bbox가 하나만 있으면 물체는 하나만 있구나~ 이렇게 이해하면 된다.

이 물체의 정답은 이런 것이다라고!

<br/>

이게 2차 관문이다.

<br/>

직접 보자...

![image](https://user-images.githubusercontent.com/78403443/122192685-da8a1780-cece-11eb-8178-adf17874254a.png)

train.jpg 원본 이미지

![image](https://user-images.githubusercontent.com/78403443/122192563-bcbcb280-cece-11eb-9550-5eeb9d25ad28.png)

답지를 확인하기 위해 labels/train.txt파일을 보자

![image](https://user-images.githubusercontent.com/78403443/122192748-e83f9d00-cece-11eb-9b88-e30d815c32e1.png)

train.jpg 이미지에 대한 물체들을 train.txt에 집어넣는다는 얘기인 것이다.

물체가 하나밖에 없기 때문에 boundary box도 하나밖에 없다.

<br/>

맨 앞은 카테고리정보이다. (PDF에서는 맨 뒤에 있었는데...)

아무튼, 0은 여기서 train을 뜻하는 것이다.

<br/>

txt 답지에 있는 x, y, w, h 토대로 계산을 해보니

![image](https://user-images.githubusercontent.com/78403443/122192834-f7bee600-cece-11eb-914a-5e9af0177961.png)

답지대로라면 이렇게 그려진다고 예측할 수 있다.

(정확한 답지가 맞다는 것을 알 수 있다)

<br/>

그리고 마지막... 3차 관문은 각각 잘 해석해서 그려낼 수 있어야한다.
