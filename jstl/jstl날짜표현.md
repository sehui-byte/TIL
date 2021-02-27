
fmt태그를 추가한다.
```
<%@ taglib prefix="fmt" uri="http://java.sun.com/jstl/fmt" %>
```

문자열을 Date 타입으로 변환한뒤,
```
<fmt:parseDate value="${alarmList.insertdate}" var="insertdate" pattern="yyyy-MM-dd"/>			
```
바꿀 패턴을 표현한다.

```
<fmt:formatDate value="${insertdate}" var="insertdate2" type="DATE" pattern="yyyy-MM-dd"/>
<c:out value="${insertdate2}" />
```
결과는 2020-02-28 과 같이 나온다.

---------

#### 참고자료
- https://jang2r.tistory.com/27
