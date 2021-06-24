### ORM(object-relational mapping)

- object-relational mapping (객체와 RDB 매핑) → **<u>객체와 RDB의 테이블이 매핑</u>**을 이루는 것.
- 즉, **RDB 테이블을 객체지향적으로 사용하기 위한 기술**이다.



이전에 MyBatis를 쓴 적이 있었는데 이는 SQL Mapper이다. ORM은 객체를 매핑하는 것이고, SQL Mapper는 쿼리를 매핑하는 것이다.



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

- JPA (Java Persistence API) : **자바 ORM 기술에 대한 API 표준 명세.**

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





----

### 참고자료

- https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/

- https://goddaehee.tistory.com/209

- [lombok 기능정리-getter, setter, MoArgsConstructor, RequiredArgsConstructor, AllArgsConstructor](https://dingue.tistory.com/14)