### 2021-01-28  

vue.js 공부 시작.

---

# Vue.js란? & 특징

- 웹프론트엔드 프레임워크
- **컴포넌트(Componet)**
    - 웹을 구성하는 웹페이지 내의 다양한 UI요소를 의미한다. 이러한 요소들을 재사용 가능하도록 구조화하였다.
- **SPA(Single Page Application)**
    - 전체 영역을 미리 로딩해둔 후에 페이지 전환시마다 페이지에서 필요한 부분만 로딩하여 빠른 페이지 변환이 가능하고, 적은 트래픽 양을 가진다.  다만 초기에 모든 것을 미리 로딩해두기 때문에 초기 로딩속도가 느릴 수 있다는 단점이 있다.
- **Vue Router**
    - 라우팅이란? **웹페이지간의 이동방법**을 의미.
    - 페이지를 이동할 때 서버에 요청하여 새로 갱신하는 것이 아니라 **미리 해당 페이지를 받아놓고 페이지 이동시 클라이언트의 라우팅을 이용하여 화면을 갱신**한다. → 이러한 방식을 `SPA`라고 함.
    - `vue`, `react`, `angular` ~~~~모두 라우팅을 이용하여 화면을 전환한다.

---

# 세팅 작업

## node.js 설치

- **node.js 설치 → 14.15.4 버전 다운**
    - 자바스크립트는 보통 인터넷 브라우저에 내장되어있는 자바스크립트 엔진에 의해 돌아간다. 가장 중적인 엔진은 크롬으 V8엔진이 있다. 이러한 V8엔진을 인터넷 브라우저 없이 윈도우, 맥, 리눅스 등의 다양한 플랫폼에서 실행할 수 있도록 만들어준 것이 바로 node.js이다. 즉 **인터넷 브라우저 없이 자바스크립트를 사용할 수 있게 해주는 것**이다.

        ![image](https://user-images.githubusercontent.com/64109506/106159381-1181ba00-61c8-11eb-9ea7-a28e2b3e1ab9.png)

        - `node -v` 설치 확인

     
     
 ------------------------------
  
  ## VSCode설치
![image](https://user-images.githubusercontent.com/64109506/106159393-16466e00-61c8-11eb-8a76-73dfac409c55.png)

 최소 약 245MB정도의 디스크 공간이 필요하다고 합니다.
  
    
------------------------
    
## **Vue CLI** 설치

### Vue CLI란?
- 기본 Vue 개발환경을 설정해주는 도구. vu
- vue.js 프로젝트 생성을 돕는 vue공식 `CLI`이다. Vue CLI를 통해서 **`vue`명령어를 사용**할 수 있게 되고, 빠른 프로젝트 생성 및 관리를 할 수 있다.
- vue-cli가 **기본적인 프로젝트 세팅**을 해주기 때문에 폴더구조에 대한 고민, lint, build,어떤 라이브러리로 구성을 해야하는지, webpack설정은 어떻게 해야하는지 등에 대한 고민을
덜을 수 있다.
- `cli`란?
  - `명령 줄 인터페이스(CLI, Command Line Interface) 또는 명령어 인터페이스`는 텍스트 터미널을 통해 사용자와 컴퓨터가 상호작용하는 방식을 뜻한다.
    즉, 작업명령은 사용자가 컴퓨터 키보드 등을 통해 문자열의 형태로 입력하며, 컴퓨터로부터 출력 역시 문자열의 형태로 주어진다. (위키백과)
  
```bash
npm install -g @Vue/cli
```
![image](https://user-images.githubusercontent.com/64109506/106159404-18103180-61c8-11eb-8695-e830a419819b.png)
좀 시간이 걸린다.
설치 중...


![image](https://user-images.githubusercontent.com/64109506/106159411-1a728b80-61c8-11eb-8047-b828ace78b01.png)

`preset`을 `babel`로 할지, `eslint`로 할건지 선택한다.

- 일단 default - `babel`로 설치한다. → 그냥 엔터 누른다.

역시나 시간이 좀 걸린다.

- `vue cli`설치 후 프로젝트 폴더 생성

```bash
vue create test 
```

refresh해서 보면 vue로 프로젝트를 할 때 필요한 모듈들 등을 `vue cli`가 알아서 구성해준 것을 확인할 수 있다.
![image](https://user-images.githubusercontent.com/64109506/106159421-1c3c4f00-61c8-11eb-9294-4a865e6e495a.png)
![image](https://user-images.githubusercontent.com/64109506/106159426-1f373f80-61c8-11eb-90ca-ff3dfb2cb2ad.png)
```bash
npm run serve
```


아래 나온 [localhost](http://localhost):8080 을 ctrl키를 누른채로 눌러서 클릭해보면 아래와 같은 화면이 뜬다. 
아래 화면이 나온다면 모든 설치가 정상적으로 된 것이다.

![image](https://user-images.githubusercontent.com/64109506/106159438-21999980-61c8-11eb-9905-be567505abf4.png)
---

## vue router설치

```bash
npm install vue-router --save
```

---

# vue파일 생성

1. **src/component에 layout폴더 생성.**
2. **Header.vue파일 생성.**

### bootstrap vue

- boostrapvue : [https://bootstrap-vue.org/](https://bootstrap-vue.org/)


```bash
npm install vue bootstrap bootstrap-vue
```

**main.js에 아래 부분 추가**

```jsx
// Import Bootstrap an BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)
```

**아까 생성한 Header.vue 파일에 boostrap 에서 navbar 부분을 복사해와서 붙여넣는다.** 이때 `<template>`태그 안에 붙여넣는다.

vue에서 보여지는 부분은 `<template>`태그 안에 넣고,

동작하는 부분은 `<script>`내에 넣는다.

```jsx
<template>
<div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">NavBar</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#">Link</b-nav-item>
        <b-nav-item href="#" disabled>Disabled</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
        </b-nav-form>

        <b-nav-item-dropdown text="Lang" right>
          <b-dropdown-item href="#">EN</b-dropdown-item>
          <b-dropdown-item href="#">ES</b-dropdown-item>
          <b-dropdown-item href="#">RU</b-dropdown-item>
          <b-dropdown-item href="#">FA</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template #button-content>
            <em>User</em>
          </template>
          <b-dropdown-item href="#">Profile</b-dropdown-item>
          <b-dropdown-item href="#">Sign Out</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>

<script>
export default {
    name : "header",
}
</script>
```

---

# 참고자료

- 유튜브 : 한시간만에 끝나는 vue.js 입문 - 개발자의 품격
- VSCode & node.js 설치 : [https://doncolmi.github.io/Vue-1/](https://doncolmi.github.io/Vue-1/)
- vue router : [https://cchoimin.tistory.com/entry/Vuejs-Vue-라우터란](https://cchoimin.tistory.com/entry/Vuejs-Vue-%EB%9D%BC%EC%9A%B0%ED%84%B0%EB%9E%80)
- (vue-cli알아보기)[https://simplevue.gitbook.io/intro/01.-vue-cli]
