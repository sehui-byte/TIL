[TOC]



## [Spring] @Transactional

- spring framework는 코드 기반의 트랜책션 처리를 위해 **declarative transaction 을 지원**한다. -> 그게 바로 이 `@Transactional` 어노테이션이다.

  - 🧐**declarative transaction이란?** **비즈니스 코드로부터 트랜잭션 관리를 분리**한 것.

    이와 반대되는 개념으로는 **programmatic transaction** (`TransactionTemplate`) 이 있는데, 이는 우리가 소스코드에 직접 프로그래밍해서 트랜잭션을 관리하는 것이다. 그래서 비즈니스 로직 사이에 트랜잭션 로직을 하드코딩해야한다. 

    > Declarative means you **separate transaction management from the business code**

- ✨spring transaction은 **AOP Proxy를 통해 처리**된다.

  - **AOP**(Aspect Oriented Programming) : 반복 사용되는 로직들을 모듈화하여 필요할 때 호출해서 사용하는 방법.

- `@Transactional`은 `RuntimeException`과 그 자식들인 `unchecked exception`에 대해서만 rollback하기 때문에 `checked exception`이 발생했을 때도 `rollback`하고 싶다면, ` @Transactional(rollbackFor = Exception.class)`와 같이 롤백할 예외를 지정해줘야 한다.

- `private`에는 `@Transactional`이 적용되지 않는다. 왜냐하면 <u>proxy형태로 동작하기 때문에 외부에서 접근 가능한 메서드만 @Transactional설정이 가능</u>하기 때문이다.

  

🖍정리하자면, spring은 선언적 트랜잭션(declarative transaction)을 지원하고, 그것이 바로 `@Transactional`이다. 

이는 편리해서 programmatic transaction보다 자주 사용하지만, programmatic transaction을 사용해야 하는 경우도 있다. 왜냐하면 declarative transaction은 proxy방식으로 동작하기 때문에 proxy 외부에서 접근해야 AOP가 적용된다.

 이럴 땐TransactionTemplate을 사용해서 직접 트랜잭션을 관리해야한다.





## Spring AOP Proxy

Spring은 @Transactional 어노테이션을 선언한 메서드가 실행되기 전 `transaction begin` 코드를 삽입하고, 메서드가 실행된 후 `transactional commit` 코드를 삽입한다. 

Spring의 코드 삽입 방법은 크게 2가지가 있다.

