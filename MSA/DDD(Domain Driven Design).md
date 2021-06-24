### DDD(Domain Driven Design)

- 도메인(domain)이란?
  - 실세계에서 사건이 발생하는 집합.
  - ex) 쇼핑몰에서 손님이 옷을 주문하는 Order Domain, 점주가 옷을 관리하는 Manage Domain ...

- **Bounded Context**: 문맥(Context)에 따라 객체(object)의 역할이 바뀐다.

- **<u>서비스별로 도메인을 분류</u>**하라!

  

- aggregate(집합): 각각의 도메인 영역을 대표하는 객체.

- Repository: 모델을 저장하는 곳

- Service: 도메인 간의 연산을 처리하는 모델



#### Entity vs VO

- Entity 

  - JPA의 Entity :`@Entity` : DB와 매핑되는 객체.

  - JPA의 `@Table`과 매핑해서 사용.

  - DDD의 Entity: unique key를 바탕으로 객체의 정체성 부여.

    

- VO 

  - 불변(immutable)하는 상태(attribute)나 값을 바탕으로 객체의 정체성 부여.

  - 식별자가 필요 없는 고유 모델.

    

#### Facade





----

### 참고자료

- https://huisam.tistory.com/entry/DDD
  - 정말 이해하기 쉽게 설명되어있는 글

- [필요한 내용만 추려서 ddd 당장 써먹기](https://www.popit.kr/%ED%95%84%EC%9A%94%ED%95%9C-%EB%82%B4%EC%9A%A9%EB%A7%8C-%EC%B6%94%EB%A0%A4%EC%84%9C-ddd-%EB%8B%B9%EC%9E%A5-%EC%8D%A8%EB%A8%B9%EA%B8%B0/)

- [카카오헤어샵의 DDD](https://brunch.co.kr/@cg4jins/7)

- [DDD와 JPA의 Entity](https://namocom.tistory.com/980)