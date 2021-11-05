# 2021-11-05 ES6 문법

# 목차
- [2021-11-05 ES6 문법](#2021-11-05-es6-문법)
- [목차](#목차)
  - [let](#let)
  - [Const](#const)
  - [Object](#object)
  - [For](#for)
  - [템플릿 리터럴(Template Literal) - Backtick](#템플릿-리터럴template-literal---backtick)
  - [Arrow function](#arrow-function)
  - [Destructuring](#destructuring)
  - [스프레드 연산자](#스프레드-연산자)
  - [promise](#promise)
  - [정리하면서 필요한 부분 정리](#정리하면서-필요한-부분-정리)
    - [callback 함수란?](#callback-함수란)
    - [자바스크립트에서 use strict 이란?](#자바스크립트에서-use-strict-이란)
    - [slice() 함수](#slice-함수)
    - [javaScript map() 함수](#javascript-map-함수)
    - [비동기 처러? 그게 뭔데](#비동기-처러-그게-뭔데)

---
<br>

## let
> 변수 선언을 위한 ES6의 새로운 키워드이다.  
> let은 선언된 블록에서만 사용할수 있는 변수이다.  
> 중복선언이 불가능하다.

예제
```js
var msg = 1;
if(msg === 1){
    let msg = 2; // 이 블럭에서 쓸 수 있는 msg를 만든다.
    console.log(msg); // 2를 출력
}
console.log(msg); // 1을 출력하다.
```

```js
let b = 1;
if(b === 1){
    let c = 2;
    console.log(c);
}
let c = 3;
console.log(c); 
//이렇게는 let을 같은 변수로 2번 사용 가능하다.
```

---  
<br/>

## Const
> 변수 선언을 위한 ES6의 새로운 키워드이다.  
> Const에 변수를 할당하면 재할당 할 수 없다.  
> let 키워드와 값을 변경할 수 없다는 것만 제외하고 동일한 기능으로 처리된다.

에제
```js
const msg = '상수';
console.log(msg); // 상수 출력됨.
msg = '1'; //상수를 변경할려고 하면 VM376:3 Uncaught TypeError: Assignment to constant variable. 발생
```

---
<br>

## Object
> 객체의 프로퍼티를 단축해서 사용가능하다.  
> 프로퍼티 초기화 단촉 (Property Initializer Shorthand) 기능    
> 간결한 메서드 (Concise Method)    

객체의 프로퍼티를 단축한 예제  

```js
// ES6 이전
// 이전에는 name: name age: age 이렇게 다 써주어야 했다.
function createPerson(name, age) {
    return {
        name: name,
        age: age
    };
}

// ES6 이후
// 객체 리터럴의 프로퍼티에 이름만 있으면 JavaScript 엔진은 Scope내의 같은 이름의 변수를 조사합니다. 변수를 찾으면 해당 변수의 값이 객체 리터럴의 동일한 이름에 지정됩니다
//즉, 객체 리터럴 프로퍼티 name에는 로컬 변수 name의 값이 할당된다.
function createPerson(name, age) {
    return {
        name,
        age
    };
}
createPerson("김영훈", 26);
//만들어진 결과
{
    "name": "김영훈",
    "age": 26
}
```

간결한 메서드 (Concise Method) 예제

```js
//ECMAScript 5 및 이전 버전에서는 다음과 같이 이름을 먼저 지정하고 함수 정의를 지정하여 객체에 메서드를 추가해야했다.
let person = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};
//ECMAScript 6에서는 콜론 및 function 키워드를 제거하여 구문을 보다 간결하게 만듭니다. 이전 예제를 다음과 같이 다시 작성할 수 있습니다.
let person = {
    name: "Nicholas",
    sayName() { //바로 함수를 만들수 있다.
        console.log(this.name);
    }
};
```

프로퍼티의 계산된 이름 예제
```js
//ECMAScript 5 및 이전 버전에서는 프로퍼티를 점 표기 대신 대괄호로 설정하면 객체 인스턴스의 프로퍼티 이름을 계산하여 지정할 수 있었다.
// 대괄호를 사용하여 변수의 식별자를 사용하면, 구문 오류가 발생할 수 있는 문자가 포함된 문자열 및 문자열 리터럴을 사용하여 프로퍼티 이름을 지정할 수 있다.
var person = {},
    lastName = "last name";

person["first name"] = "Nicholas";
person[lastName] = "Zakas";
console.log(person["first name"]);      // "Nicholas"
console.log(person[lastName]);          // "Zakas"

//객체 리터럴의 프로퍼티 이름으로 직접 사용할 수 있다.
var person = {
    "first name": "Nicholas"
};
console.log(person["first name"]);      // "Nicholas"

//ECMAScript 6에서 계산된 프러퍼티 이름은 객체 리터럴 구문의 일부이며 객체 인스턴스에서 계산된 프로퍼티 이름을 참조하는데 사용된 동일한 대괄호 표기법을 사용한다.
var lastName = "last name";
var person = {
    "first name": "Nicholas",
    [lastName]: "Zakas"
};
console.log(person["first name"]);      // "Nicholas"
console.log(person[lastName]);          // "Zakas"

//객체 리터럴 안의 대괄호는 속성 이름이 계산됨을 나타내므로 내용이 문자열로 평가된다.
var suffix = " name";
var person = {
    ["first" + suffix]: "Nicholas",
    ["last" + suffix]: "Zakas"
};
console.log(person["first name"]);      // "Nicholas"
console.log(person["last name"]);       // "Zakas"
```

---
<br>

## For
> for~of 반복문이 새롭게 생겨났다.

`foreach` 구문
- foreach 반복문은 오직 Array 객체에서만 사용가능한 메서드이다.(ES6부터는 Map, Set 등에서도 지원됩니다) 배열의 요소들을 반복하여 작업을 수행할 수 있다.

예제
```js
var items = ['item1', 'item2', 'item3'];

items.forEach(function(item) {
    console.log(item);
});
// 출력 결과: item, item2, item3
```

`for in`구문
- 반복 가능한 객체(Array, Map, Set, String, TypeArray, arguments 객체 등)을 반복하는 기능 수행을 한다.
- 즉, 객체의 요소를(Data)를 순회하기 위한 구문이다.  

```js
let data = [1,2,undeined,NaN,null,""];

for(let index in data){
    console.log(data[index]);
}
```
`for in` 구문의 단점
- 인덱스가 문자로 반환
- 루프 구문이 요소들만 순회하는 것이 아니라 프로토타입 체인(Chain)도 순회
- 루프 순회 순서가 무작위

`for of`구문
- 배열 순회를 지원하는 문법 중에서 가장 간결하고 직접적으로 접근 가능
- for-in 구문의 단점을 보완
- forEach 문에서 지원하지 않는 break, continue, return 구문 사용 가능

`for in` `for of`의 차이 예제
```js
//For in 예제1
const numbers_g1 = [1,2,3,4,5];
for(let number in numbers_g1) {
        console.log(number);
}

//For of 예제1
const numbers_g2 = [1,2,3,4,5];
    for(let number of numbers_g2) {
        console.log(number);
    }

//For in 예제2(Conllection)
const CarObj1 = {
    color: 'red',
    height: 1.7,
    witdh: 5
}
for(let prop in CarObj1) {
        console.log(prop); //프로토 타입 체인을 순회 한다. -> color , height, witdh 이렇게
}

//For of 예제2(Conllection)
const CarObj2 = {
    color: 'red',
    height: 1.7,
    witdh: 5,
    [Symbol.iterator]: function* (){
    yield this.color;
    yield this.height;
    yield this.witdh;
    }
}
for(let prop of CarObj2) {
    console.log(prop);
}
//결과
0
1
2
3
4
//
1
2
3
4
5
//
color
height
witdh
//
red
1.7
35 5
undefined
```
---
<br>

## 템플릿 리터럴(Template Literal) - Backtick
> ES6부터 새로 도입된 문자열 표기법이다.    
> 문자열 생성시 따옴표 대신, 백틱(`)을 사용한다. 
예제
```js
let str = `안녕하세요`;
```

`Backtick`의 기능
- 줄바꿈(개행) - 백틱을 사용하면, 줄바꿈 등을 쉽게 표현 할 수 있다.
```js
let str1 = `
Hi!
    It's me!
            JavaScript!
Cool!`;

//기존 방식
var str_01 = "Hi! \n\t It's me! \n\t\t\t JavaScript! \n So Cool!";
```
- 표현식 삽입 - ${} 사이에 변수나 연산 등을 삽입할 수 있게 되었다.

```js
let name = "apple";

console.log(`${name}은 엄청 맛있다.`);
//결과
apple은 엄청 맛있다.
```

---
<br>

## Arrow function
> ES6에서 추가된 화살표 함수(arrow Function)이다.   
> 함수를 심플하게 정의할 수 있도록 해준다.

형태
```
    (매개변수) => {명령어, ...}
    작성순서
    function 키워드를 삭제한다. -> ()안에 파라미터 이름을 넣는다.
    소괄호 다음에 화살표를 붙인다.
    {}을 작성하고 블럭안에 코드를 넣는다.
```
예제
```js
// ES6 이전
let fun1 = function() {
    console.log("fun1 동작");
};
fun1();

//ES6 이후
fun1 = () => {
    console.log("fun1 동작");
}
fun1();

//매개변수의 수에 따른 분류
//매개변수가 하나인 경우
fun1 = num => {
    console.log('fun1 :', num);
};
fun1(12);

//매개변수가 하나 이상일 경우
func3 = (num1, num2) => {
    console.log('익명함수 func3', num1, num2);
};

// {} 없이 사용할 경우에는 return 문을 생략한다. return 쓰면 에러
fun1 = num1 => num1*num1;
fun1(10)
//결과
100
```

---
<br>

## Destructuring
> 디스트럭처링은 구조화된 배열 또는 객체를 디스트럭처링(비구조화, 파괴)하여 개별적인 변수에 할당하는 것이다.    
> 배열 또는 객체 리터럴에서 필요한 값만 추출하여 변수에 할당하거나 반환할 떄 유용하다.  

1. 배열 디스트럭처링

ES5에서 배열의 각 요소를 배열로부터 디스트럭처러링하여 변수에 할당하기 이한 방법

```js
// ES5
var arr = [1, 2, 3];

var one   = arr[0];
var two   = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

ES6의 배열 디스트럭처링
```js
// ES6 Destructuring
const arr = [1, 2, 3];

// 배열의 인덱스를 기준으로 배열로부터 요소를 추출하여 변수에 할당
// 변수 one, two, three가 선언되고 arr(initializer(초기화자))가 Destructuring(비구조화, 파괴)되어 할당된다.
const [one, two, three] = arr;
// 디스트럭처링을 사용할 때는 반드시 initializer(초기화자)를 할당해야 한다.
// const [one, two, three]; // SyntaxError: Missing initializer in destructuring declaration

console.log(one, two, three); // 1 2 3
```

활용 예제
```js
const today = new Date(); // Tue May 21 2019 22:19:42 GMT+0900 (한국 표준시)
const formattedDate = today.toISOString().substring(0, 10); // "2019-05-21"
const [year, month, day] = formattedDate.split('-');
console.log([year, month, day]); // [ '2019', '05', '21' ]
```


2. 객체 디스트럭처링

ES5에서 객체의 각 프로퍼티를 객체로부터 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티 이름(키)을 사용해야 한다.

```js
let obj = {name: "hoony", age: 26};

let name = obj.name;
let age = obj.age;

```
ES6의 객체 디스트럭처링은 객체의 각 프로퍼티를 객체로부터 추출하여 변수 리스트에 할당한다. 이때 할당 기준은 프로퍼티 이름(키)이다.

```js
let obj = {name : "hoony", age: 26};
// 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미가 없다.
let {name, age} = obj;
```


---

<br>

## 스프레드 연산자
> 스프레드 연산자를 이용하면 배열, 문자열, 객체 등 반복 가능한 객체를 개별 요소로 분리할 수 있다.   

표현법
```js
let arr1 = [1,2,3,4,5];
let arr2 = [...arr1, 6, 7, 8, 9];
console.log(arr2);
//결과
[1, 2, 3, 4, 5, 6, 7, 8, 9]

let str = "hoony";
let str2 = [...str];
console.log(str2);
//결과
 ['h', 'o', 'o', 'n', 'y']

```

위의 코드를 보면 스프레드 연산자가 어떤 것인지 감이 좀 온다.  
스프레드 연산자는 연결, 복사 등의 용도로 활용도가 높은 편이다.

실질적인 사용 예제에 대해 알아보자  

배열에서 Spread Operator  
☑️  배열 병합  
기존에 두 개의 배열을 결합하는 데 있어서 concat 매서드를 이용했다면 ES6에서는 spread 연산자를 이용하여 좀 더 깔끔한 배열 병합이 가능하다.  

```js
// ES6 이전
let arr1 = [1,2,3];
let arr2 = [4,5,6];

let arr = arr1.concat(arr2);

// ES6 스프레드 연산자
let arr1 = [1,2,3];
let arr2 = [4,5,6];

let arr = [...arr1, ...arr2];
let arr3 = [1,2,3,...arr2,7,8,9];

```
☑️  배열 복사
```js
let arr1 = ["철수", "영희"];
let arr2 = arr1;

arr2.push("짱구");
console.log(arr2); // ['철수', '영희', '짱구']
console.log(arr1); // ['철수', '영희', '짱구']
// 원래의 것도 변경되었다. 문제!!

// 기존의 복사 방법
let arr1 = ["철수", "영희"];
let arr2 = arr1.slice();
arr2.push("짱구");
console.log(arr2);//['철수', '영희', '짱구']
console.log(arr1);//['철수', '영희']

//ES6 이후
let arr1 = ["철수", "영희"];
let arr2 = [...arr1];

arr2.push("짱구");
console.log(arr2); //['철수', '영희', '짱구']
console.log(arr1); //['철수', '영희']
```
⚠️ 주의 사항 Spread 연산자를 이용한 복사는 얕은(shallow) 복사를 수행하며, 배열 안에 객체가 있는 경우에는 객체 자체는 복사되지 않고 원복 값을 참조한다.

```js
let arr1 = [{name:"철수", age: 10}, "영희"];
let arr2 = [...arr1];

arr2[0].name = "영희";
arr2.push("짱구");

console.log(arr2); 
console.log(arr1);
// 출력 결과 객체가 바뀝니다.
(3) [{name: 영희, age: 10}, '영희', '짱구']
(2) [{name: 영희, age: 10}, '영희']
```

<br>

함수에서의 Spread Operator  
☑️Rest Parameter  
>함수를 호출할 때 함수의 매개변수(parameter)를 spread operator로 작성한 형태를 Rest Parameter라고 부른다.  
> Rest 파라미터를 사용하면 함수의 파라미터로 오는 값들을 모아서 "배열"에 집어 넣는다.   
> 깔끔한 함수 표현 적용이 가능해진다.

예제  

```js
function plus(...input) {
    let sum = 0;
    for (const item of input) {
        sum += item;
    }
    return {
        sum,
    }
}
plus(10, 20, 30, 40); // 출력 : {sum: 100}
```

<br>

☑️함수 호출 인자로 사용
> 함수를 Call 할 때 spread operator를 사용할 수 있다.  
> 기존에는 배열로 되어 있는 함수의 인자로 넣을려면 손으로 풀어서 넣어주던지, Apply를 이용했다.  

예제
```js
let arr1 = [123213213,141,24,123,15,1];
Math.min(...arr1); // 1
```

<br>

☑️ 객체 복사 또는 업데이트
> 객체에서 spread operator를 이용하여 객체의 복사 또는 프로퍼티를 업데이트 할 수 있다.

```js
var currentState = { name: '철수', species: 'human'};
currentState = { ...currentState, age: 10}; 

console.log(currentState)// {name: "철수", species: "human", age: 10}

currentState = { ...currentState, name: '영희', age: 11}; 
console.log(currentState); // {name: "영희", species: "human", age: 11}
```

---

<br>

## promise
> 프로미스는 자바스크립트 비동기 처리에 사용되는 객체이다.  
> 비동기 처리란? '특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성`을 의미한다.  

[비동기 처리 그게 뭔데?](#비동기-처러-그게-뭔데)

Promise는 왜 필요할까?
- 프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다.  
- 일반적으로 웹 앱플리케이션 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 아래와 같은 API를 사용한다.
```js
// url 주소에 pathVariance 로 요청하는 방식
$.get('url 주소/products/1', function(response) {
   // ... 
});
```
- 위 API가 실행되면 서버에다가 데이터 주세요! 라는 요청을 보낸다. 
- 그런데 여기서 데이터를 받아오기도 전에 마치 데이터를 다 받아온 것 마냥 화면에 데이터를 표시하려고 하면 오류가 방생하거나 빈 화면이 출력된다.  
- 이와 같은 문제점을 해결하기 위한 방법 중 하나가 프로미스 입니다.


---


<br>

## 정리하면서 필요한 부분 정리

### callback 함수란?
>즉, 콜백 함수란  
>다른 함수의 인자로써 이용되는 함수.  
>어떤 이벤트에 의해 호출되어지는 함수.  

<br>



### 자바스크립트에서 use strict 이란?
- strict 모드의 정의
  - strict 모드로 설정하는 방법은 간단합니다. 코드 앞쪽에 "use strict" 를 추가하는 것 입니다.

- 왜 strict 모드를 사용하는가?

  - "보안" 자바스크립트를 작성하는 쉬운 방법이기 때문입니다. 다른 이유는 "올바르지 않은 문법" 을 사전에 검출할 수 있습니다.
  - strict 모드는 쓰기금지 프로퍼티의 정의, getter 전용 프로터피, 존재 하지 않는 프로퍼티, 존재하지 않는 변수, 존재하지 않는 객체에 대해 에러를 발생시킵니다.

> 즉, 미리 오류가 발생할 것 같은것을 사전에 차단하는 거라고 생각하면 편하다.

<br>


### slice() 함수


<br>


### javaScript map() 함수


<br>


### 비동기 처러? 그게 뭔데   
- 자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미한다.

- 비동기 처리의 첫 번째 사례
  - 비동기 처리의 가장 흔한 사례는 우리가 사용했던 제이쿼리 ajax 이다.  
```js
function getData() {
	var tableData;
    //$.get()이 ajax 통신을 하는 부분
    // https://domain.com에 다가 HTTP GET 요청을 날려 1번 상품 정보를 요청하는 코드이다.
    // 쉽게 말하면 지정된 URL에 '데이터 하나 보내주세요1'라는 요청을 날리는 것과 같다.
	$.get('https://domain.com/products/1', function(response) { //서버에서 받아온 데이터는 response 인자에 담긴다.
		tableData = response; // tableData에 받아온 데이터를 저장한다.
	});
	return tableData; //끝까지 기다려주지 않고 다음 코드인 retrun tableData 를 실행해기 때문에 -> getData()는 undefined가 출력된다.
}
console.log(getData()); // undefined
```
위 코드와 같이 특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것이 비동기 처리입니다.

- 비동기 처리의 두 번째 사례
  - setTimeout()  
```js
// #1
console.log('Hello');
// #2
setTimeout(function() {
	console.log('Bye');
}, 3000);
// #3
console.log('Hello Again');
```
#1 -> #2 -> #3의 순서로 console.log가 실행되는 것이 아닌  
#1 -> #3 -> #2의 값이 출력된다.  
>setTimeout() 역시 비동기 방식으로 실행되기 때문에 3초를 기다렸다가 다음 코드를 수행하는 것이 아니라 일단 setTimeout()을 실행하고 나서 바로 다음 코드인 console.log('Hello Again');으로 넘어갔습니다.

