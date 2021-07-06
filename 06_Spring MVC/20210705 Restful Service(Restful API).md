**Restful Service(Restful API)**

![image](https://user-images.githubusercontent.com/78403443/124435127-a019e900-ddaf-11eb-86db-daf82aeed232.png)

WAS(Service 하는 대상들이 존재하는 메모리적인 환경)

디바이스가 다르다는 얘기는 화면이 나오는 것도 다르다.

웹을 제외한 다른 Android나 iOS 디바이스에는 맞는 구조가 아니다.

그래서, 이걸 바꾸는 기술이 Restful API이다.

<br/>

그럼 어떻게 바뀌어지는지?

![image](https://user-images.githubusercontent.com/78403443/124435169-ac05ab00-ddaf-11eb-8887-045af7ab90a9.png)

일단 우리가 배웠던 WAS는 그대로 돌아간다.

여기에 자원들이 존재하는데, 어떤 자원만 있냐면 Controller, Model

<br/>

컴포넌트가 수행된 결과 Data만 반환

결과 페이지는 반환 안한다, 이게 핵심...

요청하면 JSON 데이터 반환.. Ajax가 중요하게 쓰이는 부분...

화면은 자기들한테 맞는 view 알아서 쓰면 된다.

<br/>

그래서, Service 요청이 일어나는 Client의 디바이스가 점차 다양해짐에 따라서

화면 관련 자원을 WAS안에서 생성하고 저장해서 그 서비스를 응답하는 방식보다도

데이터 자체만 응답 함으로서 view자원은 각각의 디바이스에서 담당하게 됨

<br/>

이게 가능하려면 Server Side 기술과 Client Side 기술의 완벽한 분리가 일어나야한다.

이걸 가능케 해주는게 Restful Service!

![Client_Platform](https://user-images.githubusercontent.com/78403443/124435336-db1c1c80-ddaf-11eb-88b2-8867953fef53.jpg)

우리가 쓰던건 그대로 쓰고... 

리턴 타입만 없는 것이다. (ModelAndView String 이렇게 안한다)

Data만 리턴

<br/>

원래 정식명칭은 Restful Service

![image](https://user-images.githubusercontent.com/78403443/124435393-e8d1a200-ddaf-11eb-8483-e918d941579b.png)

doGet 은 SELECT 요청

doPost 는 INSERT

doPut 은 UPDATE

doDelete는 DELETE

반드시 외우기

<br/>

Spring MVC 동작 그림

![image](https://user-images.githubusercontent.com/78403443/124435468-fe46cc00-ddaf-11eb-9b4b-2cb5b23b747c.png)

Spring MVC는 최종적인 결과가 VIEW다

Restful은 VIEW가 없어지고, DB에서 받아오는 데이터만 준다.

이게 Restful..

데이터가 파편적인 쪼가리로 왔다갔다하는게 아니라 객체로 반환 (JSON형식으로)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124435519-0a328e00-ddb0-11eb-8b4d-a0b048379ce2.png)

REST는

REpresentational State Transfer의 약자

"하나의 URI는 하나의 고유한 리소스(Resource)를 대표한다" 는 의미

<br/>

- **sp13_SpringRestfulAPI 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/124435883-672e4400-ddb0-11eb-8b30-cfc69697bb75.png)

Restful Service 쓰려면 버전을 높은 것을 써야하기 때문에 이렇게 셋팅해줬다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124436012-85943f80-ddb0-11eb-9d85-6de0fd055d5c.png)

나머지 뒷단은 했다고 가정하고(생략) Controller부분만 해서 Restful Service를 만들어본다.

![image](https://user-images.githubusercontent.com/78403443/124436062-93e25b80-ddb0-11eb-9417-488d0f852dda.png)

그동안에는 컨트롤러에는 Controller를 어노테이션했지만, 이제는 RestController로 어노테이션한다. 

차이점은 주석내용 확인

다 작성하면 실행은 Controller에서 실행한다(view가 없기 때문)

![image](https://user-images.githubusercontent.com/78403443/124436101-9cd32d00-ddb0-11eb-8fb6-225bbba43a68.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124436132-a65c9500-ddb0-11eb-800f-8d4dd37fe850.png)

500 오류는 서버에 책임... 로직이 잘못됐다는 얘기

Restful 서비스는 데이터를 리턴한다. 데이터는 객체... JSON형태로 리턴한다.

그러면 객체를 JSON으로 리턴해야하는데, 그게 Converting이 안된다는 얘기임

라이브러리를 추가해야한다...

![image](https://user-images.githubusercontent.com/78403443/124436170-afe5fd00-ddb0-11eb-8d09-b647aa6c6706.png)

추가하고 다시 요청보냈더니

![image](https://user-images.githubusercontent.com/78403443/124436223-b83e3800-ddb0-11eb-8ad9-82e6f76c8cb9.png)

JSON형식.. Key, value 한쌍으로 잘 나왔다.

Restful Service는 JSON형식으로 데이터 객체가 리턴된다. 꼭 알아야함

<br/>

객체를 여러개로 리턴... 리스트로 묶여진 경우

![image](https://user-images.githubusercontent.com/78403443/124436292-c55b2700-ddb0-11eb-9d19-181fb152c52b.png)

![image](https://user-images.githubusercontent.com/78403443/124436316-cc823500-ddb0-11eb-8252-1b2f586726fd.png)

어떻게 주소가 매겨지는지도 확인...

<br/>

Map으로 리턴되는 경우

![image](https://user-images.githubusercontent.com/78403443/124436494-fb98a680-ddb0-11eb-9180-412b4da07164.png)

이렇게 리턴된다. 파이썬의 딕셔너리를 생각...

<br/>

여러개의 Map으로 리턴되는 경우

![image](https://user-images.githubusercontent.com/78403443/124436536-07846880-ddb1-11eb-86f9-ef4388e87dd7.png)

Restful 요청 형태는 위와 같이(http://127.0.0.1:8888/rest/simple/mapCustom) "/" 이런식으로 가기 때문에

web.xml에서도 "/" 이렇게 해줘야한다.

<br/>

다시 객체를 만들어서 컨트롤러 돌려본다.

![image](https://user-images.githubusercontent.com/78403443/124436591-13702a80-ddb1-11eb-9977-0145680f5493.png)

잘 나왔다.

<br/>

주소창에 파라미터를 포함시키는 방법 (중요한 문법임)

![image](https://user-images.githubusercontent.com/78403443/124436625-1e2abf80-ddb1-11eb-8d63-0c0a64dd862c.png)

입력한 num이 PathVariable로...

객체랑 상관없이 단순한 파라미터 값을 받는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124436660-2a168180-ddb1-11eb-9879-4da2b43ec233.png)

새로고침 할 때마다 id 숫자도 증가

<br/>

RequestMapping에서 get방식으로 할 때 반드시 알아야하는 중요한 것...

![image](https://user-images.githubusercontent.com/78403443/124436697-36024380-ddb1-11eb-9eed-010a87047aed.png)

![image](https://user-images.githubusercontent.com/78403443/124436725-3dc1e800-ddb1-11eb-8962-6e2d1b2ff50f.png)

<br/>

이제 Step 2로 넘어간다.

<br/>

---

- **sp14_Restful_BookTest 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/124436844-60ec9780-ddb1-11eb-9ee2-0d823a669856.png)

DB테이블을 이렇게 셋팅하고,<br>전에 BookTest에서 했던 것에서 컨트롤러만 Restful로 적용해본다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124436902-719d0d80-ddb1-11eb-84ef-2f8643200ae7.png)

![image](https://user-images.githubusercontent.com/78403443/124436925-78c41b80-ddb1-11eb-9ed5-0494b4a51b83.png)

하나의 URI는 하나의 고유한 리소스(Resource)를 대표한다.

http://127.0.0.1:8888/rest/api/book으로 요청하면 books를 리턴하는 것임

![image](https://user-images.githubusercontent.com/78403443/124436986-8a0d2800-ddb1-11eb-85d7-1a21dfd00172.png)

![image](https://user-images.githubusercontent.com/78403443/124437011-91cccc80-ddb1-11eb-8e01-88353cc7417e.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124437179-c50f5b80-ddb1-11eb-97e8-2dcc8297c809.png)

지금까지 get만 돌렸고

insert, delete, update 쫙 해본다.

<br/>

Service, DAO에서 void 리턴 타입으로 되어있는 것을 boolean으로 바꿈...

DML은 SqlSession은 int...

따라서 DAO에서 int로 쓰던지 boolean으로 바꾸고 ==1 ? true : false(삼항 연산자) 넣어준다.

Restful에선 이렇게 많이 한다... (BookDAOImpl 코드 참고)

<br/>

주소를 쳐서는 데이터를 읽어오는 것 밖에 확인이 안된다.

화면이 없기 때문에 Restful Client Tool을 사용해서 insert, delete, update가 잘 수행되었는지 확인할 수 있다.

Postman 설치방법... https://meetup.toast.com/posts/107, https://kibua20.tistory.com/149 확인

<br/>

![image](https://user-images.githubusercontent.com/78403443/124437264-dc4e4900-ddb1-11eb-9a89-97f481603c5c.png)

(Seweager는 나중에 자세히 본다)<br>① 노란색 글씨는 서버 개발자가 개발시 필요한 부분을 말하는 것<br>② Seweager는 클라이언트 개발자한테 필요

<br/>

![image](https://user-images.githubusercontent.com/78403443/124437413-0142bc00-ddb2-11eb-91d6-ef7f329bf91e.png)

![image](https://user-images.githubusercontent.com/78403443/124437502-17507c80-ddb2-11eb-8899-38c5c7c4ad40.png)

이렇게 잘 만들어졌는지 안만들어졌는지 확인... <br>200과 OK가 확인되면 잘 된다는 것

<br/>

아까 작성했던 INSERT문 정상동작 확인해본다.

![image](https://user-images.githubusercontent.com/78403443/124437558-27685c00-ddb2-11eb-994a-404312036e35.png)

POST는 객체를 body로 보낸다. 

JSON으로 Convert 되어지기 때문에 JSON 선택한다.

![image](https://user-images.githubusercontent.com/78403443/124437727-4ff05600-ddb2-11eb-94f1-08bcd832bdad.png)

INSERT 했다. 

확인 (확인방법 :: GET으로 Send해서 확인하는 것임)

![image](https://user-images.githubusercontent.com/78403443/124437836-71514200-ddb2-11eb-9a99-58d77abf40c6.png)

<br/>

UPDATE문 Controller에서 작성하고나서, PUT으로 UPDATE 요청 Send한 후 <br>GET으로 확인함 (아래)

![image](https://user-images.githubusercontent.com/78403443/124437882-7dd59a80-ddb2-11eb-8b5c-86294f3c688c.png)

<br/>

DELETE 요청 Send

![image](https://user-images.githubusercontent.com/78403443/124437934-8af28980-ddb2-11eb-9ab1-145e480ed734.png)

확인

![image](https://user-images.githubusercontent.com/78403443/124438118-c2f9cc80-ddb2-11eb-9238-53996dca32ed.png)

삭제가 되어서 안보인다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124438160-cf7e2500-ddb2-11eb-821f-251b40efa573.png)

처음부터 끝까지 book인데 CRUD가 문제없이 돌아가는 것은<br>각각 다른 Mapping이기 때문이다.

<br/>

---

- **sp15_Restful_PhoneTest 프로젝트 보기 (오늘 한 내용 정리 코드)**

주문서를 보고 그것을 토대로 파일을 찾고 만들기 때문에<br>web.xml 맨 처음에 잘 확인해야한다.

![image](https://user-images.githubusercontent.com/78403443/124438383-12d89380-ddb3-11eb-8022-fe7571d111dc.png)

Restful Service에서는 "/" 를 기준으로 요청을 찾아나가기 때문에 전과 다르게 "/"로 바꿔준다. 

<br/>

**수업 때 다룬 코드 리딩하면서 잘 살펴보기!!!**
