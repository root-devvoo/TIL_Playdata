**오늘 할 내용**

![image](https://user-images.githubusercontent.com/78403443/115686790-895d1c00-a394-11eb-9b0c-0bed080ab62e.png)

---

**web36_Transaction 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/115687260-f670b180-a394-11eb-8bba-d29eb25da42d.png)

![image](https://user-images.githubusercontent.com/78403443/115687295-ff618300-a394-11eb-9b60-a4793121664c.png)

MySQL에서 Transaction을 실습하려면 자동커밋 해제해야한다. 

1은 자동커밋되고 있다는 얘기이므로 해제해야한다.



![image](https://user-images.githubusercontent.com/78403443/115687365-0daf9f00-a395-11eb-8811-ca19984fd02c.png)

transaction 실습은

rollback, commit 직접 실행해보는 실습을 해보는 것이다.

직접 해보고 코드로도 실습해본다.



트랜잭션 기본 기능은 rollback, commit, set autocommit이 전부다

![image](https://user-images.githubusercontent.com/78403443/115687431-20c26f00-a395-11eb-8eb1-f7ab35621e60.png)

smith의 급여를 800 에서 2100으로 수정해본다(update 진행)



![image](https://user-images.githubusercontent.com/78403443/115687472-2ae46d80-a395-11eb-8326-96c508ebe9b9.png)

다른(우측) 사용자 측에서 SMITH의 급여를 수정한 것이 반영되지 않았다.

이 얘긴, 별도의 임시저장소에서 수정되었다는 얘기

완벽하게 반영을 하려면 commit을 시켜줘야한다. 

해당 (좌측) 사용자 측에서만 보여주는 것이지 영구적으로 반영된 것이 아니다.



![image](https://user-images.githubusercontent.com/78403443/115687540-3df73d80-a395-11eb-83e0-30a0488f8f12.png)

![image](https://user-images.githubusercontent.com/78403443/115687580-48193c00-a395-11eb-8a33-bb6a96d6ce76.png)

![image](https://user-images.githubusercontent.com/78403443/115687616-536c6780-a395-11eb-8b74-51a4f0ccd84c.png)

다른(좌측) 곳에서 3000으로 바꿔서 설정했지만.. 커서가 깜박거리기만 한다. 

Lock 이 걸려서 그렇다. 

rollback이나 commit을 하면 락이 풀린다. 

다른(우측) 사용자 측에서 rollback을 하면 2100으로 돌아간다. 

다른(우측) 사용자 측에서 commit을 하면 1800으로 돌아간다.



![image](https://user-images.githubusercontent.com/78403443/115687664-60895680-a395-11eb-9a87-0d5e8aba20f2.png)

rollback하는 순간 좌측 사용자 측에서 업데이트됨.



![image](https://user-images.githubusercontent.com/78403443/115687722-6d0daf00-a395-11eb-8c0f-fb9d1a405c91.png)

우측 사용자쪽에서 rollback을 하였기 때문에 우측은 2100으로 돌아갔고

좌측에서는 lock 걸렸던 3000 업데이트 쿼리문이 실행되서 3000이 보여진다.



---

**CTAS**

![image](https://user-images.githubusercontent.com/78403443/115687815-8151ac00-a395-11eb-80eb-46c5ede869bf.png)

![image](https://user-images.githubusercontent.com/78403443/115687843-8a427d80-a395-11eb-837e-6c295c4bae38.png)

사람들이 가장 놓치는 것이 TRUNCATE



DELETE 와 TRUNCATE 

공통점: 데이터는 삭제 + 구조는 남김

차이점: Rollback, TRUNCATE는 자동 commit



DROP은 데이터와 구조 다 날린다.



DELETE는 전체 삭제할때 쓰면 안된다. 

전체 삭제할 때 쓰는 것은 TRUNCATE 구조는 안날린다.

구조까지 날리는 것은 DROP



![image](https://user-images.githubusercontent.com/78403443/115687927-9e867a80-a395-11eb-9560-5e0b1ab8660c.png)

auto_increment == 자동증가하는 기능

내가 넣어주지 않아도 자동증가 숫자

무조건 num은 pk로 지정해야한다.



**web36_Transaction 프로젝트**

- TXAppTest1.java 파일 보기

![image](https://user-images.githubusercontent.com/78403443/115687975-acd49680-a395-11eb-973c-428977cfb7e1.png)

![image](https://user-images.githubusercontent.com/78403443/115688006-b4943b00-a395-11eb-8c16-fead74e36449.png)

![image](https://user-images.githubusercontent.com/78403443/115688039-bcec7600-a395-11eb-91ee-20b3b8f41ecb.png)

rollback 하면 setAutoCommit(false)로 가고, 커밋하면 true로 간다.



- 계좌이체 시나리오를 만들어본다.

![image](https://user-images.githubusercontent.com/78403443/115688101-ca096500-a395-11eb-9810-abc45cb62893.png)

---

---

**분석함수**

![image](https://user-images.githubusercontent.com/78403443/115688156-d8578100-a395-11eb-9d30-842bdc2cf15d.png)

긁어서 사용해보면서 공부하기...



ntile: 설정한 등급별로 알아서 알맞게 나눠줌

![image](https://user-images.githubusercontent.com/78403443/115688203-e4dbd980-a395-11eb-9180-809c57b31caf.png)

---

---

**web37_DBModeling 프로젝트**

![image](https://user-images.githubusercontent.com/78403443/115688267-f7eea980-a395-11eb-908f-2f403d0b39e3.png)

- DB모델링

- - \1. 개념 설계 === Entity 추출
  - \2. 논리 설계 === 0) Entity 관계, 1) 기본키, 일반키, 2) 정규화
  - \3. 물리 설계 === Table 작성



version1, DB 설계 → CODE 수정, 개발, 문제발견

→ version2 ... (반복)



하지만 version은 3개 이상 넘어버리면 안된다. 

그건 설계단계에서 이미 잘못했다는 것... 



1. 개념설계... eXERD

2. 1. 먼저 각 테이블과 각 테이블의 기본키를 설정
   2. association을 구분하기 위한 pk를 줄 필요가 있다. === 유지보수 용이

![Geha1](https://user-images.githubusercontent.com/78403443/115688423-1eace000-a396-11eb-8bcf-5020bedbe267.png)

2. 논리설계

![Geha2](https://user-images.githubusercontent.com/78403443/115688557-3ab08180-a396-11eb-838c-8a7e9885b261.png)

![Geha3](https://user-images.githubusercontent.com/78403443/115688614-43a15300-a396-11eb-940e-a8c405528105.png)

논리설계의 가장 마지막은 정규화이다.



- DB모델링 정규화

![image](https://user-images.githubusercontent.com/78403443/115688683-53b93280-a396-11eb-8001-facd3a9f007b.png)

정규화는 메모리를 잘게 쪼개는 것이다. 

장점: 메모리를 절약할 수 있고, 유지보수가 편함

단점: JOIN을 많이 걸면 질의 응답속도가 늦어지고, 쿼리문이 복잡해진다.



- 정규화를 적용하기 전

![image](https://user-images.githubusercontent.com/78403443/115688751-6469a880-a396-11eb-9cb0-71e0094c3026.png)

정규화를 안했을 때 가장 큰 문제점.

회사가 이전하거나 정보변경시 만약 1만명 → 1만번을 변경해야함. 가장 큰 문제점...



![image](https://user-images.githubusercontent.com/78403443/115688792-6fbcd400-a396-11eb-816b-c76942def923.png)

정규화 했을 때 

정규화 foreign key 갖고 있는 상황에서 큰 문제점... 

삭제가 안된다. 부모 테이블이 기본키로 갖고 있는 외래키는 삭제가 안됨

그래서,

![image](https://user-images.githubusercontent.com/78403443/115688854-7e0af000-a396-11eb-92a3-fb30542b2184.png)

자식을 먼저 지워야한다. on DELETE CASCADE SET null



**정규화**

- 1차 정규화 위배

- - "반복되는 속성을 찾아낸다"
  - 해결책 :: 새로운 엔터티 추가

![image](https://user-images.githubusercontent.com/78403443/115688915-8cf1a280-a396-11eb-9672-31c413fa5603.png)

제품에 대한 엔터티가 하나 더 나와야하고

창고에 대한 엔터티가 나와야 한다.



![image](https://user-images.githubusercontent.com/78403443/115688966-9844ce00-a396-11eb-891f-0131505504a3.png)

1차 정규화 위배된 것을 해결했다.



- 2차 정규화 위배

- - pk에 종속적이지 않은 일반 속성을 걸러낸다.

![image](https://user-images.githubusercontent.com/78403443/115689022-a7c41700-a396-11eb-9c96-eb0175a29411.png)

Non key 영역 → 일반속성을 걸러내야한다.



- 3차 정규화 위배

- - Non key 영역에서 서로 종속적인 관계를 찾는다.

![image](https://user-images.githubusercontent.com/78403443/115689080-b4e10600-a396-11eb-84e1-4e8e76138065.png)

주문자번호와 주문번호가 겹친다.

주문자번호가 다른 non key와 서로 종속적인 관계

![image](https://user-images.githubusercontent.com/78403443/115689261-de9a2d00-a396-11eb-9a84-b122a03e8640.png)

너무 많으면 JOIN 시 어려움이 발생하므로, 3차까지만 한다.  

1차, 2차, 3차 정규화



1. 반복되는 속성을 찾아서 Entity 로 분리 추출
2. 기본key에 종속적이지 않는 속성 분리
3. Non key 종속관계인 속성 제거

![image](https://user-images.githubusercontent.com/78403443/115689326-ed80df80-a396-11eb-9821-03e46a21ff6b.png)

![image](https://user-images.githubusercontent.com/78403443/115689355-f5408400-a396-11eb-8f8f-132b105ea83c.png)

