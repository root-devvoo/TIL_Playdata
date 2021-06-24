1. 오늘은 Spring MVC.. 새롭게 Back에서 Front까지 강사님과 다 구현
2. Spring MVC로 Back에서 Front까지 직접

<br/>

**sp05_Products 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123219785-3fb1be80-d508-11eb-8a4d-ecaf3d8ee3d7.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/123219817-493b2680-d508-11eb-85d0-f7f965fbf8d0.png)

![image](https://user-images.githubusercontent.com/78403443/123219841-4fc99e00-d508-11eb-8998-2ad90d4bc9d8.png)

![image](https://user-images.githubusercontent.com/78403443/123219868-56581580-d508-11eb-9cfc-25a688c7eae7.png)

② 아무것도 안넣었을 때 모든상품 검색하도록 하기

<br/>

Form이름, vo의 필드 이름 일치하면

Controller의 메소드 인자값으로 자동 바인딩

이 부분을 적극적으로 사용하기

그렇게 되면, request.getParameter() 코드가 날아간다. (필요 없어짐)

팀 작업...

<br/>

---

팀 작업 후...

![image](https://user-images.githubusercontent.com/78403443/123219946-6839b880-d508-11eb-869f-6c445181a20f.png)

INSERT문을 작성할 때 디비에서 ID가 자동증가되고, PK값일 경우

위에 밑줄 친 두 옵션을 줘서 DB테이블과 VO를 동기화시켜줘야한다.

<br/>

정리

![image](https://user-images.githubusercontent.com/78403443/123219983-72f44d80-d508-11eb-8b60-c32c2850be40.png)

빨갛게 그려놓은 것은 라이브러리 빈으로 만들어놓아야한다. (DI 컨테이너에서)

ServiceImpl과 DAOImpl은 사용자정의 빈이다.

<br/>

지금부터 새로운 내용... (이것만 남겨두고있음)

빈 설정문서를 모듈화해야한다.

① 모듈화를 하는 기준이 우리는 Layer별로 모듈화하고 있다.

<br/>

의존이기 때문에 뒤에껄 먼저 만들고 앞을 만들어야 뒤에꺼가 Hasing됨

그렇기 때문에 BusinessBean.xml을 만들고, Presentation.xml을 만든다.

web.xml이 이것을 wiring(와이어링)한다.

② Domain별로 모듈화

<br/>

web.xml을 연다

![image](https://user-images.githubusercontent.com/78403443/123220036-82739680-d508-11eb-8844-bd7dc45ca0e0.png)

①번 빈이 (뒤) 먼저 만들어지고

② 만들고 연결

<br/>

![image](https://user-images.githubusercontent.com/78403443/123220062-8c959500-d508-11eb-84c9-e5b1fefa7209.png)

이렇게 모듈화 시킨다.

이 파일들은 resources패키지로 갈 것이다.

![image](https://user-images.githubusercontent.com/78403443/123220111-96b79380-d508-11eb-9f00-4d5eec064efa.png)

위 파일들의 자세한 코드는 직접 열어서 보기 
