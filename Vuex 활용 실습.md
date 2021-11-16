# Vuex 활용 실습

# 목차
- [Vuex 활용 실습](#vuex-활용-실습)
- [목차](#목차)
- [Vuex 리뷰](#vuex-리뷰)
- [아파트](#아파트)
- [교수님 보충 설명](#교수님-보충-설명)

# Vuex 리뷰

`Getters`

```
state에서 view로 값을 가공해서 가지고 오는 것을 말한다.
```

`dispatch`

```
view에서 actions으로 데이터를 넘기는 것
```

`commit`

```
actions에서 Mutation으로 데이터를 넘기는 것
```

`Actions`

```
시간이 많이 걸리는 일을 처리하는 곳이라고 생각하면 된다.
```

`Mutations`

```
Setter라고 생각하면 된다. 
빠르게 값만 수정하는 일을 처리하는 곳이라고 생각하면 된다.
```

---

# 아파트 

✅ 초기 셋팅

```
npm install
vue add vuex
```

✅ HouseSearchBar.vue

```
시군구를 선택할 수 있는 select를 만든다.

store를 이용해서 데이터를 받아온다.
```

---

<br>

# 교수님 보충 설명 


✅ HouseSearchBar.vue

```
컴포넌트에 들어가 있는 created() 는 화면이 호출될 때 마다 호출된다.
created(){
    this.CLEAR_SIDO_LIST() // 여기에 넣는 것 보다 destroyed 에 넣어준다.
    this.getSido();
}

컴포넌트가 소멸할 때 destroyed를 사용해서 데이터를 날리면 좋다.
destroyed(){
    this.CLEAR_SIDO_LIST() 
},
```

✅ store/index.js

```
axios의 baseURL을 설정해 놓으면 -> baseURL 을 relative URL을 붙여서 이동할 수 있다.

axios의 baseURL을 설정해 놓았지만, https://를 붙여서 url을 적어주면 baseURL을 무시하고 https:// 주소로 가게 된다.

axios은 콜론으로 절대 주소인지 판단한다.
```

✅ CORS란?

> CORS는 Cross-Origin Resource Sharing의 약자입니다.  
> 교차 출처 리소스 공유로 번역될 수 있는데, 브라우저에서 다른 출처의 리소스를 공유하는 방법입니다.  

<br>

 
```
res.header("Access-Control-Allow-Origin", "*");
res.header("Access-Control-Allow-Headers", "X-Requested-With");
//위 두 줄을 추가해주면 CORS 를 허용하게 한다.
```

<br>

✅ STS에서 webConfig.java

- addCorsMappings을 보면 CROS를 어떻게 허용해 놓았는지 볼 수 있다.

<br>

```java
	public void addCorsMappings(CorsRegistry registry) {
//		System.out.println("CORS Setting");
//		default 설정.
//		Allow all origins.
//		Allow "simple" methods GET, HEAD and POST.
//		Allow all headers.
//		Set max age to 1800 seconds (30 minutes).
		registry.addMapping("/**")
			.allowedOrigins("*")
//			.allowedOrigins("http://localhost:8080", "http://localhost:8081")
			.allowedMethods("GET", "POST", "PUT", "DELETE")
			.maxAge(6000);
	}
```


✅ .env.local

```

git에 올라가지 않는다.
pair랑 할 때 .env.local 파일을 만들고 index.js에 불러서 사용했다면 나는 되고 친구는 안 될 수 있다.
git ignore에 대한 내용도 좀 알았으면 좋겠다.
```


✅ WEB에서 데이터를 저장

```
# 메모리 저장

--- build 끝나면 결과물 => JS(1개) => 일시적 저장(Web 페이지를 보는동안)
Component 저장 : 지역 변수 
=> 함수안에 선언되는 변수가됨 => class 멤버 변수

Vue 인스턴스 data 
=> Vue vm = new Vue() vm.$data.sid;

Vuex에 저장하는 방법 

로그인 정보 => 일시적, 서버랑 통신 Token(겹치지 않는 아주 긴 문자열) => Id pass 대신
// RESTGul API(서버) 쓰겟다라는 것은 => 서버쪽에서 세션 안 쓰겠다.
	상태를 유지 안함
	URI + 메소드로 업무 처리
	JWT => JSON Web Token => 나의 id를 대신하는 것

# 파일 저장 => 영구적

localstorage 저장 
=> 혼자서 사용되는 데이터로 영구적으로 저장된다.

Cookie 저장 
=> 서버랑 동기적 데이터 관리 
=> 서버에 저장되어 있는 세션을 구분할 ID 저장 
=> 쿠키가 무조건 파일 저장 아님 
=> 저장 시간 설정 가능 0이면 바로 지움 
=> 브라우저가 열려 있는 동안에 사용이 되고, 브라우저가 다하면 사라짐.

--- 서버

세션 저장 
=> 일시 저장(메모리 저장)

DB 저장 
=> 영구 저장, 나 외의 다른 사람들이 참고 할 수 있다.

```

✅ JWT 개념

```
JWT(Json Web Token)란 Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token이다. 
JWT는 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달한다. 
주로 회원 인증이나 정보 전달에 사용되는 JWT는 아래의 로직을 따라서 처리된다.

출처: https://mangkyu.tistory.com/56 [MangKyu's Diary]
```

<img src="https://user-images.githubusercontent.com/44612896/141945729-f9248046-8557-4399-b7b1-19851e879b1f.png" width="450">

- ref : https://mitny.github.io/articles/2019-01/jwt



✅ build

```
npm run build : 내부적인 src에 있는 모든 정보들을 잘 정리해준다.
build 처리후 -> build 폴더에 있는 데이터를 -> STS에 있는 static에 import 하면 된다.

npm run lint : 오류를 자동으로 잡아준다.?
```

✅ vue.config.js

```js
//빌드 할 때 이렇게 하겠다라고 정의 해놓은 것
// '이런게 있었는데'라는 기억을 가지고 구글링해서 넣어두자
module.exports = {
  outputDir: 'C:/ssafy/dist',
  configureWebpack: {

    output: {
      filename: 'app.js',
    },
    optimization: {
      splitChunks: false,
    },
  },
  filenameHashing: false,
};
```