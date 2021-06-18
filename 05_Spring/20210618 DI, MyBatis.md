**DI** (어제에 이어서...)

우리가 만든 Dice 구조

![image](https://user-images.githubusercontent.com/78403443/122534786-d4767100-d05d-11eb-9b78-86b8a49578c2.png)

빨간박스는 재사용성을 보기 위해 결합시킨 부분...

그렇기 때문에, 나중에는 Player02를 Player한테 상속받아서 구현해서 연결해야한다.

<br/>

Player02만 있는 경우...

Property는 setter()에서만 받아온다.

빨간 부분이 변경되면 Player02의 로직도 바뀌어야하는데

변경에 있어서 무조건 바꿔야 하는게 setter와 getter이다. (여러개 있을 것이다)

코드에 있어서 무조건 가장 필요한게 setter와 getter인데

나중에는 재사용을 가장 방해하는 옵션이 된다.

![image](https://user-images.githubusercontent.com/78403443/122534859-eb1cc800-d05d-11eb-87ae-b53c3b6b47c1.png)

결론 :: 이렇게 직접적으로 연결을 맺으면 안된다.

그럼 어떻게 연결을 맺냐?

방법은 하나밖에 없다. 

Interface로 Dice와 Player02를 연결시킨다.

이걸 갖다가 Loose한 Coupling (느슨한 Hasing)이라고 한다.

이렇게 느슨하게 하면 재사용성이 올라간다. 

Player02가 Dice dice; 만 상대하면 된다. 

그렇다는 얘기는 Dice 하나만 넣으면 된다.

setDice(), getDice() 하나씩만으로 끝난다

![image](https://user-images.githubusercontent.com/78403443/122534901-f53ec680-d05d-11eb-8c7f-a8bad5580a50.png)

그런데 문제는 Player02를 또 가져다 쓰는 코드가 있을 것이다.

Test 클래스

여기선 진짜 가져다 써야된다.

setDice 얘를 가져다 써야되는데, 이때 new가 나올 수 밖에 없다.

Impl뒤에는 실체클래스가 노출되어야 할 수 밖에 없다.

결론은 :: 이 코드가 안나오게 하려면... Interface로도 해결 안된다.

뭘해야하냐? IoC(제어의 역전)해야한다. 

이건 다시 말해서 "객체 생성의 주체를 바꾼다" Container에게

<br/>

그럼 여기서 Container

- WAS == 요청이 들어온 것을 바탕으로 Servlet Request, Servlet Config 등등 다 알아서 만든다.

  - 이게 IoC이다.

- BeanFactory == 이게 DI Container

  - 이것도 Container
  - 하지만, WAS처럼 자동적으로 다 만들지 않는다.

- 결론적으로는, 여기서 Container는 Factory이다!, 이렇게 해결했다

<br/>

결론 :: 앞으로,

![image](https://user-images.githubusercontent.com/78403443/122534991-0f78a480-d05e-11eb-9c41-1dd0e50a0eec.png)

1. 빈 설정문서 ~.xml 정확하게 만들고 이해할 수 있어야한다.

   - 만들 때 코드를 잘 보면서 만들어야한다.

   - ① 코드에서 주입의 통로를 확인

   - ② 코드에서 입력되는 값이 단순한 값인지 객체인지 파악해야함

     - 단순 값일 때 : value
     - 객체 일 때 : ref 

   - 코드 정의 Bean

     - API Bean
     - User Definition Bean (사용자 정의 빈)

2. 그리고

   - Code(test코드) 절대로 실체 클래스 이름이 노출되지 않는다! (재사용성 떨어지니까)
   - Bean Configuration File : 반면에 빈 설정문서에서는 무조건 실체 클래스만 정의됨

<br/>

이 두 가지를 꼭 기억해야함!

어제 딱 여기까지 살펴봤었다!

<br/>

Package 계층 구조는 강사님이 잡아주신 패키지명들 보면서 감 익히면 된다.

값 주입 통로는

- 생성자
- Setter

이거, 전에 자바할 때 자동차와 엔진, 자동차와 네비게이션 비유를 가지고 얘기하신 적이 있다.

엔진은 생성자로 주입한다.

네비게이션은 setter로 주입한다.

<br/>

자동차의 생성과 사망을 같이 할 때(자동차가 만들어질 떄 같이 만들어지고, 폐차할 때 같이 없어지는)

이런 것들은 생성자 주입해야한다.

하지만, 네비게이션은 아니기 때문에(네비게이션 없다고 자동차 폐차 안함)

네비게이션은 setter로 주입한다. 

이게 Life Cycle이다.

<br/>

setter로 주입하는거 거의 80%이상 사용 (setter로 훨씬 더 많이 사용한다)

이게 더 명료한 면이 있다.

<br/>

하지만 생성자를 쓰던 setter를 쓰던 거의 자유롭다.

<br/>

---

sp02_SpringDI 프로젝트

빈 설정 문서 만들기.. 좀 더 구체적으로 들어가본다 

![image](https://user-images.githubusercontent.com/78403443/122535485-94fc5480-d05e-11eb-9dcb-0616980f334b.png)

강사님이 주신 파일들 패키지로 배포했다.

![image](https://user-images.githubusercontent.com/78403443/122535514-9e85bc80-d05e-11eb-9532-76758e0b8bb5.png)

getBean은 서비스를 요청하는 것과 같다.

<br/>

빈 설정문서 만든다.

![image](https://user-images.githubusercontent.com/78403443/122535587-ab0a1500-d05e-11eb-94c2-67960d6deb68.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122535629-b4937d00-d05e-11eb-876f-df94c480ccd0.png)

두번째 빨간 박스 표시되있는 기본생성자를 주석으로 막고(사진상에는 주석처리 안되어있음)

실행 클래스파일을 돌렸더니 에러가 떴다.

Framework에서 기본 생성자가 무조건 있어야 한다!!!

<br/>

![image](https://user-images.githubusercontent.com/78403443/122535837-e1479480-d05e-11eb-91cd-e1d80b91d2ba.png)

UserTest 파일 : "빈의 서비스를 요청하는 입장" Client라 보면됨

<br/>

Ⅰ이 진행되어야지<br>Ⅱ가 진행된다.

<br/>

그리고 빈을 달라고 Test가 서비스 요청을 할 수 있다.

그러면 Factory에서 빈이 언제 생성되는가? 를 알아야함.

<br/>

Factory가 먼저 준비된 상태에서 클라이언트 요청을 받아야 한다.

다시 말해서, Factory의 준비상태 확인!

확인해보자

![image](https://user-images.githubusercontent.com/78403443/122535961-076d3480-d05f-11eb-93ba-85c24ecf3090.png)

확인하기 위해서 일부러 sysout으로 달아놨고

![image](https://user-images.githubusercontent.com/78403443/122536123-2b307a80-d05f-11eb-80e5-e2756d3bad32.png)

1. 밑에 출력되었다.

   그 말은 빈 생성이 ==== 다음이다.

2. 빈 기본 생성자가 무조건 생성

<br/>

====다음이 의미하는 바는?

Factory에서 빈이 생성되는 시점?

<br/>

지금 코드를 봤을 때 

![image](https://user-images.githubusercontent.com/78403443/122536203-3f747780-d05f-11eb-8a63-9f32c086c842.png)

19라인 :: 공장 생성 → 주문서 읽어들일 때 생성된다.

31라인 → getBean()할 때 빈이 생성

getBean은 빈을 줘! 라는 얘기임

다시 말해서 서비스를 요청할 때 공장에서 빈을 생성한다(만든다)

<br/>

원래는 19라인에서 공장생성해서 미리 빈을 만들어야되는데...

지금은 클라이언트가 요청해야지만 공장에서 빈을 만든다.

이것을 Lazy Loading이라고 한다. (분홍색 박스)

Factory는 Lazy Loading으로 돌아갈 수 있다. 그렇게 돌아가면 안된다.

그럼 앞에껀(연두색)은 Pre Loading이라고 한다.

<br/>

우리는 Pre Loading을 해야한다.

<br/>

예전에 Pre Loading할 때 옵션 넣는 것이 있었다.

```
web.xml에서 annotation해서 썼던 <load-on-startup> 
```

로드 온 스타트업 같은 것이다!

<br/>

그래서 이제 이렇게 안쓸 것이다.

![image](https://user-images.githubusercontent.com/78403443/122536268-53b87480-d05f-11eb-9ee8-59a797e0232e.png)

19, 20라인은 주석으로 막고

28라인 주석을 풀어서 사용하도록 했다.

<br/>

BeanFactory의 자식 중에

ApplicationContext라는 자식이 있다. (얘도 인터페이스다)

얘 자식 중에 우리는 지금 ClasspathXmlApplication을 쓰고있다.

얘네들의 계보는 Pre Loading이다.

그리고, ClasspathXmlApplication는 File system이 아닌 ClassPathSystem이 기반이다.

ClassPathSystem쓰는 애들은 Classpath라고 이름이 앞에 붙는다

Classpath는 무조건 클래스가 src 하위에 들어가기 때문에, 디폴트로 아예 잡혀져있다.

src로 그냥 인식하고 들어간다. 그래서 따로 붙여줄 필요가 없다.

그래서 config부터 경로를 진행해주면 된다.

<br/>

앞으로는 얘를 쓰겠다는 얘기이다.

<br/>

이렇게 바꿔서 다시 돌려본다!

![image](https://user-images.githubusercontent.com/78403443/122536348-63d05400-d05f-11eb-84c4-1019d2b190ec.png)

readyojn 상태를 만들었기 때문에 getBean() 하기 전에 

즉, client가 서비스를 요청하기 전 이미 Factory에서 Bean을 생성, 보관하고 있다는 것을 알 수 있다.

"Pre Loading" 은

```
 우리가 전에 썼었던 <load-on-startup>
```

과 동일한 부분(개념)이다.

<br/>

이렇게 구동하는게 ApplicationContext다. 앞으로 얘 쓸거다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122536682-c1fd3700-d05f-11eb-9022-e24f01c117db.png)

![image](https://user-images.githubusercontent.com/78403443/122536709-c9244500-d05f-11eb-98f8-b7622a69246f.png)

user03은 주입이 안되어있기 때문에 각각 기본값으로 나왔다는 것을 알 수 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122536754-d6413400-d05f-11eb-8e5c-9264d75fccc7.png)

생성자 두개짜리가 있으니까 이렇게 하는 것

![image](https://user-images.githubusercontent.com/78403443/122536788-df320580-d05f-11eb-83c4-e165430de366.png)

그런데 다행히도 앞에가 age고 뒤에가 user다

![image](https://user-images.githubusercontent.com/78403443/122536848-ee18b800-d05f-11eb-83f0-f704a1ea981c.png)

잘 나온다 .

근데...

![image](https://user-images.githubusercontent.com/78403443/122536902-fa9d1080-d05f-11eb-8a96-4d2c4e40f7fa.png)

만약에 바꾼다면...?

타입이 안맞으니까 에러가 날 것이다.

(타입이 같으면 앞뒤가 바뀌어서 나옴... 이것도 잘 봐야한다)

![image](https://user-images.githubusercontent.com/78403443/122536934-04bf0f00-d060-11eb-9a7c-bbfca9895774.png)

타입 안맞으니까 에러남

이게 생성자 주입에 굉장히 골치아픈 부분

여러개의 인자값을 생성자로 주입할 경우 순서 갯수 타입을 정확하게 지켜줘야 하기 때문에 setter주입에 비해서 다소 까다로운 측면이 생긴다.

<br/>

순서를 바꿔놓고 에러를 안나게 하려면 어떻게 해결할 수 있을까?

위와 같이 index라는 옵션을 주면된다.

![image](https://user-images.githubusercontent.com/78403443/122537003-17d1df00-d060-11eb-99ce-c4aa9559dd8e.png)

잘 나왔다. 

어쨋든 생성자가 setter보다 이런 부분에서 불편...

그래서 setter를 많이 쓰는 것이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122537051-23bda100-d060-11eb-883d-ae0c76bdf600.png)

생성자로 넣을 떄는 이런 서브 옵션을 넣어주는게 중요하다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122537098-2ddf9f80-d060-11eb-8d91-eda38660cad6.png)

섞어쓸 수도 있다.

하지만 인덱스 옵션을 써주는게 훨씬 더 정확하고 낫다. 

![image](https://user-images.githubusercontent.com/78403443/122537137-3932cb00-d060-11eb-91b2-47da9afca491.png)

이렇게!

<br/>

여기까지 DI 를 배웠다.

![image](https://user-images.githubusercontent.com/78403443/122537168-4485f680-d060-11eb-8bb7-df09bbdfb39c.png)

코어 스프링 :: 6개의 라이브러리를 Build Path로 잡아서 사용했었다.

이제 이게 끝났다.

<br/>

이와 별개로 Data Access 부분을 프레임워크로 따로 이제부터 다룬다.

(Spring JDBC는 일본이 많이 씀.. 우리는 안쓴다)

우리는 이  Data Access 자리에 한국에서 많이 쓰는 MyBatis를 끼워넣는다.

<br/>

그리고 나중에는 코어 스프링과 연결

<br/>

---

---

두번째로 넘어간다.

- **MyBatis (마이 바티스)**

<br/>

![image](https://user-images.githubusercontent.com/78403443/122537532-9cbcf880-d060-11eb-8eee-d573e1a7b02c.png)

살살 다뤄보면서 시작하기 위해서 sample...

<br/>

![image](https://user-images.githubusercontent.com/78403443/122537592-ac3c4180-d060-11eb-8659-8b0cad91ec4a.png)

이 파일 두개는...

![image](https://user-images.githubusercontent.com/78403443/122537700-caa23d00-d060-11eb-8331-8aaf44c51b7c.png)

https://blog.mybatis.org/p/products.html 여기서 다운 받았다. (첫번째 파일이 이것)

MyBatis는 굉장히 경량 프레임워크이다.

그래서 어떤 사람은 이걸 프레임워크라고 하지 않고 SQL Mapper라고 얘기한다.

<br/>

어쨋든, 우리는 얘를 가지고 DB부분 완벽하게 돌려놓고

DI랑 나중에 배울 Spring MVC랑 연결할거라고 했는데

Spring MVC랑 연결할 때는

![image](https://user-images.githubusercontent.com/78403443/122537799-e4dc1b00-d060-11eb-9b65-cdce4b3f546c.png)

이것이 반드시 필요한데

이게 두번째 파일이다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122537860-f45b6400-d060-11eb-868c-3c144eb287f4.png)

https://mybatis.org/mybatis-3/

API를 한국어로 만들어놓은 사이트는 유일하게 MyBatis가 있다.

MyBatis는 IBatis라는걸로 먼저 시작했다. 

영어 말고 제일 먼저 나온게 한국어인데...

이 배경은 IBatis가 나오자마자 한국에 있는 개발자들이 전세계적으로 유일하게

엄청나게 끌어다 썼다. (초창기에)

그래서 IBatis 사이트에서 한국어를 번역한 API문서를 먼저 올리기 시작했다.

한국 개발자들의 지대한 관심을 받았던게 IBatis고, MyBatis로 바뀌게 된 것이다.

MyBatis 3버전 우리가 쓸 것이다.

<br/>

여기에 MyBatis 기술 어떻게 사용하는지에 대해서 쫙 나와있다.

<br/>

MyBatis는 경량 프레임워크 시중에 책이 많이 나와있는데

책을 사서 볼 필요없이... 여기 사이트에 다 나와있으니까 여기서 보면 된다.

<br/>

[MyBatis-3-User-Guide_ko.pdf](https://github.com/iceman-brandon/TIL/files/6676004/MyBatis-3-User-Guide_ko.pdf)<br>

이 PDF파일이 바로 MyBatis 한국어 번역본 API문서이다.

<br/>

pdf 12 페이지보기

![image](https://user-images.githubusercontent.com/78403443/122538756-d6423380-d061-11eb-8330-63304c0c4dd5.png)

DI 할 때도 이런식으로 소문자로 alias를 붙이는게 좋은데 그게 안되서 index로 그냥 하라고 했다.

타입명을 소문자 alias로 가는게 보통의 규칙임... 어쨋든 그래서 이렇게 소문자로 따라가는게 좋다.

<br/>

어제 처럼... 라이브러리 추가

진짜 좋은 이름은 mybatis 설치 파일명 그대로 쓰는게 좋다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122538816-e4904f80-d061-11eb-8e69-531d6957fc4b.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122538849-ee19b780-d061-11eb-8d7e-86d8e3459b05.png)

이렇게..

<br/>

이제 MyBatis 어떻게 사용해서 만드는지 차근차근 살펴본다.

![image](https://user-images.githubusercontent.com/78403443/122538885-fa057980-d061-11eb-9a0b-a68d60197eba.png)

이렇게 먼저 테이블을 만들 것이다.

![image](https://user-images.githubusercontent.com/78403443/122538915-02f64b00-d062-11eb-909f-e65329ed31f2.png)

그리고 VO를 생성한다.

![image](https://user-images.githubusercontent.com/78403443/122538953-0c7fb300-d062-11eb-9051-0a9cd213ab6a.png)

<br/>

MyBatis가 무엇인가?

![image](https://user-images.githubusercontent.com/78403443/122539000-173a4800-d062-11eb-8e92-10ab88497854.png)

퍼시스턴스(Persistence) 프레임워크!

<br/>

![image](https://user-images.githubusercontent.com/78403443/122539186-4781e680-d062-11eb-9891-abb40374f058.png)

DB서버에 대한 파편적인 정보를 저장하는 메타데이터이다! (위 이미지)

![image](https://user-images.githubusercontent.com/78403443/122539281-62ecf180-d062-11eb-9aa9-9f7eabdaea84.png)

선택

![image](https://user-images.githubusercontent.com/78403443/122539318-6da78680-d062-11eb-802d-8fd2e6a2c21a.png)

앞으로 계속 이런 이름으로 간다.

<br/>

pdf 5페이지

![image](https://user-images.githubusercontent.com/78403443/122539373-7dbf6600-d062-11eb-9b60-67ba0f26fa4c.png)

XML 설정파일이라고 나오는데...

이게 SqlMapConfig 파일이다.

이게 MyBatis 기술 핵심문서이다. 

이걸 써야한다.

![image](https://user-images.githubusercontent.com/78403443/122539412-8b74eb80-d062-11eb-8d5d-3852347c64ef.png)

이렇게 하고 디비정보에 대한 것을 Wiring(와이어링)해야한다. (문서끼리는 Wiring이라고 한다)

![image](https://user-images.githubusercontent.com/78403443/122539443-9596ea00-d062-11eb-9d1a-c737a8605449.png)

(클래스 사이에서는 Hasing...)

클래스가 아니라 문서끼리(그냥 파일끼리)

오른쪽 문서가 왼쪽 문서의 정보를 필요로 한다. 그래서 갖다 쓴다.

이런걸 wiring(연결)이라고 한다.

클래스는 Has a relation이라고 하고

문서는 Has 라고 안하고 wiring이라고 한다.

![image](https://user-images.githubusercontent.com/78403443/122539492-a0517f00-d062-11eb-95f5-2b9a27bc61d1.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122539536-ac3d4100-d062-11eb-88c9-515626e11bae.png)

wiring 하는 옵션 == resource

<br/>

![image](https://user-images.githubusercontent.com/78403443/122539587-b8290300-d062-11eb-8078-933c78946d35.png)

복수태그로 끝나는 그 밑에는 무조건 단수 태그가 온다.

![image](https://user-images.githubusercontent.com/78403443/122539617-c119d480-d062-11eb-9105-a239b6371822.png)

단수 태그가 왔고, 단수 태그 안에

이렇게 긴 type명을 짧게 부르는걸 alias 옵션을 이용해 정의해준다.

mySawon으로

![image](https://user-images.githubusercontent.com/78403443/122539735-e1e22a00-d062-11eb-99fd-3f988a306a76.png)

알리야스는 무조건 이렇게 규칙을 따른다. 맨 앞은 소문자... vo클래스명과 같도록

![image](https://user-images.githubusercontent.com/78403443/122539851-05a57000-d063-11eb-855e-877f14bdd740.png)

default는 반드시 넣어야한다. id와 반드시 같은 값을 넣어야한다.

의미는 없어도 된다. 그래도 조금 연관성있게 넣어주는게 좋겠다.

그리고 JDBC 환경 구축이기 때문에 transactionManager 태그에 type="JDBC"로 넣어주면 된다.

![image](https://user-images.githubusercontent.com/78403443/122539910-1524b900-d063-11eb-879d-9f5bb86d0fa2.png)

dataSource는 미리 Connection을 가지고 있는 Resource Factory...

그게 Datasource...

![image](https://user-images.githubusercontent.com/78403443/122540035-31c0f100-d063-11eb-8c41-b7cad5d628e0.png)

UNPOOLED 하게 되면 메인에서 돌리는 DriverManager 방식이다. 

원래는 POOLED 해야된다. (서버에서 돌림)

하지만 우리는 서버로 돌리는게 아니기 때문에 UNPOOLED로 해준다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122540112-43a29400-d063-11eb-86af-a15fc968e26f.png)

단순파라미터는 Value로 넣는다.

![image](https://user-images.githubusercontent.com/78403443/122540147-4d2bfc00-d063-11eb-8588-6cdced4cb3e3.png)

EL문법으로 key를 넣으면 value를 받아온다.

이렇게 value를 간단하게 넣을 수 있도록 하기 위해 변수명 설정해줬다. (driver, url, username, password 등) 

이런것도 굉장히 중요하다.

<br/>

아무튼... 이렇게 환경구축 구현하기 위해서 위에서 wiring(와이어링)을 시킨 것이다.

![image](https://user-images.githubusercontent.com/78403443/122540183-587f2780-d063-11eb-8f19-1717cfcb6921.png)

DB와 DAO가 연결되는 부분이 Persisence 인스턴스 부분이다.

이쪽 부분을 효율적으로 연결하기 위해서 MyBatis 프레임워크를 쓰는 것이다.

1. DB정보 와이어링
2. Connection 받아온다
3. EL로 value값 넣어준 부분에서 vo의 값이 실려져서 나온다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/122540231-659c1680-d063-11eb-9a22-8e3e8313bc15.png)

그리고 이렇게 다른 xml파일을 매핑

다르다는 얘기는 다른 내용이 들어간다는 얘기(mysawon_mapping.xml)에

다르다는 얘기는 DOCTYPE도 다르다!

![image](https://user-images.githubusercontent.com/78403443/122540269-6f257e80-d063-11eb-9c7a-a7815f6da28b.png)

이렇게 바꿔주고

mapper 태그 자동완성해서 닫는 태그 까지 나온다면 성공!

<br/>

우리 DAO 작성할 때 전에 JDBC할 때는 10줄을 썼지만

MyBatis를 쓰면 10줄 썼던 코드가 1줄 정도로 확 줄 것이다.

![image](https://user-images.githubusercontent.com/78403443/122540478-a3993a80-d063-11eb-96f3-b540a49cc0a2.png)

매핑하는 기술이 MyBatis 기술의 핵심이기 때문

<br/>

![image](https://user-images.githubusercontent.com/78403443/122540511-aeec6600-d063-11eb-9524-e6af89f9d147.png)

parameterType는 아까 SqlMapConfig.xml파일에서 alias 줬던 mysawon이 들어갔다.

mybatis에서는 빨간 밑줄 친 형식으로 값이 들어간다!

<br/>

test파일 작성

![image](https://user-images.githubusercontent.com/78403443/122540580-bf9cdc00-d063-11eb-931f-fa26181d6704.png)

Resources밑줄 친 얘를 써야한다

다른 것들도 import 잘 봐야한다. (위와 같이 ibatis 밑에 있는걸 써야함)

<br/>

![image](https://user-images.githubusercontent.com/78403443/122540650-cb889e00-d063-11eb-84c8-268a57ee16c2.png)

작성 완료

<br/>

지금까지 했던 모든 내용을 다 포괄하는 그림 그려서 설명

![image](https://user-images.githubusercontent.com/78403443/122540692-d7746000-d063-11eb-9055-662c6829233e.png)

1. 가장 Back단에 DB가 있다. (우리는 Scott 계정을 사용하여 mysawon이란 테이블 만들어서 사용)

2. 테이블의 정보를 인스턴스 시킬 수 있는 vo객체를 만들었다. (이름은 테이블 이름과 동일하게 만들었다)

3. MyBatis에서 가장 핵심이 되는 설정문서

   - SqlMapConfig.xml
   - 왜 핵심이 되는 설정문서냐? 얘가 뭘 쥐고있는지 보면 된다.
   - dbconn.properties 파일을 wiring 하고 있기 때문이다.
   - vo에 대한 정보도 wiring하고 있다.
   - 그리고, 정말 결정적으로 모든 쿼리문을 담고(매핑하고) 있는 mysawon_mapping.xml도 연결되어있다.
   - 이 모든 정보를 다 가지고 있기 때문에 MyBatis에 가장 핵심이 되는 문서라고 하는 것이다.
   - 이 모든걸 다 가지고 있는 것을 누가 가져가?

     - 코드보면, SqlSessionFactoryBuilder라는 애가 있다. 얘가 가져감 (주입 == DI)
     - SqlSessionFactoryBuilder를 또 누가 가져가냐면 SqlSessionFactory가 가져간다 (주입 == DI)
     - SqlSessionFactory또 누가 가져가나면 SqlSession이 가져간다 (주입 == DI)
     - 그리고 SqlSession이 연결된다. DB 엑세스 한다는 말... 
       
       - insert(), delete(), update()
       - 하나 가지고 올 때 SelectOne()
       - 여러개 가져올 때 SelectList()

<br/>

이것을 모듈화한 프레임워크가 MyBatis고, 이게 Persistence 영역이다.

<br/>

그럼 DAO는 어떻게 될까?

![image](https://user-images.githubusercontent.com/78403443/122540773-ec50f380-d063-11eb-8a5d-310806692dc8.png)

DAO는 아예 언급 안했다. 

하지만, MySawonDAO를 만들거고 SqlSession과 연결할거다.

먼저 연두색 표시한 부분을 완전히 이해하고나서 이후에 DAO 만들어서 연결할 것이다.

<br/>

아무튼, 다시 test파일을 보자

![image](https://user-images.githubusercontent.com/78403443/122540837-fb37a600-d063-11eb-9d0c-dcaa9e0cb4ca.png)

어쨋든 순서는 이렇다

중요하게 볼 부분은 이것

![image](https://user-images.githubusercontent.com/78403443/122540879-0559a480-d064-11eb-9664-2b3aa0410236.png)

\#은 get을 의미하는 것이다.

<br/>

테이블안에 있는 데이터를 받아오는 것이다.

selectList()를 해서 다 받아온다. (어차피 하나 있기 때문에 하나만 나온다)

(selectOne()은 하나만 받아오는 것)

![image](https://user-images.githubusercontent.com/78403443/122540935-130f2a00-d064-11eb-8ec3-f181f4bef0ce.png)

이 쿼리문 돌릴 것임 SELECT * FROM mysawon

<br/>

![image](https://user-images.githubusercontent.com/78403443/122540970-1e625580-d064-11eb-9e39-3e52c372ff24.png)

resultType이 필요하다. 뭐가 들어갈까?

우리 비즈니스 로직 할 때 모든걸 다 받아오는거... 이 리턴타입이 ResultType에 해당되는 것이다.

ArrayList썼었으니까 ArrayList를 쓸건데

MyBatis는 ArrayList안에 들어가는 제너릭을 넣어야한다. 타입을...

그래서 mysawon 넣어준다.

<br/>

MySawonTestApp2.java파일에 방금 넣어준 SELECT 쿼리문 실행하는 테스트 구문을 작성해서 실행시켜볼 것이다.

![image](https://user-images.githubusercontent.com/78403443/122541028-2cb07180-d064-11eb-907a-c292ad9b1d54.png)

select 쿼리문

첫번째 :: selectList("namespace.id이름") ## 조건이 없는 것, 다 불러옴

두번째 :: selectList("namespace.id이름", XXX) ## 조건 있음, ex) 30번 부서 다 가져와라, 가져옴

![image](https://user-images.githubusercontent.com/78403443/122541078-376b0680-d064-11eb-83a2-141ab303a53d.png)

![image](https://user-images.githubusercontent.com/78403443/122541108-3e921480-d064-11eb-913b-1e8575d3e1f8.png)

ArrayList가 리턴타입이 아니기 때문에 List로 받아야한다. (java.util)

![image](https://user-images.githubusercontent.com/78403443/122541175-5073b780-d064-11eb-84f5-7d1ff0c153c7.png)

다 작성하고 잘 출력했다.

근데, 이제 약간 변형해서 모듈화 시킨다.

<br/>

FactoryService.java 파일 따로 만든다.

![image](https://user-images.githubusercontent.com/78403443/122541229-5f5a6a00-d064-11eb-954d-7d7d56e6d98a.png)

위위 이미지에 보이는 1, 2번을 여기다 옮긴다.

![image](https://user-images.githubusercontent.com/78403443/122541260-67b2a500-d064-11eb-8c5d-187861913bb5.png)

작성완료

MySawonTestApp3.java 파일을 만든다.

![image](https://user-images.githubusercontent.com/78403443/122541305-7305d080-d064-11eb-98aa-ce117545da7a.png)

만들어서 코드 작성해서 실행했다

SELECT문 잘 실행되어서 나왔다.

<br/>

이렇게 Factory를 따로빼서 Test를 돌리는 방법을 해보았다.

보통 이렇게 많이 쓴다.

<br/>

---

sp03_MyBatis_Sample 에서 다룬 내용을 바탕으로 

sp04_MyBatis_Team & sp04_MyBatis_Team_sol 프로젝트 폴더에

팀 작업으로 DB 테이블 CRUD를 다루어보았다. (코드 참고)

(sp04_MyBatis_Team은 내가 한거+sol참고, sol은 잘하는 팀원분이 하신 거)

<br/>

팀 작업 통해서 오늘 한 내용이 정리가 되어야 월요일날 MyBatis 제대로 나갈 수 있다!
