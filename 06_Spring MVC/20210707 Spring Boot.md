![image](https://user-images.githubusercontent.com/78403443/124726757-01c18b00-df49-11eb-8e88-55371513fc6d.png)

Front Controller의 Front라는 뜻은 Server side에서 가장 최전방에 있다는 뜻임 (Front End랑 다름)

요청의 결론이 결과페이지가 전부... (jsp파일)

<br/>

모든 것이 WAS안에서 Maven 구조 안에서 이뤄진다.

결과페이지(.jsp)가 Server side에서 만들어지고 리턴된다.

<br/>

모바일 환경은... 기존의 PC 화면 구성과는 다른 Device

그러나, 기존하고 똑같이 요청하고 응답을 받는다는 얘기는 jsp를 받는다는 얘기이다.

서버사이드에서 만들어서 리턴하는 jsp를 쓸 수 없다.

못쓴다는 얘기는 이렇게 요청, 응답하지 않는다는 얘기이다.

그럼 어떻게 요청, 응답하나?

@RestController에서 요청... ResponseEntity로 데이터를 받기 때문에 자기들 페이지는 디바이스에 맞게 알아서 짠다.

(이것이 Restful Service)

<br/>

이런건 Maven기반으로 돌리지 않고, Spring Boot기반으로 만든다.

① Spring Boot는 Tomcat Engine이 자체적으로 내장되어있다.

② Spring Boot는 jsp가 장착되어있지 않다. (최종적인 결과로 jsp를 안쓴다는 얘기임.. 데이터만 리턴)

<br/>

여기서 모든 통신은 Ajax (비동기) 로 이뤄진다.

jsp안쓴다는 얘기는 세션(Session)도 사용 안한다는 얘기임

<br/>

그리고, Front End 기술은 Vue.js 같은걸로 연결되어진다.

<br/>

---

※ Spring boot 세팅_제공.txt 파일 에버노트에다 첨부해놓음

<br/>

![image](https://user-images.githubusercontent.com/78403443/124726921-2b7ab200-df49-11eb-949d-74316de20877.png)

이것이 Spring Boot starter의 줄임말로 보면 된다. 이거 선택해서 프로젝트 만든다.

![image](https://user-images.githubusercontent.com/78403443/124727008-464d2680-df49-11eb-834f-0e7b4e1f2ee9.png)

Springboot는 특이한게 하나 있다.

① Artifact ID가 Context 되지 않는다. (Context path가 없다)

② Tomcat 내장 되어져 있다.

③ jsp 지원 안한다.

④ web.xml이 없다.

![image](https://user-images.githubusercontent.com/78403443/124727062-5238e880-df49-11eb-9d78-61f60c55bae5.png)

Spring Boot는 라이브러리를 이런식으로 검색, 체크해서 추가한다. 

![image](https://user-images.githubusercontent.com/78403443/124727101-5c5ae700-df49-11eb-8617-f1092eac02cf.png)

Spring Boot Devtools는

우리가 서버를 가동하고 나서 코드를 수정한다. 

이게 정적인 문서가 아닐 경우 서버를 재가동해야 적용이 되는데, 

Devtools는 내가 코드 수정할 때마다 알아서 서버를 재가동해준다. (알아서 Boot 서버 가동)

![image](https://user-images.githubusercontent.com/78403443/124727131-65e44f00-df49-11eb-8d5b-7ad7ab15c135.png)

Spring Boot는 이렇게 알아서 버전 잡는다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124727195-75639800-df49-11eb-9a65-870f5a0923b7.png)

webapp 폴더가 끝... WEB-INF 폴더가 없다.

그 얘기는 web.xml 이런거 없다는 얘기이다.

그럼 난 예전에 Maven기반으로 했던거를 boot기반으로 만들고 싶다.

컨트롤러 만들어주고 다른 것도 만들어주면 된다.

<br/>

우리가 프로젝트를 만들면 Application.java가 만들어진다.

![image](https://user-images.githubusercontent.com/78403443/124727256-82808700-df49-11eb-8299-a610d275f9c1.png)

이걸 실행하면 Boot 서버가 가동된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124727306-8f04df80-df49-11eb-9b71-3d056bb94d26.png)

Spring Boot App으로 실행해야지만 실행된다.

![image](https://user-images.githubusercontent.com/78403443/124727391-a17f1900-df49-11eb-9aed-b5c40531891d.png)

이렇게 떠야 Boot 서버가 잘 돌아가는(실행되는) 것이다.

Default port는 8080인데... 수업에서는 7788로 통일할 것이다.

![image](https://user-images.githubusercontent.com/78403443/124727520-c2476e80-df49-11eb-99fb-a7e798ce6359.png)

webapp 폴더 밑에 html파일을 만들고, 맞는 주소와 port를 쳐줬다.

html파일에 입력한 내용이 잘 나오면, Spring boot 서버 정상적으로 가동되고있다는 얘기이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124727576-d12e2100-df49-11eb-80ea-0ea9a5ea1064.png)

요청할 때마다 Initializing 이 콘솔에 뜬다.

우리가 배운 DispatcherServlet 매커니즘이 비슷하게 돌아가는 듯 하다.

<br/>

Hashtable의 자식이 Properties이다.

Key :: String

Value :: String

<br/>

boot 할 때

![image](https://user-images.githubusercontent.com/78403443/124727722-ed31c280-df49-11eb-9613-bdd898a440cb.png)

(강사님의 경우) 얘를 쓴다. application.properties

(사람에 따라서 webapp밑에 static 폴더 만들어서 정적 문서 관리하는 사람들도 있긴 하다)

우리는 application.properties 쓴다.

![image](https://user-images.githubusercontent.com/78403443/124727771-f91d8480-df49-11eb-900d-b9ee29cf1c8a.png)

별도의 context-path를 이렇게 추가해줄 수 있다.

<br/>

재가동할 때는 서버를 멈췄다가 다시 실행해야 한다. (그래야 에러가 안남)

![image](https://user-images.githubusercontent.com/78403443/124727986-2d914080-df4a-11eb-9c49-c96bb22dc207.png)

설정해준대로 port번호 바꾸고 depth 하나 더 들어가야함

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728129-4b5ea580-df4a-11eb-86fc-2bdc781e6c0a.png)

이렇게 Controller를 만들어주고

![image](https://user-images.githubusercontent.com/78403443/124728182-56193a80-df4a-11eb-81ff-a472de7af466.png)

이렇게 폴더를 만들었다. 

결과들을 여기에(webapp/WEB-INF/results 폴더에)다 넣겠다는 얘기임

![image](https://user-images.githubusercontent.com/78403443/124728250-66311a00-df4a-11eb-9bf6-da46aaab30f8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728302-70ebaf00-df4a-11eb-88ad-f6cab5df44fb.png)

이렇게 한 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728345-7ba64400-df4a-11eb-92e5-21a7995a865d.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728385-84971580-df4a-11eb-9d38-0179dd5c9c85.png)

prefix에 슬러시("/") 닫아줘야한다.

![image](https://user-images.githubusercontent.com/78403443/124728478-95478b80-df4a-11eb-8b08-343cf9d155f8.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728510-9f698a00-df4a-11eb-8a7c-3cc8ad058fda.png)

![image](https://user-images.githubusercontent.com/78403443/124728546-a5f80180-df4a-11eb-8fc4-7295403ad117.png)

지금까지 적용한 내용을 업데이트 한다 (위 방법대로)

<br/>

그리고 다시 Boot 서버 실행

![image](https://user-images.githubusercontent.com/78403443/124728616-b4461d80-df4a-11eb-9393-80c1263cf2fe.png)

위와 같이 올바르게 요청해주고, 출력 확인

<br/>

---

아까 한 내용을 다시 새 프로젝트에서 해본다.

<br/>

- **spboot17 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/124728708-c4f69380-df4a-11eb-8b41-c93bd9544325.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124728754-cde76500-df4a-11eb-8d9c-13f8f9e526e5.png)

위 링크 클릭하면

![image](https://user-images.githubusercontent.com/78403443/124728805-d6d83680-df4a-11eb-848d-437eb37b2661.png)

이렇게 MainController에서 설정해준대로 이동

<br/>

---

- **spboot18_Product 프로젝트**

back에서 front까지 Spring boot로 연결하는 프로젝트

![image](https://user-images.githubusercontent.com/78403443/124728868-e6577f80-df4a-11eb-9f22-0567cde94503.png)

<br/>

---

- **spboot19_emp 프로젝트**

scott계정에 이대로 테이블 셋팅해서 넣어줌

(※ sql파일은 에버노트에다 첨부해놓음)

![image](https://user-images.githubusercontent.com/78403443/124729191-30406580-df4b-11eb-998c-547b03c9a548.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124729229-39313700-df4b-11eb-94fb-c8fac0e59bd7.png)

<br/>

- SimpleController 작성

지금은 Spring Boot에서 그냥 @Controller로 만들고

최종적으로는 @RestController로 만들 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124729307-49491680-df4b-11eb-9f8d-4245fe33db12.png)

Context-path 따로 설정안했기 때문에 위와 같이(depth없이) 요청

<br/>

![image](https://user-images.githubusercontent.com/78403443/124729346-549c4200-df4b-11eb-8fea-6ce682ecf75e.png)

views폴더 밑 list.jsp에 toString 바인딩한 데이터 잘 나왔다.

<br/>

- EmployeeController 파일 작성

얘는 @RestController (적용)

![image](https://user-images.githubusercontent.com/78403443/124729457-6bdb2f80-df4b-11eb-89bc-b692567a7edf.png)

JSON형식으로 모든 사원 리턴 받았다.

<br/>

나머지는 알아서 작성... 

Postman으로 확인하면서 짠다.

다 작성했다 (EmployeeController 코드보기)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124729534-7ac1e200-df4b-11eb-8851-2e9b4af17dfc.png)

지금은 그렇게 안했지만... 비동기로 구현했을 때 다른 컴퓨터에서 똑같이 요청하면 다른 컴퓨터에서 값 절대 못받아온다. (해킹방지)

요청 제한임...

그래서 CrossOrigin 써줘야한다.

![image](https://user-images.githubusercontent.com/78403443/124729578-87463a80-df4b-11eb-8bd7-510619f8dc39.png)

이것을 크로스도메인 이슈 처리라고 함

![image](https://user-images.githubusercontent.com/78403443/124729626-9200cf80-df4b-11eb-8555-0017fe237ca1.png)

(출처 : http://jmlim.github.io/spring/2018/12/11/spring-boot-crossorigin/)

<br/>

지금부터 Swagger를 단다.

![image](https://user-images.githubusercontent.com/78403443/124729814-bc528d00-df4b-11eb-82ea-d1bcdc018c75.png)

**(이후에 오류때문에 json설정은 지웠고, swagger만 남겼다 참고!!!!!!!!!!!!!.. 그런데 지우고 다시 추가하니 또 됐음... 또 안될 때 지우자)**

<br/>

SwaggerConfig.java파일

![image](https://user-images.githubusercontent.com/78403443/124730027-ec9a2b80-df4b-11eb-81c1-5c1af2b1cfe2.png)

EmployeeController에 @Api를 상단에 어노테이션해주고, @ApiOperation을 각 기능마다 달아주었다.

<br/>

Swagger를 할 때는 SwaggerConfig 파일이 꼭 있어야한다.

![image](https://user-images.githubusercontent.com/78403443/124730074-fa4fb100-df4b-11eb-8e0b-b066e8211361.png)

실행하고 swagger-ui.html페이지 요청

![image](https://user-images.githubusercontent.com/78403443/124730109-03d91900-df4c-11eb-979e-444f3d8b9826.png)

![image](https://user-images.githubusercontent.com/78403443/124730146-0b98bd80-df4c-11eb-8c0c-08f8878525de.png)

Swagger는 Restful 서버 개발자가 반드시 만들어야 한다.

Swagger는 누가 필요로 할까? Front End(Client)개발자가 필요로 한다.

Front End(Client)개발자한테 전달... 주소만 가르쳐주면 된다.

<br/>

---

**내일은 Vue.js나간다.** 

**Vue.js랑 Swagger랑 연결함**

<br/>

spboot18 프로젝트 팀 작업하고 발표하고, 그거 바탕으로 Vue 연결한다.

팀 작업한거 spboot18_Product_Team1 프로젝트 보기

<br/>

**오늘 한 내용 코드 잘 살펴보기**
