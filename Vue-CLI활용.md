# 2021-11-12 Vue-CLI 활용

# 목차  
<br>

- [2021-11-12 Vue-CLI 활용](#2021-11-12-vue-cli-활용)
- [목차](#목차)
- [Vue Cli 만들어보기](#vue-cli-만들어보기)
- [Vue에서 bootstrap 사용하기](#vue에서-bootstrap-사용하기)
- [localtunnel 사용하기](#localtunnel-사용하기)

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
