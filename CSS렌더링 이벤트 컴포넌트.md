# 20201-11-08 CSS렌더링 이벤트 컴포넌트

# 목차
- [Vue.js](#vuejs)



# Vue.js
## Vue method
> Vue Intstance는 생성과 관련된 data 및 method의 정의 가능  
> method안에서 data를 this.데이터 이름 으로 접근 가능  

예제
```html
<div id="app">
  <div>data : {{message}}</div>
  <div>method kor : {{helloKor()}}</div>
  <div>method eng : {{helloEng()}}</div>
</div>
<script>
  new Vue({
    el: '#app',
    data: {
      message: 'Hello 싸피',
      name: '안효인',
    },
    methods: {
      helloEng() {
        return 'Hello ' + this.name;
      },
      helloKor() {
        return '안녕 ' + this.name;
      },
    },
  });
</script>
```


## filter
- 전역 필터, 로컬 필터
> 뷰의 필터는 화면에 표시되는 텍스트의 형식을 쉽게 반환해주는 기능이다.  
> 가장 간단하게는 단어의 대문자화부터 다국어, 국제 통화 표시 등을 다양하게 사용할 수 있다.

<br>

사용방법

```js
<div id="app">
  {{ message | captalize }}
</div>

new Vue({
  el: "#app",
  data() {
    return {
      message: "hello",
    };
  },
  filters: {
    capitalize: function (value) {
      if (!value) return "";
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
  },
});
//출력 값
Hello
```

## computed
> 템플릿 내에 표현식을 넣으면 편리하다.  
> 많은 연산을 템플릿 안에서 하면 코드가 비대해지고 유지보수가 어렵게 된다.  
> 그래서 복잡한 로직이라면 반드시 computed 속성을 사용해야 한다.  

예제 
```html
<div id="example">
  <p>원본 메시지: "{{ message }}"</p>
  <p>역순으로 표시한 메시지: "{{ reversedMessage }}"</p>
</div>

<<script>
  var vm = new Vue({
    el: '#example',
    data: {
      message: '안녕하세요'
    },
    computed: {
      // 계산된 getter
      reversedMessage: function () {
        // `this` 는 vm 인스턴스를 가리킵니다.
        return this.message.split('').reverse().join('')
      }
    }
  })
</script>>
<!-- 
원본 메세지: "안녕하세요"
역순으로 표시한 메세지:"요세하녕안"
-->
```
이 예제에서는 computed 속성인 reversedMessage를 선언했습니다.  
작성한 함수는 vm.reversedMessage속성에 대한 getter 함수로 사용됩니다.
```js
console.log(vm.reversedMessage) // => '요세하녕안'
vm.message = 'Goodbye'
console.log(vm.reversedMessage) // => 'eybdooG'
```


## computed속성의 캐싱 vs method 
computed 속성 대신 메소드와 같은 함수를 정의해서 사용할 수 도 있다.  
최종 결과에 대해서는 computed와 method 접근 방식은 서로 동일하다.  
차이점은 `computed 속성은 종속 대상을 따라 저장(캐싱)` 된다는 것이다.  
쉽게 말하면, method : 요청을 할 때마다 실행  
computed :  종속 대상이 바뀌지 않으면 계산을 다시 하지 않고 계산되어 있던 결과를 즉시 반환한다.


## watch
> watch 속성은 지켜보자 라는 의미를 가지고 있다.  
> data 혹은 computed 속성의 데이터 값이 변경될 때 실행되는 속성이다.  

예제
```html
<div id="app">
  <div>{{ msg }}</div>
  <div>{{ msgReversed }}</div>
</div>
<script>
  const vm = new Vue({
    el: "#app",
    data: { msg: "abc" },
    computed: {
      msgReversed: {
        get() {
          return this.msg.split("").reverse().join("");
        },
        set(value) {
          this.msg = value;
        },
      },
    },
    watch: {
      msg(newMsg) {
        //data -> msg 데이터가 변경될 때 실행
        console.log("New msg: " + newMsg);
      },
      msgReversed(newMsg) {
        //computed -> msgReversed 데이터가 변경될 때 실행
        console.log("New msgReversed: " + newMsg);
      },
    },
  });
</script>
```


//method (기능)  computed(캐싱) watch(변수변화값 보기)

## event
1. `v-on`
> v-on directive를 사용하여 DOM 이벤트를 듣고 트리거 될 때 javaScript를 실행할 수 있다.

```html
<div id="app">
  <button v-on:click="counter += 1">클릭</button>
  <p>위 버튼을 클릭한 횟수는 {{ counter }} 번 입니다.</p>
</div>

<script>
  new Vue({
    el: "#app",
    data() {
      return {
        counter: 0,
      };
    },
  });
</script>
```


2. 이벤트의 함수를 등록(메서드)
> 이벤트 발생시 처리 로직을 v-on에 넣기 힘들고 보기도 어렵게 된다.  
> v-on에서 이벤트 발생시 처리해야 하는 method의 이름을 받아 처리한다.

```js
<div id="app">
  <button v-on:click="plus">클릭</button>
  <p>위 버튼을 클릭한 횟수는 {{ counter }} 번 입니다.</p>
</div>

<script>
  new Vue({
    el: "#app",
    data() {
      return {
        counter: 0,
      };
    },
    methods:{
      plus: function (event) {
        this.counter += 1;
      }
    }
  });
</script>
```

3. preventDefault
> 이벤트를 취소할 수 있는 경우, 이벤트 전파를 막지 않고 그 이벤트를 취소하는 것

예제
```html
<p>체크박스 컨트롤을 클릭해 주세요</p>

<form>
  <input type="checkbox" onclick="stopDefAction(event);" />
  <label for="checkbox">체크박스</label>
</form>

<script type="text/javascript">
  function stopDefAction(evt) {
    evt.preventDefault();
  }
</script>
<!-- 체크박스 클릭이 되지 않는다 -->
```

## ref, $refs
> 뷰에서는 $refs 속성을 이용해 DOM에 접근할 수 있다.  
> 하지만 뷰의 목적 중 하나는 개발자가 DOM을 다루지 않게 하는 것이므로, 되도록 ref를 사용하는 것을 피하자.

<br>

예제

```html
<div id="app">
  아이디 : <input type="text" v-model="id" ref="id"/>
  <button @click="search">아이디 중복 체크</button>
</div>

<<script>
  new Vue({
    el: "#app",
    data() {
      return {
        id: '',
      }
    },

    methods: {
      search() {
        if (this.id.length == 0){
          alert('아이디를 입력하세요 !!');
          this.$refs.id.focus();
          return;
        }

        console.log(this.$refs.id.value); // ref="id"의 값을 콘솔 로그로 찍음
        alert('아이디 중복체크 성공');
      },
    },
  });
</script>
```

## class bonding
> v-bind: class 조건에 따라 class를 적용할 수 있다.  
> class css를 적용할 수 있게 한다.

<br>

예제

```html
<style>
.active {
  background: rgb(111, 111, 111);
}
</style>

<div id="app">
  <div v-bind:class="{ active: isActive }"> </div>
  <button v-on:click="toggle">VueCss</button>
</div>

<script>
  new Vue({
    el: "#app",
    data() {
      return {
        isActive: false,
      }
    },
    methods: {
      toggle: function (event) {
        this.isActive = !this.isActive;
      }
    },
  })
</script>
```

## 폼 입력 바인딩
> v-model directive를 사용하여 폼 input과 textarea element에 양방향 데이터 바인딩을 생성할 수 있다.  
> text와 textare 태그는 value 속성과 input 이벤트를 사용한다.  
> 체크박스들과 radio버튼들은 checked 속성과 change 이벤트를 사용한다.  
> select 태그는 value를 prop으로, change를 이벤트로 사용한다.

<br>

예제

```html
<div id="app">
  <div>
    아이디 :
    <input v-model.trim="id" placeholder="아이디를 입력하세요" />
    <!-- v-model은 기본적으로 모든 key stroke가 발생할 때마다 값을 업데이트 시킨다.
        .lazy 수식어를 추가하여 change 이벤트 이후에 동기화 할 수 있습니다. -->
    <input v-model.lazy="id" placeholder="아이디를 입력하세요" />
  </div>
  <div>
    메세지 :
    <textarea v-model="message" placeholder="내용을 입력하세요"></textarea>
  </div>
  <p>{{ id }} 님에게 보내는 메세지 : {{ message }}</p>
</div>
<script>
  new Vue({
    el: '#app',
    data: {
      id: '',
      message: '',
    },
  });
</script>
```


---


# Component

## 컴포너트란
> 컴포넌트란 조합하여 화면을 구성할 수 있는 블록을 의미한다.  
> 컴포넌트를 활용하면 화면을 빠르게 구조화하여 일괄적인 패턴으로 개발 할 수 있다.  
> 또한 코드를 쉽게 이해하고 재사용할 수 있다.  

컴포넌트는 두 종류가 존재한다.
1. Local(지역) Component
2. Global(전역) Component


## Local component (지역 컴포넌트)

선언방법

```js
let 변수명 = {
  template: '들어갈 내용'
}
```

사용 예제

```html
<!DOCTYPE html>
<html>
  <head>
    <title>제목</title>
    <meta charset="utf-8" />
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  </head>
  <body>
    <div id="pooney">
      <!-- 3번 -->
      <local-component></local-component>
    </div>
    <script>
      //1번
      let local = {
        template: "<div>pooney의 지역컴포넌트</div>",
      };
      //2번
      new Vue({
        el: "#pooney",
        components: {
          "local-component": local,
        },
      });
    </script>
  </body>
</html>
```
```
출력결과
pooney의 지역컴포넌트
```

실행 순서  
1. 1번의 local에 지역변수를 선언
2. 2번 생성자를 통한 인스턴스를 생성하면서 components에 해당 지역 컴포넌트인 local-component(태그)를 사용하겠다고 등록.
3. 해당 컴포넌트 태그를 입력하여 사용
4. 랜더링하면서 해당 `<local-component>`는 local 컴포넌트에서 정의한 `<div>`pooney의 지역 컴포넌트 `</div>`로 바뀌게 된다.

<br>

## Global component (전역 컴포넌트)

선언방법

```js
Vue.component('컴포넌트명',{
  template: '<div>pooney의 전역 컴포넌트 입니다. <div>'
})
```

예제

```html
<!DOCTYPE html>
<html>
  <head>
    <title>제목</title>
    <meta charset="utf-8" />
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  </head>
  <body>
    <div id="pooney">
      <div>pooney 영역입니다.</div>
      <global-component></global-component>
    </div>

    <div id="other">
      <div>other 영역입니다.</div>
      <global-component></global-component>
    </div>
    <script>
      Vue.component("global-component", {
        template: "<div>pooney의 전역 컴포넌트입니다.</div>",
      });

      new Vue({
        el: "#pooney",
      });

      new Vue({
        el: "#other",
      });
    </script>
  </body>
</html>
```

결과
```
pooney 영역입니다.
pooney의 전역 컴포넌트입니다.
other 영역입니다.
pooney의 전역 컴포넌트입니다.
```

## 지역 컴포넌트 전역 컴포넌트 차이점

> 지역은 해당 컴포넌트를 사용하기 위해서 인스턴스에 등록을 해줘야 한다.  
> 하지만 전역은 별다른 등록을 하지 않고 어느 인스턴스에서도 사용할 수 있다.


## 컴포넌트간 통신

✔️ 상위에서 하위 컴포넌트로 data 전달하는 방법  
