

### mobX

- state 관리
- React에 종속되어있는 라이브러리가 아니다.

- `@observer`: 관찰하는 데이터가 변경되면 컴포넌트의 `shouldComponentUpdate()`메소드가 호출되고, `render()`메소드가 호출된다. 그러므로 `render()`메소드를 익명함수로 `render= () => {}`과 같이 호출시, 해당 클래스가 인스턴스화하기 전에 해당 메소드가 프로토타입에 존재하지 않아서 실행할 `render()`함수가 없으므로 에러가 발생한다.



----------



### 참고자료

- https://helloinyong.tistory.com/175