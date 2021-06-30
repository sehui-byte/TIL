### ORM(object-relational mapping)

- object-relational mapping (객체와 RDB 매핑) → **<u>객체와 RDB의 테이블이 매핑</u>**을 이루는 것.
- 즉, **RDB 테이블을 객체지향적으로 사용하기 위한 기술**이다.



이전에 MyBatis를 쓴 적이 있었는데 이는 SQL Mapper이다. **ORM은 객체를 매핑**하는 것이고, SQL Mapper는 쿼리를 매핑하는 것이다.



> **MyBatis 예제** 
>
> MyBatis의 경우 SQL문이 xml로 작성되어 자바 코드로부터 완전히 분리되고, SQL쿼리를 매핑한다.
>
> (https://github.com/sehui-byte/spring-study/blob/main/ksh/2021-01-12.md)

```java
@Repository
public class LoginDAOImpl implements LoginDAO {

	@Autowired(required=false)
	private SqlSessionTemplate sqlSession;
	
	@Override
	public List<MemberVO> loginCheck(MemberVO mvo) {
		return sqlSession.selectList("loginCheck", mvo);
	}
}
```



------------------



### JPA

- JPA (Java Persistence API) : <u>**자바 ORM 기술에 대한 API 표준 명세.**</u>

- Hibernate, OpenJPA 등이 JPA를 구현한 구현체이다.

  

```java
@Getter
@Setter
@NoArgsConstructor
@Entity
@Table(name="STUDENT")
public class Student {
    
    @Id
    private String id;
    private String name;
    private String age;
    
}
```



---------



### spring-data-JPA

- 개발자는 인터페이스만 작성하고, spring data JPA가 구현 객체를 동적으로 생성해서 주입한다.



```yaml
jpa:
    hibernate.ddl-auto: none
    generate-ddl: false
```



#### hibername.ddl-auto

- `none`
- `create-drop`
- `create`
- `update`
- `validate`





### JPA Persistence Context

- `entity`를 영구히 저장하는 환경.

- 쓰기 지연 SQL 저장소



#### Dirty Checking







----------



### QuerySDL

- **SQL 쿼리를 메소드 기반으로 작성**할 수 있도록 도와주는 프레임워크.
  - JPA를 사용하면서 복잡한 조회 쿼리의 경우 `QuerySDL`을 사용하면 편리하다.
  - 컴파일 타임에 문법 오류를 잡을 수 있고, IDE의 도움을 받을 수 있어 편리하다.
- `QueryDSL`로 쿼리문을 작성하기 위해 `Q타입 클래스`(QueryDSL전용 객체, prefix 'Q'가 붙는 클래스들 자동생성) 를 사용한다.
- `JPAQuery` 클래스를 사용하면 `EntityManager`를 통해서 질의가 처리되고, 이때 사용하는 쿼리문은 `JPQL`이다.



#### QuerySDL - dynamic query



- **BooleanBuilder**
  - 조건들을 이어붙여서 where에 넣어주는 방식.
  - **쿼리의 형태를 예측하기 어렵다**는 단점이 있다.

```java
public List<Student> findDynamicQuery(String name, String age){
    BooleanBuilder builder = new BooleanBuilder();
    
    if(!StringUtils.isEmpty(name)) {
        builder.and(student.name.eq(name));
    }

    if(!StringUtils.isEmpty(age)) {
        builder.and(student.age.eq(age));
    }	
    return queryFactory.selectFrom(student).where(builder).fetch();
}

```



- **BooleanExpression**

  - `Querydsl`의 `where`은 `null`이 파라미터로 올 경우 조건문에서 제외한다.

    

아래 코드에서 만약 `age` 값이 없으면 해당 조건 제외.

```java
public List<Student> findDynamicQueryAdvance(String name, String age) {
	return queryFactory
		.selectFrom(student)
		.where(eqName(name),
				eqAge(age))
		.fetch();
}

private BooleanExpression eqName(String name) {
	return StringUtils.isEmpty(name) ?  null : student.name.eq(name);
}

private BooleanExpression eqAge(String age) {
	return StringUtils.isEmpty(age) ?  null : student.name.eq(age);
}
```







----

### 참고자료

- https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/

- https://goddaehee.tistory.com/209

- [lombok 기능정리-getter, setter, MoArgsConstructor, RequiredArgsConstructor, AllArgsConstructor](https://dingue.tistory.com/14)

- https://ict-nroo.tistory.com/117

- http://ojc.asia/bbs/board.php?bo_table=LecJpa&wr_id=341

- https://perfectacle.github.io/2018/01/14/jpa-entity-manager-factory/

- [[Querydsl] 다이나믹 쿼리 사용하기](https://jojoldu.tistory.com/394)

- https://velog.io/@aidenshin/Querydsl-%EB%8F%99%EC%A0%81-%EC%BF%BC%EB%A6%AC