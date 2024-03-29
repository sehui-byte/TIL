2021-04-16

이번엔 자바스크립트 클로저에 대해 공부해보려고 한다.



## Closure란?

- **내부함수가 외부함수의 context에 접근할 수 있는 것.**
- 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성 의미.
- **`closure`는 자바스크립트의 고유개념이 아니라, 함수를 일급 객체로 취급하는 `functional programming language`에서 사용되는 중요한 특성**이라고 한다.
- **lexical scoping** : scope는 함수가 호출될때가 아니라, **함수를 어디에 선언했는지에 따라 결정**된다. 



```javascript
function parent(){
  var a = 100;

    //내부함수
  var child = function(){
    console.log('I am a child!');
    console.log(a); //외부함수의 변수에 접근 가능
  }
  
  return child;
}

var inner = parent();
inner();
```

위 코드 마지막줄에 **렉시컬 스코프 밖에서 함수를 호출해도 원래 선언되었던 렉시컬 스코프를 기억하고 접근할 수 있도록 하는 특성**이 `closure`이다. 즉, 함수 실행이 끝났음에도 불구하고 여전히 스코프를 기억하고 있어 함수 호출이 끝난 후에도 해당 함수의 내부함수에 접근할 수 있는 것이다.





----------

## 참고자료

- [생활코딩-클로저](https://opentutorials.org/course/743/6544)
- https://poiemaweb.com/js-closure
- 모던 자바스크립트
- 인사이드 자바스크립트

- https://leehwarang.github.io/2019/10/07/scope.html