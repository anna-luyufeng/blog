---
title: ""
date: 2022-01-28T10:25:21+08:00
layout: layouts/post.njk
draft: true

---

ES6+ 語法 → ES5

babel.config.js

推薦用 JavaScript 寫設定檔，而不是 JSON，這樣可以根據環境動態配置需要的 presets 和 plugins

### @babel/preset-env

- presets 用來編譯的預置

透過 targets 讓 Babel 知道目標環境，從而只轉譯環境不支援語法

如果沒有配置會預設轉譯所有 ES6 語法

- plugins 配置完成編譯的外掛
- regenerator???

### @babel/polyfill

polyfill 直譯是墊片的意思

Babel 把 ES6 的標準分為 syntax 和 built-in 兩種型別。

syntax 指的是語法，如 const、=>

built-in 可以通過改寫覆蓋的語法，如 includes、Promise

預設只轉譯 syntaxt 型別的，built-in 需要透過 @babel/polyfill 完成轉譯

原理就是覆蓋那些 ES6 的新增的 built-in

7.4.0 版本廢棄 @babel/polyfill，通過 core-js 和 regenerator-runtime/runtime  （用來轉譯 generator function）取代

### @babel/runtime

包含 Babel 運作時的 helper 和一種 `regenerator-runtime` 的版本

被用來作為與 `@babel/plugin-transform-runtime` 的依賴



### @babel/plugin-transform-runtime

複用每個模組的轉譯 helper 函式，縮小程式碼體積。

為編譯後的程式碼提供一個 sandbox 環境，避免全域性污染

按需引入

注意： `@babel/plugin-transform-runtime` 和 `@babel/preset-env` 的 `useBuiltIns` 是互斥的，兩者都用來加入所需的 polyfills；用 `useBuiltIns` 會將 polyfills 加到全域範圍，而 `@babel/plugin-transform-runtime` 會在不汙染全域範圍的情況下，加入 polyfills，你應該視情況選擇其中一種方式
ref: https://github.com/babel/babel/issues/10271#issuecomment-528379505



###   @babel/register（babel-register）

https://www.babeljs.cn/docs/babel-register

babel-register 實際上為require加了一個鉤子（hook），之後所有被 node 引用的 .es6、.es、.jsx 以及 .js 文件都會先被 Babel 轉碼。

透過 require 是其中一種使用 Babel 的方式，它會將自己綁定到 node.js 的 `require` 上，並且在運作時自動的編譯
（過去 node.js 對 ES6 的支援度不是很好，babel/register 會將 ES6 語法轉換成 ES5，而現在基本上不會需要用到此套件）

=> 看懂 require 這個方法

只適合在開發環境使用

### @babel/node (babel-node)

內建在 babel-cli 內，可以直接運行 ES6 程式碼

### @babel/plugin-syntax-dynamic-import

讓瀏覽器可以支援動態載入 `import()`
（現在大多數瀏覽器都支援，主要是 IE 有影響 ）

更新：Babel 7.8.0 後預設支援動態載入 `import()` ，因此這個 plugin也不需要了，但目前有 [bug](https://github.com/babel/babel/issues/9872)，需要確定有 `es.array.iterator` 的 polyfill 才可以正常在 IE 上使用

### 特別注意（與 webpack 和 @babel/preset-env 一起使用）：

目前 `@babel/preset-env` 無法得知與 webpack 依賴內部 Promise 一起使用的 import()

> `@babel/preset-env` is unaware that using `import()` with Webpack relies on `Promise` internally

目標環境如果本身不支援 `Promise` （像是 IE），會需要手動引入 `promise` 和 `iterator` polyfills

https://hsuehyungtan.medium.com/babel-%E7%AD%86%E8%A8%98-7-7-0-5274be4eed93