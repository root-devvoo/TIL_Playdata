![image](https://user-images.githubusercontent.com/78403443/124563431-fef86480-de7a-11eb-81ef-e811438641c2.png)

오늘은 Restful Service에서 Client Side 코드를 짜본다.

어제는 Server Side 코드를 다뤘다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/124563504-0b7cbd00-de7b-11eb-8d69-0f4d994ca26c.png)

Restful 기반은 Spring Boot, Spring Boot에는 web.xml이 없다.

Maven 기반으로 하다가 Spring Boot로 바꿀 예정이다.

Boot에서는 url-path *.do 나 /(슬러시) 표시 둘 중 아무거나 써도 됨

<br/>

- sp14_Restful_BookTest 프로젝트

![image](https://user-images.githubusercontent.com/78403443/124563562-1c2d3300-de7b-11eb-918b-a610123cb9c6.png)

도서목록조회를 누르면 비동기로 @RestController에서 List<Book> 형식으로 데이터 반환

bookmgr.jsp파일의 book-list 태그쪽에 뿌릴 것이다. (bookmgr.jsp파일 참고)

<br/>

![image](https://user-images.githubusercontent.com/78403443/124563619-2818f500-de7b-11eb-9002-078798397305.png)

<br/>

---

- **sp15_Restful_PhoneTest 프로젝트**

<br/>

작성한 코드 잘 리딩하면서 학습하기

<br/>

**내일은 Spring Boot 설치하고, 어제 오늘 배운 Restful Service와 연결하는 수업 진행함**
