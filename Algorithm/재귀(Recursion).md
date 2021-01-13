  
  
  재귀와 관련된 개념을 공부하다보니 재귀에 대한 기억이 조금 흐릿한 것 같아서 간단하게만 다시 정리했다.  
재귀는 다른 알고리즘과 관련해서도 정말 자주 나오는 개념이기 때문에 잘 숙지해두어야 한다.  
지금은 간단히만 적어두고, 이후에 조금씩 업데이트해나가야겠다.   

----

# 재귀(Recursion)

- 자기 자신을 호출하는 함수.
>![image](https://user-images.githubusercontent.com/64109506/104472329-30e0ea80-55ff-11eb-899a-8e8af3a4488f.png)
> 재귀란 마치 이런 것.. 

## 팩토리얼 구현

- 팩토리얼은 대표적인 재귀함수(recursion) 예제이다.

`4!` 를 구한다고 치자.

![image](https://user-images.githubusercontent.com/64109506/104472337-34747180-55ff-11eb-8dcc-6fec79cfea4d.png)  
`4!`을 구하는 과정은 마치 위와 같다. 

이런 방식으로 팩토리얼을 계산하면 코드는 아래와 같이 된다.

```java
public static int factorial(int n){
	if(n == 1)
		return 1;
	
	else
		return n*factorial(n-1);
}
```


![image](https://user-images.githubusercontent.com/64109506/104472351-3807f880-55ff-11eb-8c03-d99ce9c47a76.png)  
![image](https://user-images.githubusercontent.com/64109506/104472378-3e967000-55ff-11eb-9ab7-b5cfb303ed6e.png)  
결국 `n`이 1이 되면 1을 반환 받아서 계산을 쭉 해서 최종 결과값을 도출해낸다.

이는 **스택(Stack)을 이용하여 비재귀적(non-recursive)인 코드**로 바꿀 수도 있다.

```java
public static int factorial(int n){
	    Stack<Integer> s = new Stack<Integer>();
	    int result =  1;
	    
	    while(true){
	        if(n >= 1){
	            s.push(n);
	            n = n - 1;
	            continue;
	        }
	        if(!s.isEmpty()){
	            int top = s.pop();
	            result *= top;
	            continue;
	        }
	        break;
	    }
	    return result;
	}
}
```
