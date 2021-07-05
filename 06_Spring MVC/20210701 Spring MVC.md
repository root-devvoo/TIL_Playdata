오늘 할 내용 ::

JOIN을 MyBatis로 어떻게 쓰는지 

<br/>

---

- **sp11_PhoneTest 프로젝트 보기**

![image](https://user-images.githubusercontent.com/78403443/124070139-4eecbb00-da78-11eb-87ca-c5c8892f1125.png)

vcode == 회사 코드 (10: 삼성, 20: 엘지, 30: 애플)

<br/>

vo는 com.encore.pms.dto 패키지에 있다. (Hasing 관계)

<br/>

- src/main/resources mybatis 패키지... SqlMapConfig.xml 파일 작성

<br/>

- web.xml 파일

![image](https://user-images.githubusercontent.com/78403443/124070199-66c43f00-da78-11eb-89ec-898a17142e87.png)

<br/>

- application-config.xml 파일

![image](https://user-images.githubusercontent.com/78403443/124070254-7cd1ff80-da78-11eb-9a2e-a1170f3da091.png)

<br/>

- mvc-config.xml 은 주문서...

이 주문서를 보고 만들게 된다.

<br/>

- phone_query.xml 파일

JOIN 이용... SELECT문 동적쿼리 작성

CRUD...

<br/>

단위테스트까지 다 끝나면 MyBatis 부분 끝

<br/>

- Presentation layer 부분 작성
- com.encore.pms.dao 패키지 IPhoneDAO 작성

phone_query.xml 파일 보기

![image](https://user-images.githubusercontent.com/78403443/124070298-8fe4cf80-da78-11eb-93c0-52401a90bd63.png)

함수이름은 달라야하기 때문에 selectAll(), selectOne(), login(), selectUser()

이렇게 나올 수 밖에 없다.

이렇게 일일히 쓰면 가독성이 떨어질 수 밖에 없다.

이럴 때 Overloading을 쓰는게 좋다.

하는 일은 똑같다. select 하는건 다 똑같다.

<br/>

Dynamic 쿼리에서는 id 하나당 매핑이 안된다.

그래서 Overloading기법 써야한다.

![image](https://user-images.githubusercontent.com/78403443/124070330-a12ddc00-da78-11eb-83f1-38dbe74dcc26.png)

<br/>

DAO와 service로 나눴다.

Impl을 만들 때 어떤 사람은 com.encore.pms.dao.impl로 하거나

패키지를 같게 하고 파일을 IPhoneDAO 이런식으로 I를 붙여서 한다.

지금 경우는 Interface의 I를 붙인 것임

<br/>

- PhoneDAOImpl 파일 작성

<br/>

![image](https://user-images.githubusercontent.com/78403443/124070370-b1de5200-da78-11eb-9d6f-d149cd293c46.png)

Service layer쪽도 작성

<br/>

- MainController 작성

![image](https://user-images.githubusercontent.com/78403443/124070400-c15d9b00-da78-11eb-9362-a7e207e4a614.png)

mvc-config.xml 파일 보기

![image](https://user-images.githubusercontent.com/78403443/124070429-cc183000-da78-11eb-90eb-4413c3a4671c.png)

이렇기 때문에... 바로 Login만 써주면 가는 것임

<br/>

- 다시 MainController 작성

<br/>

- PhoneList.jsp 작성

![image](https://user-images.githubusercontent.com/78403443/124070490-dd613c80-da78-11eb-9ecc-141fb8cb47bb.png)

다른 테이블인 company테이블에 있는 vendor(제조사)를 가져오려면 phone.company.vendor 를 해야한다.

![image](https://user-images.githubusercontent.com/78403443/124070523-ea7e2b80-da78-11eb-8ed6-0a081f14ba4f.png)

잘 나옴

- 다시 MainController 작성

<br/>

- PhoneList.jsp 작성
- 다시 MainController 가서 a태그는 무조건 get방식이므로 GetMapping("detail.do")
