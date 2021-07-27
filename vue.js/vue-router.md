## vue-router

- node.js 에서 잘 쓰던 그 라우터 기능
- URI 에 컴포넌트를 맵핑해서 사용한다.

install
```
npm install vue-router
```

main.js
```js
import Vue from 'vue'

import VueRouter from 'vue-router'    // import
Vue.use(VueRouter)                    // 사용등록
const router = new VueRouter({
  mode: 'history',                    // [옵션, 근데 대부분 사용할듯]
  routes: [
    { path: '/', name: 'Home', component: Home },             // 경로에 컴포넌트 맵핑
    { path: '/list', name: 'List', component: List },         // 경로에 컴포넌트 맵핑
    { path: '/config', name: 'Config', component: Config }    // 경로에 컴포넌트 맵핑
  ]
})

import App from './App.vue'
new Vue({
  el: '#app',
  router,                   // 라우팅 설정 적용
  render: h => h(App)
})
```

App.vue
```vue
<template>
  <div id="app">
      <router-view></router-view>    <!-- 라우팅 경로에 맵핑된 컴포넌트가 랜더링 될 위치 -->
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
