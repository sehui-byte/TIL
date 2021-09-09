

## [Spring] @Transactional

- spring framework는 코드 기반의 트랜책션 처리를 위해 declarative transaction 을 지원한다.
- spring transaction은 AOP Proxy를 통해 처리된다.

- `@Transactional`은 RuntimeException과 그 자식들인 unchecked exception에 대해서만 rollback하기 때문에 checked exception이 발생했을 때도 rollback하고 싶다면, ` @Transactional(rollbackFor = Exception.class)`와 같이 롤백할 예외를 지정해줘야 한다.



---

## Spring AOP Proxy

Spring은 @Transactional 어노테이션을 선언한 메서드가 실행되기 전 `transaction begin` 코드를 삽입하고, 메서드가 실행된 후 `transactional commit` 코드를 삽입한다. 

Spring의 코드 삽입 방법은 크게 2가지가 있다.

- **CGLib(Code Generator Library) Proxy**

  - springBoot의 경우 기본적으로 프록시 객체를 생성할 때 `CGLib`을 사용하고 있다.
  - **CGLib란 ?** 코드 생성 라이브러리로서 런타임에 동적으로 자바 클래스의 프록시를 생성해주는 기능을 제공한다.

  ![pasteImage.png](https://static.podo-dev.com/blogs/images/2019/07/10/origin/I8ECVM190222205849.PNG)

- **JDK Dynamic Proxy**

  - **interface가 필요하다.** (Proxy 클래스가 구현 클래스를 감싼다.)
  - 반드시 public 메서드에 적용되어야 한다.

![pasteImage.png](https://static.podo-dev.com/blogs/images/2019/07/10/origin/Q3NZGK190222204715.PNG)



----------

DB에서 transaction이란 **DB의 상태를 변화시키는 작업 단위**이다. 즉 하나의 작업을 수행하기 위해 필요한 query를 하나의 묶음으로 처리해서 실행시키는 논리적인 단위로, 중간에 장애가 발생했을시 트랜잭션 단위로 rollback되고, 정상적으로 수행되었을시 commit된다고 보면 된다.

ACID는 이런 **트랜잭션의 4가지 특성**의 앞글자만 따서 모아둔 것이다.

## ACID

- **Atomicity** (원자성) : All or Nothing의 개념으로 작업단위의 일부만 실행되지 않는다는 뜻이다. 즉 트랜잭션의 일부 연산만이 수행되거나 할 수는 없다는 것이다. 
- **Consistency** (일관성) : 트랜잭션이 성공적으로 수행되었을 때 일관적인 DB 상태를 유지한다는 것이다. 예를 들면 트랜잭션 후에 데이터의 타입이 바껴있다든가 하면 안된다.
- **Isolation** (격리성) : transaction 작업이 수행되고 있을 때, 다른 작업이 끼어들지 못하도록 보장해주는 것. 원칙적으로 트랜잭션끼리는 서로 간섭을 할 수 없어야하지만, 성능 이슈들이 많아 가장 유연하게 설정이 가능한 제약조건이다.
- **Durablility** (지속성) : 성공적으로 수행된 트랜잭션은 영구히 반영된다는 의미이다. MYSQL을 포함해 많은 DB들의 구현에서는 트랜잭션 조작을 하드디스크에 로그로 기록하고, 시스템에 이상이 발생하면 그 로그를 이용하여 복원하는 것으로 지속성을 실현하고 있다고 한다.

---



## @Transactional 옵션

### isolation level (격리 레벨)

- **isolation이란?** 

  동시에 여러 트랜잭션이 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것.

이 격리 레벨(격리수준)이 높아질수록 동시성(concurrency)은 높아지고 속도는 느려진다.

1. **READ_UNCOMMITED (level 0)**

   : 트랜잭션 처리 중이거나 아직 커밋되지 않은 데이터를 다른 트랜잭션에서 read하는 것을 허용한다. => `Dirty read` 발생 

   - **dirty read**란 ? 커밋하지 않은 데이터를 읽는 것

2. **READ_COMMITED (level 1)**

   : 트랜잭션이 커밋되어 확정된 데이터만을 읽도록 허용하여 `dirty read`가 발생하지 않도록  보장한다.

3. **REPEATABLE_READ (level 2)**

   : 데이터 조회시 항상 동일한 데이터 응답을 보장하는 격리수준이다. `READ_COMMITED`는 한번 데이터를 조회 후, 다시 조회했을 때 두 데이터가 동일하다는 것을 보장해주지 않는다. 왜냐면 그 사이 다른 트랜잭션에서 해당 데이터가 갱신되었을 수 있기 때문이다. 이를 `Non-repeatable read`라고 한다. 이 격리수준은 트랜잭션이 완료될 때까지 select를 사용하는 모든 데이터에 `shared lock`이 걸린다. 

   `phantom read`가 발생할 수 있다.

   - phantom read란?

4. **SERIALIZABLE (level 3)**

   :  가장 높은 격리수준을 제공한다. 그만큼 동시성 처리효율은 떨어진다.



**각 DB별 격리수준**

- MYSQL : REPEATABLE READ 

- ORACLE : READ COMMITTED 

- H2 : READ COMMITTED



### propagation (전파속성)



### readOnly 속성

- true인 경우 insert, update, delete 실행시에 예외가 발생된다.

```java
@Transactional(readOnly = true)
```



----

@Transactional 어노테이션은 **서비스단에 위치**하는 것을 권장한다. 

아래는 스택오버플로우 답변이다.

> Ideally, Service layer (**Manager**) represents your business logic and hence it should be annotated with `@Transactional`.
>
> Service layer may call different DAOs to perform DB operations. Lets assume a situation where you have 3 DAO operations in a service method. If your 1st DAO operation failed, other two may be still passed and you will end up with an inconsistent DB state. Annotating Service layer can save you from such situations.



--------

## 참고자료

- https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/transaction.html
- [spring 공식문서 한글화](https://godekdls.github.io/Spring%20Data%20Access/transactionmanagement/)

- https://mommoo.tistory.com/92
- https://imiyoungman.tistory.com/9
- https://lion-king.tistory.com/3
- https://minkukjo.github.io/framework/2021/05/23/Spring/
- [Spring AOP proxy](http://wonwoo.ml/index.php/post/1576)
- http://wonwoo.ml/index.php/post/1708
- https://www.podo-dev.com/blogs/133 - @Transactional 옵션
- [StackOverflow - [Where should “@Transactional” be placed Service Layer or DAO](https://stackoverflow.com/questions/3886909/where-should-transactional-be-placed-service-layer-or-dao)]
- [CGLIB란?](https://javacan.tistory.com/entry/114)
- https://chrisjune-13837.medium.com/db-transaction-isolation-level-f21b6d1e64eb
- https://n1tjrgns.tistory.com/267
- https://velog.io/@lsb156/Transaction-Isolation-Level

- [어떤 @Transactional을 사용해야 할까?](https://interconnection.tistory.com/123)