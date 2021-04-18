#### 2021-04-16

오늘은 **hoisting**에 대해 정리를 해보려고 한다.



## var키워드

- ES6 이전에 변수를 선언하는 방식은 `var`뿐이었다. 

  이 `var`는 `functinon-level-scope`로, **함수 내부**의 `var`로 선언된 변수들은 모두 끌어올려진다.

  ```javascript
  var apple = 'apple';
  
  //1. var키워드 생략 가능
  banana = 'banana';
  
  //2. 중복 선언 가능
  var apple = '사과';
  
  //'사과'가 출력된다
  console.log(apple);
  
  
  //3. hoisting
  console.log(computer); //undefined
  var computer = '컴퓨터';
  console.log(computer);
  
  
  ```





## Hoisting 이란?

- **<u>함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효범위의 최상단에 선언하는 것.</u>**
- 자바스크립트 parser가 함수 실행 전 해당 함수를 한번 훑고, 함수 내부에 존재하는 **변수/함수 선언**에 대한 정보를 기억하고 있다가 실행시킨다.
- <u>**`var`변수** 선언과 **함수선언문**에서만 호이스팅</u>이 일어난다.

아래는 직접 작성해본 **함수 호이스팅 예제**이다.

```javascript

//var로 변수 선언만 한 상태
var func1;
var func2;
var func3;

function func1(){
  console.log('func1');
}

func1();

//정상적으로 실행됨
func2();

//Uncaught TypeError: func3 is not a function 
func3();

//hoisting으로 인해 끌어올려져서 에러가 발생하지 않고 상단의 func2()가 정상적으로 실행된다
function func2(){
  console.log('func2');
}

//변수에 할당된 함수표현식은 끌어올려지지 않는다
func3 = function(){
  console.log('func2');
}
```



## const, let

- ES6에서 `const`와 `let`이 등장했다.
- `let`과 `const`는 `block-level-scope`이다. 호이스팅X
- 변수 중복 선언X
- `const`의 경우 상수를 선언할 때 사용할 수 있다.

```javascript
//1. 호이스팅X
//Uncaught ReferenceError: Cannot access 'love' before initialization 
console.log(love);
const love = 'love';

//2. 변수 중복선언X
let star = 'star';
//Uncaught SyntaxError: Identifier 'star' has already been declared 
let star = '별';
```



## Function Declarations, Function Expressions

한국말로는 **함수선언식, 함수표현식** 이라고 한다.



- **함수선언식(function declarations)**

```javascript
function funcName(){
    //...
}

funcName();
```

- **함수 표현식(function expression)**

```javascript
var variable = function(){
    //
}

variable();
```

함수표현식에서는 호이스팅이 발생하지 않는다.

그래서 **클로져, 콜백함수**로 사용된다고 한다.  해당 부분에 대해서는 게시물을 새로 파서 살펴보도록 하겠다.



----------

## 참고자료

- https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html
- https://happycording.tistory.com/entry/let-const-%EB%9E%80-%EC%99%9C-%EC%8D%A8%EC%95%BC%EB%A7%8C-%ED%95%98%EB%8A%94%EA%B0%80-ES6
- https://gmlwjd9405.github.io/2019/04/20/function-declaration-vs-function-expression.html

- [함수표현식 vs 함수선언식](https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/)