### java-비트연산자(bit shift 연산자)

말 그대로 bit를 shift시켜주는 연산자이다.

#### 종류
- `<<` : bit를 왼쪽으로 이동. 빈 자리는 0으로 채운다. 
- `>>` : bit를 오른쪽으로 이동. 빈 자리는 양수일 때 0으로, 음수일 때는 -1로 채운다.
- `>>>` : unsigned right shift

#### 주의점
- 연산 가능한 타입은 byte, short, int, long, char타입이 있는데 int보다 작은 타입의 경우 int로 변환되서 shift되므로 주의해야 한다.


#### >>>
`>>>` 연산자는 **최상위 부호 비트(MSB)를 신경쓰지 않고** 비트값들을 오른쪽으로 이동시킨 후에 왼쪽의 빈 공간은 모두 0으로 채운다. 그러므로 항상 '양수'이다.

------------------------
### bit shift연산 활용법
#### 1. byte형으로 형변환
```java
//long값을 바이트 배열로 변환
public static byte[] toBytes(long longValue){  
        return new byte[]{    
  (byte)((longValue >> 56) & 0xff),  
  (byte)((longValue) >> 48 & 0xff),  
  (byte)((longValue) >> 40 & 0xff),  
  (byte)((longValue) >> 32 & 0xff),  
  (byte)((longValue) >> 24 & 0xff),  
  (byte)((longValue) >> 16 & 0xff),  
  (byte)((longValue) >> 8 & 0xff),  
  (byte)((longValue) >> 0 & 0xff)  
        };  
  }  
}
```

위의 코드는 long형을 byte배열로 변환하는 것이다.   

먼저 그냥 `(byte)` 이런식으로 명시적으로 변환할 경우, java에서 byte 자료형의 범위는 -128~ 127 이다. 1개는 부호비트이므로 7개의 비트로만 수를 표현한다.  
그래서 127을 넘는 숫자는 모두 음수로 인식하게 된다. (부호비트가 0이면 양수이고, 부호비트가 1이면 음수이기 때문)

java에서 long 타입의 경우 -2^63 ~ 2^63-1 까지 표현한다. 비트연산자로 `[long타입숫자]>>56`을 해주면 7개의 비트만이 남는다.   
이런식으로 쪼갠 다음에 그 부분을 0xff와 논리연산자 `&`를 이용하여 연산한다. 0xff는 16진수로 표현하였지만 10진수 255, 2진수 1111 1111 이라는 숫자이다. 0xff는 int형이므로 byte형과 연산할 때 더 큰 타입인 int형으로 형변환이 일어난다. 그럼 남은 7개의 비트와 int형(4byte=32bit)가 연산을 하면   

```
0000 0000 0000 0000 0000 0000 0100 1001 (shift연산 후 남은 7개의 비트)
1111 1111 1111 1111 1111 1111 1111 1111 (0xff)
-------------------------------------------
0000 0000 0000 0000 0000 0000 0100 1001
```

이렇게 int형과 &연산을 함으로써 부호비트를 건드리지 않고 값만 가져올 수 있게 된다.

-----------------------------
    
 아래 코드로 2진수로 변환해보았다.
 `-1`의 경우 int형은 32bit이므로 `11111111111111111111111111111111`라는 결과를 보여주지만, char형은 16bit이므로 `1111111111111111`가 된다.  
 
 ```java
 public class MyClass {
    public static void main(String args[]) {
    int a = -1;
    char b = (char)-1;
    
    System.out.println(Integer.toBinaryString(a));//11111111111111111111111111111111
    System.out.println(Integer.toHexString(a));//ffffffff
    System.out.println(b & 0xff);//255
    System.out.println(Integer.toBinaryString((int)b));//1111111111111111
    }
}
 ```

-------------------------
### 참고자료
- [자바에서 비트연산자를 사용한 byte양수표현 및 0xff사용법](https://emflant.tistory.com/133)