- **CGLib(Code Generator Library) Proxy**

  - springBoot의 경우 기본적으로 프록시 객체를 생성할 때 `CGLib`을 사용하고 있다.
  - **CGLib란 ?** 코드 생성 라이브러리로서 **런타임에 동적으로 자바 클래스의 프록시를 생성**해주는 기능을 제공한다.

  ![pasteImage.png](https://static.podo-dev.com/blogs/images/2019/07/10/origin/I8ECVM190222205849.PNG)

- **JDK Dynamic Proxy**

  - **interface가 필요하다.** (Proxy 클래스가 구현 클래스를 감싼다.)
  - 반드시 public 메서드에 적용되어야 한다.

![pasteImage.png](https://static.podo-dev.com/blogs/images/2019/07/10/origin/Q3NZGK190222204715.PNG)



----------

DB에서 transaction이란 **DB의 상태를 변화시키는 작업 단위**이다. 즉 하나의 작업을 수행하기 위해 필요한 query를 하나의 묶음으로 처리해서 실행시키는 논리적인 단위로, 중간에 장애가 발생했을시 트랜잭션 단위로 rollback되고, 정상적으로 수행되었을시 commit된다고 보면 된다.

ACID는 이런 **트랜잭션의 4가지 특성**의 앞글자만 따서 모아둔 것이다.

## ACID

- **Atomicity** (원자성) : All or Nothing의 개념으로 **작업단위의 일부만 실행되지 않는다**는 뜻이다. 즉 트랜잭션의 일부 연산만이 수행되거나 할 수는 없다는 것이다. 
- **Consistency** (일관성) : **트랜잭션이 성공적으로 수행되었을 때 일관적인 DB 상태를 유지**한다는 것이다. 예를 들면 트랜잭션 후에 데이터의 타입이 바껴있다든가 하면 안된다.
- **Isolation** (격리성) : **transaction 작업이 수행되고 있을 때, 다른 작업이 끼어들지 못하도록 보장해주는 것**. <u>원칙적으로 트랜잭션끼리는 서로 간섭을 할 수 없어야하지만, 성능 이슈들이 많아 가장 유연하게 설정이 가능한 제약조건이다.</u>
- **Durablility** (지속성) : **성공적으로 수행된 트랜잭션은 영구히 반영된다**는 의미이다. MYSQL을 포함해 많은 DB들의 구현에서는 트랜잭션 조작을 하드디스크에 로그로 기록하고, <u>시스템에 이상이 발생하면 그 로그를 이용하여 복원하는 것으로 지속성을 실현</u>하고 있다고 한다.



---



## @Transactional 옵션

### isolation level (격리 레벨)

- **isolation이란?** 

  **동시에 여러 트랜잭션이 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있도록 허용할지 말지를 결정**하는 것.

![img](http://www.skby.net/blog/wp-content/uploads/2018/11/1-27.png)

이 격리 레벨(격리수준)이 높아질수록 **동시성(concurrency)은 높아지고 속도는 느려진다.**

1. **READ_UNCOMMITED (level 0)**

   : 트랜잭션 처리 중이거나 아직 커밋되지 않은 데이터를 다른 트랜잭션에서 read하는 것을 허용한다. => `Dirty read` 발생 

   - **dirty read**란 ? 커밋하지 않은 데이터를 읽는 것

2. ✏**READ_COMMITED (level 1)**

   : 트랜잭션이 커밋되어 **확정된 데이터만을 읽도록 허용**하여 `dirty read`가 발생하지 않도록  보장한다.

   -  `Non-repeatable read` 발생

   

3. ✏**REPEATABLE_READ (level 2)**

   : **데이터 조회시 항상 동일한 데이터 응답을 보장**하는 격리수준이다. `READ_COMMITED`는 한번 데이터를 조회 후, 다시 조회했을 때 두 데이터가 동일하다는 것을 보장해주지 않는다. 왜냐면 그 사이 다른 트랜잭션에서 해당 데이터가 갱신되었을 수 있기 때문이다. 이를 `Non-repeatable read`라고 한다. **이 격리수준은 트랜잭션이 완료될 때까지 select를 사용하는 모든 데이터에 `shared lock`이 걸린다.** 

   ![Phantom Read](https://i.stack.imgur.com/aCtew.png)

    (위 이미지에서 보면 bob이 두번째 select문을 수행했을 때 post_comment가 하나 더 증가한 값이 조회된다.)

   

   <절차>

   1. read 트랜잭션이 n개의 레코드를 read함. : select
   2. write트랜잭션에 의해 insert수행됨. (레코드 카운드 n+1로 증가) : **insert** **or delete**
   3. read트랜잭션은 동일한 데이터에 대해 재수행했으나 처음보다 n+1증가함. : select

   

   `phantom read`가 발생할 수 있다.

   - **phantom read란?** read 트랜잭션 도중에 다른 트랜잭션(write)으로 인해 데이터가 수정되고, 두번째 조회시에 이전 쿼리의 결과와 다른, 변경된 값이 조회되는 것을 의미한다,

     > A phantom read occurs when, in the course of a transaction, two identical queries are executed, and the collection of rows returned by the second query is different from the first. 
     >
     > 출처 : 위키피디아 

4. ✏**SERIALIZABLE (level 3)**

   ​	 가장 높은 격리수준(매우 엄격하다)을 제공한다. 그만큼 동시성 처리효율은 떨어진다.



---



### 💡non-repeatable-read와 phantom read 간의 차이점

그래서 스택오버플로우에도 non-repeatable-read와 phantom read 간의 차이점에 대해 묻는 글(아래 참고자료 확인)이 올라올 정도로 좀 헷갈릴 수 있는데, 정리하자면

- non-repeatable-read는 1개의 행을 조회했을 때 발생한다. 
  1. A의 a계좌의 잔액을 조회했음  -> 잔액: 4000원 (A 트랜잭션) : select
  2. 그 사이에 B가 A의 a계좌로 1000원을 이체했음. (B 트랜잭션) : **update**
  3. A의 a계좌의 잔액을 조회했음 -> 잔액 : 5000원 (A트랜잭션) : select

- phantom read는 여러 레코드를 조회했을 때 발생한다. (그 사이에 insert나 delete 트랜잭션이 발생했을 수 있음)

> - ***Dirty reads***: read UNCOMMITED data from another transaction
> - ***Non-repeatable reads***: read COMMITTED data from an `UPDATE` query from another transaction
> - ***Phantom reads***: read COMMITTED data from an `INSERT` or `DELETE` query from another transaction



---



**각 DB별 격리수준**

- MYSQL : REPEATABLE READ 
- ORACLE, PostgreSQL : READ COMMITTED 
- H2 : READ COMMITTED

DB에서 이러한 격리수준을 변경하는 표준 명령어는 `SET TRANSACTION `이다.

---



### propagation (전파속성)

transaction propagation이란 현재 transaction에서 다른 transaction으로 이동할 때를 이야기한다.

- 기본값은 `Propagation.REQUIRED` 이다.
  - 부모트랜잭션 내에서 실행되며 부모트랜잭션이 없을 경우, 새로운 트랜잭션을 생성한다.



#### @Transactional(propagation = Propagation.NEVER)

- 참고자료 : https://n1tjrgns.tistory.com/266

```java
@Transactional(propagation = Propagation.NEVER)
public void doSomeThing() {...}
```

- non-transactional 로 실행되며 부모 트랜잭션이 존재하면 Exception이 발생한다.
- **non-transactional**이란? transaction은 존재하지만, 커밋과 롤백이 되지 않는 상태.
- **JPA의 객체 변경감지는 transaction이 커밋될때 작동.** → 그래서 `NOT_SUPPORTED` 같은 트랜잭션은 `TransactionSynchronizationManager.getCurrentTransactionName()` 메소드로 조회했을 때 이름이 존재하지만 **JPA Dirty Checking 은 동작하지 않습니다.**
- 여기에서 `Dirty`란 **상태의 변화가 생긴** 정도로 이해하시면 됩니다. 즉, Dirty Checking이란 **상태 변경 검사**입니다.
- 당연히 이런 상태 변경 검사의 대상은 **영속성 컨텍스트가 관리하는 엔티티에만**적용됨.



#### Propagation.REQUIRES_NEW

- **부모 트랜잭션이 존재하더라도 현재 트랜잭션을 새로 만든다.**

- 새로운 트랜잭션 안에서 예외가 발생해도 호출한 곳에는 롤백이 전파되지 않는다.

  (자식이 실패해도 부모 트랜잭션에 영향을 미치지 X)

  ```java
  @Transactional(propagation = Propagation.NEVER)
  public void transactionService() {
    log.info("currentTransactionName : {}", TransactionSynchronizationManager.getCurrentTransactionName());
  }
  ```

---



### readOnly 속성

- true인 경우 insert, update, delete 실행시에 예외가 발생된다.

```java
@Transactional(readOnly = true)
```



----

✨👍@Transactional 어노테이션은 **서비스단에 위치**하는 것을 권장한다. 

아래는 스택오버플로우 답변이다.

> Ideally, Service layer (**Manager**) represents your business logic and hence it should be annotated with `@Transactional`.
>
> Service layer may call different DAOs to perform DB operations. Lets assume a situation where you have 3 DAO operations in a service method. If your 1st DAO operation failed, other two may be still passed and you will end up with an inconsistent DB state. Annotating Service layer can save you from such situations.



--------

## 참고자료

- 💚[spring framework reference: transaction](https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/transaction.html)
- 💚[spring 공식문서 한글화](https://godekdls.github.io/Spring%20Data%20Access/transactionmanagement/)

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

- http://blog.skby.net/phantom-read/

- https://stackoverflow.com/questions/11043712/what-is-the-difference-between-non-repeatable-read-and-phantom-read

- 💛[Declarative or Programmatic Transaction in Spring](https://stackoverflow.com/questions/11222103/declarative-or-programmatic-transaction-in-spring)

- [TransactionTemplate 을 이용한 Spring Transaction 사용](https://blog.naver.com/tkstone/50192724315)|

- https://cobbybb.tistory.com/17

- [Spring AOP에서 proxy란?](https://velog.io/@gwontaeyong/Spring-AOP%EC%97%90%EC%84%9C-Proxy%EB%9E%80)