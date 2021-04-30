

csrf token에 대해 들어본 적은 있으나 무엇인지 잘 몰라서 이에 대해 간단히 정리해보겠다.



- CSRF : **C**ross-**S**ite **R**equest **F**orgery (사이트 간 요청 위조)

[나무위키](https://namu.wiki/w/CSRF) 글에 이해하기 쉽게 정리되어있는데 `<img src="https://namu.wiki/member/logout">` 이런식으로 상대가 이미지를 클릭하면 로그아웃되게 한다거나 글을 올린다거나 하는 등의 공격을 할 수 있다. 

이러한 공격에 대해 방어하기 위해 `csrf token`을 사용할 수 있다.



----------------------



사용자의 세션에 임의의 난수 값을 저장하고, 이후 백엔드에서 요청을 받을 때 세션에 저장된 토큰 값과 요청 파라미터에 전달되는 토큰 값이 일치하는지 확인을 하여 검증하는 방법이다.



```
session.setAttribute("CSRF_TOKEN", UUID.randomUUID().toString());

<input type="hidden" name="_csrf" value="${CSRF_TOKEN}"/>
```





----

### 참고자료

- https://namu.wiki/w/CSRF

- https://m.blog.naver.com/lstarrlodyl/221943397270