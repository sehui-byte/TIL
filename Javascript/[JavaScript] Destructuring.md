## [JavaScript] Destructuring



- **destructuring** : 배열이나 객체의 속성을 해체하여 그 값을 개별변수에 담을 수 있게 하는 javascript 표현식.

```javascript
var a  = { first : "1", second : "2"};

//destructuring
var {first, second} = a;

document.getElementById('a').innerHTML = a.first;
document.getElementById('b').innerHTML = second;
```



