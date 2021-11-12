# 2021-11-11 Vue CLI

# 목차
- [2021-11-11 Vue CLI](#2021-11-11-vue-cli)
- [목차](#목차)
- [Vue CLI](#vue-cli)
- [Vue CLI 요소](#vue-cli-요소)
- [Vue 요소 분석](#vue-요소-분석)

<br>

---

<br>


# Vue CLI

Vue CLI란?
>vue-cli 는 기본 vue 개발 환경을 설정해주는 도구입니다.  
vue-cli 가 기본적인 프로젝트 세팅을 해주기 때문에 폴더 구조에 대한 고민, lint, build, 어떤 라이브러리로 구성을 해야되는지 webpack 설정은 어떻게 해야되는지에 대한 고민을 덜을 수 있습니다.


<br>

Vue CLI 사용하기 위해 설치 해야할 것.  
1. Node js 설치  

    [Node js](https://nodejs.org/ko/) 사이트에 들어가서 운영체제에 맞는 LTS 버전을 다운로드 한다.  
    <img src="https://user-images.githubusercontent.com/44612896/141279378-a1dd937a-e58e-4910-b321-0de37d8149b5.png" width="400" >  


    설치확인 하는 방법  
    <img src="https://user-images.githubusercontent.com/44612896/141279898-3e5945f1-4c4d-4712-9f65-e90669af0f9e.png" width="400">  

2. NPM 설치하기     
    NPM : Command에서 써드 파티 모듈을 설치하고 관리하는 툴     
    NPM 명령어
    ```cmd
    npm init : 새로운 프로젝트나 패키지를 만들 때 사용 (ppackage.json이 생성됨)
    npm install package : 생성되는 위치에서만 사용 가능한 패키지로 설치
    npm install -g package : 글로벌 패키지에 추가 모든 프로젝트에서 사용 가능한 패키지로 설치
    ```

3. Vue/cli 설치     
    
    [@vue/cli](https://www.npmjs.com/package/@vue/cli)로 들어간다.      
    ```cmd
    npm install -g @vue/cli
    vue create 프로젝트이름
    ```  

4. 프로젝트 생성
    ```cmd
    vue create project-name
    생성 중 중지 : ctrl + c
    실행 : npm run serve
    파일만 존재하면 npm install로 할 수 있다.
    ```     

5. 프로젝트 생성 후 별도 플로그인이 필요할 떄
    ```cmd
    vue add plugin-name
    ex) vue add router

    axios 추가하는 방법
    npm install axios // packags.json 파일의 dependencies에서 axios가 설치되었는지 확인 한다.
    ```     

6. 생성된 project 실행하는 방법
    ```cmd
    npm run serve
    ```     


---

# Vue CLI 요소

<br>

`SFC(Single File Component)`
1. `<template>`
- 기본 언어 : html
- 각 *.vue 파일은 한번에 최대 하나의 `<template>` 블록을 포함 할 수 있다.
- 내용은 문자열로 추출되어 컴파일 된 Vue Component의 template 옵션으로 사용된다.

<br>

2. `<script>`
- 기본 언어 : js
- 각 *.vue 파일은 한번에 최대 하나의 `<scrip>` 블록을 포함 할 수 있다.
- ES2015 (ES6) 지원하여 import와 export를 사용 할 수 있다.


3. `<style>`
- 각 *.vue 파일은 여러 개의 `<style>` 태그를 지원
- `<style scoped>` scoped 속성을 이용하여 현재 컴포넌트에서만 사용 가능한 css를 지정 가능하다. 

<br>


---

<br>

# Vue 요소 분석

<br>

<img src="https://user-images.githubusercontent.com/44612896/141282506-29d47f67-e154-4fd5-8973-b975fd41184a.png" width="400">

<br>

```
.
├─ README.md
├─ index.html
├─ webpack.config.js
├─ package.json
└─ src
   ├─ main.js
   ├─ App.vue
   ├─ components        컴포넌트
   │  ├─ common
   │  └─ ...
   ├─ routes            라우터
   │  ├─ index.js
   │  └─ routes.js
   ├─ views             라우터 페이지
   │  ├─ MainView.vue
   │  └─ ...
   ├─ store             상태 관리
   │  ├─ auth
   │  ├─ index.js
   │  └─ ...
   ├─ api               api 함수
   │  ├─ index.js
   │  ├─ users.js
   │  └─ ...
   ├─ utils             필터 등의 유틸리티 함수
   │  ├─ filters.js
   │  ├─ bus.js
   │  └─ ...
   ├─ mixins            믹스인
   │  ├─ index.js
   │  └─ ...
   ├─ plugins           플러그인
   │  ├─ ChartPlugin.js
   │  └─ ...
   ├─ translations      다국어
   │  ├─ index.js
   │  ├─ en.json
   │  └─ ...
   ├─ images            이미지
   ├─ fonts             폰트
   └─ assets            기타 자원
```
