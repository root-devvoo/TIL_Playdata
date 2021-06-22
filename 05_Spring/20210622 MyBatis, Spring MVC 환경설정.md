## 2021.06.22 MyBatis 수업, Spring MVC 환경설정(IDE Tool 변경)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122887909-4b707a00-d37c-11eb-90e6-e094c86c2c53.png)

이걸 최종 버전으로 만든다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888067-7529a100-d37c-11eb-9c46-d8bd7af2fd37.png)

mapUnderscoreToCamelCase

굳이 ResultMap이나 AS 라는 alias를 안쓰더라도 이거 하나로 끝난다.

언더바 되있는걸 카멜케이스로 바꿔주는 옵션.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888171-8d012500-d37c-11eb-8818-d2adcd461bf5.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888212-968a8d00-d37c-11eb-8b00-4e72731ba4f5.png)

resultMap을 안쓰고 resultType으로 간다. 

(캡쳐 파일에는 없지만 resultMap도 지워줌)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888283-ab672080-d37c-11eb-8405-29adc12e91cf.png)

<br/>

Test파일 돌려보자

![image](https://user-images.githubusercontent.com/78403443/122888333-b752e280-d37c-11eb-90db-cdc1c75b5526.png)

잘 돌아간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888487-e0737300-d37c-11eb-860e-2a841276d843.png)

mapping.xml이 3개면, 위 이미지 표시한 부분 같은 식으로...

SqlMapConfig01.xml의 mapper도 3개로 늘어나고 typeAlias도 3개로 다 늘어난다.

각각 등록해야되기 때문에... 늘어난다

<br/>

그래서 vo들이 저장되있는 패키지 FQCN을 typeAlias 안에 package태그를 이용해 넣어준다.

