인텔리제이 + springBoot 환경에서 테스트코드를 짜는 법에 대해 학습해보려고 한다.



## Junit이란?

- java에서 독립된 단위테스트(unit test)를 지원해주는 프레임워크.
- junit4 이후부터는 어노테이션을 지원한다. (`@Test`, `@Before` 등)
- `@Test`메서드를 호출할 때마다 새로운 인스턴스를 생성하여 독립적인 테스트가 이루어지게 한다.



## spring-boot-starter-test

`spring-boot-starter-test`에는 다음 라이브러리들이 포함되어있다.

- junit5
- assertJ
- **Mockito** : 개발자가 동작을 직접 제어할 수 있는 가짜(Mock) 객체를 지원하는 테스트 프레임워크. Mockito를 활용함으로써 가짜 객체에 원하는 결과를 Stub하여 단위 테스트를 진행할 수 있다.
- JSONassert
- JsonPath
- Hamcrest











----

## 참고자료 

- https://goddaehee.tistory.com/210
- https://mangkyu.tistory.com/145

- https://junit.org/junit5/docs/current/user-guide/