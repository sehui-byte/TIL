
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

String birthDay = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE);

```

## java8 - java.time패키지

- **java.time 패키지** : **java8에 추가된 날짜와 시간에 대한 api**이다**.** 이전에 자바의 기본 SDK에서 java.util.Date클래스와 java.util.Calendar클래스의 불편함을 개선하기 위해 나온 api라고 한다.

    **<Date클래스와 Calendar클래스의 문제점>**

    - **not immutable** : 불변객체가 아니라서 Calendar객체나 Date객체가 여러 곳에서 공유될 경우 영향을 받을 수 있다 ( 값이 바뀔 수 있다).
    - **month값이 헷갈린다** : `Calendar.OCTOBER`의 값은 9이다. Date클래스는 1월을 0으로 시작해서 값이 1씩 차이나서 헷갈릴 수 있다는 단점이 있다.

    이밖에도 다양한 문제점들이 있다고 하는데 추후 더 참고자료를 꼼꼼히 읽어볼 예정이다.

    ### java.time패키지

    - This class is **immutable and thread-safe.**
    - `LocalDate` : 날짜 정보만 필요할 때 사용.
    - `LocalTime` : 시간 정보만 필요할 때 사용.
    - `LocalDateTime` : 날짜, 시간 정보 모두 필요할 때 사용.

형식을 지정하려는 경우 DateTimeFormatter클래스에서 `format()`과 `parse()` 를 사용할 수 있다.

- `format()` → String으로 반환
- `parse()`  → LocalDate로 반환
- `DateTimeFormatter.ISO_DATE`  → `"yyyy-mm-dd"`

------------------

### 참고자료
- [자바8 java.time 패키지](http://blog.eomdev.com/java/2016/04/01/%EC%9E%90%EB%B0%948%EC%9D%98-java.time-%ED%8C%A8%ED%82%A4%EC%A7%80.html)
- [자바의 날짜와 시간 api](https://d2.naver.com/helloworld/645609)
