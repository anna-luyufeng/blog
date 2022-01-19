---
title: "[JS] 為什麼 0.1 + 0.2 不等於 0.3？"
date: 2019-11-12T03:10:57Z
layout: layouts/post.njk
draft: true
---

```js
console.log( 0.1 + 0.2 == 0.3 ); // false
```

因為數字是以二進制的形式處存在記憶體內，一個 1 和 0 的序列。但在十進制的數字系統中 `0.1` 這樣的小數，實際在二進制形式中是無限循環小數。

不僅僅只會在 JavaScript 內發生

=> 需要真正理解原因

為什麼？

IEEE 754 是什麼？

如何解決？

toFixed



- [不精确的计算](https://zh.javascript.info/number#bu-jing-que-de-ji-suan)