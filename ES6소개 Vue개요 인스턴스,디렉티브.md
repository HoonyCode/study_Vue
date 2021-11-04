# 2021-11-04 ES6소개 Vue개요 인스턴스, 디렉티브

# 목차
- [2021-11-04 ES6소개 Vue개요 인스턴스, 디렉티브](#2021-11-04-es6소개-vue개요-인스턴스-디렉티브)
- [목차](#목차)
  - [ES6](#es6)
      - [ES6의 특징](#es6의-특징)
  - [Vue.js](#vuejs)
      - [Vue.js 특징](#vuejs-특징)
      - [MVVM Pattern](#mvvm-pattern)
    - [Vue Instance](#vue-instance)
      - [Vue 인스턴스 Life Cycle](#vue-인스턴스-life-cycle)
    - [template](#template)
    - [디렉티브](#디렉티브)
    - [교수님이 말씀하신 시험문제](#교수님이-말씀하신-시험문제)


## ES6
> ES6 는 ECMA라는 국제 기구에서 만든 표준문서인 ECMAScript(=ES)의 6번째 개정판 문선에 있는 표준 스펙을 말한다. 
> 6번째 버전이 2015년에 나왔기 때문에 ES2015라고도 합니다.

### ES6의 특징
1. class 지원한다.
2. let & const 문법이 추가되었다.
3. Arrow Function
4. Modules
5. Promises
6. 비구조화 할당 지원
7. 객체 리터럴
8. Template Literals
9. 매개변수 기본값  

---


## Vue.js
> Vue.js란 사용자 인터페이스를 만들기 위해 사용하는 오픈 소스 Progressive Framework 이다.

### Vue.js 특징
1. Approachable (접근성)
2. Versatile (유연성)
3. Performant (고성능)

### MVVM Pattern
- Model + View + ViewModel
- Model : 순수 자바스크립트 객체
- View : 웹페이지의 DOM
- ViewModel : Vue의 역할
    - 기존에는 자바스크립트로 view에 해당하는 DOM에 접근하거나 수정하기 위해 jQuery와 같은 library 이용했다.
    - Vue는 view와 Model을 연결하고 자동으로 바인딩하므로 양방향 통신을 가능하게 한다.

---


## Vue Instance
- Vue 인스턴스 생성방법  
예제
```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> <!-- Vue 추가 -->
<script>
    <!-- 새로운 뷰 만들기-->
    new Vue({
        el: "#app", <!-- Vue 요소 지정하는 곳 #app <- html id나 class css Selector -->
        data() {  <!-- Vue에서 사용되는 정보 저장, 객체 또는 함수 형태 -->
            return {
                message: "예제 입니다",
            }
        }
    })
</script>
```
    
|   속성   |                                                                 설명                                                                 |
| :------: | :----------------------------------------------------------------------------------------------------------------------------------: |
|    el    |                                        Vue가 적용될 요소 지정 CSS Selector 또는 HTML Element                                         |
|   data   |                                           Vue에서 사용되는 정보 저장, 객체 또는 함수 형태                                            |
| template |           화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성, 뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있다.           |
| methods  | 화면 로직 제어와 관계된 method를 정의하는 속성. 클릭 이벤트 처리와 같이 화면의 전반적인 이벤트와 화면 동작과 관련된 로직을 추가한다. |
| created  |                                           뷰 인스턴스가 생성되자 마자 실행할 로직을 정의.                                            |

- Vue 인스턴스가 화면에 적용되는 과정
1. 뷰 라이브러리 파일 로딩
2. 인스턴스 객체 생성(옵션 속성 포함)
3. 특정 화면 요소에 인스턴스를 붙임  - el 속성에 지정한 화면 DOM에 인스턴스가 부착된다.
4. 인스턴스 내용이 화면 요소로 변환
5. 변환된 화면 요소를 사용자가 최종 확인

- 정리
> DOM은 리얼 DOM 과 가상 DOM으로 나뉘어지는데 리얼 돔은 사용자가 실제로 보는 곳이고 가상 DOM은 Vue가 관리하는 곳이라고 생각하면 된다.
> 리얼 DOM에 데이터가 바뀌면 가상 DOM의 데이터가 바뀌게 되고 바뀐 값을 리얼DOM으로 맵핑한다.

### Vue 인스턴스 Life Cycle
1. Instance의 생성
2. Instance를 화면에 부착
3. 화면에 부착된 Instance의 내용을 갱신
4. Instance가 제거되는 소멸

---


## 디렉티브

### 보간법
-  데이터 바인딩의 가장 기본 형태는 "Mustache" 구문(이중 중괄호)을 사용한 텍스트 보간
   -  `{{ 속성명 }}`
-  v-once 디렉티브를 사용하면 데이터 변경 시 업데이트 되지 않는 일회선 보간을 수행할 수 있다.
```html
<!-- msg 값이 바뀌어도 사용자가 바라보는 값은 변화지 않음 -->
<div v-once> {{msg}} </div>
```

### v-text
- 요구값 : string
- 설명 :   
    엘리먼트의 textContent (opens new window)를 업데이트합니다. textContent 의 일부를 업데이트해야하는 경우 머스태시 보간법(mustache interpolations)을 사용해야합니다.
- 예시 :
```html
<span v-text="msg"></span>
<!-- 같은 방법 -->
<span>{{msg}}</span>
```
### v-html
- 요구값 : string
- 설명 :   
    요소의 innerHTML (opens new window)을 업데이트 합니다. 컨텐츠는 일반 HTML 로 삽입됩니다 - Vue 템플릿으로 컴파일 되지 않습니다.  
     `v-html` 을 사용하여 템플릿을 작성하려는 경우에, 컴포넌트를 사용하는 해결법으로 다시 생각해보세요.
- 예시 :
```html
<div v-html="html"></div>
```

### v-show
- 요구값 : any
- 설명 :   
    표현식 값의 참-거짓을 기반으로 엘리먼트의 display CSS 속성을 전환합니다.  
이 디렉티브는 조건이 변경 될 때 transition 을 전환합니다
- 예시 :
```html

```

### v-if
- 요구값 : any
- 설명 :   
    표현식 값의 참-거짓에 따라 엘리먼트를 조건부로 렌더링 합니다. 엘리먼트와 포함된 디렉티브 / 컴포넌트는 전환하는 동안 파괴되고 재구성 됩니다.   
    엘리먼트가 `template` 엘리먼트인 경우 해당 컨텐츠가 조건부 블록으로 추출됩니다.  
    이 디렉티브는 조건이 변경 될 때 transition 을 전환합니다.
- 예시 :
```html
<div v-if="Math.random() > 0.5">
Now you see me
</div>
```
### v-else
- 요구값 : 없음
- 제약조건 : 이전 형제 엘리먼트에는 v-if 또는 v-else-if 가 있어야 합니다.
- 설명 :   
    
- 예시 :
```html
<div v-if="Math.random() > 0.5">
Now you see me
</div>
<div v-else>
Now you don't
</div>
```
### v-on
- 약칭 : @
- 요구값 : Function | Inline Statement | Object 
- 전달인자 : event
- 수식어 :  
.stop - event.stopPropagation() 메서드를 호출.  
.prevent - event.preventDefault() 메서드를 호출.  
.capture - 이벤트 리스너에 캡쳐모드를 추가.  
.self - 해당 엘리먼트에서 이벤트가 전달된 경우에만 동작.  
.{keyAlias} - 특정 키에 대해서만 동작.  
.once - 한번만 핸들러가 동작.  
.left - 마우스 왼쪽 버튼 이벤트에만 핸들러 동작.  
.right - 마우스 오른쪽 버튼 이벤트에만 핸들러 동작.  
.middle - 마우스 가운데 버튼 이벤트에만 핸들러 동작.  
.passive - { passive: true } 속성을 DOM 이벤트에 추가.  
- 사용방법 :
    엘리먼트에 이벤트 리스너를 연결합니다. 이벤트 유형은 인자로 표시됩니다. 표현식은 메서드명, 인라인 구문이거나 수식어가있는 경우 생략 될 수 있습니다.  

    일반 엘리먼트에서 사용되는 경우 native DOM events (opens new window)만 수신합니다.   커스텀 엘리먼트 컴포넌트에서 사용되는 경우 해당 자식 컴포넌트에서 내보낸 custom events 를 수신합니다.  

    네이티브 DOM 이벤트를 수신 할 때, 메서드는 유일한 인자로 네이티브 이벤트를 받습니다. 인라인 구문을 사용하는 경우, 구문은 특별한 $event 속성인 v-on:click="handle('ok', $event)" 에 접근 할 수 있습니다.  
- 예시
```html
<!-- 메서드 핸들러 -->
<button v-on:click="doThis"></button>

<!-- 동적 이벤트 -->
<button v-on:[event]="doThis"></button>

<!-- 인라인 구문 -->
<button v-on:click="doThat('hello', $event)"></button>

<!-- 약칭 -->
<button @click="doThis"></button>

<!-- 약칭 동적 이벤트 (2.6.0+) -->
<button @[event]="doThis"></button>

<!-- 전파 중지(stop propagation) -->
<button @click.stop="doThis"></button>

<!-- 전파 방지(prevent default) -->
<button @click.prevent="doThis"></button>

<!-- 표현식이 없는 전파 방지 -->
<form @submit.prevent></form>

<!-- 체이닝 수식어 -->
<button @click.stop.prevent="doThis"></button>

<!-- 키 수식어(키 별칭) -->
<input @keyup.enter="onEnter" />

<!-- 클릭 이벤트는 단 한번 동작 -->
<button v-on:click.once="doThis"></button>

<!-- 오브젝트 구문 -->
<button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
```
### v-bind
- 약칭 : `:`
- 요구값 : `any (with argument) | Object (without argument)`
- 전달인자 : attrOrProp (optional)
- 수식어 :  `.camel` - 케밥 케이스(kebab-case) 속성 이름을 카멜 케이스(camelCase) 로 변환.
- 사용방법 : 하나 이상의 속성 또는 컴포넌트 prop을 표현식에 동적으로 바인딩합니다.
    
    class 또는 style 속성을 바인딩하는 데 사용되는 경우 Array 또는 Objects 와 같은 추가 값 유형을 지원합니다. 자세한 내용은 아래 링크된 가이드 섹션을 참조하세요.
    
    prop 바인딩에 사용되는 경우 prop 은 자식 컴포넌트에서 올바르게 선언 되어야합니다.
    
    인자없이 사용하면 속성 이름-값 쌍을 포함하는 객체를 바인딩하는 데 사용할 수 있습니다. 이 모드에서는 class 및 style 이 배열 또는 객체를 지원하지 않습니다.

- 예시
```html
<!-- 속성 바인드 -->
<img v-bind:src="imageSrc" />

<!-- 동적 속성 이름 -->
<button v-bind:[key]="value"></button>

<!-- 약어 -->
<img :src="imageSrc" />

<!-- 약어를 적용한 동적 속성 이름 -->
<button :[key]="value"></button>

<!-- 인라인 문자열 연결 -->
<img :src="'/path/to/images/' + fileName" />

<!-- CSS 클래스 바인딩 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">

<!-- CSS 스타일 바인딩 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<!-- 속성 객체 바인딩 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- prop 바인딩. "prop" 은 my-component 에서 선언되어야 합니다. -->
<my-component :prop="someThing"></my-component>

<!-- 자식 컴포넌트와 공통으로 부모 props 전달 -->
<child-component v-bind="$props"></child-component>

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
</div>
```
### v-cloak
- 표현식을 요구하지 않습니다.
- 사용방법: 이 디렉티브는 연결된 컴포넌트 인스턴스가 컴파일을 완료 할 때 까지 엘리먼트에 남아있습니다.   `[v-cloak]` `{ display: none }` 과 같은 CSS 규칙들이 합쳐진, 이 디렉티브는 컴포넌트 인스턴스가 준비될 때 까지 컴파일 되지 않은 mustache 바인딩을 숨기는데 사용할 수 있습니다.  
- 예시
```html
[v-cloak] {
  display: none;
}

<div v-cloak>
  {{ message }}
</div>
<!-- <div>은 컴파일이 완료 될 때까지 표시되지 않습니다. -->
```
---  

## 교수님이 말씀하신 시험문제

1. MVVM Pattern이 무엇인지 서술하시오.
2. created : 서버에 데이터를 요청(http 통신)하여 받아오는 로직을 수행하기 좋다
3. `v-if` 와 `v-show` 차이
