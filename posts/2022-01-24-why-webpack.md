---
title: "[Note] 為什麼要用 webpack？他可以做什麼？"
date: 2022-01-24T10:51:48+08:00
layout: layouts/post.njk
draft: true
---

https://blog.huli.tw/2020/01/21/webpack-newbie-tutorial/

## 為什麼要模組化？

可以讓程式碼更好維護、更容易重複使用（用別人造好的輪子）。

在 JavaScript 會帶來的優點：

1. 抽象化
2. 封裝，只用 API 對外溝通
3. 增加可複用性，符合 DRY 原則
4. 更好管理

## ES5 之前如何模擬模組化？

### 立即執行函式（IIFE）

- 複雜的邏輯都封裝在函式內
- function 隔離了作用域，IIFE 內宣告的任何變數都會當作 IIFE 內的區域性變數，不會污染到全域性變數

```js
(function(){ 
  // ...
})()
```

### 模組化模式

```js
// 將封裝的模組賦值給一個變數
var helloApi = function(){  
  // 內部實現
  function sayHello(){    
      console.log('Hello');
  }  
  // 對外暴露 API
  return {      
  	sayHello: sayHello
  }
}()

// 呼叫模組 API
helloApi.sayHello(); // Hello
```



## Node.js 的模組

`require()` 引入模組；`module.exports` 導出模組

```js
// utils.js
function calculate(n) { 
  return ((n * 100 + 20 - 4)) % 10 + 3  // 計算價格公式
}

module.exports = calculate // 把這個函式 export 出去
```

```js
// main.js
var calculate = require('./utils')
console.log(calculate(30)) // 9
```

`module.exports` 決定了引入的時候是什麼內容。

此模組機制不在 JavaScript 的規範裡，而是「CommonJS」的標準。

在 ES6 之前，由於 JavaScript 沒有規範任何與模組相關的使用機制，大家各自定義如何去使用、導出模組。

然而瀏覽器並不支援 CommonJS 這個標準。

如何改寫成在瀏覽器也能運行的程式碼？（讓瀏覽器好像支援 CommonJS 的寫法）

`var calculate = require('./utils')` => `var calculate = （utils.js 裡的）module.exports`

```js
function main(require) {
  var obj = require('./utils')
  console.log(obj.cal(30)) // 9
  console.log(obj.name) // hello
}
```

```js
function main(require) {
  // 原本 main.js
  var obj = require('./utils')
  console.log(obj.cal(30))
  console.log(obj.name)
}
  
function utils(module) {
  // 原本 utils.js
  function calculate(n) { 
    return ((n * 100 + 20 - 4)) % 10 + 3
  }
    
  module.exports = {
    cal: calculate,
    name: 'hello'
  }
}
// 加入這兩行
var m = {}
utils(m)

// 加入底下這幾行
function r() {
  // 取得 module 被導出的內容 m.exports
  return m.exports
}

main(r)
```

1. 把檔案包成 function 並接收 `module` 及 `require` 等參數
2. 在外面呼叫 function，傳入一個物件及 `require` 函式

> 不支援的東西，寫工具自己支援就好

Babel、webpack、PostCSS 都是藉由工具來實現瀏覽器原生不支援的功能。

## Browserify：讓你在瀏覽器上使用 require 的工具

```bash
npx browserify main.js -o bundle.js
```

`main.js` 是我們主要執行的檔案，就是我們常聽到的入口點（entry point）。

## Webpack

本質與 Browserify 相似，只是需要把參數變成設定檔。

`webpack.config.js`

```js
module.exports = {
  entry: './main.js', // 入口點
  output: {
    path: __dirname, // 代表跟 webpack.config.js 檔同一個目錄
    filename: 'webpack_bundle.js' // 輸出的檔案名稱
  }
}
```

```bash
npm init -y
# 安裝 webpack
npm install webpack webpack-cli --save-dev 
# 執行 webpack
npx webpack --config webpack.config.js
```

webpack 有兩個模式，production 跟 development，預設是 production。

在開發的時候通常使用 development 這個模式，打包速度較快。

```js
module.exports = {
  mode: 'development', // 👈 
  entry: './main.js',
  output: {
    path: __dirname,
    filename: 'webpack_bundle.js'
  }
}
```

1. webpack 與 browserify 類似
2. 要在瀏覽器上面使用 CommonJS 的模組機制，就必須使用工具先把程式碼打包才能做到

## ES6 的標準化模組

JavaScript 模組化有了正式規範，`import` 與 `export`。

```js
// main.js
import obj from './utils'
console.log(obj.cal(30))
console.log(obj.name)
```

```js
//utils.js
function calculate(n) { 
  return ((n * 100 + 20 - 4)) % 10 + 3  // 計算價格公式
}
  
export default {
  cal: calculate,
  name: 'hello'
}
```

### 在 Node.js 使用 import 與 export

1. 把副檔名從 `.js` 改成 `.mjs`。Node.js 版本低於 13 的話，在使用 Node 的時候加上 flag `node --experimental-modules main.mjs`。
2. 透過 Babel 把 ES6 轉成 ES5。[簡易線上轉換器](https://babeljs.io/repl#?browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=JYWwDg9gTgLgBBARgKzgMyhEcDkA6AegFcZgAbAZxwCgBjCAOwojIFM8yIBzACiWTy0AhmR4BmAAwBKKXUbM2HbnxR4GQkK1lA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.8.3&externalPlugins=) 把 `main.js` 的內容從 import 轉成 require。

### 在瀏覽器使用 import 與 export

建立一個 `index.html`

```html
<html>
  <head>
    <script src="./main.js"></script>
  </head>
  <body>
  </body>
</html>
```

`Uncaught SyntaxError: Cannot use import statement outside a module`

需要告訴瀏覽器以 module 的形式來執行。

```html
<html>
  <head>
    <script src="./main.js" type="module"></script>
  </head>
  <body>
  </body>
</html>
```

若是要使用 import 必須要用伺服器的方式開啟才行，直接開檔案（點擊兩下打開瀏覽器）是不行的（網址開頭會是 `file://`）。

簡單起一個 file server：[http://localhost:8080](http://localhost:8080/)

```bash
python -m SimpleHTTPServer 8080
```



```
GET http://localhost:8080/utils net::ERR_ABORTED 404 (File not found)
```

要把 main.js 裡的 `import obj from './utils'` 改成：`import obj from './utils.js'` 才行，要明確指定是要引入 .js 這個檔案。



## 如何使用別人寫好的模組？

> 前端的世界很簡單，不支援或是**支援度很差的東西**，寫工具自己支援就好了

```bash
npx webpack --config webpack.config.js
```



Webpack 把任何資源都當作是一個模組。

圖片 `import Image from './assets/banner.jpn'`；CSS `import styles from 'styles.css'`

為了支援這樣的功能，webpack 定義了許多 loader，不同的資源有不同的 loader，要透過 loader 處理才能把資源以模組的方式載入。

## 想用我的模組嗎？想用的話可以全部給你，去找吧！我把所有模組都放在 NPM 。

NPM 是 Node Package Manager 的縮寫，是 Node.js 延伸出來的套件管理系統。

`npm -v` 查看現在使用的 npm 版本

`npm init` 建立 Node.js 專案的描述檔 `package.json`

`npm install axios` 安裝 axios 這個套件

1. package-lock.json：紀錄安裝套件的版本和依賴套件（dependencies）
2. node_modules/axios：裡面放安裝的套件資料

在 `.gitignore` 檔案內加入 `node_modules` 避免進到版本控制內
