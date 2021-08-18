## 2021.08.18 (Team3) Docker Study

환경 :: Ubuntu 18.04

참고사이트 :: (도커(Docker) 입문편 컨테이너 기초부터 서버 배포까지)

https://www.44bits.io/ko/post/easy-deploy-with-docker

<br/>

---

---

강사 :: 김도커님 (실명 거론은 좀 그래서... 닉네임으로 ^^)

<br/>

**Front단 배포**

<br/>

윈도우 이클립스에서 war파일로 배포해서 Ubuntu 로컬에 넣기 전에

EC2에서 사용할 수 있게 EC2에 할당된 탄력적 IP 주소로 코드를 다 바꾸었다.

<br/>

도커 톰캣 컨테이너 진입 ::

docker exec -it tomcat bash

![image](https://user-images.githubusercontent.com/78403443/129879046-098bbb04-cff1-4616-8407-bfe70dd79a47.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129879098-e557daeb-bdd4-4a99-b3f3-1402106a88c0.png)

war파일 docker 톰캣 컨테이너에 배포

<br/>

톰캣 컨테이너에 배포만 하면 알아서 구동시켜준다

![image](https://user-images.githubusercontent.com/78403443/129879136-b7a10c53-0ce9-4b69-9bd1-d4150b8e978d.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129879195-854f3ad8-cf2d-4893-aef5-a0229e7423d3.png)

이렇게 셋팅한 도커 컨테이너를 Docker Hub에 내 계정 밑에 tracycle_front이란 이름으로 local태그를 붙여 커밋한다.

(로컬에서만 돌아가는 ip주소로 설정되어있기 때문에 local이라고 태그이름 붙임)

![image](https://user-images.githubusercontent.com/78403443/129879303-816fd145-40f4-4063-afcc-b074f82362ea.png)

이미지가 생성되었다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129879359-1b43ae25-a6ae-4ce1-a658-20b685311b76.png)

그리고, 컨테이너 삭제 해줬다.

<br/>

그리고, 커밋했던 이미지 구동

![image](https://user-images.githubusercontent.com/78403443/129879424-60e29da0-8e4a-4506-92bb-ab0284a40341.png)

컨테이너가 생성되어 잘 구동됐다는 결과나오고 페이지도 뜬다.

![image](https://user-images.githubusercontent.com/78403443/129879476-021d362c-4bfb-45d0-8a4f-25ec24c9d99a.png)

![image](https://user-images.githubusercontent.com/78403443/129879509-d70e17ee-e2ac-4dbc-8dd7-73619a19e450.png)

<br/>

컨테이너 내부에 진입해보니

![image](https://user-images.githubusercontent.com/78403443/129879721-ded572db-c36f-4449-9b8c-2ab536cf286a.png)

이렇게 파일이 잘 배포되어있음을 확인했다.

컨테이너도 생성되어 잘 돌아가고 있다.

![image](https://user-images.githubusercontent.com/78403443/129879764-850c2529-591b-4543-ba9f-24bc582df898.png)

<br/>

도커 로그인

![image](https://user-images.githubusercontent.com/78403443/129879807-fa140b8d-1cc4-41d3-9c60-e986107a34ae.png)

로그인 성공

<br/>

이미지 push

![image](https://user-images.githubusercontent.com/78403443/129879844-c01854f7-fbca-42a2-99f7-bacd217c2818.png)

id 저장소 밑에 repository에 local 태그로 넣는다고 해서.. 이렇게

내 계정 밑에 넣으려면 이렇게 해야만 한다

<br/>

![image](https://user-images.githubusercontent.com/78403443/129879904-1df44df3-eabf-493d-97f6-232acc8c0bb2.png)

![image](https://user-images.githubusercontent.com/78403443/129879944-85413d55-4bfa-4b9e-bc0d-875a2184495c.png)

Docker Hub에 잘 Push 되었다.

<br/>

EC2에서 사용할 이미지는 위와 같은 과정으로 똑같이 진행해서 PUSH까지 하면 된다.

테스트를 위한 웹 요청은 똑같이 localhost로 요청하면 된다.

![image](https://user-images.githubusercontent.com/78403443/129880006-3e0f5318-6146-4da4-a525-454485cf0bea.png)

오른쪽 파이어폭스 브라우저 화면과 같이 이렇게 잘 나오면 테스트 완료

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880104-5ed88f8c-a35c-435e-b46b-9de54f8ae65f.png)

Push가 잘 되었다면 이렇게 지정해서 Push했던 태그명으로 추가되었음이 확인된다.

<br/>

---

**Back단 배포**

**SpringBoot 서버**

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880218-2ed993c9-0104-44f3-846f-60dbbe640ba6.png)

![image](https://user-images.githubusercontent.com/78403443/129880258-615869fc-1398-4473-bcce-20e636b0f4ab.png)

로컬에서 프로젝트 압축파일을 가져왔다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880313-276ac49b-0cac-4611-8bd9-5be0dc145298.png)

back 폴더로 옮겨서 압축 풀어주었다.

<br/>

sudo vi pom.xml 명령어 입력해서 vi 편집기로 pom.xml 열어서

![image](https://user-images.githubusercontent.com/78403443/129880413-9bb6c7d0-17d2-40c8-8e93-46106cd1bc47.png)

war를 jar로 바꿔주었다.

![image](https://user-images.githubusercontent.com/78403443/129880456-ed46ff6b-88c7-4cc3-b9f9-9c60ac8331a6.png)

잘 바뀐것을 확인했다.

<br/>

이제 maven을 설치한다. (이미 설치되어있다면 필요 없는 부분)

![image](https://user-images.githubusercontent.com/78403443/129880515-c0968cce-7e90-44f7-a2fc-dd3775b7eba1.png)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880565-0e68b1e5-1972-4cfa-8176-5b90e921db8d.png)

maven 설치완료되었고 target 폴더 안에 파일들 확인했다.

<br/>

pom.xml이 있는 폴더 안에서

![image](https://user-images.githubusercontent.com/78403443/129880608-f2a65f09-8e14-4404-8b38-4b44325a2591.png)

sudo mvn package 명령을 쳐서 빌드를 진행한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880661-9184a04a-94ea-4282-b853-bd57a2725c4e.png)

빌드가 끝났고 target 폴더에 빌드 파일들이 배포된 것을 확인했다.

<br/>

그리고 sudo vi Dockerfile 해서

![image](https://user-images.githubusercontent.com/78403443/129880734-9bdaf5ee-6fc0-4bbd-854a-b38f3d595ce9.png)

오른쪽 표시한 터미널 창과 같이 Dockerfile을 작성하고 저장해준다.

![image](https://user-images.githubusercontent.com/78403443/129880767-fb191efb-1194-4e7b-b3f1-0a1ab707da29.png)

저장 확인했다.

![image](https://user-images.githubusercontent.com/78403443/129880821-19023781-0818-422a-9e90-494ae77e81d1.png)

잘 작성된 것도 확인했다.

(From 부분 의미는 openjdk 8버전 기반으로 한다는 걸 설정해준것임)

(Copy는 recycle 뭐시기.jar 파일을 app.jar 라는 이름의 파일로 복사하겠다는 얘기)

(Entrypoint 는 .jar를 실행시켜주라는 의미)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880857-0c8cd3bd-30f0-4140-aa9e-349260568766.png)

위 명령어로 도커파일로 이미지를 빌드하도록 해준다. 

local . 을 붙여줘야지 그 밑에 있는 것을 전부 빌드한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129880997-fa701574-2c17-4049-8f57-3c04f0edddb2.png)

도커 이미지로 도커에 빌드를 완료했고, 확인되었다.

(openjdk 설치되있는 이유는 아까 Dockerfile에서 openjdk 기반으로 한다는 걸 설정해줬기 때문)

(Copy는 recycle 뭐시기.jar 파일을 app.jar 라는 이름의 파일로 복사하겠다는 얘기)

(Entrypoint 는 .jar를 실행시켜주라는 의미)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881048-9f094f84-3280-4192-a01d-6783b4b5a05b.png)

위와 같이 docker run 시킨다. 

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881092-3f36615e-1dbb-4ab6-ba77-8da592702bff.png)

back 컨테이너가 잘 작동되고 있다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881131-29fa50f9-7d00-4bf8-8a1b-43d251e0686d.png)

log 확인 명령어로 서버가 잘 구동되었는지 확인했다.

(fea는 컨테이너ID 명 앞 3글자를 지정, 해당 컨테이너 로그를 보여주도록 명령함)

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881164-d36879af-7190-4854-ae57-cf772c294e70.png)

이제 Docker Hub에 Push해준다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881204-9e793ea9-bbc0-42d2-a1ee-a77ad0e77eca.png)

도커 내부에 진입해서 파일들 확인함

<br/>

<EC2용 Spring Boot 서버 빌드해서 Docker Hub에 배포하기>

sudo vi application.properties 명령어로 vi 편집기 열고

![image](https://user-images.githubusercontent.com/78403443/129881296-bb812618-3c8e-4f14-ad2e-4e2449410c6e.png)

ip를 EC2 ip주소로 바꿔준다.

<br/>

그리고 cd config 해서 config 폴더로 이동하고

sudo vi dbconn.properties 명령어를 쳐서 vi편집기를 들어간다.

![image](https://user-images.githubusercontent.com/78403443/129881369-f5f6858a-bcf4-433c-b5c3-f9dde4c8d7d1.png)

그리고 ip주소를 EC2 주소로 바꿔준다.

<br/>

나머지는 로컬로 했던 과정과 동일한 방식으로 진행하면 된다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881416-68d1762f-0694-42ab-ae16-818a56f28624.png)

Docker Hub에 Push까지 진행했고, 위와 같이 잘 Push되었음을 확인했다!

<br/>

---

**Flask 서버**

<br/>

김도커님의 Flask서버 Docker 이미지 다운

(시간과 AWS 프리티어 사양 관계로 이미지만 받아서 로컬에서 돌릴듯?)

![image](https://user-images.githubusercontent.com/78403443/129881492-3af67398-79f1-47cb-884b-663042ec4ca2.png)

다운 완료

![image](https://user-images.githubusercontent.com/78403443/129881585-018624ad-e99e-4caf-9795-009753921f29.png)

![image](https://user-images.githubusercontent.com/78403443/129881633-d8736330-d715-4c8a-ac97-c705e8aa414c.png)

<br/>

ubuntu 로컬에 docker-compose.yml 파일을 넣어주었다.

![image](https://user-images.githubusercontent.com/78403443/129881693-7f10f386-e72b-4f76-8a8c-38897a97cd42.png)

<br/>

sudo apt install docker-compose 명령어로 docker compose를 설치한다.

![image](https://user-images.githubusercontent.com/78403443/129881741-aa80297f-09f4-46a3-a88d-02af6016370e.png)

<br/>

vi docker-compose.yml 명령어를 쳐서 vi 편집기로 들어간다.

![image](https://user-images.githubusercontent.com/78403443/129881802-adc64e4a-2a68-4c08-92c1-27a6b8f9f23d.png)

docker-compose.yml 파일을 위와 같이 내가 지정한 Docker 이미지에 맞게 설정을 작성해준다.

<br/>

그리고 docker-compose.yml 파일이 있는 곳에서

![image](https://user-images.githubusercontent.com/78403443/129881852-43a06400-f7bb-408b-a05f-0d8c8098786a.png)

docker-compose up 명령어를 쳐서 compose를 해준다.

(오류때문에 AWS ec2로 이동해서 Front와 Springboot 이미지만 pull해서 위 과정 진행함)

(Flask 서버는 용량이 너무 커서 AWS EC2 프리티어로는 택도 없음...)

![image](https://user-images.githubusercontent.com/78403443/129881891-6bcd8aae-1d3d-4cca-8cce-30d2b82c3bc3.png)

<br/>

※ 여기서 참고사항

docker-compose stop 이나 restart 로 하면 컨테이너가 안내려간 채로 정지되거나 재시작한다.

(멈췄다가 다시 시작할 계획이 있을 때는 꼭 이 명령어를 쳐야한다)

<br/>

아예 중단하면서 컨테이너도 함께 내릴 때는 docker-compose down 명령어를 사용한다.

내려져 있는 상태에서 로그 출력 없이 다시 실행할 때는 docker-compose up -d 명령어를 사용한다.

<br/>

![image](https://user-images.githubusercontent.com/78403443/129881951-6039a3e9-cda8-480d-bdab-169443529844.png)

EC2 서버에 요청한 페이지가 DB데이터와 함께 잘 나오는 것을 확인했다.

<br/>

---

++ 추가

<br/>

모든 컨테이너 삭제하기

docker stop $(docker ps -a -q)

docker rm $(docker ps -a -q)

<br/>

모든 이미지 삭제하기

docker rmi $(docker images -q)

<br/>

Exit 상태의 모든 컨테이너 삭제하기

docker rm $(docker ps --filter 'status=exited' -a -q)

<br/>

선택지우기

docker rmi 이미지id or 이름

docker image rm 이미지id or 이름
