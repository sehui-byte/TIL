  
이벤트 이름은 카멜 표기법을 사용한다.  
ex) onclick(X), onClick(O)
  
  
## event 종류  
- mounting event : React엘리먼트(컴포넌트 클래스의 인스턴스)를 DOM에 추가할 때 발생. React가 이벤트를 한번만 실행한다.
- updating event : 속성이나 상태가 변경되어 React element를 갱신할 때 발생. React가 이벤트를 여러번 실행한다.
- unmounting event : React가 element를 DOM에서 제거할 때 발생. React가 이벤트를 한번만 실행한다.   


  ![image](https://user-images.githubusercontent.com/64109506/113665096-d6c86080-96e7-11eb-99ed-a181820ac11e.png)

    
    
   
     
     
   mounting event 중 하나인 `constructor()`
   ```javascript
   class App extends Component{
  constructor(props){
    super(props);
    }
   }
   ```
   updating event 중 하나인 `shouldComponentUpdate()`.
  ```javascript
  //변화가 있을 때만 렌더링하도록
  shouldComponentUpdate(newProps, newState){
    if(this.props.data === newProps.data){
      return false;
    }
    return true;
  }
  ```
 ----------------  
   
 ## 참고자료  
 - 리액트 교과서
 - 생활코딩
