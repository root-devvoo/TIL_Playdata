**오늘 다룬 수업 내용**
1. SQL
2. jdbc 04 같이 마무리
3. 사용자 관점 시스템 활용도 > DB 모델링 > Business logic template

**SQL문 실습 및 함수 사용**
MySQL 함수관련 정리

1. 문자 관련 함수 

- ASCII(문자) - 문자의 아스키 코드값 리턴
- CONCAT('문자열1','문자열2','문자열3'...) - 문자열(혹은 컬럼)들을 이어준다
- INSERT('문자열','시작위치','길이','새로운문자열') - 문자열의 시작위치부터 길이만큼 새로운 문자열로 대치 
- REPLACE('문자열','기존문자열','바뀔문자열') - 문자열 중 기존문자열을 바뀔 문자열로 바꾼다
- INSTR('문자열','찾는문자열') - 문자열 중 찾는 문자열의 위치값을 출력 

= 문자열 일부분 가져오기(LEFT, RIGHT, MID) ==
- LEFT('문자열',개수) - 문자열 중 왼쪽에서 개수만큼을 추출.
- RIGHT('문자열',개수) - 문자열 중 오른쪽에서 개수만큼을 추출
- MID('문자열',시작위치,개수) - 문자열 중 시작위치부터 개수만큼 출력 (SUBSTR or SUBSTRING과 동일)
 - SUBSTRING('문자열',시작위치,개수) - 문자열 중 시작위치부터 개수만큼 출력 

2. 숫자 관련 함수 

- ABS(숫자) - 절대값 출력   
- CEILING(숫자) - 값보다 큰 정수 중 가장 작은 수(올림)  
- FLOOR(숫자) - 소수점 버림[실수를 무조건 버림(음수일 경우는 제외)]
- ROUND(숫자,자릿수) - 숫자를 소수점 이하 자릿수에서 반올림.(자릿수는 양수,0,음수를 갖을 수 있다.) 
- TRUNCATE(숫자,자릿수) - 소수점 자리수 버림
- POW(X,Y) or POWER(X,Y) - X의 Y승 
- MOD (분자, 분모) - 분자를 분모로 나눈 나머지를 구한다.(연산자 %와 같음) 
- GREATEST(숫자1,숫자2,숫자3...) - 주어진 수 중 제일 큰 수 리턴
- LEAST(숫자1,숫자2,숫자3...) - 주어진 수 중 제일 작은 수 리턴
- INTERVAL(a,b,c,d.....) - a(숫자)의 위치 반환

3. 날짜 관련 함수 
- NOW() or SYSDATE() or CURRENT_TIMESTAMP() - 현재 날짜와 시간 출력 
- CURDATE() or CURRENT_DATE() -현재 날짜 출력 
- CURTIME() or CURRENT_TIME() -현재 시간 출력 
- DATE_ADD(날짜,INTERVAL 기준값) -날짜에서 기준값 만큼 더한다
- DATE_SUB(날짜,INTERVAL 기준값) -날짜에서 기준값 만큼 뺸다
- YEAR(날짜) -날짜의 연도 출력
- MONTH(날짜) -날짜의 월 출력
- MONTHNAME(날짜) -날짜의 월을 영어로 출력
- DAYNAME(날짜) -날짜의 요일일 영어로 출력
- DAYOFMONTH(날짜) -날짜의 월별 일자 출력
- DAYOFWEEK(날짜) -날짜의 주별 일자 출력(월요일(0),화요일(1)...일요일(6)) 
- WEEKDAY(날짜) -날짜의 주별 일자 출력(월요일(0),화요일(1)...일요일(6)) 
- DAYOFYEAR(날짜) -일년을 기준으로 한 날짜까지의 날 수
- WEEK(날짜) -일년 중 몇 번째 주
- FROM_DAYS(날 수) --00년 00월 00일부터 날 수 만큼 경과한 날의 날짜 출력
- TO_DAYS(날짜) --00 년 00 월 00일 부터 날짜까지의 일자 수 출력
- DATE_FORMAT(날짜,'형식') : 날짜를 형식에 맞게 출력

![20210322_170558](https://user-images.githubusercontent.com/78403443/111960315-edd95100-8b32-11eb-8f87-c69fdf7a54cc.png)

**4. 그룹함수를 이용한 데이터 집계**
- 그룹합수란?
  - 전체에서 모든 데이터를 다 봐야하기 때문
  - 유형
    - AVG - 평균 값
    - SUM - 합계
    - MIN - 최소값
    - MAX - 최대값
    - COUNT - 행의 수

    1. 숫자데이터에만 적용되는 함수 = AVG, SUM
    2. NULL 값을 건너뛰고 계산
    - 이 두가지를 유념해서 조심해서 다뤄야한다.

**SQL쿼리문**
- ROUND(avg(sal),2) - 메소드 중첩...
- 수업 때 다루는 쿼리문은 반드시 알아야 하는거 중심으로 함 >> 잘 익혀두기
- Group by 절 = 그룹을 세분화한다.
- Group by 절에 Alias가 된다 -- 기억하기!
- 절의 순서 (기억하기!)
  - SELECT > FROM > WHERE > GROUP BY > ORDER BY
------------------------------------------------------------------------------------------------------------------------------------------------
**JDBC**
- class DriverManager - 자원을 너무 많이씀, 접속하고 보내기 때문에 >> 몰리면 힘들다 Heavy!, DB연결 때 리소스 많이 든다.
- javax.sql > eXtensive
  - datasource
    - Connection 들의 공장
    - getting a connection >> (JNDI) API ## JNDI = Naming service
    - 미리 만들어놓은 connection들 가지고 있다. 그걸 가져옴
    - 쓰고 반환
    - 나중에 WAS에서 이런걸 쓴다

1. 사용자 입장 SYSTEM 활용도
  1. DB모델링
  2. 프론트 화면작업
  - SRS
  - Usecase Diagram

2. DB모델링
  1) ENTITY 추출 >> 개념적
  2) ENTITY 간 Relationship >> 논리적
  3) Entity 속성 >> 논리적

  eXERD 
    - 多 대 多 관계해결

![20210322_163748](https://user-images.githubusercontent.com/78403443/111961473-73a9cc00-8b34-11eb-8e0a-6e60cec4e8f2.png)
eXERD 기본키 설정 : Ctrl + shift + enter
![20210322_164224](https://user-images.githubusercontent.com/78403443/111961506-7f958e00-8b34-11eb-88c3-ceda6d930112.png)
![20210322_164342](https://user-images.githubusercontent.com/78403443/111961538-87553280-8b34-11eb-92b9-cbc3566e8fc8.png)
![20210322_164704](https://user-images.githubusercontent.com/78403443/111961560-8c19e680-8b34-11eb-8437-f17109226192.png)
관계지정

점선 - 비실체관계 - ⓕ일반속성 영역안 - 부서정보로 사원정보 모름

실선 - 실체관계 - ⓕ기본속성 영역안 - 사원번호를 통해 사원정보 알 수 있다
![20210322_164828](https://user-images.githubusercontent.com/78403443/111961584-92a85e00-8b34-11eb-95dd-a21c0d14673c.png)
일반키 설정: ctrl + Enter

DB모델링에서 多 대 多 관계는 물리적모델 생성 안됨
논리적으로만...
그럼 어떻게? --- 사진
![20210322_165608](https://user-images.githubusercontent.com/78403443/111961596-95a34e80-8b34-11eb-919b-184400f0e43e.png)

Association Entity에 pk를 안넣게되면 나머지 정보가 모여서 pk처럼 됨
따라서, pk(기본키) 넣어도 되고 안넣어도 된다.
