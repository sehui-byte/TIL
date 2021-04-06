
## 개발환경 세팅  
- node.js 설치
- VSCODE 설치
- 작업용 폴더 생성
 
       
         

## 프로젝트 생성 및 실행
```
npx create-react-app [project name]

//생성된 프로젝트 디렉토리로 이동
//서버 실행
npm start

//실제 서비스할때 사용
npm run build
```
    
    
   
## npm, npx 란?
 - **npm** : node.js로 만들어진 모듈을 웹에서 받아서 설치하고 관리해주는 프로그램.
 - **npx** : npm의 5.2.0 버전부터 새로 추가된 도구. **일회성으로** 원하는 패키지를 npm 레지스트리에 접근해서 실행시키고 설치하는 실행 도구.
    
   
 ----------------
 
 ## react 프로젝트 디렉토리 구조
 ### index.js, index.html, App.js  
   
 react에서는 직접 html을 코딩하는 것이 아닌, src폴더에서 JSX문법을 이용해서 html 뷰를 생성해내게 된다.
 그렇게 생성된 html이 id가 root인 div안에 들어가게 되는 것이다. 즉, 리액트는 동적으로 html 뷰를 생성하게 되고, index.html은 마치 껍데기와 같은 역할을 하게 되는 것이다.
 
 #### public/index.html
 ```html
...
<div id="root"></div>
...
```  

#### index.js  
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

reportWebVitals();

```  
#### App.js  
```javascript
...
class App extends Component{
  constructor(props){
    super(props);
    }
 }
 
 ...
```

---------------------  
  
 ## React 동작 원리 
 > HTML은 브라우저가 문서 객체 모델(DOM)을 구성하기 위해 따라야 하는 절차라고 말할 수 있습니다. HTML 문서를 이루는 엘리먼트는 브라우저가 HTML 문서를 읽어 들이면 DOM 엘리먼트가 되고, 이 DOM이 화면에 사용자 인터페이스를 표시합니다. 리액트는 이러한 DOM 엘리먼트를 직접 조작하지 않습니다. 대신 가상 DOM을 다루며 리액트가 가상 DOM을 생성하고 브라우저가 이를 렌더링하도록 하는 방식을 따릅니다. 이러한 가상 DOM을 리액트 엘리먼트라고 합니다. 리액트 엘리먼트는개념상 HTML 엘리먼트와 비슷하지만 실제로는 자바스크립트 객체입니다. 따라서 HTML의 DOM API를 직접 다루는 것보다 자바스크립트 객체인 리액트 엘리먼트를 직접 다루는 편이 훨씬 빠릅니다.
출처 : https://penguingoon.tistory.com/213
 
  
 -------------------  
 ## 참고자료 
 - [React에서 화면을 만드는 흐름](https://1nnovator.tistory.com/49)
 - [React에는 html이 없나요?](https://ljh86029926.gitbook.io/coding-apple-react/1/where-is-html)
 - [React의 동작원리](https://penguingoon.tistory.com/213)
