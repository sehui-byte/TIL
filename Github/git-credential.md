git을 쓰다보니 pull/push 실행 시에 계속해서 계정과 패스워드를 물어보는 경우가 발생하여 이 부분에 대해서 찾아보게 되었다.   

먼저 계속해서 다시 입력해야 하는 것을 방지하기 위해 아래와 같이 credential 정보 저장을 할 수 있다.

```
git config credential.helper store
```

#### 그렇다면 이 credential이란 뭘까?  
```
git config --global credential.helper <옵션>
```
Http프로토콜을 사용하여 리모트 저장소에 접근하는 경우 매번 사용자 이름과 암호를 입력해야 한다. git은 매번 인증정보(credential)를 입력하는 경우 인증정보를 저장해두고 자도응로 입력해주는 시스템을 제공한다고 한다.
- 옵션을 설정하지 않을 경우 어떤 암호도 저장하지 않는다. 인증이 필요한 경우 매번 인증정보(사용자 이름과 암호)를 입력해야 한다.
- `cache`모드로 설정하면 일정시간동안 메모리에 사용자 이름과 암호와 같은 인증정보를 저장하여 기억한다. disk에 저장하지는 않으며 메모리에서 15분까지만 유지한다.
- `store`모드로 설정하면 인증정보를 disk에 텍스트 파일로 저장하여 계속 유지한다. 리모트의 인증정보를 변경하지 않는 한 인증정보를 다시 입력하지 않아도 접근할 수 있다고 한다. 다만 **주의할 점은 인증정보가 사용자 홈 디렉토리 아래에 있는 일반텍스트 파일로 저장된다는 점**이다. 
    - 파일을 찾아서 열어보니 정말 일반 텍스트파일로 저장이 되어있어서 주의해야될 것 같다.
    ![image](/uploads/5951e26d410f70a1fcc06cf30a60f292/image.png)


----------
### 참고자료
- https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Credential-%EC%A0%80%EC%9E%A5%EC%86%8C

- https://www.hahwul.com/2018/08/22/git-credential-helper/ 
- https://readpost.co/post/git-push%EC%8B%9C-%EB%A7%A4%EB%B2%88-github-%EC%9D%B8%EC%A6%9D%EC%A0%95%EB%B3%B4-%EB%AC%BB%EC%A7%80-%EC%95%8A%EA%B8%B0-%EC%84%A4%EC%A0%95--mU
