



## Junit 5

- java8부터 지원한다.

- **Junit platform + junit jupiter + junit vintage**
  - **Junit platform** : JVM에서 테스트 프레임워크를 실행하는데 기초를 제공한다. 또한 TestEngine api를 제공해 테스트 프레임워크를 개발할 수 있다.
  - **Junit jupiter** : Junit5에서 테스트를 작성하고 확장을 하기 위한 
  - **Junit vintage** : 하위호환성을 위해 Junit3,4기반으로 돌아가는 플랫폼에 테스트 엔진을 제공해준다.



### Assertions

- Junit jupiter는 junit4로부터 온 assertion 메소드와 새롭게 자바8 람다 표현식으로 추가된 메소드들이 있다.
- 모든 Junit Jupiter assertion은 **정적 메소드**이다.
- third party assertion library : AssertJ, Hamcrest, Truth 등



---

## 참고자료

- [junit5 완벽가이드](https://donghyeon.dev/junit/2021/04/11/JUnit5-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C/)

  