![image](https://user-images.githubusercontent.com/78403443/122888567-f123e900-d37c-11eb-90c4-b61b6eb7173a.png)

이렇게 하면 20줄 넣어야 할 것도 한 줄만 치게된다.

vo가 저장된 패키지, user userName 앞글자만 소문자로 알아서 바꿔서 Alias로 지정해줌

<br/>

이렇게 바꿔서...

![image](https://user-images.githubusercontent.com/78403443/122888623-fc771480-d37c-11eb-9b4d-6ff56e2a3435.png)

테스트 돌렸더니 잘 나온다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888686-07ca4000-d37d-11eb-8df5-80c8a0425d5b.png)

SqlMapConfig.xml이 vo, ~mapping.xml, dbconn.properties 파일을 와이어링함

SqlSession까지 DI로 연결이 되고,

최종적으로 SqlSession이 DB에 insert, delete, update문을 통해 질의를 하고

DB가 selectOne() 함수나 selectList() 함수를 통해 응답한다.

그림의 가운데 부분이 MyBatis Framework부분이다.

<br/>

여기서 DAO를 재사용성을 높이며 연결하려면

① 인터페이스와 연결

② 실체 클래스(DAOImpl)의 객체 생성을 DI Container(Factory)에 맡긴다.

<br/>

지금부터 이걸 할 것이다.

Interface의 실체를 연결... DAO와 DAOImpl을 연결하고

SqlSession이 DAOImpl과 연결된다. (MyBatis Framework와 DAO 연결)

(DAOImpl이 SqlSession을 가진다, Hasing)

<br/>

DAO와 DAOImpl을 DI로 연결하는 Persistence Layer를 지금부터 구현해서

MyBatis Framework와 연결한다.

<br/>

102Test파일 배포

![image](https://user-images.githubusercontent.com/78403443/122888773-1dd80080-d37d-11eb-82d4-463db1490578.png)

그리고, 이제 DAO Interface를 만든다.

![image](https://user-images.githubusercontent.com/78403443/122888806-26c8d200-d37d-11eb-9dae-118819897c74.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888847-321bfd80-d37d-11eb-9f1e-62d9c294c34b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888892-3d6f2900-d37d-11eb-91bd-899c981e9b5d.png)

인터페이스 작성했다. (주석 잘 참고하기!)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122888928-49f38180-d37d-11eb-885d-781bdecffc02.png)

실체 클래스 파일(DAOImpl) 만든다.

![image](https://user-images.githubusercontent.com/78403443/122888973-54ae1680-d37d-11eb-8e5e-fd8bd87dbdad.png)

<br/>

DAOImpl이 MyBatis 프레임워크의 최상위 포식자 SqlSession을 가진다, Hasing

Hasing 코드는

1. 필드 선언
2. 생성자, setter로 주입

![image](https://user-images.githubusercontent.com/78403443/122889030-61326f00-d37d-11eb-8282-d03901be7a31.png)

잘 만들어졌는지 확인하려면

Test102 파일을 돌려본다.

![image](https://user-images.githubusercontent.com/78403443/122889056-6abbd700-d37d-11eb-92c3-373d99a48ef3.png)

결과 잘 출력되었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889102-760f0280-d37d-11eb-992c-bd1216d71ec9.png)

지금 DAOImpl에 addUser();가 있다. 

여기서 무슨일을 하느냐면 

Test에서 DAOImpl의 addUser();를 호출하면

얘가 SqlSession을 호출한다.

그러면 SqlSession에서 Insert가 동작을 해서 집어넣는다.

아까랑 뭐가 달라졌냐면 이제 DAOImpl에서 호출하는 것...

DAOImpl에서 removeUser();를 호출하면 SqlSession의 removeUser를 호출하게 되고

remove 시킴

나머지도 이런식...

<br/>

DAOImpl에서 SqlSession으로 가는게 호출 진행 방향이고, 이것은 서비스 흐름 방향이랑 같다.

반면에 SqlSession에서 DAO쪽으로 진행되는 방향은 주입 방향이고, 개발 방향이다

(우리는 개발을 이 순서로 해야한다)

<br/>

그래서

① MyBatis를 먼저 개발하고 (개발 + 단위테스트)

② Persistence Layer(여기서는 102.java)를 개발해야한다.

<br/>

MyBatis에서 단위테스트가 잘 돌아갔다는건

나중에 에러나 나도 MyBatis 부분은 확인할 필요가 없다. (그래서 단위테스트가 중요함)

나중에 Persistence Layer을 연결하면서 에러가 발생해도 Persistence Layer 부분만 잘 확인하면 된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889199-8b842c80-d37d-11eb-835e-9158aaac0a25.png)

개발은 위 그림 ①, ②, ③ 순서로 하는 것이다. (중요!!! ★)

① DB Tier, Resource

② MyBatis Framework

③ Persistence Layer

이 순서로! (용어 정리도 확실하게 해둘 것)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889259-98088500-d37d-11eb-9e01-e20ced06559b.png)

이 외에 Spring에서 Layer가 하나 더 있다.

Service Layer가 바로 그것이다. 

Persistence Layer와의 차이점을 지금 간단하게 언급하고, 나중에 Spring MVC에서 직접 다뤄본다.

<br/>

예를 들어, 참치를 구해야 하는데

직접 대서양을 가서 싱싱한 생 참치를 구해오는게 Persistence Layer이다.

구해온 생 참치를 가공해서 통조림으로 만들어서 소비자들에게 제공하는것이

Service Layer이다.

<br/>

바로 데이터를 가공했느냐 안했냐의 차이이다.

Service Layer :: Data 가공한 레이어

Persistence Layer :: 생생한 데이터를 다룸

<br/>

게시판의 page라는건 뭐냐면 원본 DB 테이블에는 없는 것

row한(생생한) 데이터를 가공해서 페이지로 나눈 것임

<br/>

그래서, Service Layer에서 할 수 있는 알고리즘이 페이징 알고리즘

<br/>

Spring Framework를 쓰면 데이터 가공을 하든 안하든 무조건 Service Layer를

사용해야 한다. (서비스 제공시에는 어떻게 하든 무조건 가공이 필수적이기 때문)

<br/>

 Service Layer에 컴포넌트 기반의 Service, DAOServiceImpl이 있고

이것을 Persistence Layer의 DAO와 DI로 연결하고

Service Layer의 단위테스트는 ~103(11).java로 한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889364-b2426300-d37d-11eb-86ba-0139c7e485e6.png)

이렇게 파일을 새로 배포했다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889406-bcfcf800-d37d-11eb-9eb8-71500df18e03.png)

