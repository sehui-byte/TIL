
 
## Component  

```javascript
class Subject extends Component{
  render(){
    return (
      //하나의 최상위 태그만 써야 한다
      <header>
        <h1>{this.props.title}</h1>
        {this.props.sub}
      </header>
    );
  }
}
```  

## props  
  
- props란? : 부모컴포넌트가 자식 컴포넌트에게 값을 전달할 때 사용하는 것.
- 읽기 전용.


#### index.js
```javascript
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

```

#### App.js
```javascript
import React, { Component } from 'react';
import './App.css';

class Subject extends Component{
  render(){
    return (
      <header>
        <h1>{this.props.title}</h1>
        {this.props.sub}
      </header>
    );
  }
}

class App extends Component{
  render(){
    return (
      <div className="App">
        Hello, React!
        <Subject title="WEB" sub="world wide web!"></Subject>
        <Subject title="HELLO" sub="hello world"></Subject> 
      </div>
    );
  }
}


export default App;

```
  
   
     
     
위의 소스코드는 App.js에 여러 개의 Components를 만들어 넣었다.   
이를 아래의 소스코드와 같이 쓰면,  
하나의 파일에 다 담지 않고 여러개의 파일로 쪼개서 각 컴포넌트를 담고, App.js에 import하여 사용할 수 있다.

#### App.js  
  
아래와 같이 import 해줘야 한다.
```javascript
import React, { Component } from 'react';
import Subject from "./components/Subject";
import TOC from "./components/TOC";
import './App.css';


class App extends Component{
  render(){
    return (
      <div className="App">
        Hello, React!
        <Subject title="WEB" sub="world wide web!"></Subject>
        <Subject title="HELLO" sub="hello world"></Subject>
        <TOC></TOC>       
      </div>
    );
  }
}


export default App;

```  
  

## State
  
- state란? : 컴포넌트 자신이 가지고 있는 값. 
- 상위컴포넌트의 state를 이용해서 하위컴포넌트에게 전달할 수 있다.

```javascript
...

class App extends Component{
  constructor(props){
    super(props);
    this.state = {
      Subject: {title: 'WEB', sub: 'World Wide Web!'}
    }
  }
  render(){
    return (
      <div className="App">
        Hello, React!
        <Subject title={this.state.Subject.title} sub={this.state.Subject.sub}></Subject>
       ...
      </div>
    );
  }
}


export default App;

```

### props vs state
- 참고자료 : https://github.com/uberVU/react-guide/blob/master/props-vs-state.md
- `props`는 함수의 매개변수처럼 컴포넌트에 **전달**되는 반면, `state`는 함수 내에 선언된 변수처럼 **컴포넌트 안에서 관리**된다.  

![image](https://user-images.githubusercontent.com/64109506/113539626-2b50da80-9619-11eb-8aae-26f9e53584ba.png)  

  
  
 -------------------------------
 
 ## 이벤트  
   
 - e.preventDefault() : a태그나 submit태그(페이지 이동이나 페이지 새로 실행되는 등...) 같은 경우 기본적인 동작을 하는데 `preventDefault()`는 이러한 기본 동작을 막아준다.
 - this와 bind() : JS에서 바인딩하지 않고 함수 호출시에 `this`는 `undefined`가 되기 때문에 바인딩을 해주어야 한다.
 ```javascript
  <header>
    <h1><a href="/" onClick={function(e){
      e.preventDefault();
      this.setState({
        mode:'read'
      });
      //바인딩하지 않으면 함수호출시에 this는 undefined가 된다
    }.bind(this)}>{this.state.subject.title}</a></h1>
    {this.state.subject.sub}
 </header> 
 ```
 
 ### JavaScript에서 this란?  
 인터프리터에 의해 **현재 실행되는 자바스크립트 코드**를 **실행컨텍스트**(execution context)라고 한다. 자바스크립트 내부에서는 이러한 실행 컨텍스트를 stack으로 관리하고 있고, 실행되는 시점에 자주 변경되는 실행 컨텍스트를 this가 가리키고 있다.
 
 - 기본적으로 this는 전역객체를 가리킨다.
   - node환경 : global 객체
   - browser : window 객체
   를 가리킨다.
- 일반적인 함수 내부에서 this를 호출하면 전역객체를 가리킨다.
- 만약 함수 내부 or 외부에서 strict모드를 사용한다면 함수 내부에서 this는 전역객체를 바인딩하지 않는다.
- 객체 내부의 메소드에서 this를 바인딩할 경우, 그 객체 자신을 가리키게 된다.
   
    

## setState()    

컴포넌트 생성이 끝난 후에 **동적으로 state 값을 바꾸려면** `setState()`메서드를 사용해야 한다.    
  
  
아래 코드는 TOC의 `<li>`를 클릭하면 해당 번호에 해당하는 `contents` 값이 하단에 출력되는 코드이다.  
 
#### App.js
```javascript
import React, { Component } from 'react';
import Subject from "./components/Subject";
import TOC from "./components/TOC";
import Content from "./components/Content";
import './App.css';


class App extends Component{
  constructor(props){
    super(props);
    this.state = {
      mode: 'welcome',
      selected_content_id : 2,
      welcome: {title: 'Welcome', desc:'Hello, React!'},
      subject: {title: 'WEB', sub: 'World Wide Web!'},
      contents: [
        {id:1, title:'html', desc:'Html is HyperText...'},
        {id:2, title:'css', desc:'css is for design...'},
        {id:3, title:'JavaScript', desc: 'Javascript is for interactive...'}
      ]
    }
  }
  render(){
    console.log('App render');
    var _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    }else if(this.state.mode === 'read'){
      var i= 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i = i+1;
      }
      
    }

    return (
      <div className="App">
      
      //...중략
      
       <TOC 
          onChangePage={
            function(id){
                this.setState({
                mode:'read',
                selected_content_id: Number(id)
              });
          }.bind(this)}

          data={this.state.contents}>
        </TOC>

```
  
 #### TOC.js
 ```javascript
 import React, { Component } from "react";

class TOC extends Component{
  render(){
    var data = this.props.data;
    var i = 0;
    var lists = [];
    while(i < data.length){
      //여러개의 element를 자동으로 생성할 경우 
      //각각 key라는 props를 갖고 있어야 한다
      lists.push(
        <li key={data[i].id}>
          <a href={"/content/" + data[i].id}
            data-id = {data[i].id}
            onClick={function(e){
              e.preventDefault();
              this.props.onChangePage(e.target.dataset.id);
            }.bind(this)}
            >{data[i].title}
          </a>
        </li>);
      i += 1;
    }
    return(
      lists
    );
  }
}

export default TOC;
 ```

  
-----------
### 참고자료 
- 생활코딩 react 강좌
- https://webruden.tistory.com/275
- [react 공식 문서](https://ko.reactjs.org/docs/faq-state.html)
- [javascript this binding 정리](https://medium.com/sjk5766/javascript-this-binding-%EC%A0%95%EB%A6%AC-ae84e2499962)
- [js- 실행 컨텍스트](https://poiemaweb.com/js-execution-context)
