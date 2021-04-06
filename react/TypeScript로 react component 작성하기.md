
## 프로젝트 생성  
뒤에 `--typescript`가 있으면 타입스크립트 설정이 적용된 프로젝트가 생성된다.
```
npm create-react-app [project name] --typescript
```
  
그렇다면 이미 만든 프로젝트에 typescript를 적용하려면?  
```
npm install --save typescript @types/node @types/react @types/react-dom @types/jest

# or

yarn add typescript @types/node @types/react @types/react-dom @types/jest
```
그 다음에 `src/index.js`를 `src/index.tsx`로 바꾸고 서버를 restart한다.  

----------  
타입스크립트를 사용하는 리액트 컴포넌트의 경우 `*.tsx`확장자를 사용한다.
  
--------------------   
## 참고자료
- https://create-react-app.dev/docs/adding-typescript/
- https://react.vlpt.us/using-typescript/02-ts-react-basic.html
