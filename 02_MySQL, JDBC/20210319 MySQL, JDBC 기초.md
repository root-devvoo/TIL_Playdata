**3/17 ~ 18 학습노트 내용 - 간단하게 작성...**

※ JDBC 4단계 (java.sql)
  1) Driver Loader - Class.forName(FQCN)
  2) DB 서버 연결  - conn = DriverManager.getConnection(url, user, pass);
  3) PreparedStatement ps = conn.PrepareStatement
  4) Query문 실행
    - ps.executeQuery() : Select 쿼리문 실행일 때 - Select(Query) - return type ResultSet >> 3월 18일자 에버노트에 참고하기<br>
    - ps.executeUpdate() : DML 쿼리문일때 사용 (쿼리문이 Insert, Delete, Update 일 때!)

※ Project시 작업 순서
  1. 사용자 입장에서 System 활용도 분석 ☞ 설계
    1) 시나리오 도출
    2) 요구사항 명세서 작성 (SRS 문서)
    3) UseCase Diagram

  2. DB모델링 
    1)개념적 단계 - Entity 추출
    2)논리적 단계 - 기본, 일반 속성 추출 + 정규화
    3)물리적 단계 - 실제 Table 작성

  3. VO 클래스 작성
    - 이때 컬럼명 == 필드명 확인한다!

  4. Business Logic 의 Template ☞ DAO Interface 작성

------------------------------------------------------------------------------------------------------------------------------------

※ MySQL
  - 외래키를 가지는 쪽이 자식 Table...
  - 
  - Entity 관계 모델
   - Row(행) 열이 교차되는 지점 = Field
   - Null은 나름의 의미를 가진다
    1) 미확정
    2) 자격 없음
   
------------------------------------------------------------------------------------------------------------------------------------

**3/19 학습노트 내용**

**MySQL 기본 SQL문장 작성 방법**
![20210319_120043](https://user-images.githubusercontent.com/78403443/111774980-841f3400-88f3-11eb-8d0c-097d75d15c0f.png)

- SELECT문 (★중요) 
  - 조건을 어떻게 다는지에 따라 다양하게 쓰인다. 
  - Displaye... 다시 리턴

※ JDBC 프로젝트 제작 과정 (★중요)
  0. 사용자 입장에서 System 활용도 분석 >>> Usecase Diagram
  1. DB Server >> (DB 모델링) Table생성 == Entity 추출 
  2. VO 클래스 작성
  3. DAO Template 작성 - DAO 인터페이스를 상속받아 DAOImpl 정의 
    - 사용자적 입장에서 해당 Project가 어떻게 사용되는지 이해하고 정의해야한다!
  4. Test클래스에서 기능들 실행

 - 지금부터는 그냥 설계 안된다.
 - 사용자적 DAO, Usecase Diagram 그리고.. 설계하기
 - Product 만들기 전에 사용자적 관점에서 어떻게 사용하는지를 모색, 분석, 설계 >>> 구현, 개발 (★제일 중요) 
 - 따라서, 프로젝트 할 때 Usecase Diagram, Class Diagram 반드시 있어야 한다. (★중요)

※ Usecase Diagram (jdbc04_프로젝트 파일 확인하기)
  1) Actor == 사용자
  2) Usecase 기능 표시
  3) Relation(관계선 폴더) 4개

    - Relation 
      - Relation 선으로 Actor와 제품의 가장 중심적인 기능과 관계 맺어준다
    - include 
      - 우선순위(우선적인 기능 관계표시할 때 사용)
    - Extend 
      - 기능을 세분화 할 때 Extend 선으로 그려준다
    - Generalization 
      - Actor들간의 관계 표시할 때 사용 
  
  - Usecase Diagram은 기능별로 나눠 그려야한다.

  (★중요) JDBC 기능구현 할 때 Connection을 필드에서 선언하면 안되고 각 메소드마다 잡아줘야한다.
