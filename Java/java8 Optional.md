### java8 Optional

- **java8에서 null값을 쉽게 처리하기 위해 제공되는 wrapper 클래스**



- `Optional.empty()` : null을 담고 있는 비어있는 Optional객체를 가져온다.
- `Optional.of(value)` : null이 아닌 객체를 담고 있는 Optional객체를 생성. null이 넘어올 경우 NPE를 발생시킨다.

- `Optional.ofNullable()` :
  - 명시된 값이 null이 아닐 경우 명시된 값을 가지는 Optional객체를 반환
  - null일 경우 비어있는 Optional객체 반환.

- `get()`메소드를 이용하여 Optional객체의 값에 접근할 수 있다. 그러나 만약 값이 비어있다면(null이라면) `NoSuchElementException`을 발생시키므로 이전에 `isPresent()`메소드를 이용하여 Optional객체에 저장된 값이 null인지 아닌지를 먼저 확인해볼 수 있다.

```java
 @Override
 public boolean exists(String memberId) {
 //isPresent() : 객체 존재 여부를 boolean타입으로 반환
	return Optional.ofNullable(memberMap.get(memberId)).isPresent();
  }
```

- `ifPresent()` : Optional 객체가 non-null일 경우에 인자로 넘긴 함수를 실행시키는 메서드이다.

- `orElse()` : Optional에 값이 있든 없든 ***무조건 실행***한다.
  - 값이 있는 경우 해당 값을 리턴하고, 값이 없는 경우 orElse(T other) 의 `other`값을 리턴한다.

- `orElseGet()` : 새로운 객체를 생성하거나 새로운 연산을 수행하는 경우에는 orElse()대신 orElseGet()을 써야한다.

- `map()` 메서드는 해당 값이 null이 아니면 mapper를 이용해 계산한 값을 저장하는 Optional객체를 리턴한다. 만약 값이 null이라면 빈 Optional객체를 리턴한다.

- `filter()` 메서드는 단순히 값을 확인하고 ***boolean을 리턴***한다.



----



아래 코드는 Optional을 이해하기 위해 간단히 짜본 것이다.

```java
import java.util.*;

public class Main
{
	public static void main(String[] args) {
		String s = null;
		//String s = "hi";
	
	    //ofNullable()은 null일 경우 빈 optinal객체를 리턴한다
		if(Optional.ofNullable(s).equals(Optional.empty())){
		    s = "빈 null 객체";
		}
		System.out.println(s);
		
		//orElse() : null이든 아니든 무조건 실행한다
		String s2 = "s2";
		System.out.println(Optional.ofNullable(s2).orElse("null이다"));
	}
}
```



---

### 참고자료

- [java8 doc - optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html#orElse-T-)