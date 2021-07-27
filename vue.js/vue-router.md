## vue-router

- node.js 에서 잘 쓰던 그 라우터 기능
- URI 에 컴포넌트를 맵핑해서 사용한다.

### install
```
npm install vue-router --save
```

### main.js
```js
import Vue from 'vue'

const Home = { template: '<div id="home">Home Component</div>' }    // 임시 컴포넌트
const List = { template: '<div id="List">List Component</div>' }    // 임시 컴포넌트

import VueRouter from 'vue-router'    // import
Vue.use(VueRouter)                    // 사용등록
const router = new VueRouter({
  mode: 'history',                    // [옵션, 근데 대부분 사용할듯]
  routes: [
    { path: '/', name: 'Home', component: Home },                     // 컴포넌트 맵핑
    { path: '/list', name: 'List', component: List },                 // 컴포넌트 맵핑
    { path: '*', component: { template: '<div>Not Found</div>' } }    // 예외처리는 이렇게
  ]
})

import App from './App.vue'
new Vue({
  el: '#app',
  router,                   // 라우팅 설정 적용
  render: h => h(App)
})
```

### App.vue
```vue
<template>
  <div id="app">
      <router-link to="/">Home</router-link>        <!-- http://localhost/ 로 이동하는 링크 생성 -->
      <router-link to="/list">List</router-link>    <!-- http://localhost/list 로 이동하는 링크 생성 -->
      <router-view></router-view>                   <!-- 각 라우팅 경로에 맵핑된 컴포넌트가 랜더링 될 위치 -->
  </div>
</template>
<script>
export default {
  name: 'App'
}
</script>
<style>
#app {
  font-family: 'Malgun Gothic', Verdana;
  font-size: 13px;
}
</style>
```

## 라우터 링크
```vue
<router-link to="/">Home</router-link>
```
- <a> 태그처럼 지정된 위치로 이동하는 기능을 제공한다.
- 굳이 별도로 만들다는건 뭔가 확실한 기능이 있다는건데 ..
  - ``<a>`` 로 이동하면 페이지 전체를 다시 그리는데, ``<router-link>`` 를 쓰면 필요한 부분만 다시 그린다.
  - router.mode 의 모드 변경시 주소가 바뀌는데, ``<a>`` 를 쓰면 일일이 주소를 바꿔야 한다.

## 라우터 링크 스타일
```css
.router-link-active { font-weight: 900; }
.router-link-exact-active { background-color: #777 ; }
```
- 위와 같이 예약된 클래스 스타일을 재정의하면 활성 상태의 링크를 강조 할 수 있는것 같다.
- 두 클래스의 차이점은 경로 단계가 깊을때 전체 경로가 일치해야 하는지 부분 경로만 일치해도 되는지를 구분한다고 한다.
