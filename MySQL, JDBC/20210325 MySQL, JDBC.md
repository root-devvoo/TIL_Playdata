*JDBC*

- ① Broker 3tier
  - JDBC
  - Network
  - More Advanced Feature

- ② SQL
  - Join
  - Transaction

- J2SE Spec
  - Java, JDBC 마무리

---

**JDBC 3tier**

jdbc07_ 프로젝트 파일들 보기!

- 요청, 응답 (Network 설계)
- jdbc07_프로젝트 Broker 파일, 맨 하단부 보기
- DB관리자가 주식종목을 (showStockList) 업데이트 할 때 getAllstocks 메소드를 일정한 시간마다 호출하도록...
- jdbc07_프로젝트 실행순서
  - ProtocolHandler → StreamingData → Broker 순으로 실행 

---

**MySQL**

6. JOIN (pdf파일 보기)

   - Join 

     > :: Equi Join
     >
     > :: Outer Join
     >
     > :: JOIN은 서로 다른 (2개 이상의) 여러 테이블로부터 데이터를 가져오는 것
     >
     > 
     >
     > :: 하나의 테이블로부터도 데이터를 가져올 수 있다! - Self Join
     >
     > :: Join을 반드시 여러 테이블로만 하는 것은 아니다.
     >
     > 
     >
     > :: WHERE절에 Join 조건 단다.
     > 그래서 비조인조건, 조인조건 잘 구분해야한다. 사진 맨 위 3)번 문제랑 관련 

     ![20210325_155209](https://user-images.githubusercontent.com/78403443/112450621-e961a200-8d97-11eb-85ce-5eb9a45b3ca5.png)


     
