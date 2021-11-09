# 2021-11-09 axios 라우트 템플릿

# 목표
axios 라우트 템플릿에 대해 설명할 수 있다.


# 목차
- [2021-11-09 axios 라우트 템플릿](#2021-11-09-axios-라우트-템플릿)
- [목표](#목표)
- [목차](#목차)
  - [axios](#axios)
  - [vue-router](#vue-router)
  - [교수님이 집어 주신 것](#교수님이-집어-주신-것)

<br>

---

<br>

## axios

<br>

> Vue에서 권고하는 HTTP 통신 라이브러리이다.  
> Promise 기반의 HTTP 통신 라이브러리이며 상대적으로 HTTP 통신 라이브러리들에 비해 문서화가 잘 되어 있고 API가 다양하다.

<br>

<details>
<summary> promise 예제 코드 </summary>
<div markdown = "1">

<br>

```js
// 객체 생성하기
const promise = new Promise((resolve, reject) => {
console.log("Promise");
let f = true;
if (f) resolve("resolve");
// >> then 부분 실행
else reject("reject"); // >> catch 부분 실행
});

promise
.then((data) => { //성공했을때는 then으로 간다.
    console.log("then : " + data);
})
.catch((data) => { // 실패 했을 때는 catch로 간다.
    console.log("catch : " + data);
});
```
</div>
</details>

<br>

<details>
<summary>axios 예제 코드</summary>
<div markdown="1">

<br>

```js
// 객체 생성하기
function axios() {
return new Promise((resolve, reject) => {
    console.log('Promise');
    resolve('success');
    //reject('reject');
});
}
axios()
.then((data) => { //성공시 실행 되는 코드
    console.log('then : ' + data);
})
.catch((data) => { // 실패시 실행 되는 코드
    console.log('catch : ' + data);
})
.finally(() => { //무조건 실행 되는 코드
    console.log('finally');
});
```

<div>
</details>


<br>

<details>
<summary> axios를 배우기 전에 데이터를 받아오는 방법
</summary>
<div markdown = "1">

<br>

```js
const todosURL = "https://jsonplaceholder.typicode.com/todos/1";

const xhr = new XMLHttpRequest();
xhr.open("GET", todosURL); // 주소로 겟 방식으로 간다.
xhr.send();

//   const response = xhr.response; // 데이터를 받아와라 <- 데이터를 받아오기전에 값을 넣기 때문에 response는 값이 존재 하지 않는다
//   console.log(response);
xhr.onload = () => {
// 200이라면 뜻은 정상적으로 데이터가 넘어 왔다면
    if (xhr.status === 200) {
        const response = xhr.response;
        console.log(response);
    }
};
```
</div>
</details>

<br>

<details>
<summary> axios를 배운뒤 데이터를 받아오는 방법
</summary>
<div markdown = "1">

<br>

```js
const todosURL = "https://jsonplaceholder.typicode.com/todos";
const promise = axios(todosURL);
console.log(promise);

promise
// promise에서 받아온 데이터 : response
.then((response) => {
    console.log(response);
    return response.data[0].id;
})
//promise chaining
//id는 위에 then이 retrun 한 값을 받게 된다
//즉, id = response.data[0].id 값을 가지게 된다.
.then((id) => {
    console.log(id);
    return axios.get(`${todosURL}/${id}`);
})
//todo = todolist id가 1인 값을 받아 올 수 있다.
.then((todo) => {
    console.log(todo);
});
```

<br>

</div>
</details>
<br>




---

## vue-router

<br>

라우팅이란?
>웹 페이지 간의 이동 방법

Vue-router 역할
> 라우터는 컴포넌트와 매핑한다.

CDN 방식으로 연결한다.

```js
<script src="/path/to/vue.js"></script>
<script src="/path/to/vue-router.js"></script>
```

vue-router 사용방법

1. router-link to라는 속성을 가지고 router 링크를 걸어준다.
```<router-link to="/board/30">30번 게시글</router-link>```
2. 라우터 객체를 생성해야 한다.
```const router = new VueRouter({}) ```
3. 반드시 Vue 인스턴스를 만들때 내가 사용할 router를 주입시켜 줘야 한다.
```const router = new VueRouter({ router }) ```
4. 보여라 부분 : `<router-view>` 영역을 잡아줘야 한다.

<br>

<details>
<summary> vue-router 예제 </summary>
<div markdown="1">

```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vue.js</title>
    <style>
      .router-link-exact-active {
        color: red;
      }
    </style>
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
  </head>

  <body>
    <div id="app">
      <h1>SSAFY - Router</h1>
      <p>
        <router-link to="/">HOME</router-link>
        <router-link to="/board">게시판</router-link>
        <router-link to="/qna">QnA</router-link>
        <router-link to="/gallery">갤러리</router-link>
      </p>

      <!-- 현재 라우트에 맞는 컴포넌트가 렌더링 -->
      <router-view></router-view>
    </div>
    <script>
      // 라우트 컴포넌트
      const Main = {
        template: "<div>메인 페이지</div>",
      };
      const Board = {
        template: "<div>자유 게시판</div>",
      };
      const QnA = {
        template: "<div>질문 게시판</div>",
      };
      const Gallery = {
        template: "<div>갤러리 게시판</div>",
      };

      // 라우터 객체 생성
      const router = new VueRouter({
        routes: [
          {
            path: "/",
            component: Main,
          },
          {
            path: "/board",
            component: Board,
          },
          {
            path: "/qna",
            component: QnA,
          },
          {
            path: "/gallery",
            component: Gallery,
          },
        ],
      });

      // Vue 인스턴트 라우터 주입
      const app = new Vue({
        el: "#app",
        router,
      });
    </script>
  </body>
</html>

```
</div>
</details>

<br>

라우터를 3가지를 기억하라 `불등보`
1. 불러오기
2. 등록하기
3. 보여주기

✔️ Vue debuggin Tip    

components -> Vue 인스턴스의 값들을 쉽게 볼 수 있다.

Routing -> 어떤 값을 가지고 route 하는지 쉽게 볼 수 있다.


$router, $route

전체 라우터 정보

```this.$router```

현재 호출된 해당 라우터 정보

```this.$router   this.$route.params.no   this.$route.path```

---

이름을 가지는 라우트 
> 라우트는 연결하거나 탐색을 수행할 때 이름이 있는 라우트를 사용한다.  
> Router Instance를 생성하는 도안  routes 옵션에 지정

```js
{
  path: '/board/:no',
  name: 'boardview',
  component: CoardView,
}
```
<br>

프로그래밍 방식 라우터  
> <router-link>를 사용하여 선언적 네비게이션용 anchor 태그를 만드는 것 외에도 라우터의 instance method를 사용하여 프로그래밍으로 수행

사용방법
```js
$router.push('home')
```


중첩된 라우트  
>URL의 세그먼트가 중첩 된 컴포넌트의 특정 구조와 일치하는 것을 활용한다.





## 교수님이 집어 주신 것

`axios`

>우리는 CDN 방법을 사용하고 있다.


`promise`  

> axios 함수는 promise 객체를 발생 시킨다.

<details>
<summary>axios 예제 코드</summary>
<div markdown="1">

```js
function axios(url) {
    return new Promise((resolve, reject) => {
        console.log(url + ' 호출함');
        setTimeout(() => {
        resolve('처리결과 성공');
        // reject('처리결과 에러');
        }, 3000);
    });
    }

    axios('http://localhost:8000/board')
    .then((data) => { //성공 했을 때
        console.log(data);
    })
    .catch((data) => { //실패 했을 때 
        console.log(data);
    })
    .finally(() => { // 무조건 해야 하는 것
        // 최종 실행할 내용이 있다면 사용한다.
        console.log('마지막 항상 실행');
    });
```
</div>
</details>

<br>


then 메소드로 메소드 체이닝을 할 수 있다.  

axios의 안에 함수(function)에서 this를 쓰면 Vue를 벗어난 변수를 가르치게 된다.

function을 arrow function으로 바꾸면 this를 가르키면 Vue를 가리키게 된다.

`router`  

라우터
> 클라이언트에서 자기에서 왔다갔다 하는 것이다.  
> URL 주소에는 바뀌는 모양이 보인다. 이게 서버로 가는 것이 아니라 URL 표시만 바뀌는 것이다.  

? 뒤에 쓰는 것은 queryString 이다  

객체가 넘어오는건 분해해서 받을 수 있다. : destructing을 사용함.
예시
```js
let {id, name} = member;
```

시험 문제  
`<router-view>` 와 `<router-link>`는 짝꿍이다

router 연결할때 권장은 name을 이용하는 것이다.

중첩 라우팅은 나중에 봐도 된다.  
앞에서 배운거는 무조건 알았으면 한다.  
