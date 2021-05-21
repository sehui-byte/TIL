자바스크립트에서는 실행 컨텍스트에 따라서 `this`의 값이 상황에 따라 다르게 나온다.



### this 바인딩

- 메서드 내부 코드에서 사용된 `this`는 해당 메서드를 호출한 객체로 바인딩된다.

  - *메서드 : 객체의 property가 함수일 때.*

- 자바스크립트에서 <u>함수를 호출하면 해당 함수 내부 코드에서 사용된 `this`는 전역객체에 바인딩</u>된다. `strict mode`에서는 함수 호출시 `this`가 `undefined`이다.

  브라우저에서 자바스크립트를 실행하는 경우 전역객체는 `window`이다.

  내부함수도 '함수'이기 때문에 <u>내부 함수 호출시에도 전역객체에 바인딩</u>된다.




```javascript
var value = 100;

var myObj = {
  name : 'myObj',
  value : 1,
  func1: function(){//func1 : 메서드
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



### apply(), call()



### bind()



### arrow function



----------

### 참고자료

- 인사이드 자바스크립트

- https://velog.io/@imacoolgirlyo/JS-JavaScript-Function-Invocation%EC%99%80-this