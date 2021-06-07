
## 비동기처리  
- Promise
- Ajax
- callback function
- await

--------------------------------------------

## Promise  

>주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다고 한다.    
일반적으로 웹어플리케이션을 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 API를 사용하는데, 
API가 실행되면 서버에 데이터를 보내달라는 요청을 하는데, 여기서 데이터를 받아오기도 전에
마치 데이터를 다 받아온 것처럼 여기고 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜬다.
이런 문제를 해결하기 위한 방법 중 하나가 `promise`이다.  
>출처 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/  
  
```javascript
$.get('url 주소/products/1', function(response) {
  // ...
});
```  

  
  
----------------

## 참고자료 
- https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
- [MobX의 상태변화, Action을 알아보자](https://hoontae24.github.io/posts/8)
