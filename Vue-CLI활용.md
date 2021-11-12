# 2021-11-12 Vue-CLI 활용

# 목차  
<br>

- [2021-11-12 Vue-CLI 활용](#2021-11-12-vue-cli-활용)
- [목차](#목차)
- [Vue Cli 만들어보기](#vue-cli-만들어보기)
- [Vue에서 bootstrap 사용하기](#vue에서-bootstrap-사용하기)

<br>

--- 

<br>

# Vue Cli 만들어보기

<br>

```cmd
vue create testapp(프로젝트이름)

spacebar : 선택
enter : 넘어가기

node-modules이 생기기 때문에 npm install을 하지 않아도 된다.

실행하는 명령어
npm run serve

```
  
정상적으로 작동 되었을 때
<img src='https://user-images.githubusercontent.com/44612896/141388786-208b6083-e57a-4b99-8c58-12e14739a465.png'>

<br>

✔️ history 모드  

<br>

history의 특징  
```
1) 해쉬뱅 모드와 달리 링크에 #이 붙지않는다.
2) 라우터를 사용해 컴포넌트를 이동(교체)할 때 마다 스택이 쌓인다.
    └─ 이 중 히스토리 모드의 두 번째 특징과 라우터 메소드를 사용하면 뒤로가기, 홈으로 가기 같은 기능을 구현 할 수 있다.
```

---

# Vue에서 bootstrap 사용하기

<br>

[bootstrap 공식 문서 사이트](https://bootstrap-vue.org/docs/#using-module-bundlers)  

bootstrap vue 설치하는 명령어

```cmd
# With npm
npm install vue bootstrap bootstrap-vue
```

✔️설치 확인  

package.json

<img src='https://user-images.githubusercontent.com/44612896/141389285-d4e8ad64-0513-479e-9025-b98cb2fba643.png' width="250">


<br>

✔️bootstrap vue 주입하기

```js
main.js에 주입시키기
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Import Bootstrap an BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)
```

<br>

bootstrap vue 예제

```
태그를 신기하게 <b-button>으로 사용한다.

<div>
  <b-button>Button</b-button>
  <b-button variant="danger">Button</b-button>
  <b-button variant="success">Button</b-button>
  <b-button variant="outline-primary">Button</b-button>
</div>
```

예제를 하다가 bootstrap이 적용 안 되는 상황이 발생했을때  

```
package.json 
bootstarp vue의 버전을 안정화 버전인 4.5.3으로 바꾸어 준다.
```

<img src="https://user-images.githubusercontent.com/44612896/141390308-79563d2d-4878-4c5c-8c32-ce2a35916ccb.png" width="250">

---

