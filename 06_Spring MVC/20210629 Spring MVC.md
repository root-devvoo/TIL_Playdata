- **sp08_BookTest 프로젝트 보기**

<br/>

<구현에 있어서 작업 순서>

1. 테이블 작성

2. vo 작성

3. SqlMapConfig.xml 작성

   - mapping.xml

4. 3번까지 다 되면 단위테스트 진행

<br/>

그리고, MemberController 클래스 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123763883-35743380-d8ff-11eb-871d-64a1192ede2e.png)

redirect 써야 하는 경우... 위 이미지 참고

<br/>

redirect는 서버에서 이동하는게 아니기 때문에 viewResolver랑 상관이 없다.

그래서, 확장자 써줘야 함

![image](https://user-images.githubusercontent.com/78403443/123763931-41f88c00-d8ff-11eb-8e26-042ac4f31fd8.png)

redirect: 하고 반드시 확장자를 써줘야한다.

<br/>

index.jsp 파일 작성... 코드 보기

<br/>

BookController 클래스 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123763978-4f157b00-d8ff-11eb-981d-fbf23d1e63c3.png)

![image](https://user-images.githubusercontent.com/78403443/123764001-56d51f80-d8ff-11eb-894f-3e31662167d5.png)

bookList로 forwarding한다.

<br/>

bookList.jsp 작성

![image](https://user-images.githubusercontent.com/78403443/123764053-62c0e180-d8ff-11eb-9025-5fd0eccfd926.png)

<br/>

MemberController 파일 작성

HttpServletRequest를 써야할 경우에는 Session 사용할 때 인자값 더 넣을 필요 없이

HttpServletRequest에서 getSession()해서 Session사용하면 된다.

<br/>

bookForm.jsp 파일 작성

<br/>

BookController 클래스 파일 작성

① result.jsp가 book폴더 안에 없기 때문에 리다이렉트 해야한다.

② 에러났을 경우 Error페이지를 보여줘야하기 때문에 리다이렉트 해야한다.

<br/>

bookList.jsp 작성

도서명, 출판사, 가격별 검색하는거 적용해본다.

![image](https://user-images.githubusercontent.com/78403443/123764179-83893700-d8ff-11eb-88d4-7c08844309c6.png)

주황색 밑줄 친 부분을 바인딩 시켜야한다.

BookController에서 작성

![image](https://user-images.githubusercontent.com/78403443/123764229-8edc6280-d8ff-11eb-892f-3e3c498c29cd.png)

<br/>

책 누르면 상세페이지 연결

bookList.jsp파일 작성

<br/>

BookController 클래스 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123764302-9d2a7e80-d8ff-11eb-98d6-92ba90abb7a7.png)

<br/>

bookView.jsp 파일 작성

![image](https://user-images.githubusercontent.com/78403443/123764346-a87daa00-d8ff-11eb-9f83-babd305ffea3.png)

<br/>

- **sp07_FileUpload 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/123764389-b5020280-d8ff-11eb-95b0-676ffbde5c57.png)

여러개 업로드 시키게 할 때는 이런식으로 표현하면 된다.

upload[0]번째, upload[1]번째, upload[2]번째

![image](https://user-images.githubusercontent.com/78403443/123764440-be8b6a80-d8ff-11eb-850c-851bae596c6d.png)

이렇게 multiple하게

<br/>

다운로드...

![image](https://user-images.githubusercontent.com/78403443/123764484-c8ad6900-d8ff-11eb-8982-a409bf49a821.png)

![image](https://user-images.githubusercontent.com/78403443/123764512-cfd47700-d8ff-11eb-9b9e-c81677a7eec7.png)

BeanNameViewResolver로 써야 처리된다.

<br/>

- **sp09_MultipleFileUpload 프로젝트**

스터디 팀에서 인터넷 검색결과 참고해서 만듬

<br/>

참고 사이트 : https://velog.io/@ednadev/%EC%8A%A4%ED%94%84%EB%A7%81-7-File-Upload-Download
