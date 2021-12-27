## constant interface



인터페이스를 상수 클래스로 사용하다가 궁금해서 찾아보니 이러한 패턴은 **안티패턴(anti-pattern)**이라고 하여 이에 대해 찾아보게 되었다.

이러한 패턴을 **"constant interface**"라고 하고, 위키피디아에 이에 대해 등록되어있다.

- 위키피디아 글 : https://en.wikipedia.org/wiki/Constant_interface

 

> 자바 프로그래밍에서 상수 인터페이스 패턴(constant interface pattern)은
>
>  
>
> **인터페이스를 오직 상수를 선언하기 위해 사용하는 것**과 **인터페이스를 implements한 클래스들이 해당 상수들에 접근할 수 있도록 하는 것**
>
> 을 말한다.
>
> 그러나 상수들은 그저 구현세부사항이고, 클래스들에 의해 구현된 인터페이스들은 노출되는 API의 일부이기 때문에 이런 식으로 쓰는 건
>
>  API에 구현세부사항을 넣는 것으로 부적절
>
> 하게 여겨진다. 일반적으로 행위와 별개로 시스템 상수들만을 클래스에 모아두는 건 좋지 못한 객체지향 디자인이다. 왜냐하면
>
>  
>
> 낮은 응집도(cohesion)
>
> 을 갖기 때문이다. 이러한 이유들로 constant interface는 anti-pattern으로 여겨진다.
>
> 이러한 패턴을 사용하면 아래와 같이 몇가지 단점이 있다.
>
> \1. 사용되지 않는 read-only 변수들로 class namespace를 오염시킬 수 있다.
> \2. 컴파일 시점에 전략적인 유틸리티로 쓰이는 것과 달리, 런타임에는 실용적이지 않다.
>
>  
>
> (marker interface는 메서드는 없지만, 컴파일시에 유용하다)
>
> \3. 만약 다음 릴리즈 때 해당 상수가 필요 없어도 이전 버전과 호환성을 유지하려면 해당 상수는 영원히 인터페이스에 남아있어야 한다.
>
> \4. 해당 상수가 어디에서 오는지를 쉽게 보여주는 IDE가 없다면 해당 상수를 찾기 위해 많은 시간을 소모할 수 있다.
>
> \5. 인스턴스를 나타내는 인터페이스 변수는 인터페이스 이름 자체보다 유용하지 않다. (메서드가 없으므로)
>
> \6. 개발자가 클래스에 상수를 추가할 때 구현된 인터페이스를 확인하지 않으면 상수의 값이 변할 수 있다.
>
> 6번 내용은 아래 코드 참고.
>
> ```java
> public interface Constants {
> 
> 	public static final int	CONSTANT = 1;
> }
> 
> public class Class1 implements Constants {
> 
> 	public static final int CONSTANT = 2;	// *
> 
> 	public static void main(String args[]) throws Exception {
> 		System.out.println(CONSTANT);
> 	}
> }
> ```

 

이러한 이유들로 인해 constant interface를 쓰기보다는 **final 클래스**를 쓰는 것을 더욱 추천하는 것 같다.

```java
public final class Constants {

	private Constants() {
		// restrict instantiation
	}

	public static final double PI = 3.14159;
	public static final double PLANCK_CONSTANT = 6.62606896e-34;
}
```

 

- 관련 스택오버플로우 링크 : https://stackoverflow.com/questions/29382728/constant-interface-anti-pattern-clarification



---



출처: https://coffee-and-coding.tistory.com/entry/Java-Constant-interface은-안티패턴이다 [Coffee and Coding]