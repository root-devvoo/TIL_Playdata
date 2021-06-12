## 2021.03.12 Thread(쓰레드) 2, Stream 1

<br/>

쓰레드들이 동작 > Sharing(공유) 하는 상황때문에 문제점이 발생한다.

![20210312_094122](https://user-images.githubusercontent.com/78403443/121762690-987d7080-cb72-11eb-9e56-bafed7fad6f5.png)

![20210312_103057](https://user-images.githubusercontent.com/78403443/121762693-a206d880-cb72-11eb-919d-4addc47ef02e.png)

Thread에서 무조건 해결해야하는 문제 (Interrupted)

![20210312_105940](https://user-images.githubusercontent.com/78403443/121762709-afbc5e00-cb72-11eb-89b8-9616be5f2d8a.png)

<br/>

---

메소드에 동기화 처리 - 이 방법 권장 - 24_Thread 프로젝트 step6 MegaBoxUser 파일 참고!

ex) public synchronized void

![20210312_110535](https://user-images.githubusercontent.com/78403443/121762729-c1056a80-cb72-11eb-8e9c-0d43d7b4d25e.png)

![20210312_110835](https://user-images.githubusercontent.com/78403443/121762737-cb276900-cb72-11eb-94ee-1f2f0c79d407.png)

노란색은 오늘 새로 배운 부분, 나머지는 어제 배웠음

24 프로젝트 step7.test 패키지에서 노란색 부분 원리 볼 수 있다.

(Deadlock 발생)

---

(Deadlock 발생)

![20210312_114050](https://user-images.githubusercontent.com/78403443/121762752-df6b6600-cb72-11eb-8c2e-31ae0e94445f.png)

Deadlock 이 발생하지 않게 하기 위한 해결책은 wait 과 notify

그림은 개인공책에... 위에 대한 그림 다음 쪽에 있음

<br/>

---

**Stream**

![20210312_115500](https://user-images.githubusercontent.com/78403443/121762769-f90cad80-cb72-11eb-8c79-3f5a732e1b72.png)

Data는 소스에서 싱크로 흘러간다. 흘러가는 관이 Stream

상하수도 공사 직접 x - 하드웨어에 이미 설치되어있다.

자원을 열어서 사용만 하면 된다. > 생성의 의미

---

![20210312_122426](https://user-images.githubusercontent.com/78403443/121762783-0a55ba00-cb73-11eb-9493-c5941fdbe674.png)

![20210315_092501](https://user-images.githubusercontent.com/78403443/121762788-15a8e580-cb73-11eb-9889-2e48929920a4.png)

**BufferedReader**

![20210316_171408](https://user-images.githubusercontent.com/78403443/121762799-248f9800-cb73-11eb-8e3b-a991aaa3560c.png)

(출처: https://snupi.tistory.com/48 [SNUPI])

데이터의 양이 적을 때는 차이가 미미하겠지만 양이 많을 경우에

하나하나씩 전달하지 않고 버퍼에 한 번에 모아서 전달하는 BufferedReader클래스가

속도면에서 **빠르고 효율적**이다.
