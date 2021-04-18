
## 콜백함수(Callback function)란?

- **파라미터로 함수를 전달**하는 함수.
- **다른 함수 실행 후에 실행되는 함수.**
- 자바스크립트는 null과 undefined 타입을 제외하고 모든 것을 객체로 다루기 때문에 함수를 변수나 다른 함수의 변수로 사용할 수 있다.





## this 보호하기    
콜백함수에서 `this`사용시에   

- call() : 첫번째 인자로 this객체 사용, 나머지 인자들은 `,`로 구분.
- apply() : 첫번째 인자라ㅗ this객체 사용, 나머지 인자들은 배열 형태로 전달.  
  



## 콜백지옥 (Callback Hell)    

비동기 호출이 자주 일어나는 프로그램의 경우 콜백 지옥이 발생한다.        
- `Promise`사용하여 해결할 수 있다.
  - Promise 선언부
    - pending : 아직 약속을 수행중인 상태 (fullfilled나 rejected가 되기 전)
    - fulfilled : 약속이 지켜진 상태
    - rejected : 약속이 지켜지지 못한 상태. exception이 발생한 상황











----



## 참고자료

- [자바스크립트 콜백함수](https://velog.io/@minidoo/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98Callback-Function)
- [콜백지옥에 promise 적용하기](https://preiner.medium.com/callback%EC%A7%80%EC%98%A5%EC%97%90-promise-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-d02272ecbabe)
