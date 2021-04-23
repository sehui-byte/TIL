이번에 프로젝트에서 타임리프(Thymeleaf)라는 것을 사용하게 되어서 이에 대해 간단히만 정리해보려고 한다.

타임리프는 jstl하고 비슷한 방식으로 사용한다.  `jstl`처럼`prefix`를 달아서 사용한다. 

타임리프에 대해 찾아보니 `jsp`와 비교한 글들이 많았다. 그래서 이 점도 한번 짚어보고 가려고 한다.  

-----------------



### thymeleaf vs jsp



#### jsp

`jsp`는 MVC모델에서 View를 구성할 때 사용된다. **`html`코드 안에 `java`코드를 넣어서 사용하는 것으로, `<% %>`안에 자바 코드를 넣어서 동적으로 페이지를 구성할 수 있게 한다.** 

그런데 이런식으로 html 안에 java코드를 넣어서 쓸 때 html 코드 중간 중간 `<% %>`로 자바 코드가 들어가니까 코드 가독성이 떨어지게 된다. 이 점 때문에 `jstl`를 사용하게 되었다.  

​	- **`jstl`이란 jsp 개발을 단순화하기 위한 태그 라이브러리**이다. `<c:if>`와 같이 사용하여 뷰를 구성할 때 편리하게 사용할 수 있었다.

그리고 `jsp`는 그 자체로 실행될 수 없기 때문에 결국`servlet(.java)`으로 변환되어 컨테이너에 적재된다. 



#### thymeleaf

**thymeleaf는 서버사이드 자바 템플릿 엔진의 한 종류**이다. 

jsp와 다르게 servlet코드로 변환되지 않아 WAS를 켜서 확인하지 않고, html 파일 그 자체로 열어서 화면을 확인을 할 수 있다. (그러나 별로 유용하진 않은듯)

	- **서버사이드 템플릿엔진** : 서버에서 가져온 데이터를 미리 정의된 템플릿에 넣어 html을 그린 뒤, 클라이언트에게 전달해준다. 
	- html 코드에서 고정적으로 사용되는 부분은 템플릿으로 만들어두고, 동적으로 생성되는 부분만 템플릿에 소스코드를 끼워넣는 방식으로 동작.



```html
<table id ="companyList" border="1">
	<thead>
		<tr>
			<th>회사명</th>
			<th>사업자등록번호</th>
			<th>주소</th>
		</tr>
	</thead>
	<tbody>
		<tr th:each="company : ${companyList}">
			<td><a th:text =${company.name} th:href="@{/company/} + ${company.name}"></a></td>
			<td th:text =${company.registerNumber}></td>
			<td th:text =${company.address}></td>
		</tr>
	</tbody>
</table>
```



아래와 같이 `layout`과 `fragment`를 사용하여 html 화면을 구성할 수 있다.

```html
<th:block layout:fragment="content">
    <div th:if="${company.layoutType eq 'table'}">
      <th:block th:replace ="fragments/employeeList :: fragment-content"></th:block>
    </div>
    
    <div th:if="${company.layoutType eq 'list'}">
      <th:block th:replace ="fragments/employeeList2 :: fragment-content"></th:block>
    </div>
  </th:block>
```

```html
<div th:fragment="fragment-content">
	<h3 th:text="${company.name} + ' 의 정보'"></h3>
	<ul>
		<li th:text=${company.name}></li>
		<li th:text=${company.registerNumber}></li>
		<li th:text=${company.address}></li>
	</ul>

	<h3 th:text="${company.name} + ' 의 직원 리스트'"></h3>
	<ul th:each="employee : ${company.getEmployees()}">
		<li th:text=${employee.name}></li>
		<li th:text=${employee.number}></li>
		<li th:text=${employee.phoneNumber}></li>
	</ul>
</div>
```



`th:block`에서 `th:replace`를 사용할 수 있다.



----



### 참고자료

- [thymeleaf vs jsp](https://offbyone.tistory.com/410)

- https://velog.io/@dsunni/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9B%B9-MVC-Thymeleaf

- [thymeleaf 인라인 표현식](https://noritersand.github.io/java/java-%ED%83%80%EC%9E%84%EB%A6%AC%ED%94%84-thymeleaf-%EA%B8%B0%EB%B3%B8/#heading-%EC%9D%B8%EB%9D%BC%EC%9D%B8-%ED%91%9C%ED%98%84%EC%8B%9D--)

