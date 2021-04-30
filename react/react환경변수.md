

### react 환경변수

`create react app`(CRA) 로 생성된 앱에서 전역설정과 같은 환경변수를 사용하기 위해 env파일을 활용할 수 있다.

앱의 버전정보, api주소, 타이틀 등 모든 정보를 jsx, html 파일에서 전역변수처럼 사용할 수 있다.

API 통신시에 개발서버와 운영서버의 url이 다를 때 유용하게 사용할 수 있다.

![image-20210430141116092](C:\Users\nextree\AppData\Roaming\Typora\typora-user-images\image-20210430141116092.png)

- **`.env.development` or `.env.production`  파일 생성** 
  - 변수설정시 반드시 앞에 `REACT_APP_`을 붙여야 한다.
  - `npm start` : `.env.development` 사용.
  - `npm run build` : `.env.production` 사용.

```
REACT_APP_API_URL=http://127.0.0.1:8080
```

- **환경변수 사용시**

```typescript
clubApiUrl = `${process.env.REACT_APP_API_URL}/club`;
```



-------

### 참고자료

- https://velog.io/@devyang97/React-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-productiondevelopment
- https://m.blog.naver.com/legend25/222033372402