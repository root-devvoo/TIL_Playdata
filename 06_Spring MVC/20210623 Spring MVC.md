## 2021.06.23 Spring MVC

**Spring MVC, Maven기반**

<br/>

Maven기반의 핵심은 프로젝트를 만드는 순간 직접 원격지에 있는 라이브러리를

끌어당겨서 내 머신 로컬에 저장한다.

로컬에 저장되는 위치가 .m2

![image](https://user-images.githubusercontent.com/78403443/123062378-6b20a480-d447-11eb-9614-4e0a1389c160.png)

어떻게 알았냐라고 할 수 있냐면

내가 Build path를 잡지도 않았는데 Maven Dependences가 있다.

Dependences는 의존, Hasing의 뜻 

필요한 라이브러리를 원격지에서 직접 받아서 Build Path 잡아버린다

![image](https://user-images.githubusercontent.com/78403443/123062417-75db3980-d447-11eb-92fd-3fa381b8dd37.png)

프로젝트를 만드는 순간 Dependencies 잡아버린다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123062457-82f82880-d447-11eb-94ce-8a901567af25.png)

위 밑줄이 우리 머신 로컬의 경로가 되겠다.

불러오도록 시킨게 아닌데 이것들을 어떻게 알고, 뭘 보고 이렇게 불러왔을까?

pom.xml파일!

![image](https://user-images.githubusercontent.com/78403443/123062498-8be8fa00-d447-11eb-8ec6-44ad9dbc0640.png)

pom.xml파일을 보면

![image](https://user-images.githubusercontent.com/78403443/123062536-94d9cb80-d447-11eb-98ac-b577befba70d.png)

프로젝트 파일 만들때 경로를 필수로 3번 나누도록 되어있었다.

앞은 pom.xml의 GroupId가 되는 것이고, 뒤는 ArtifactId... 이게 Context path가 된다.

그래서 주소의 맨 마지막 경로가 spring이 되는 것이다.

<br/>

그리고 아래 내려보면

![image](https://user-images.githubusercontent.com/78403443/123062595-a1f6ba80-d447-11eb-9588-0ca75be6f049.png)

![image](https://user-images.githubusercontent.com/78403443/123062614-a7ec9b80-d447-11eb-861a-35b483a43dc0.png)

dependencies의

dependency 태그 하나가 라이브러리인 .jar파일이 된다.

![image](https://user-images.githubusercontent.com/78403443/123062648-b0dd6d00-d447-11eb-9a94-c8b9ecf7ebc3.png)

결론 :: pom.xml에는 dependency 들이 여러개 있는데

이 dependency 하나가 라이브러리 하나다

그리고 그걸 local의 .m2폴더에 저장하는 것이다.

<br/>

build path잡아보지 않은 사람이면 모른다. 

잡아봐야지 아는 것... 이런 자동화가 편리성도 있지만

많은 바보들을 대량생산한다는 것에 치명적이라는 얘기이다.

뭐든지 그냥 그렇구나 하고 넘어가는 것이 아니라

왜, 어떻게? 그리고 전체적인 구조 이런 것을 계속적으로 고민해야한다.

<br/>

①

기업에서는 생산성을 높이는데 눈이 빨갛게 되어있다.

그래서 이런 프레임구조를 사용할 수 밖에 없다. 

이것을 통제하는 사람은 소수면 된다. 다수는 반복적인 작업을 할 수 밖에 없다.

그래서 시장 진입하는 문이 넓다고 해서 결코 좋다는 것이 아니다.

<br/>

②

4차 산업시대에서는 문과생이 굉장히 기술에 Jumping up을 하고 있다.

두드러지게 이런 현상이 나타나는 시대가 4차 산업혁명시대이다.

<br/>

Maven 구조로 바로 안들어오고 우리가 과정을 거쳐서 온 이유가 있다.

Maven 구조

![image](https://user-images.githubusercontent.com/78403443/123062783-ce123b80-d447-11eb-8432-41bd3050807c.png)

1. src의 다각화 (단위테스트)

2. 라이브러리

   - 프레임워크라는 얘기는 이미 누군가가 만들어놓은 것을 갖다 쓴다는 얘기다
   - 근데 이게 되게 많다... 방대, 서로 Wiring 되어져있다... 개발자가 일일히 넣기에는 상당히 힘들다
   - 그래서 이걸 자동화시킨 것이다. 
   - 여기서, pom.xml, Remote되어서 local에 저장되서 자동으로 Build Path를 잡아버린다는 것을 알아야 한다.

그래서 이렇게 아는 과정을 거쳐서 지금에서야 Spring MVC로 오게 된 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123062835-da969400-d447-11eb-958f-06998c6dc6d7.png)

Core Container와 Data Access 부분은 다 했고

Web부분만 Spring MVC로 독자적으로 한다. 

이걸 이해하면 Core Container와 Data Access 부분까지 전체를 연결할 수 있다.

<br/>

시작한다.

![image](https://user-images.githubusercontent.com/78403443/123062918-e84c1980-d447-11eb-95e5-b255ae0a2fbc.png)

자바코드는 Java Resources 클릭

web은 전에 건들지 말라고 했던 src 폴더를 봐야한다.

src/webapp을 건드려야한다.

거기에 web.xml 있다. 

web.xml을 무슨 문서라고 했었냐면 D.D파일이라고 한다. Deploy Descriptor

D.D파일에서 ServeletContext만들어놓고, Servlet 만들고, ServletConfig(initparam)

ServeletContext가 Global한(광범위한) 초기화 담당

ServletConfig 하나의 서블릿에서만 초기화 담당

<br/>

결론은

web.xml 보면

![image](https://user-images.githubusercontent.com/78403443/123062982-f7cb6280-d447-11eb-9509-32d52f0f46ff.png)

두 파일이 다 존재...

<br/>

처음에 DD파일을 읽어옴, 이 DD파일이 web.xml

```
그리고 ServletContext만들어짐... <context-param> 태그
그다음 서블릿 객체... <servlet> 태그
```

<br/>

그리고 servlet-context.xml과 root-context.xml을 web.xml이 와이어링한다.

![image](https://user-images.githubusercontent.com/78403443/123063244-319c6900-d448-11eb-8c5c-5cbc600387f5.png)

이게 하나가 되어 유기적으로 돌아간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123063302-3bbe6780-d448-11eb-9ddf-5f47cf2b2059.png)

표시한건 어제 빈 설정문서에서 봤던 bean태그

<br/>

![image](https://user-images.githubusercontent.com/78403443/123063339-47119300-d448-11eb-92e8-0418a8865dbb.png)

WAS(Tomcat)에서 가동... web.xml

그리고 web.xml에서 여러가지가 와이어링 될 수 있는데(a.xml, b.xml, c.xml)

이것들이 빈 설정문서이고,

이것들이 DI Container에 의해서 돌아간다.

<br/>

가장 크게 보면 WAS에 DI Container가 올라가 있는 것이다.

WAS에서는 web.xml에서 정의되어있는 것들 생성되고

DI Cointainer에서는 a.xml, b.xml, c.xml을 생성한다.

<br/>

이런 것들이 모듈화되고 각각 읽어들이는 파일이 다르다는 것을 알아야한다.

<br/>

결론은, 그래서 모든 것들의 시발점은 web.xml에서 시작된다는 것이다.

![image](https://user-images.githubusercontent.com/78403443/123063407-5690dc00-d448-11eb-900d-1e2be5314cd0.png)

클라이언트로부터 요청을 받으면 appServlet이 받는다.

요청이 들어오면 17번줄~26번줄에서 DispatcherServlet이 받고, 

얘가 받은 요청을 HandlerMapping한테 줬고

HandlerMapping이 요청에 해당되는 컴포넌트를 만들고 그게 리턴된다.

<br/>

그러면 만들어본다.

<br/>

컴포넌트 만드는거니까 class파일 만든다.

![image](https://user-images.githubusercontent.com/78403443/123063464-64def800-d448-11eb-8e01-d94a46e0ef52.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123063507-6f998d00-d448-11eb-9f47-b71d12662288.png)

우리가 이렇게 베이스 패키지를 주면 자동으로 다 들어간다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123063542-7a542200-d448-11eb-8e99-5dd52b5318cc.png)

result만 넣어도

![image](https://user-images.githubusercontent.com/78403443/123063572-8344f380-d448-11eb-9c9a-85e82a6b2363.png)

여기서 알아서 돌아감

<br/>

![image](https://user-images.githubusercontent.com/78403443/123063641-90fa7900-d448-11eb-9544-6fdfc5eaa14f.png)

이것이 context path == spring

![image](https://user-images.githubusercontent.com/78403443/123063806-b091a180-d448-11eb-9942-b64387aac9a0.png)

요기

![image](https://user-images.githubusercontent.com/78403443/123067824-4aa71900-d44c-11eb-89a9-4375a4714792.png)

이렇게 돌아가는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123067874-57c40800-d44c-11eb-9453-89899840c381.png)

아까 우리가 IndexController.java(클래스)파일에서

바인딩 해준 message를 result.jsp에서 EL로 받아왔다.

<br/>

돌리면

![image](https://user-images.githubusercontent.com/78403443/123067931-65798d80-d44c-11eb-80b2-808e74a048d9.png)

이렇게 결과 나왔다.

<br/>

구조 파악 (그림)

![image](https://user-images.githubusercontent.com/78403443/123067979-6f9b8c00-d44c-11eb-8ed6-16d71b6ad56b.png)

지금 짰던게 어떤 원리인건지 그림으로 이해한다.

- WAS가 가동하면 모든 것의 시작점인 web.xml의 D.D파일을 가동한다
- 그리고 이 환경에 WAS가 ServletContext를 생성한다
- 서블릿을 생성하는데 이름이 Dispatchcer Servlet이다... 라이브러리
- (빨간색은 다 라이브러리임)
- ① ServletContext를 생성하고 Dispatcher Servlet을 생성하는 그 사이에 root-context.xml을 와이어링함(root-context.xml 없으면 에러남)
- ② 그리고, Dispatcher Servlet을 생성하고 servlet-context.xml을 찾아서 와이어링한다.
- 여기까지가 WAS에서 하는 일이다.
- ③ 요청, 응답 작업 진행

<br/>

있는 것 그대로 사용해서 간단하게 만들어봤다.

<br/>

**sp02_SpringMVC 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123068047-80e49880-d44c-11eb-8785-ecac9348b6d9.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123068081-89d56a00-d44c-11eb-8b61-b5511cf2d27c.png)

우린 이 전체를 컨트롤러 컴포넌트라고 하고

실체적인 컴포넌트는 MainController가 된다.

인터페이스 기반으로 작성된 자바 클래스는 컴포넌트... 컴포넌트와 Bean은 같은 말

Bean은 실체클래스

<br/>

WAS도 컨테이너고 DI Container도 컨테이너

그러나 다른 종류의 컨테이너 (서로 다른 객체를 만들기 때문에 다름)

하지만 둘다 객체를 생성하는 IOC이다.

<br/>

WAS 객체생성

이쪽의 주문서는 web.xml(D.D파일)

<br/>

DI Container 객체생성

이쪽의 주문서는 Servlet-context.xml파일

<br/>

주문서 동은 WAS가 가동되면서 web.xml이 먼저고

그리고 이게 와이어링되서

Servelet-context.xml파일이 만들어진다.

<br/>

서로 다른 객체를 만들기 때문에 다르다고 했는데 둘이 뭐가 다르나?

WAS는 서블릿임... 자바 클래스 파일이 아니다. (웹 기반)

DI Container 인터페이스 기반의 컴포넌트... 클래스 파일

이게 다르다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123068195-a1145780-d44c-11eb-9ea7-7c207369177b.png)

result는 결과페이지 이름이다.

여기에 저장폴더(위치)와 jsp라는 확장자가 생략되어 있는 것이다.

<br/>

InternalResourceViewResolver에서 저장폴더(위치)는 prefix로 넣었고, 확장자는 suffix로 명시해서 넣었다.

![image](https://user-images.githubusercontent.com/78403443/123068249-ad98b000-d44c-11eb-8a02-54e108cf157b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123068290-b7baae80-d44c-11eb-831a-eca606afbc86.png)

<br/>

모든 것의 시발점은 web.xml이라고 했다.

![image](https://user-images.githubusercontent.com/78403443/123068347-c5703400-d44c-11eb-9a18-d8e9fc8a65a4.png)

한글처리 Filter이다. 앞으로 무조건 넣는다.

<br/>

예전엔 우리가 직접 만들었는데, 이제는 Spring 프레임워크에서 제공하는

라이브러리를 사용할 것이다.

![image](https://user-images.githubusercontent.com/78403443/123068391-d15bf600-d44c-11eb-83db-6b8a480aba13.png)

이것이 Dispatcher Servlet이다.

<br/>

WEB-INF 오른쪽 마우스 클릭 new

![image](https://user-images.githubusercontent.com/78403443/123068446-dd47b800-d44c-11eb-8815-ebdb57f7aec8.png)

빈 설정문서는 이걸로 만든다.

![image](https://user-images.githubusercontent.com/78403443/123068487-e6d12000-d44c-11eb-96d1-71cca50c396b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123068536-f05a8800-d44c-11eb-9287-4938b1be1b9f.png)

표시한 부분 "/" 이거 안넣어주면 에러난다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123068591-fc464a00-d44c-11eb-98c0-057cb83626a7.png)

index.jsp 서버 돌려서

![image](https://user-images.githubusercontent.com/78403443/123068629-05371b80-d44d-11eb-855b-fe1684d30bc6.png)

![image](https://user-images.githubusercontent.com/78403443/123068659-0bc59300-d44d-11eb-8836-ba2ab6dde454.png)

result.jsp로 잘 넘어간 것을 확인했다.

<br/>

<br/>

이게 안보인다는 얘기는 자동으로 Bean 설정문서가 와이어링 된다는 것이다.

Default...

![image](https://user-images.githubusercontent.com/78403443/123068709-1bdd7280-d44d-11eb-9249-de9e9350f733.png)

어떻게 되는지 설명한다.

Servlet-name으로 지정되있는 것은 dispatcher이다.

Wiring된 빈 설정문서 이름이 dispatcher로 알아서 지정된다.

dispatcher 뒤에 대시("-")가 붙고 xml 파일인

dispatcher-servlet.xml파일을 찾는다.

이게 WAS가 기본적으로 찾게되는 Bean Configuration파일이다. (이게 없거나 못찾으면 무조건 에러뜬다)

<br/>

똑같은 내용을 이렇게 두번째 했다.

<br/>

세번째...

**sp03_SpringMVC 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/123068780-2bf55200-d44d-11eb-9aff-54d84092ec86.png)

이렇게 만들면 다음에 뭐 만들어야할까?

FormController 클래스 파일 만든다(Controller implements)

![image](https://user-images.githubusercontent.com/78403443/123068821-34e62380-d44d-11eb-81c0-e61f15536312.png)

빨간색부분은 MVC가 알아서 한다.

모든 요청은 Dispatcher Servlet이 받고 HandlerMapping에 요청 Controller응답

Controller에 요청 보내고, Controller 에서 응답

<br/>

![image](https://user-images.githubusercontent.com/78403443/123069282-98705100-d44d-11eb-82d6-e8156907c826.png)

해당 위치에 form_result.jsp 만든다

![image](https://user-images.githubusercontent.com/78403443/123069344-a7ef9a00-d44d-11eb-980a-5a1bcafc83f1.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123069423-ba69d380-d44d-11eb-95f2-4f3a81ac6449.png)

form.html에서의 요청을 Dispatcher Servlet이 받는다.

HandlerMapping에 보내고

HandlerMapping에서 Controller와 매핑

FormController는 우리(개발자)가 직접 만들어야한다.

여기서 InternalResourceViewResolver라는 애가 정보 가지고 있다.

우리가 또, 만들어줘야하는 애는 결과페이지 (result.jsp)

<br/>

여기서 우리가 손대야 하는게 동그라미 친 것들 밖에 없다.

나머지는 그냥 돌아간다. 이게 프레임워크

(눈에 안보인다, 안만들어도 됨, 편리하지만 메커니즘을 알기는 힘들다(개발자로서는 우려스러운 부분))

<br/>

우리가 손 댈 것 다 손대서 만들고, 조립하는것이 중요하다.

(조립 잘 못하니까 Annotation기반으로 가버리는데 그렇게 하면 오류날 때 코드를 일일히 봐야하니까 힘들다.)

SI에서는 어노테이션 쓰는걸 좋아하지만, SM(삼성 같은곳...) 에서는 안좋아한다.

그래서 적절히 절충해서 써야한다.

<br/>

web.xml보기

![image](https://user-images.githubusercontent.com/78403443/123069686-fac95180-d44d-11eb-847b-6b0fc15aa592.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123069724-0583e680-d44e-11eb-86d9-ee99f06e3c4c.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123069753-0ddc2180-d44e-11eb-8412-5212806487ef.png)

여기부터 실행

![image](https://user-images.githubusercontent.com/78403443/123069950-454ace00-d44e-11eb-831a-0813ec551335.png)

잘 나옴..

![image](https://user-images.githubusercontent.com/78403443/123069987-53005380-d44e-11eb-9eb5-99e5d0ad469b.png)

<br/>

최종적으로는 어노테이션(Annotation)기반으로 간다.

간단하게 해본다

![image](https://user-images.githubusercontent.com/78403443/123070061-63b0c980-d44e-11eb-8b65-d28867b27120.png)

이렇게 하고, 컨트롤러 만든다

![image](https://user-images.githubusercontent.com/78403443/123070095-6ca19b00-d44e-11eb-9ad7-91119cbe12b4.png)

![image](https://user-images.githubusercontent.com/78403443/123070124-72977c00-d44e-11eb-83be-5704a03f7c94.png)

<br/>

Persistence Layer의 컴포넌트는 @Repository 라고했다

Service Layer는 @Service

Presentation Layer에서는 @Controller라고 한다!

이걸 다 해서 @Component로 묶어서 할 수도 있지만

Specific하게 각각 다르게 하는게 좋다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123070184-7f1bd480-d44e-11eb-9643-0cf25793f94f.png)

jsp페이지 만든다

![image](https://user-images.githubusercontent.com/78403443/123070225-893dd300-d44e-11eb-8c3b-0cf5a9f9fb82.png)

![image](https://user-images.githubusercontent.com/78403443/123070262-8fcc4a80-d44e-11eb-99d3-363a940c7da5.png)

<br/>

controller_bean.xml 파일에서

![image](https://user-images.githubusercontent.com/78403443/123070313-9c50a300-d44e-11eb-8f2a-161e75e97093.png)

위와 같이 Namespaces에서 체크를 해줘야지

![image](https://user-images.githubusercontent.com/78403443/123070371-a7a3ce80-d44e-11eb-9499-c3ceda09706a.png)

context:component-scan 태그 자동완성이 나오고

자동완성해서 base-package 경로 지정해준다.

<br/>

이제 실행해보면

![image](https://user-images.githubusercontent.com/78403443/123070415-b2f6fa00-d44e-11eb-8a09-a1fa809afed3.png)

![image](https://user-images.githubusercontent.com/78403443/123070447-ba1e0800-d44e-11eb-8050-e3c81683d34b.png)

잘 나왔다.

<br/>

---

![image](https://user-images.githubusercontent.com/78403443/123070498-c6a26080-d44e-11eb-8880-eccd7c00be3a.png)

지금부터 할 내용

- 작업순서
- 단위테스트
- 설정문서를 어떻게 조합하는지

<br/>

전에 했던 webWorkspace web34_FruitCart 똑같이 만든다. (Spring MVC로)

**sp04_FruitCart 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123070694-ef2a5a80-d44e-11eb-9e01-d9c1e3c6fea9.png)

MyBatis부터 Front... 

Back에서 Front까지 쭉 연결한다.

![image](https://user-images.githubusercontent.com/78403443/123070728-f81b2c00-d44e-11eb-9d1f-d85fd1e0092a.png)

이렇게 라이브러리 직접 추가해본다.

<br/>

직접 추가하는 방법을 알려준다.

홈페이지 : https://mvnrepository.com/

![image](https://user-images.githubusercontent.com/78403443/123070774-036e5780-d44f-11eb-9432-d70f412d9921.png)

검색창에 추가하고 싶은 라이브러리 검색

![image](https://user-images.githubusercontent.com/78403443/123070961-2ef14200-d44f-11eb-841f-b4d630fd1237.png)

둘중에 일단 맨 위꺼를 클릭함

![image](https://user-images.githubusercontent.com/78403443/123071005-39134080-d44f-11eb-9dd5-35e99763abd6.png)

처음에는 직접 추가했었고

step2에서는 Build Path잡아서 했었고

지금 step3에서는 Maven기반으로 한다. 

근데, Maven으로 할 때는 너무 높은 버전으로 하면 충돌위험이 있어서

충돌 안나는 MyBatis 3.4.6버전을 쓰고자 한다.

![image](https://user-images.githubusercontent.com/78403443/123071034-42041200-d44f-11eb-9a10-af88f50a82b0.png)

표시한 부분 복붙

<br/>

MyBatis Spring

![image](https://user-images.githubusercontent.com/78403443/123071066-4cbea700-d44f-11eb-95d5-b0b3c5e86d11.png)

![image](https://user-images.githubusercontent.com/78403443/123071097-547e4b80-d44f-11eb-9944-33b00885f85b.png)

그리고

![image](https://user-images.githubusercontent.com/78403443/123071152-5e07b380-d44f-11eb-9d3f-320995acce5d.png)

![image](https://user-images.githubusercontent.com/78403443/123071187-66f88500-d44f-11eb-9d7f-cc6587bf41c0.png)

5.1.3버전 쓴다.

![image](https://user-images.githubusercontent.com/78403443/123071225-6fe95680-d44f-11eb-9329-dab757dece48.png)

![image](https://user-images.githubusercontent.com/78403443/123071247-77106480-d44f-11eb-8bcb-aa1ea4bc6f0e.png)

Spring Transaction 5.1.3으로 

(시간상 캡쳐생략)

![image](https://user-images.githubusercontent.com/78403443/123071302-82fc2680-d44f-11eb-8c85-55c60b6068c9.png)

dbcp도 넣고

![image](https://user-images.githubusercontent.com/78403443/123071342-8becf800-d44f-11eb-9d65-118e111a652d.png)

이거랑

![image](https://user-images.githubusercontent.com/78403443/123071384-93ac9c80-d44f-11eb-9f80-ce37a9c3fd2a.png)

이것도

![image](https://user-images.githubusercontent.com/78403443/123071430-9c9d6e00-d44f-11eb-904b-65d2e8cad020.png)

이런식으로 받아야되는 필요한 라이브러리들을 pom.xml 파일에 설정해줬다.

<br/>

우리가 만들 구조 그림

![image](https://user-images.githubusercontent.com/78403443/123071496-a921c680-d44f-11eb-9cd5-a87341f1d98c.png)

크게 보면 컴포넌트는 하늘색 다이아몬드로 묶은 것..

꼭 짚어서 가리키면 MainController, ServiceImpl, DAOImpl을 컴포넌트라고 한다.

한데 묶으면 @Component

하나하나로 보면 순서대로 @Controller @Service @Repository

<br/>

이것들을 한데 묶어서 CBD라고 한다. Component Based Development

<br/>

![image](https://user-images.githubusercontent.com/78403443/123071553-b8a10f80-d44f-11eb-8a10-2027bbdd70e0.png)

vo만들었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123071602-c35ba480-d44f-11eb-8490-b182a8ea46a2.png)

![image](https://user-images.githubusercontent.com/78403443/123071631-ca82b280-d44f-11eb-9336-5d64ddcacb59.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123071690-d8d0ce80-d44f-11eb-9a33-d21b6911f352.png)

![image](https://user-images.githubusercontent.com/78403443/123071725-dff7dc80-d44f-11eb-8777-606888a910b7.png)

id값을 넣어서 검색하는 것이기 때문에 아이디getItem 부분에서는  parameterType="int"로 해야한다.

그리고 LIKE문의 '%${value}%'는 꼭 소문자로 해야한다. 대문자 VALUE로 하면 에러난다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123071812-f0a85280-d44f-11eb-876d-ef090eb5d771.png)

이렇게 했고 이제 단위테스트 해야한다.

이쪽에서 하는 단위테스트가 가장 중요하다.

<br/>

단위테스트 클래스 파일 만들기

![image](https://user-images.githubusercontent.com/78403443/123071865-fdc54180-d44f-11eb-831d-a80951e9645c.png)

![image](https://user-images.githubusercontent.com/78403443/123071911-07e74000-d450-11eb-80fb-8d94758acc84.png)

단위테스트 돌려서 잘 나오는 것을 확인했다.

<br/>

JUnit사용해서 단위테스트 해본다

![image](https://user-images.githubusercontent.com/78403443/123071958-12a1d500-d450-11eb-9dc4-9f75d6c542ce.png)

![image](https://user-images.githubusercontent.com/78403443/123071986-19c8e300-d450-11eb-9445-48cab5c6c673.png)

![image](https://user-images.githubusercontent.com/78403443/123072020-22211e00-d450-11eb-98bf-f77b58c0cd07.png)

잘 된 것을 확인했다.

<br/>

여기까지 MyBatis 프레임워크 깔끔하게 끝냈다.

<br/>

그리고 Persistence Layer 간다

![image](https://user-images.githubusercontent.com/78403443/123072082-3238fd80-d450-11eb-9e0e-d501246c79c7.png)

![image](https://user-images.githubusercontent.com/78403443/123072116-38c77500-d450-11eb-8441-34f791915c9d.png)

item-shopping-mapper.xml 파일의 코드 보면서 잘 짜줬다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072160-44b33700-d450-11eb-8317-4ba4b6565a4f.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072251-55fc4380-d450-11eb-8065-88e48153f93e.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072302-62809c00-d450-11eb-9d6a-aabfda223194.png)

여기까지가 어제 배운 것까지이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072352-6dd3c780-d450-11eb-8654-fe7e9da04620.png)

DB물리적인 설계가 끝났으면 

vo 클래스를 만든다. (이름은 DB 테이블명과 같이 간다)

그리고 SqlMapconfig를 만든다. 

이걸 만들다보면 properties파일을 연결해야하고

xml기반으로 만들어져있는 sql문 (~mapper.xml 파일)

이게 SqlMapconfig 중심으로 연결될 수 밖에 없다.

<br/>

이쪽 부분이 MyBatis Framework이다.

<br/>

이걸 다 작성을 했으면 반드시 단위테스트를 돌린다. (JUnit으로 돌림)

이게 ok 사인이 떨어지면 그 다음은 뒤도 볼 필요가 없다.

두번째 레이어로 간다. 

두번째 레이어는 Business Logic Layer이다.

Business Logic Layer를 Spring Framework 단에서는 두개로 쪼개서 쓴다.

생생한 데이터를 사용하느냐, 데이터를 가공했느냐에 따라 나뉨

생생한 데이터를 클라이언트쪽으로 보내는 것이 Persistence Layer이다.

그리고 Service Layer에서 가공해서 쓴다.

<br/>

여기서 단위테스트는 생략한다.

<br/>

그리고 여기서 멈춘다는 얘기는 (다음은 Presentation Layer이다. Presentation Layer로 안간다는 얘기)

@Controller , 중개자... (front와 back단을 merge한다)

그래서 먼저 화면을 만들고 Presentation Layer 건드려야지 확실히 merge된다.

(화면 == Front UI)

그래서 순서는 위 그림과 같이 된다. (Ⅰ, Ⅱ, Ⅲ, Ⅳ, Ⅴ 순서)

<br/>

화면(Front UI) 구현한다

![image](https://user-images.githubusercontent.com/78403443/123072493-90fe7700-d450-11eb-8940-454954eaced9.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072537-9b207580-d450-11eb-9381-af7256c6fa55.png)

![image](https://user-images.githubusercontent.com/78403443/123072593-a4114700-d450-11eb-9054-02d621930b1e.png)

최종적으로 조립만 남았다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072667-b12e3600-d450-11eb-996b-554fbd4316d8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123072713-bb503480-d450-11eb-8499-e440da339f67.png)

![image](https://user-images.githubusercontent.com/78403443/123072756-c5723300-d450-11eb-8801-8e2b25bb252b.png)

![image](https://user-images.githubusercontent.com/78403443/123072789-cc994100-d450-11eb-8878-96362497c957.png)

<br/>

index.jsp부터 실행

![image](https://user-images.githubusercontent.com/78403443/123072845-db7ff380-d450-11eb-883c-4be99eeb36ac.png)

![image](https://user-images.githubusercontent.com/78403443/123072873-e2a70180-d450-11eb-9886-5060c0de5e31.png)

잘 나왔다.
