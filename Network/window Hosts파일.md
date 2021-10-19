윈도우에서 Hosts파일은 아래 경로에 있다.

```
C:\Windows\System32\drivers\etc
```

윈도우10에서 hosts파일 수정시에 복사하여 복사한 파일을 수정 후, 다시 돌아와서 덮어쓰기를 하면 된다.



------

### Hosts파일이란?

> 운영체제가 호스트 이름을 IP주소에 매핑할 때 사용하는 컴퓨터 파일.
>
> 호스트 이름에 대응하는 IP 주소가 저장되어 있어서 도메인 이름 시스템(DNS)에서 주소 정보를 제공받지 않고도 서버의 위치를 찾게 해주는 파일.



**IP주소 + 호스트 이름** 순으로 한 줄로 작성하면 되고, IP주소 다음에 한 칸 이상 띄우고 호스트 이름을 쓰면 된다.



그래서 hosts파일에

```
[임의의 IP주소] www.naver.com
```

으로 적으면, 네이버 사이트에 접속할 때 우리가 알고 있는 네이버 사이트로 접속하는게 아니라, 임의의 IP주소로 이동하게 된다고 한다. 그래서 예전에 hosts파일을 변조시키는 악성 프로그램들이 있었다고 한다.

![image-20210514143913217](C:\Users\nextree\AppData\Roaming\Typora\typora-user-images\image-20210514143913217.png)





---

### 참고자료

- https://goddaehee.tistory.com/90

- https://m.blog.naver.com/PostView.nhn?blogId=weekamp&logNo=220962747718&proxyReferer=https:%2F%2Fwww.google.com%2F

- http://w2.kings.co.kr/i/help/hosts/