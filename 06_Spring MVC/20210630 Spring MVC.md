![image](https://user-images.githubusercontent.com/78403443/123921026-8c424180-d9c1-11eb-8bea-a82c017ad648.png)

1. Ajax로 비동기...

   - 자바스크립트, JQuery

   - 순수 자바스크립트로는 이벤트 처리가 어려움이 있기에...

   - 거기에 Maven기반 Spring Framework연결

     - pom.xml, Dependency... → Bean 설정문서

2. 프로그램

   - 아키텍처 구조, Front 기술 (끌어다 사용... Template)

     - Bootstrap
     - JQuery
     - CSS3
     - html, javascript, css
     - Maven기반 디렉토리 (resources) or webapp 밑에 css, js 폴더 만들어서

3. 기존의 내용 (저번주 + 이번주 월, 화 내용)... Template

<br/>

---

- **sp09_Ajax 프로젝트**

<br/>

**servlet-context.xml 파일 보기**

WEP-INF

![image](https://user-images.githubusercontent.com/78403443/123921141-aa0fa680-d9c1-11eb-8ad6-022c11b8dc52.png)

실행된 결과를 가지고 뿌리고 들어갈 때는 webapp밑으로...

<br/>

![image](https://user-images.githubusercontent.com/78403443/123921267-cb709280-d9c1-11eb-8ae5-70f1911fa43e.png)

화면을 구성하는데 필요한 정적인 문서들을 resources에 모조리 때려넣어라는 권장사항임

html과 jsp는 당연히 아님.. css, javascript기술, image 파일들임

(jsp는 동적인 문서, html은 정적인 문서와 엮여져서 나오는 것뿐이기 때문)

<br/>

- AjaxController 클래스 파일 작성

<br/>

- synchro_result.jsp 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123921397-ecd17e80-d9c1-11eb-8472-3888606e1285.png)

<br/>

확인

<br/>

![image](https://user-images.githubusercontent.com/78403443/123921484-01ae1200-d9c2-11eb-9b1c-3a559102ddac.png)

비동기 통신에서 결과페이지는 없기 때문에 요청한 곳으로 되돌아간다. 파일 다운로드 될 뿐... BeanNameViewResolver필요

<br/>

- Person 클래스 파일 작성

<br/>

- synchro_result.jsp 파일 작성

<br/>

- appServlet 밑에 servlet-context.xml 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123921539-125e8800-d9c2-11eb-9a75-4ebc030393af.png)

빨간 박스표시...

이게 Ajax에 결과페이지 연결하는 법

<br/>

![image](https://user-images.githubusercontent.com/78403443/123921577-1e4a4a00-d9c2-11eb-8be8-ed473fe4e769.png)

이 라이브러리 추가해야 에러 안떨어짐

![image](https://user-images.githubusercontent.com/78403443/123921617-27d3b200-d9c2-11eb-9ed2-2804043113a9.png)

![image](https://user-images.githubusercontent.com/78403443/123921639-2efac000-d9c2-11eb-8c84-b603044ab159.png)

<br/>

여기까지 비동기 했음

<br/>

---

- **sp08_BookTest 프로젝트 보기**

여기다가 비동기 연결한다.

<br/>

---

- **sp10_BoardTest 프로젝트**

파일 업로드 가능한 게시판 만들기 팀 작업
