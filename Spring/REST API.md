

### REST API란?

- Representational State Transfer
- 하나의 URI는 하나의 고유한 Resource를 대표하도록 설계된다는 개념.



#### 구성

- 자원(Resource)- URI
- 행위(Verb)- HTTP method
- 표현(Representations)



#### 디자인 가이드

- **URI는 정보의 자원을 표현해야 한다.**
  - 자원을 나타내기 위해서는 명사(noun)를 사용해야하며, 표현하고자 하는 자원이 복수형일 경우에는 이것을 명시해야 한다.
- **자원에 대한 행위는 Http method(GET, POST, PUT, DELETE)로 표현**한다.



----



### Spring & REST API

- spring MVC패턴의 경우 서버에서 html을 그려서 데이터를 내보내는데, **REST API 아키텍처 스타일은 클라이언트와 서버가 분리되며 데이터는 HTTP 프로토콜 위에서 주고받는 방식**이다.

<img src="https://blog.kakaocdn.net/dn/2BnED/btqybg36Dak/3HgL3gUKHBSOmyeM4hIn00/img.png" alt="img" style="zoom: 80%;" />

spring에서 controller에 `@ResponseBody`가 붙으면 **spring의 `viewResolver`대신에 `HTTP Message Converter`에 의해** view가 아닌, **data 자체를 리턴**하게 된다. 

HttpMessageConverter에는 여러 Converter가 등록되어있고, 반환해야하는 데이터의 종류에 따라 사용되는 converter가 달라진다. 

![img](https://blog.kakaocdn.net/dn/bEJ1YG/btqx8Tvu8qa/lkDg8cu2G4xMi8Pg22C1f0/img.png)

spring4부터 제공되는 `@RestController`

- class level에 선언할 수 있으며,

- `@RestController`가 붙은 컨트롤러의 모든 메서드는 자동으로 `@ResponseBody`가 적용된다.

  ![img](https://blog.kakaocdn.net/dn/7bceC/btqx8K6BbxE/LVs4KK74mUj9CZ70uHTsjK/img.png)







-----

### 참고자료

- https://meetup.toast.com/posts/92

- https://congsong.tistory.com/28

- https://engkimbs.tistory.com/855

- [spring @Controller와 @RestController 차이](https://mangkyu.tistory.com/49)