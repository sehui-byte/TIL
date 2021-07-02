

### Spring WebFlux

- **spring5부터 지원**

- **reactive-stack web framework**

- Netty, Undertow, Servlet 3.1+  컨테이너같은 `non-blocking servers`에서 `Reactive Streams API` 기반으로 reactive-stack 웹어플리케이션을 실행시키기 위한 것

- **non-blocking**

- **functional**

- **reactive 가 뭔데?**  ***변화에 반응하는 것을 기반으로 한 프로그래밍 모델.***

  - 이런 맥락에서 `non-blocking` 역시 `reactive`하다. `block`되는 대신에  동작이 끝났다거나 data가 사용 가능한 상태가 되었다든가 하는 알림에 *반응하는 방식*이기 때문이다.

    > The term, “reactive,” refers to programming models that are built around reacting to change — network components reacting to I/O events, UI controllers reacting to mouse events, and others. In that sense, non-blocking is reactive, because, instead of being blocked, we are now in the mode of reacting to notifications as operations complete or data becomes available.



- Reactor : Spring WebFlux가 채택한 reactive 라이브러리
  - `Mono`와 `Flux` api를 제공한다.

------------



### WebClient

- spring5와 springboot 2.0부터 `AsyncRestTemplate`가 deprecated 됨.
- 비동기 요청하기 위해선 `WebClient` 사용



request

```java
WebClient webClient = new WebClie

public Test findTest(String testId){
	webClient.get().uri("/test").body
}

```







----

### 참고자료

- [spring webFlux 공식문서](https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html)

- [위 공식문서 번역본](https://12bme.tistory.com/597)

- [spring webflux - webclient 사용해보기](https://akageun.github.io/2019/06/23/spring-webflux-4-webclient.html)

- https://sseambong.tistory.com/270