UserService 인터페이스를 만들었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889468-c9815080-d37d-11eb-9afb-b6a480f95ce6.png)

UserServiceImpl11 만들었다.

<br/>

단위테스트

![image](https://user-images.githubusercontent.com/78403443/122889518-d43be580-d37d-11eb-8a0a-28ffcaea7a25.png)

잘 돌아갔다.

<br/>

12 배포

다음으로 간다.

![image](https://user-images.githubusercontent.com/78403443/122889588-e158d480-d37d-11eb-8800-062784514473.png)

<br/>

MyBatisTestApp11.java파일을 보면

![image](https://user-images.githubusercontent.com/78403443/122889654-f03f8700-d37d-11eb-8352-709d01014e08.png)

이 코드에서 new가 보인다는 얘기는

MyBatis 프레임워크는 잘 썼는데,

이거랑 DI Container랑 연결이 안된 것이다

<br/>

이제 12에서 DI Container를 연결해볼 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889737-02212a00-d37e-11eb-958f-166c54cc16a7.png)

이렇게 만들고 DI 연결한다.

<br/>

빈 설정문서 배포

![image](https://user-images.githubusercontent.com/78403443/122889790-11a07300-d37e-11eb-9164-96e665df721b.png)

완료

![image](https://user-images.githubusercontent.com/78403443/122889865-22e97f80-d37e-11eb-8e1f-53d8a58d20bf.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122889898-2d0b7e00-d37e-11eb-8b25-a200951a1736.png)

MyBatis Framework에서 제공되는 라이브러리

- SqlSession
- SqlSessionFactory
- SqlSessionFactoryBuild

Persistence Layer 컴포넌트

- UserDAOImpl12

Service Layer 컴포넌트

- UserServiceImpl12

<br/>

위 그림과 같이 연결해야되는데

이걸 빈 설정문서에다가 전부 다 작성해 넣어야한다.

<br/>

userservice12.xml파일 작성

![image](https://user-images.githubusercontent.com/78403443/122890013-457b9880-d37e-11eb-8c28-183f43f674ab.png)

작성했다. (메모 :: 주석 잘 보기)

![image](https://user-images.githubusercontent.com/78403443/122890065-50cec400-d37e-11eb-93b2-777d230d8033.png)

에러 발생...

<br/>

지금부터 라이브러리 추가하는게 얼마나 골치아픈지 말한다.

기술이 올라가면 버전 문제 발생

라이브러리 추가 문제...

이런걸 해결하는게 중요하다. 

같이 해결 해본다.

<br/>

ClassNotFound에러가 뜨면 파일이 없어서 찾을 수 없다는 것이므로 해당 라이브러리를 추가한다.

(되게 어렵다... 하나 추가 하면 또 다른 에러 나오고, 꼬리에 꼬리를 물듯이 나온다, 현업에서는 이거의 10배 힘들다고 한다. 직접해야된다.)

![image](https://user-images.githubusercontent.com/78403443/122890154-65ab5780-d37e-11eb-8613-75229130561b.png)

일일히 찾아서 이렇게 WebContent/WEB-INF/lib폴더에 넣어주었다

![image](https://user-images.githubusercontent.com/78403443/122890208-6fcd5600-d37e-11eb-88e0-e06e0ac60f57.png)

DB를 연결하려면 spring jdbc를 안쓰더라도 이 두개가 반드시 필요하다

<br/>

마지막...

MyBatisUserDAOImpl12.java파일로 간다

![image](https://user-images.githubusercontent.com/78403443/122890263-7e1b7200-d37e-11eb-8b32-bf8123657cb1.png)

MyBatis만 돌릴 때는 DML → commit()을 반드시 해야한다.

근데, Spring MyBatis 라이브러리에서는 commit이 이미 포함(내장)되어있다.

그래서 명시적으로 commit()을 하면 에러가 나게 되어있다.

그래서 commit빼야한다. 

다 위와같이 주석처리한다.

<br/>

테스트

![image](https://user-images.githubusercontent.com/78403443/122890356-8e335180-d37e-11eb-823f-80523dee70fa.png)

돌려보니 잘 돌아간 것을 확인했다!

<br/>

그림 설명

![image](https://user-images.githubusercontent.com/78403443/122890434-a30fe500-d37e-11eb-94ed-ca165d8b6211.png)

DI Container(Test12파일 보면 Application Context되있음) == 공장

userservice12.xml(빈 설정문서) == 주문서

읽어서 빈을 생성

Bean(빈)은 크게 두 종류 :: API 빈, 사용자정의 빈

<br/>

여기서 제일 먼저 만드는 빈이 DataSource 빈

dbconn.properties이 갖고있는 정보를 가지고 SqlSessionFactoryBean이 만들어진다.

SqlMapConfig가 SqlSessionFactoryBean 와이어링

SqlSessionFactoryBean이 DI생성자로 주입, SqlSession이 가져간다.

SqlSession이 DML문으로 질의, 그리고 selectOne 이나 selectList로 응답받는다.

여기까지 MyBatisFramework(101.java로 만들었다.)

<br/>

그리고, 여기에 UserDAO 인터페이스... UserDAOImpl implements --- Persistence Layer

그리고, UserService 인터페이스... UserServiceImpl -- Service Layer이다.

그리고, 그 다음 Presentation Layer가 나오고

거기서 (내일 진행될 듯한데) Spring MVC가 나온다. 

지금은 라이브러리들을 Build Path로 일일히 잡아주고 있지만

그렇게 하지 않고, Maven기반으로 Update될 것이다.

(조금있다가 Maven기반으로 들어갈 것이다는 얘기)

<br/>

MyBatis Framework에서는 단위테스트를 반드시 해야한다.

MyBatis Framework의 최상위 포식자인 SqlSession이 DI로 UserDAOImpl에 주입하고

거기서 UserServiceImpl로 DI 통해서 주입

그 다음에 또 거기서 Prestentation Layer로 주입한다.

<br/>

우리가 여기까지 다 만들었는데..

총 5개의 Bean이 Bean설정문서에 지정되어있다.

(userservice12.xml 파일을 보면 알 수 있다)

API 빈 : 3개

사용자정의 빈 : 2개

<br/>

이제부터는 이것을 Annotation기반으로 바꿔서 사용할 것이다.

<br/>

Annotation은 xml기반을(xml기반의 빈 설정문서를) 이해하면, 그냥 거기서 바꿔서 사용하기만 하면 된다.

빈 설정 문서를 이해하는게 가장 중요하다는 얘기

<br/>

태그와 오타를 줄이고자 만든 것이 바로 Annotation

바로 만들어보도록 한다.

<br/>

모든 파일의 sorting 번호가 13... 마지막이다.

![image](https://user-images.githubusercontent.com/78403443/122890591-c9ce1b80-d37e-11eb-94ec-f9d0582996c0.png)

![image](https://user-images.githubusercontent.com/78403443/122890619-d05c9300-d37e-11eb-9def-10f02c5ba5f7.png)

이렇게 파일을 배치(배포)했다.

<br/>

Annotation은 빈 설정문서에서 빈 생성 부분을 줄이는 기술이다.

빈 생성을 줄인다는 얘기는

<bean> 태그가 많으면 오류가 생기니까 이걸 줄이겠다는 얘기임

xml에서 빈 태그는 줄이고 Code에서 Marking한다.

이것이 Annotation

<br/>

![image](https://user-images.githubusercontent.com/78403443/122890691-e0747280-d37e-11eb-8da2-4b1de6a2afed.png)

이렇게 하게되면

![image](https://user-images.githubusercontent.com/78403443/122890740-ebc79e00-d37e-11eb-885e-37b0a80bc8c4.png)

이 부분을 날릴 수 있다.

<br/>

그리고

![image](https://user-images.githubusercontent.com/78403443/122890799-f97d2380-d37e-11eb-8f28-6d7cb7503644.png)

이렇게 하게 되면

![image](https://user-images.githubusercontent.com/78403443/122890835-03068b80-d37f-11eb-9410-c984604f9860.png)

5번도 날릴 수 있다.

<br/>

Annotation했다는 얘기는 공장이... 컨테이너가

다시말해서 ApplicationContext가 원래는 빈 설정문서(주문서)를 보고

빈 객체를 만드는데, Annotation하게되면 코드를 일일히 훓어서

빈을 생성하는 수고로움을 해준다. (우리는 편할지 모르겠지만)

그래서 어디를 훓으라는 표식을 반드시 해야한다.

그 표식을 맨 마지막에 해주는데

![image](https://user-images.githubusercontent.com/78403443/122890922-131e6b00-d37f-11eb-83f2-70addf0bf101.png)

이렇게

<br/>

단위테스트를 해보자

![image](https://user-images.githubusercontent.com/78403443/122891003-23cee100-d37f-11eb-9c36-9e09885aa8f6.png)

돌려보니 잘 출력되었다.

여기까지 MyBatis부분... 끝

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891078-31846680-d37f-11eb-975d-c1f44836bf97.png)

각각 독자적인 라이브러리인데

DI에 6개 라이브러리 추가

MyBatis에 2개 라이브러리 추가해서

DI와 MyBatis를연동하는데 또 6개의 라이브러리를 추가했다.

이때는 라이브러리들끼리 충돌도 많이 발생하고, 버전도 맞아야되고.. 일일히 찾아야하고... 여러가지로 어려웠다.

강사님께서 다 버전이랑 잘 맞춰서 아예 제공해서 주셨기 때문에 다소 편하게 했지만

현업가면 본인이 다 일일히 찾아서 알아서 해야한다.

<br/>

---

---

**Maven을 위한 설정**

<br/>

지금까지는 필요한 라이브러리들을 직접 추가했다.

이게 현업에서는 더 스케일이 커진다.

그래서 일일히 추가하다보면 작업의 속도가 느려진다.

그래서, 라이브러리가 자동으로 추가되고 조금 더 손쉬운 방법으로

추가될 수 있는 구조가 Maven 플랫폼 구조로 가면 된다.

Maven을 구조로 갈 수 있는 방법은 여러가진데, 제일 Common한 방법으로 간다.

![image](https://user-images.githubusercontent.com/78403443/122891214-4eb93500-d37f-11eb-8947-ff5463cd9679.png)

![image](https://user-images.githubusercontent.com/78403443/122891249-5678d980-d37f-11eb-82bf-70a067a78ca3.png)

![image](https://user-images.githubusercontent.com/78403443/122891290-5ed11480-d37f-11eb-9974-2f5d1d89fe39.png)

STS.exe 파일 실행하면서 엔터프라이즈 급 IDE 툴이 실행될 것이다.

![image](https://user-images.githubusercontent.com/78403443/122891361-6d1f3080-d37f-11eb-8926-28de4176633d.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891459-7f996a00-d37f-11eb-9bf6-b0d89ce23dd2.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891505-89bb6880-d37f-11eb-8bc3-2de98d205fb2.png)

오른쪽 하단에 게이지는 

우리가 Spring Framework쓰는데 필요한 라이브러리들을

c:/user/.m2라는 폴더에 다운을 받는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891569-95a72a80-d37f-11eb-9220-3f2220830485.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891630-9fc92900-d37f-11eb-9f80-5fd7445a6a6e.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891674-a9529100-d37f-11eb-9de4-49d3b0b93e6e.png)

com.encore.spring 이런식으로 넣어야지만 Finish 할 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891723-b4a5bc80-d37f-11eb-8018-ce6be292abdd.png)

src의 다각화...

라이브러리 JavaSE-1.6은 신경안써도됨

Maven Dependencies에 우리가 써야 할 라이브러리들이 다 들어있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891786-c0917e80-d37f-11eb-8679-415e126e2da9.png)

라이브러리 사용 설정 문서

<br/>

![image](https://user-images.githubusercontent.com/78403443/122891830-cbe4aa00-d37f-11eb-9afa-b78c97a97986.png)

맨 처음에는 라이브러리들을 원격에서 받아오기 때문에 오래걸리지만

두번째부턴 로컬에 이미 받아져있는 라이브러리를 사용하기 때문에

(라이브러리 설치되면서 배치된, 라이브러리 사용 설정 문서인 poem.xml 파일 통해서)

빨리 동작이 되는 것이다.
