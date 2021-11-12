# 2021-11-12 Vue-CLI 활용

# 목차  
<br>

- [2021-11-12 Vue-CLI 활용](#2021-11-12-vue-cli-활용)
- [목차](#목차)
- [Vue Cli 만들어보기](#vue-cli-만들어보기)
- [Vue에서 bootstrap 사용하기](#vue에서-bootstrap-사용하기)
- [localtunnel 사용하기](#localtunnel-사용하기)
- [게시판 Vue CLI로 변경하기](#게시판-vue-cli로-변경하기)

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
<br>

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

```html
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

<br>


# localtunnel 사용하기
<br>

Localtunnel 사용법  
Localtunnel 에 대한 설명은 아래 사이트에서 확인 가능합니다. 

- [Web page](https://localtunnel.github.io/www/)
- [Github page](https://github.com/localtunnel/localtunnel)


사용해야 하는 명령어는 다음과 같습니다.  

```cmd
# npm이 설치되어 있다고 가정
npm install -g localtunnel

# p : port 지정
# s : subdomain 지정. 지정 안할 경우 임의 값
lt -p 8000 -s chancethecoder

# xxx.localtunnel.me 로 접속 가능
your url is: https://chancethecoder.localtunnel.me
```

페어의 restapi 데이터에 접근하는 방법  
<br>

```cmd
lt -p 포트번호를 하면 쓸 수 있다.
단, cmd 창을 닫으면 포트가 꺼진다.
```

`cmd에서 lt -p portnumber 사용시 나오는 화면`  

<br>

<img src="https://user-images.githubusercontent.com/44612896/141392451-451db954-1fef-4575-8ac4-e82f0e3781e7.png" width="500">


[ref : 리눅스-로컬-서버-외부에서-접속하기](https://chancethecoder.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EB%A1%9C%EC%BB%AC-%EC%84%9C%EB%B2%84-%EC%99%B8%EB%B6%80%EC%97%90%EC%84%9C-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0-localtunnel)

---


# 게시판 Vue CLI로 변경하기  

원래 있던 게시판 이해하기 

`App.js`  

```
각각의 컴포넌트들을 등록해 놓았다.  
```

`ArticleRegister.js`

```
글을 등록하는 부분
```

`ArticleList.js`  

```
글 내용을 v-for문을 통해 뿌려준다.
```

`ArticleView.js`  

```
글의 세부 내용을 보여준다.
```

`AtricleModify`

```
글을 수정 하게 해준다.
```

---

Vue CLI 프로젝트 만들어서 게시판 변경하기

✅ vue 프로젝트 만들기

```cmd

만들고 싶은 폴더에서 주소 창에 cmd 치기

vue create board-vue

Manually select features 선택

Router Vuex 선택

2.x 선택

history mode yes

Eslint + prettier 선택 

package.json 선택 

마지막 설정 저장 N
```

✅ vue CLI project 실행 해보기

```cmd
npm run serve
```

성공화면  

<img src="https://user-images.githubusercontent.com/44612896/141397240-5b86fa65-aae9-4c62-a84c-65c6a59237a8.png" width="300">

<br>

✅ axios 설치하기

```js
npm install axios

확인은 package.json에서 한다.
  "dependencies": {
    "axios": "^0.24.0",
    "core-js": "^3.6.5",
    "vue": "^2.6.11",
    "vue-router": "^3.2.0",
    "vuex": "^3.4.0"
  },
```

✅ vue CLI에서 가장 먼저 접근 하는 곳

```
main.js // 건드릴 부분이 없다.
```

✅ vue store/index.js

```js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export default new Vuex.Store({
  state: {}, //데이터 공간
  //메서드 공간의 역할이 조금씩 다르다.
  mutations: {}, //메서드 공간
  actions: {}, //메서드 공간
  modules: {}, //메서드 공간
});

```

<br>

✅ 실제 화면에 보이는 공간
```
App.vue // 실제 화면에 처음 보이는 공간
```

✅ assets

```
사진이나 여러 잡다한것을 담을 수 있다.
logo.png를 가지고 오자
```

✅ App.vue

```
nav부분에 게시판 header 부분을 자지고 오자

style 부분에 main.css 부분을 가지고 오자

src = "@/assets/logo.png" 써주자

router-link :to 를 이요해서 컴포넌트를 연결하자.


```

✅ router/index.js

```
route를 등록해주자

import, path, name, component를 설정하자. (불등하자 불러오고 등록하자)
```

✅ Login.vue

```
login.vue 만들기

```

✅ Board.vue

```
Board.vue 만들기

<router-view></router-view> 만들기 
<router-view></router-view>가 생기면 children이 생기는 것을 동시에 생각해줘야 한다.
```

✅ BoardList.vue

```
component에 board를 만들어서 게시판에 관련된 vue 파일들을 넣어줌

router/index.js BoardList를 import 시켜준다.

import한 것을 주입 해준다 . board children으로 주입 시켜준다.

부모 컴포넌트에  /board가 들어오면 바로 list를 보여줄 있게 redirect를 건다.
redirect: { name: "BoardList" }, // redirect할 때도 객체 쓰는것을 권장하자!


ArticleList.js에 있는 부분을 복사해서 가져오고

import axios from 'axios';를 import 한다. (npm install axios / package.json 확인!)

```

✅ BoardWriter.vue

```js
boardWriter 만들자 

ArticleRegister.js에 있는 파일을 가져오자

methods: {
    movePage() {
      this.$router.push({ name: "BoardWrite" }); // name으로 이동하게 권장 !!
    },
  },


```


✅ MainContent.vue 

- 권장사항: 이름을 합성문자로 만들어라 

```js
data를 받는 방법

  props: {
    msg: String,
  },
  
  로 받을 이름과 타입을 선언해 준다.
```

✅ http-common.js

```js
axios를 효율적으로 쓰기 위해서 만들어 주자

\import axios from "axios";

export default axios.create({
    //기본 주소 설정하는 것
  baseURL: "http://localhost:9999/vue",
});

moveList() {
      this.$router.push({ name: "BoardList" }); // 수정 name으로 옮길 수 있도록 하기 권장
    },

```


✅ BoardListRow.vue

  - list를 보여주는 component

```js
보드 리스트에서 불러다가 써야한다.

props롤 데이터를 부모에서 받아온다.
  props: {
    article: Object,
  },

```

✅ BoardView

```js

axios -> http 로 변경

ArticleView.js 가져온다.

<router-link :to="{ name: 'modify' }" class="btn">수정</router-link> 로 수정

router -> router 할때 값을 그래도 유지고 넘겨준다 !

querys -> params 로 변경해 주낟.

```

✅ BoardModify

```js

ArticleModify.js를 가져온다.

axios -> http 로 수정

this.$router.push({ name: "BoardList" });  이름으로 이동하도록 변경

querys 로 되어있는 것을 params로 변경 /api/board/${this.$route.params.no}

```

✅ BoardDelete

```js
ArticleDelete.js 가져온다

import http from "@/util/http-common.js"; import

http.delete(`/api/board/${this.$route.params.no}`) querys => params 변경

this.$router.push({ name: "BoardList" }); name으로 변경 

```

