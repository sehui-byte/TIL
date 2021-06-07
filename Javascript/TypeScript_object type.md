
## TypeScript의 Object타입  
- 타입스크립트에서 자바스크립트의 object처럼 사용하고 싶은 경우 `{}`사용.
- interface로도 사용할 수 있으며,
- object 타입에 이름을 지정할 수도 있다.  

```typescript

const obj = { 
  name:string,
  id: number
};

interface obj2 = {
  name: string,
  id: number
};

const a: obj = {
  name: string,
  id: number
};
```
  
 --------------
 ## 참고자료  
 - https://ponyozzang.tistory.com/243
