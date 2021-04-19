**오늘 할 내용!** 

1번, 2번, 3번

![image](https://user-images.githubusercontent.com/78403443/115195873-3d0ea380-a12a-11eb-8dd3-d4d7dce26032.png)

---

**web32_JQuery_Ajax 프로젝트**

- 01ajax_JQuery.html 파일

- - JQuery Ajax는 무조건 $.ajax({})로 시작한다.
  - 서버쪽에서 보내는 데이터를 받으려면 success:function() 괄호안에 결과에 대한 인자값 넣어준다

![image](https://user-images.githubusercontent.com/78403443/115195925-4bf55600-a12a-11eb-85b4-a1d20d3d38af.png)

이게 가장 기본...

- HelloAjax.java (서블릿) 파일



- 02ajax_JQuery.html 파일

- - 아까는 {} 가 없었기 때문에 = 였는데, 지금은 {}로 했기 때문에 :(콜론) 이다.

![image](https://user-images.githubusercontent.com/78403443/115195996-60d1e980-a12a-11eb-9669-745f134e8688.png)

![image](https://user-images.githubusercontent.com/78403443/115196021-692a2480-a12a-11eb-8182-b6bfef1355fa.png)



- JQueryAjax.java (서블릿) 파일

- - 서블릿 안에선 응답 하면 안된다. PrintWriter out = getWriter.. 
  - 서버에서 out.print 안쓴다. 
  - 결과 페이지(JSP)에서 attribute 통해서 응답 결과값 나타내도록 할것이다.

- resultView.jsp 파일 보기



![image](https://user-images.githubusercontent.com/78403443/115196077-79da9a80-a12a-11eb-84d1-663a50ba3e37.png)

기본적인 꼬라지는 이렇다. 

꼭 알아두기



**weather**

![image](https://user-images.githubusercontent.com/78403443/115196135-8d860100-a12a-11eb-96d8-9fe36be1a424.png)

내가 필요한 정보를 받을 weather Domain을 만들어서 알고리즘 적용하면 리스트가 반복되는 만큼 데이터 출력

알고리즘은 시각화랑 반드시 연결되어져야 한다.



- weather.xml 파일 보기

- - 공공데이터 포털 사이트에서 가지고 온 xml 오픈 데이터(OPEN API) :: 서버에 저장
  - 실제 데이터는 복잡해서 간단하게 직접 비슷한 형태로 만들었다

![image](https://user-images.githubusercontent.com/78403443/115196195-9e367700-a12a-11eb-8277-7224a61b8ade.png)

weather.xml을 서버에 저장했다. 

경로: tomcat 홈 → webapps → ROOT 



- 03ajax_openAPI.html 파일 보기

- - 응답시 전달되는 데이터 타입의 형태를 지정...json 일 때는 주로 작성한다 ..xml, text, json

![image](https://user-images.githubusercontent.com/78403443/115196243-abebfc80-a12a-11eb-9d7c-24cedaa071aa.png)



- 04ajax_serialize.html 파일 보기

![image](https://user-images.githubusercontent.com/78403443/115196326-be663600-a12a-11eb-931d-51d5992436ae.png)

선택자와 함수연결 JQuery로



- - 폼에 입력된 값을 다 서버로 보내는 기능....serialize() :: 입력값들을 쿼리스트링으로 만들어서 전송한다.

![image](https://user-images.githubusercontent.com/78403443/115196390-cd4ce880-a12a-11eb-8889-8cc55da8420b.png)

까먹으면 안된다.



- 05ajax_json.html 파일

- - 응답하는 데이터 타입이 객체일 때 json 이라고 지정한다.

- Weather.java 파일

- json.jar 라이브러리가 있어야 json을 작성할 수 있다.

![image](https://user-images.githubusercontent.com/78403443/115196437-dccc3180-a12a-11eb-94ff-e998abd5a7e9.png)

- JsonServlet.java (서블릿) 파일 보기

- - json문법...

---

---

**web33_Algorithm_Ajax 프로젝트**

- index.html 파일

![image](https://user-images.githubusercontent.com/78403443/115196486-eeadd480-a12a-11eb-9ec6-fc43caf3a867.png)

1번째 영역: 요청 관련 로직

3번째 영역: 응답 로직

2번째 영역 에러는 추가적으로 그냥 넣어봄



- MainServlet.java (서블릿 파일)

- - 해당 모듈 안에서만 사용되고 다른 모듈에서는 불려지는 일이 없을 때...함수 앞에 private 쓴다
  - 알고리즘 자바 클래스의 execute() 함수 호출하려면...Count클래스 객체를 생성

- Result.jsp 파일



- 전체적인 현재 구조 그림

![image](https://user-images.githubusercontent.com/78403443/115196538-fd948700-a12a-11eb-9e42-5fc7b65c24d5.png)

Count와 KickBoard는 클래스 

서블릿이 폼값 받아와서 알고리즘을 돌린다. 



이미 전에 배웠듯이

FactoryMethod 패턴에서는 서블릿이 돌리면 안된다.

![image](https://user-images.githubusercontent.com/78403443/115196581-09804900-a12b-11eb-9ff5-e15cf517ea33.png)

컴포넌트가 객체생성한거에서 폼값 받아와서 알고리즘 돌리고 

서블릿 통해 클라이언트 화면에 출력



- KickBoard... 지도 파일 경로

![image](https://user-images.githubusercontent.com/78403443/115196623-169d3800-a12b-11eb-8041-24a1a1200d22.png)

![image](https://user-images.githubusercontent.com/78403443/115196653-1f8e0980-a12b-11eb-8210-3d77b1f34f95.png)

webapps 밑에 배포한 것을 파일을 쓰는것이다. (꼭 알아야한다)



- index.html 보기
- MainServlet 보기



**※ context path 불러오는 기능**

getServletContext, getRealPath 사용... 중요하다!!!

![image](https://user-images.githubusercontent.com/78403443/115196739-36ccf700-a12b-11eb-93be-e27d458803a7.png)

![image](https://user-images.githubusercontent.com/78403443/115196767-3f253200-a12b-11eb-9576-5fa21f204e32.png)

꼭 알아야 한다.



구조...

![image](https://user-images.githubusercontent.com/78403443/115196810-4c422100-a12b-11eb-80d9-99448faec757.png)

지금은 frontController 패턴으로 간단하게 만든 것이다. 



FactoryMethod 패턴에서는 각 컴포넌트에서 저 과정들이 이루어져야(실행해야) 하기 때문에

프로젝트 할 때는 좀 더 복잡하고 커질 것이다.

---

---

**web31_JQuery UI 프로젝트...**

**JQuery UI... 프로그램과 연결**

- ui03_accordion.html 파일 보기

- - heightStyle :: 컨텐츠에 맞게 어코디언 높이를 조절하는 옵션... 디폴트가 fill
  - 동적으로 어코디언을 만들 때는 'destroy' 옵션으로 이전 어코디언을 완벽하게 삭제한 후 다시 어코디언을 생성한다.



프로그램과 연결하려고 함.

- servlet.controller 패키지 안에 있는 파일들 보기
