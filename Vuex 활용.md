# 2021-11-15 Vuex 활용

# 목차
- [2021-11-15 Vuex 활용](#2021-11-15-vuex-활용)
- [목차](#목차)
- [bootstrap vue 리뷰](#bootstrap-vue-리뷰)
- [vuex](#vuex)
  - [state 사용 예제](#state-사용-예제)
  - [Mutations을 사용 예제](#mutations을-사용-예제)
  - [Action 사용 예제](#action-사용-예제)
- [교수님 설명](#교수님-설명)


# bootstrap vue 리뷰

✅ 부트스트랩 쓰면서 제대로 적용이 안되는 문제가 발생   

해결방법  

```js
보통 문제는 부트스트랩의 버전 문제일 것이다.
Bootstrap-vue는 버전 4.5.3을 권장한다. 
package.json에서  
bootstarp vue의 버전을 안정화 버전인 4.5.3으로 바꾸고,
 npm install을 해서 업데이트를 해준다.
```

<img src="https://user-images.githubusercontent.com/44612896/141390308-79563d2d-4878-4c5c-8c32-ce2a35916ccb.png" width="250">


✅ 하위 컴포넌트로 리스트를 사용할 때

```
복잡하게 만들어야 하는 것들
예를 들어 쇼핑몰 같은것들을 만들 때 사용하는 것이 좋다.
보통 테이블을 만들 때는 하위 컴포넌트를 사용하지 않아도 된다.
테이블은 테이블이 제공하는 API를 사용하는 것이 좋다.
bootstrap-vue에서 테이블을 만들때 하위 컴포넌트를 쓰지 않는 것이 권장 사항이다.
```

✅ 특정 폴더에 이미지를 저장하고 나타낼 떄

```js
<b-img :src=required('@/assets/apt.png')> </b-img>
```

✅ [Vuetify](https://vuetifyjs.com/en/components/alerts/#usage)  



```
bootstrap과 같이 쓸 수 없다.
Vuetify를 사용하면 디자인하는데 도움을 받을 수 있다.
UI Components에 들어가서 oprions을 바꾸면 바로 바로 가져와서 원하는 것으로 꾸밀 수 있다.
```


<br>

---

<br>


# vuex

✅ vuex란?

> Vuex는 Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리 입니다.   
> 애플리케이션의 모든 컴포넌트에 대한 `중앙 집중식 저장소` 역할을 하며 예측 가능한 방식으로 상태를 변경할 수 있습니다


✅ 상태 관리 패턴이란 무엇인가?

>상태 관리는 여러 컴포넌트 간의 데이터 전달과 이벤트 통신을 한 곳에서 관리하는 패턴을 의미한다.  


✅ store의 기능

```
Vue 개발에서 상태를 관리해 주는 기능을 제공해 주는 것이 Vuex이고,  
어플리케이션의 모든 컴포넌트들에 대한 중앙 집중식 저장소의 역할 및 관리 를 담당한다.
```


✅ 언제 사용해야 하나요?
> Vuex는 공유된 상태 관리를 처리하는데 유용하다.  
> 하지만, 개념에 대한 이해와 시작하는 비용도 함께 든다.

✅ 상태관리 패턴

단 방향 데이터 흐름  

view => actions => state => view => ...

```js
new Vue({
    // 상태  : 앱을 작동하는 원본 소스 (= data)
    data() {
        return {
            count: 0,
        }
    },
    // 뷰 : 상태의 선언적 매핑 (= template)
    template: `
    <div> {{ count }} </div>
    `,
    // 액션 : 뷰에서 사용자 입력에 대해 반응적으로 상태를 바꾸는 방법 (= method)
    methods: {
        increment () {
            this.count++,
        }
    },
})

```


✅ 상태 관리 패턴 사이클 정리?  

`Vue Components` : 화면 단 state에 접근하고 싶으면 dispatch 해라  
`actions` : 백엔드와 통신하는 곳 / 비동기적인 방법으로 백엔드와 통신해서 데이터를 얻어온다.  
`Mutatitos` : state 값을 바꿀 수 있는 것 / state의 상태를 변경하는 유일한 방법 (동기 methods)  
`Devtools` : 누가 무엇을 바꾸었는지 알 수 있는 부분  
`state` : 데이타 저장소(멤버 변수를 가지고 있는 것, 메모리) / 데이터가 바뀌면 Vue components가 변경된다.  
단방향으로 데이터 관리가 필요하다.   

<img src="https://user-images.githubusercontent.com/44612896/141726211-73d54249-ae4a-4ff7-a82e-e5baf909bdd5.png" width="400">

- 출처 : https://vuex.vuejs.org/kr/

<br><br>

✅ vuex 설치 방법

```cmd
npm install vuex --save
vue add vuex

vuex를 설치하면 store/index.js가 생길 것이다.
main.js를 보면 store 를 vue에 등록해놓은 것을 볼 수 있다.
```

✅ step00

```js
// Vuex 배우기전에 방법
하위 컴포넌트에서 this.$emit("addtotcount"); 를 상위로 이벤트로 보낸다.
상위 컴포넌트에서는 v-on:addtotcount="addTotalCount" addTotalCount를 실행한다.
methods: {
addTotalCount() {
    this.count += 1;
    },
},
```

✅ step01

```js
하위 컴포넌트 

<button v-on:click="addCount">
methods: {
addCount: function() {
    this.count += 1;
    // this.$emit("addtotcount");
    this.$store.state.count++; // $는 뷰가 가지고 있는 내부 속성
    }
}

// store/index.js
// step01;
// 하위 컴포넌트에 있는 버튼을 누를때 마다 store에 있는 count도 증가한다.
// state가 뭔지 개념만 잡는 단계
// this.%store.state.count++ 절대 바로 접근하는 방법을 사용하지 않는다.
export default new Vuex.Store({ 
  state: {
    count: 0,
  },

```
---

## state 사용 예제

✅ step02

```js
// store/index.js
export default new Vuex.Store({
  state: {
    count: 0,
  },
  //getters를 이용하게 되면 computed처럼 캐싱해서 사용할 수 있다.
  //우리는 매번 캐싱된 값을 가지고 갈 수 있다. 효율적!
  getters: { 
    // 복잡한 계산식을 처리 : computed
    countMsg(state) { // ❗주의할점 getters의 첫번째 인자값은 state 가 꼭 들어가야 한다.!!!!!
      // return state.count + '번 호출됨';
      let msg = "10번보다 ";
      if (state.count > 10) {
        msg += "많이 ";
      } else {
        msg += "적게 ";
      }
      return msg + " 호출됨(" + state.count + ")";
    },
  },
});

// 부모 컴포넌트
countMsg() {
      return this.$store.getters.countMsg; //getters를 사용
    }
```


✅ step03

```js

result.vue
import { mapGetters } from "vuex"; // mapGetters르 쓰기 위해서는 import가 필요하다.
computed: {
    // ...mapGetters({
    //   countMsg: "countMsg", 
    //   msg1: "msg1",
    //   msg2: "msg2",
    //   msg3: "msg3",
    // }),
    //이름: "이름"  이름과 속성의 이름이 같을때는 생략이 가능하다.
    ...mapGetters(["countMsg", "msg1", "msg2", "msg3"]),
    total() {
      return this.$store.state.count;
    },
    /*
    countMsg() {
      return this.$store.getters.countMsg;
    },
    */
  },

// store/index.js
//step03
export default new Vuex.Store({
  state: {
    count: 0,
  },
  getters: {
    // 복잡한 계산식을 처리 : computed
    countMsg(state) {
      // return state.count + '번 호출됨';
      let msg = "10번보다 ";
      if (state.count > 10) {
        msg += "많이 ";
      } else {
        msg += "적게 ";
      }
      return msg + " 호출됨(" + state.count + ")";
    },
    msg1(state) {
      return "msg1 : " + state.count;
    },
    msg2(state) {
      return "msg2 : " + state.count;
    },
    msg3(state) {
      return "msg3 : " + state.count;
    },
  },
});
```

---

## Mutations을 사용 예제

<br>

Mutations

```
state의 값을 변경하기 위해 사용
각 컴포넌트에서 State의 값을 직접 변경하는 것은 권잘하지 않는 방식이다.
state의 값의 추적을 위해 동기적 기능에 사용
Mutations는 직접 호출이 불가능하고 store.commit('정의된 이름')으로 호출할 수 있다.
```


✅ step04

```js

// subject.vue
  methods: {
    addCount: function() {
      this.count += 1;
      // this.$store.state.count++; 우리는 여태까지 state에 직접 접근했다.
      this.$store.commit('ADD_ONE'); // commit('mutations의 이름') mutations의 이름은 대문자로 하는 경우가 있다.
    },
    addTenCount: function() {
      this.count += 10;
      this.$store.commit('ADD_COUNT', 10);
    },
    addObjCount: function() {
      let num = Math.round(Math.random() * 100);
      console.log(num);
      this.count += num;
      this.$store.commit('ADD_OBJ_COUNT', { num });
    },
  },


// store/index.js
  mutations: {
    ADD_ONE(state) {
      state.count += 1;
    },
    ADD_COUNT(state, payload) { // 그냥 단일 값이 넘어 올 때
      state.count += payload;
    },
    ADD_OBJ_COUNT(state, payload) { // 객체가 넘어 올 떄
      state.count += payload.num;
    },
  },

  getters: 동일
```


✅ step05

```js
//
import { mapMutations } from "vuex";

methods: {
    //mapMutations를 써서 편하게 사용할 수 있다.
    ...mapMutations({
      addMOne: "ADD_ONE",
      addMTenCount: "ADD_TEN_COUNT",
      addMObjCount: "ADD_OBJ_COUNT",
    }),
    addCount: function() {
      this.count += 1;
      // this.$store.commit('addOne');
      this.addMOne(); // 등록하지 않았을 때  this.$store.commit('ADD_ONE'); 이렇게 사용 했다.
    },
    addTenCount: function() {
      this.count += 10;
      // this.$store.commit('addCount', 10);
      this.addMTenCount(10);
    },
    addObjCount: function() {
      let num = Math.round(Math.random() * 100);
      this.count += num;
      // this.$store.commit('addObjCount', { num });
      this.addMObjCount({ num });
    },
  },

```


---

<br>

## Action 사용 예제

<br>

Actions

```
비동기 작업의 결과 적용하려고 할 때
Mutations는 상태 관리를 위해 동기적으로 처리하고 비동기적 처리는 Actions가 담당
Actions는 비동기 로직의 처리가 종료되면 Mutations를 호출
동기와 비동기 처리를 나누기 위해서 Actions와 Mutations를 나뉘어 놓은 것 같다.
```

✅ step06

```js
// store/index.js 부분 actions 추가되었다.
  actions: {
    asyncAddOne(context) { // context를 프로젝트라고 생각하면 된다. // mutations을 참조할 수 있는 객체라고 생각하면 된다.
      setTimeout(() => { // 콜백함수 비동기 예시.
        context.commit("ADD_ONE");
      }, 2000);
    },
  },


// subject.vue
    asyncCount() {
      this.$store.dispatch("asyncAddOne"); // mapActions가 나올 것 같다.
    },
```

✅ step07

우리가 결과적으로 써야하는 것

```js
import { mapMutations, mapActions } from "vuex";

    ...mapActions(["asyncAddOne"]),
    asyncCount() {
      this.asyncAddOne(); //this.$store.dispatch("asyncAddOne"); // 바뀌었다.
    },

```

```
기억하자❗
Dom => (dispatch) => actions => (commit) => mutations
```

<br>

---

# 교수님 설명

✅ mapgetters vs mapstate

```
mapgetters : state 값을 가공해서 가지고 올 때 사용
mapstate : state 값을 그대로 가지고 올 때 사용
```


✅ actions / mutations

```
actions : 시간이 많이 걸리는 것, 동기
actions의 첫번째 인자는 context

mutations : 시간 안 걸리는 것 즉, 오로지 set method만 있다고 생각해도 무방하다. 
값을 넣는 연산만 하는거구나~ 생각 (단지 상태값을 수정하는 곳)
mutation의 첫번째 인자는 : state
```

✅ getters

```md
...mapgetters 를 이용해서 데이터를 저장해서 사용하는게 권장이다.
```

