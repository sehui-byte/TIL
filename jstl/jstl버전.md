#### 2021-03-03 수요일

jstl에서 value does not support runtime expression과 같은 경고문이 떴다.  
또한 uri를 바꾸면서 작동이 안되는 부분도 있어서 jstl 버전에 대해 알아보게 되었다.

--------------------
**jstl 태그 라이브러리 설정 코드**
```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
```

jstl 사용시에 taglib uri에 아래와 같이 2가지 경우로 uri를 쓴다.
- `uri="http://java.sun.com/jsp/jstl/core"` 
- `uri="http://java.sun.com/jstl/core"` 

 
   
  jstl 1.0 버전과 그 이후의 버전은 uri가 위와 같이 다르다.
  1.0버전은 uri에 `/jsp/`부분이 빠진다.  

서블릿 버전에 맞춰서 jstl을 사용해야 하는데 
  - servlet 2.3 / jstl 1.0
  - servlet 2.4 / jstl 1.1
  - servlet 2.5 / jstl 1.2
  위와 같이 사용한다.
    
  서블릿 버전의 경우 web.xml에서 확인할 수 있다.
  ```xml
<web-app id="servlet-2_4" 
		version="2.4" 
		xmlns="http://java.sun.com/xml/ns/j2ee" 
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee 
		http://java.sun.com/xml/ns/j2ee/web-app_2_4>
```

pom.xml에jstl버전도 서블릿 버전에 맞춰서 적어주었다.
```xml
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>jstl</artifactId>
  <version>1.1.2</version>
</dependency>
<dependency>
  <groupId>taglibs</groupId>
  <artifactId>standard</artifactId>
  <version>1.1.2</version>
</dependency>
```
이렇게 바꾸고나서 maven update를 하였으나 에러가 발생하였다.
이럴 경우 project의 properties에서 버전에 맞춰 설정을 바꿔주거나 
![image](https://user-images.githubusercontent.com/64109506/109814558-fe07ba00-7c71-11eb-9fd0-f6e17eeeb694.png)
이게 먹히지 않으면 `.settings`에서 `org.eclipse.wst.common.project.facet.core.xml`에서 직접 수정해주면 정상적으로 작동하게 된다.


-----------------------

- [서블릿 버전별 dtd](https://baejangho.com/entry/webxml-%EC%84%9C%EB%B8%94%EB%A6%BFservlet-%EB%B2%84%EC%A0%84%EB%B3%84-DTD)
