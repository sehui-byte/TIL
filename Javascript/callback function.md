자바스크립트는 **단일 스레드 프로그래밍언어**이므로 '**단일 호출 스택**'이 있다. 

즉, 한번에 하나의 일만 처리할 수 있다.



```javascript
function multiply(x,y){
    return x*y;
}

function printSquare(x){
    var s = multiply(x,x);
    console.log(s);
}

printSquare(5);
```

![img](https://t1.daumcdn.net/cfile/tistory/9995544C5C32151627)

자바스크립트에선 단일호출스택만 있기 때문에 하나의 함수가 처리시간이 길 경우 다른 함수 실행에 영향을 줄 수 있다. 이럴 경우 **비동기콜백(Asynchronous callbacks)**를 사용하여 해결할 수 있다.

이러한 콜백함수들은 스택에 바로 push되지 않고, **이벤트큐(Event Queue)**에 의해 관리된다.

![img](https://t1.daumcdn.net/cfile/tistory/99A7234F5C321A7F2B)



------------



## 콜백함수(Callback function)란?

- **파라미터로 전달되는 함수.**
- **다른 함수 실행 후에 실행되는 함수.**
- 자바스크립트는 `null`과 `undefined` 타입을 제외하고 모든 것을 객체로 다루기 때문에 함수를 변수나 다른 함수의 변수로 사용할 수 있다.

```javascript
function first(){
  //first()메소드 처리를 500ms 지연
  setTimeout(function(){
    console.log(1);
  }, 500);
}

function second(){
  console.log(2);
}


first();
second();

//실행결과 :
//2
//1

//first()함수가 더 늦게 실행된다
```

`second()`가 `first()`를 기다렸다가 실행시키도록하고 싶을 경우, 콜백함수를 이용해야한다.

```javascript

function first(callback){
  setTimeout(function(){
    console.log(1);
    callback();
  }, 500);
  
}

function second(){
  console.log(2);
}

first(second);
```

위처럼 콜백함수를 사용하면 `first()`가 먼저 실행되고, 그 다음에 `second()`가 실행된다.



그러나 콜백함수를 이용하여 줄줄이 아래와 같이 쓸 경우 콜백지옥...상황이 될 수도 있으므로 `Promise`나 `async/awiat`을 이용하는 방법들로 대체되고 있다고 한다.

![Callback Hell in JavaScript | Asynchronous JavaScript with Callbacks in  Hindi - YouTube](https://i.ytimg.com/vi/fr67u98nckk/maxresdefault.jpg)

![자바스크립트 콜백지옥 탈출기 - 1.영원한 사랑](https://bravenamme.github.io/files/posts/201910/promise_01.png)





## 콜백지옥 (Callback Hell)    

비동기 호출이 자주 일어나는 프로그램의 경우 콜백 지옥이 발생한다.        



- `Promise`
  
  - Promise 선언부
    - pending : 아직 약속을 수행중인 상태 (fullfilled나 rejected가 되기 전)
    
    - fulfilled : 약속이 지켜진 상태
    
    - rejected : 약속이 지켜지지 못한 상태. exception이 발생한 상황
    
      ```javascript
      let promise = new Promise(function(reslove, reject){
         //executor 
      });
      ```
    
      `new Promise`에 전달되는 함수는 executor라고 불린다고 한다. executor는 `new Promise`가 만들어질 때 자동으로 실행된다. executor의 인수 `resolve`와 `reject`는 자바스크립트가 자체적으로 제공하는 콜백으로, 개발자는 `resolve`와 `reject`를 신경쓰지 않고 executor 코드만 작성하면 된다.
    
      - `resolver(value)` : 일이 성공적으로 끝난 경우 그 결과를 나타내는 `value`와 함께 호출.
      - `reject(error)` : 에러 발생시 에러 객체를 나타내는 `error`와 함께 호출.



## this 보호하기    

콜백함수에서 `this`사용시에   

- `call()` : 첫번째 인자로 `this`객체 사용, 나머지 인자들은 `,`로 구분.
- `apply()` : 첫번째 인자로 `this`객체 사용, 나머지 인자들은 배열 형태로 전달.  







----



## 참고자료

- [자바스크립트 콜백함수](https://velog.io/@minidoo/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98Callback-Function)
- [콜백지옥에 promise 적용하기](https://preiner.medium.com/callback%EC%A7%80%EC%98%A5%EC%97%90-promise-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-d02272ecbabe)

- https://new93helloworld.tistory.com/358

- https://medium.com/@oasis9217/%EB%B2%88%EC%97%AD-javascript-%EB%8F%84%EB%8C%80%EC%B2%B4-%EC%BD%9C%EB%B0%B1%EC%9D%B4-%EB%AD%94%EB%8D%B0-65bb82556c56

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise

- https://ko.javascript.info/promise-basics