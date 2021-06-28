![image](https://user-images.githubusercontent.com/78403443/123590018-0b4e4300-d825-11eb-9c69-94b87387e89b.png)

<br/>

Transaction은 서버사이드 레이어 중에서 Business Logic부분과 관련이 있다.

<br/>

- **sp05_Products 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123590097-2620b780-d825-11eb-896a-b351ea383036.png)

그리고 Annotation 기반으로 Transaction 처리

비즈니스 로직 레이어에다가 추가하면 된다.

![image](https://user-images.githubusercontent.com/78403443/123590130-30db4c80-d825-11eb-8ff1-e36d1a43ddf8.png)

그리고 해당 Impl클래스에서 Transaction처리하고자 하는 메소드에다 지정한다.

![image](https://user-images.githubusercontent.com/78403443/123590153-3a64b480-d825-11eb-9ca3-41af64dda8c1.png)

이렇게 해주면 Transaction을 건다.

이것이 AOP기법...

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590194-46e90d00-d825-11eb-869a-01a3bb39c045.png)

컴포넌트와 빈을 구별해야한다.

vo객체 같은 것들은 빈이 아니다.

리턴은 ModelAndView로 하지만 Bean으로 처리하지 않는다.

단순 정보를 담는 인스턴스에 불과

<br/>

ModelAndView는 어떤 정보를 담고 있냐면

① 말 그대로, Model(리턴되는 vo(들의) 정보)

② 결과페이지 이름

<br/>

반면에 InternalResourceViewResolver는

① 뷰 페이지의 물리적 위치

② 뷰 페이지의 확장자 정보를 담고 있다.

<br/>

Presentation Layer에 대해서 조금 더 깊이 있게 들어간다.

<br/>

- **sp06_ViewResolver 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123590242-5b2d0a00-d825-11eb-84a4-73d73b61884b.png)

ModelAndView 정보

View page 경로의 다각화를 하고 싶은 것...

그러나 prefix의 경로를 여러개로 할 수는 없다.

그래서 BeanNameViewResolver가 필요하다

![image](https://user-images.githubusercontent.com/78403443/123590274-654f0880-d825-11eb-99ce-e766cdfc13e1.png)

InternalResourceViewResolver를 이용해서 결과페이지로 이동

![image](https://user-images.githubusercontent.com/78403443/123590303-6f710700-d825-11eb-804d-33d7c37d8055.png)

<br/>

이렇게 폴더 만들기

![image](https://user-images.githubusercontent.com/78403443/123590351-7c8df600-d825-11eb-8e2a-eac7693a6b32.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590384-86175e00-d825-11eb-854a-dc52620c7d74.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590404-8e6f9900-d825-11eb-8eb4-9ad149b93754.png)

index.jsp실행

![image](https://user-images.githubusercontent.com/78403443/123590440-9e877880-d825-11eb-929a-71e21d2e8ee1.png)

링크와 버튼 누를 때마다 호출 잘 됨

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590481-a9daa400-d825-11eb-903c-ede8f7c51530.png)

ModelAndView 우선순위에 따라서 훓어서 이동... 

① 페이지 이동 기본 → Forward

② Request

그래서 ModelAndView로 리턴할 때 최종적으로 정리해야하는 것은 뭐냐면

① redirect 방식으로 이동할 수 있어야하고

② session이나 ServletContext에 바인딩 할 수 있어야 한다.

<br/>

결론 ::

Spring Framework를 못하는 사람은

① 자바의 oop개념이 없는 사람

② Servlet 개념을 모르는 사람

<br/>

자바 Server side 기술 중에 Servlet이 제일 중요하다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590535-b8c15680-d825-11eb-9001-687fd641480a.png)

<br/>

파일 업로드 처리

- **sp07_FileUpload 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123590566-c37beb80-d825-11eb-918a-a5c3538af6ce.png)

사용자가 업로드한 파일들의 정보를 갖고 있는게 MultiPartFile 임

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590603-ce368080-d825-11eb-8e9f-44c52677bf32.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590629-d7bfe880-d825-11eb-8d82-00f65fd88020.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590650-e1495080-d825-11eb-95d6-d253780eaa7d.png)

Multipart File Bean 등록을 안했기 때문에 null 이 출력

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590689-eefed600-d825-11eb-9dbe-9a89e6b059a9.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590721-fa520180-d825-11eb-8d20-5ead6c9a48fe.png)

pom.xml에 8번째로 위 코드 넣어준다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590760-0a69e100-d826-11eb-8baa-4f08c4168b0a.png)

MultiFile의 주요기능

getSize() :: 파일의 용량 리턴

getOriginalFilename() :: 업로드한 파일의 이름 리턴받는다

transferTo() :: 파일을 특정한 경로로 이동하는 기능

![image](https://user-images.githubusercontent.com/78403443/123590784-1655a300-d826-11eb-9d72-5c7dda147726.png)

<br/>

index.jsp 파일 실행해서 업로드해봤다.

![image](https://user-images.githubusercontent.com/78403443/123590819-22d9fb80-d826-11eb-8c4a-8efa0585b0b1.png)

웹페이지에는 오류가 떴고

업로드된 파일명과 파일의 파라미터명은 콘솔로 출력되었다.

uploadFile은 Form 이름이기도 함

<br/>

![image](https://user-images.githubusercontent.com/78403443/123590838-2ff6ea80-d826-11eb-8dfc-a6d96cc4acc7.png)

context가 위와 같이 잡히므로 경로를 하나 만들어야한다.

그래서, webapp밑에 upload 폴더를 만든다.

<br/>

다시 실행해서 파일을 올리면 제대로 잡힌다.

![image](https://user-images.githubusercontent.com/78403443/123590867-3e450680-d826-11eb-92a1-7531773451d9.png)

<br/>

메모에 없는 것들은 코드와 주석 살펴보기

