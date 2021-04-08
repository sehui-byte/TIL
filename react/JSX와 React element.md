
## JSX란?  
- javascript를 확장한 문법.
- JSX는 React elements를 생성한다. React는 JSX 사용이 필수는 아니지만, UI관련 작업을 할 때 시각적으로 더 도움이 된다고 한다.
- JSX에서 중괄호`{}`를 이용하여 자바스크립트 구문을 실행시킬 수 있다.

```javascript
const name = "JSX";
const element = <h1>Hello, {name} </h1>;
```
![image](https://user-images.githubusercontent.com/64109506/113949650-b664e700-984a-11eb-856d-c65662ed9510.png)
  
- XSS(cross-site-scripting) 공격 방지.
  React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 escape하므로 에플리케이션에서 명시적으로 작성되지 않은 내용은 주입하지 않는다.
  모든 항목은 렌더링 되기 전에 문자열로 변환된다.  
  
- react element를 생성한다. (Babel은 JSX를 `React.createElement()` 호출로 컴파일한다.)
- createElement(elementName, data, child);
- element
  react는 이 객체를 읽어서 DOM을 구성하고 최신상태로 유지하는 데 사용한다.
```javascript
const element = (<h1 className = "greeting"> Hello, world! </h1>);

const element = React.createElement('h1', {className: 'greeting'}, 'Hello, world!');

```


------------------

## 참고자료
- [react공식 문서](https://ko.reactjs.org/docs/introducing-jsx.html)
- [React공식문서-Element Rendering](https://ko.reactjs.org/docs/rendering-elements.html)
