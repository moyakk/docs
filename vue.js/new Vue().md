new Vue()
- vue-cli 로 첫 삽을 뜨게 되었다.
- main.js 가 최초로 실행되는 스크립트라고 하는데 ..

main.js
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
    - return 에서 App 을 인자로 주고 있는걸 보니 createElement 라는 함수인것 같다.
      - Vue 인스턴스야 App.vue 에 정의된 컴포넌트를 #app 위치에 생성해줘! 라고 이해하면 될듯.
    - 일단 익히기 바쁘니 자세한건 나중에 (..)

index.html
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
