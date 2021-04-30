2021-04-16

이번엔 자바스크립트 클로저에 대해 공부해보려고 한다.



## Closure란?

- **내부함수가 외부함수의 context에 접근할 수 있는 것.**
- 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성 의미.
- **closure는 자바스크립트의 고유개념이 아니라, 함수를 일급 객체로 취급하는 functional programming language에서 사용되는 중요한 특성**이라고 한다.
- **lexical scoping** : scope는 함수가 호출될때가 아니라, 함수를 어디에 선언했는지에 따라 결정된다. 



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



-----



### this 바인딩

- 메서드 내부 코드에서 사용된 `this`는 해당 메서드를 호출한 객체로 바인딩된다.

- 자바스크립트에서 함수를 호출하면 해당 함수 내부 코드에서 사용된 `this`는 전역객체에 바인딩된다.

  브라우저에서 자바스크립트를 실행하는 경우 전역객체는 `window`이다.

- 내부함수도 '함수'이기 때문에 내부 함수 호출시에도 전역객체에 바인딩된다.



```javascript

var value = 100;

var myObj = {
  name : 'myObj',
  value : 1,
  func1: function(){
    var that = this;
    console.log(that.name); //호출한 객체로 바인딩되어 this는 myObj가 됨
    console.log('that ' + that.value);
    
    console.log('this ' + this.value);
    
    //func1 의 내부함수
    var func2 = function(){
      that.value += 1;
      this.value += 1;
      console.log('that ' + that.value);
      console.log('this ' + this.value);
      
      var func3 = function(){
        that.value += 1;
        this.value += 1;
        console.log('that ' + that.value);
        console.log('this ' + this.value);
      }
      
      func3();
    }
    func2();
  }
}

myObj.func1(); 
```

위 코드에 대한 실행결과는 [여기](https://codepen.io/sehui-byte/pen/BapbOzK)에서 확인할 수 있다.







----------

## 참고자료

- [생활코딩-클로저](https://opentutorials.org/course/743/6544)
- https://poiemaweb.com/js-closure
- 모던 자바스크립트
- 인사이드 자바스크립트