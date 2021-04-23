

### 자바스크립트 프로토타입

- 자바스크립트는 **프로토타입 기반 언어(prototype-based language)**라고 불린다.

- 자바스크립트에는 **클래스가 없다. **

  - ES6부턴 `class`문법이 추가되었다.

- **그래서 프로토타입으로 '상속'을 흉내내어  객체를 구현**한다.

  

-----------

##### 1. 프로토타입이 없다면

```javascript

//javascript에선 함수도 객체이다
function Person(){
  this.eye = 2;
  this.nose = 1;
}

var kim = new Person();
var lee = new Person();

console.log(kim.nose);
console.log(lee.nose);

kim.mouth = 1;

console.log(kim.mouth);
console.log(lee.mouth); //undefined


```

##### 2. 프로토타입 사용해보기

```javascript
function Person(){};

Person.prototype.eyes = 2;
Person.prototype.nose = 1;

var kim = new Person();
var lee = new Person();

console.log(kim.nose);
console.log(lee.nose);

```

kim, lee 객체가 eyes나 nose를 직접 가지고 있지 않기 때문에 eyes나 nose 속성을 찾을 때까지 상위 프로토타입을 검색한다.

```javascript
function Person(){};
function Student(){};

Person.prototype.eyes = 2;
Person.prototype.nose = 1;

Student.prototype = Person.prototype;

var student1 = new Student();
Student.prototype.school = '';
student1.school = 'lala high school';
console.log(student1.nose);//1
console.log(student1.school);//lala high school

var student2 = new Student();
console.log(student2.nose);
student2.school = 'java high school';
console.log(student2.school);//java high school
```

이처럼 프로토타입을 통해 **상속**을 구현할 수 있다.

![img](https://miro.medium.com/max/1778/1*PZe_YnLftVZwT1dNs1Iu0A.png)

- **Prototype Object**는 일반적인 객체와 같으며 기본 속성으로 `constructor`와 `__proto__`를 갖고 있다.





#### **프로토타입 체인(prototype chain)** 

- 프로토타입 체인이란? `__proto__`속성을 통해 상위 프로토타입과 연결되어있는 형태.

- 프로토타입 객체는 상위 프로토타입 객체로부터 메소드와 속성을 상속받을 수 있다. 

----

### 참고자료

- https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67

- https://www.nextree.co.kr/p7323/