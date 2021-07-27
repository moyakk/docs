## new Vue()
- vue-cli 로 첫 삽을 뜨게 되었다.
- main.js 가 최초로 실행되는 스크립트라고 하는데 ..

### main.js
```js
import App from './App.vue'

new Vue({
  el: '#app',
  render: h => h(App)
})
```

- el
  - Vue 인스턴스가 그려질 HTML 의 DOM 요소(Element)를 지정한다.
  - CSS 에서 ID를 선택하듯이 '#+NAME' 의 형태로 작성한다.
  - 아래 index.html 의 ``<div id="app"></div>`` 과 대응된다.
- render
  - 화살표 함수를 풀어보면 다음과 같이 된다.
    - ``render: (h) => h(App)``
    - ``render: (h) => { return h(App) }``
    - ``render: function (h) { return h(App) }``
  - h 는 뭐지? 하고 찾아봤는데 createElement 가 대입된다고 한다.
    - ``render: function (createElement) { return createElement(App) }``
    - createElement 라는 함수가 내장되어 있는것 같은데 왜 하필 h 라고 -_ -?
      - 일단 익히기 바쁘니 자세한건 나중에 (..)

> Vue 인스턴스야 App.vue 에 정의된 컴포넌트를 #app 위치에 생성해줘!
 
### index.html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>simple_vue</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="/dist/build.js"></script>
  </body>
</html>
```

## 추가
- h 는 hyperscript 의 약자로 react-hyperscript 등에서도 많이 쓰이는 스타일인것 같다.
- 이런 스타일의 프레임워크를 하는 사람들의 느낌적인 느낌
