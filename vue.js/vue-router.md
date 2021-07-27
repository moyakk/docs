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
    { path: '/', name: 'Home', component: Home },       // 컴포넌트 맵핑
    { path: '/list', name: 'List', component: List }    // 컴포넌트 맵핑
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

라우터 링크
```vue
<router-link to="/">Home</router-link>
```
- <a> 태그처럼 지정된 위치로 이동하는 기능을 제공한다.
- 굳이 별도로 만들다는건 뭔가 확실한 기능이 있다는건데 ..
  - <a> 로 이동하면 페이지 전체를 다시 그리는데, <router-link> 를 쓰면 필요한 부분만 다시 그린다.
  - router.mode 의 모드 변경시 주소가 바뀌는데, <a> 태그를 쓰면 일일이 바꿔야 한다.
