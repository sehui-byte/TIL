

### 실행컨텍스트(Execution Context)

- 쉽게말하면 **코드가 실행되고 있는 구역, 범위에 대한 개념**.



자바스크립트 엔진은 **코드를 실행하기 위해 실행에 필요한 여러가지 정보**를 알고 있어야 한다. 

그 여러가지 정보란 아래와 같은 정보들이다.

- 변수 : 전역변수, 지역변수, 매개변수, 객체의 프로퍼티
- 함수 선언
- 변수의 유효범위
- this



자바스크립트 엔진은 이와 같이 코드 실행에 필요한 정보를 형상화하고 구분하기 위해서 **실행컨텍스트를 물리적 객체의 형태로 관리**한다.

![img](https://poiemaweb.com/img/excute_context_structure.png)

- **variable object**
  - 실행컨텍스트가 생성되면 자바스크립트 엔진은 실행에 필요한 여러 정보들을 담을 객체를 생성한다. 이를 VO라고 한다.
  - 변수, paramter, arguments, 함수선언(함수표현식 제외) 와 같은 정보를 담는다.
  - 
- scope chain
- thisValue



#### Types of Execution Context

- **Global Execution Context** 
  - 가장 베이스가 되는 실행구역. 특정 함수 안에서 실행되는 코드가 아니라면, 코드는 전역 컨텍스트에서 실행된다. 

- **Functional Execution Context**
  - 함수가 호출될 때마다 해당 함수에 대한 실행 컨텍스트가 생성된다. 
  - 각각의 함수들은 자신만의 실행컨텍스트를 가지지만, <u>실행 컨텍스트는 함수가 호출이 되어야 만들어진다.</u>
- **Eval Function Execution Context**
  - 



---



### 참고자료

- [모던 자바스크립트](https://poiemaweb.com/js-execution-context)

-  **[Understanding Execution Context and Execution Stack in Javascript](https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0)**
  - [번역](https://velog.io/@imacoolgirlyo/JS-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-Hoisting-The-Execution-Context-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-6bjsmmlmgy)

- [자바스크립트의 실행컨텍스트와 호이스팅](https://velog.io/@imacoolgirlyo/JS-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-Hoisting-The-Execution-Context-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-6bjsmmlmgy)