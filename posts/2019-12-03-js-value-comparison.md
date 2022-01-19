---
title: "[JS] 為什麼 0 >= null 為 true？"
date: 2019-12-03T08:52:11Z
layout: layouts/post.njk
---

今天看到[《怎樣準備技術面試 - 工程師幹話》](https://medium.com/@p5d12000/怎樣準備技術面試-263dce21b814)除了笑到內傷，在文末玩弄 `null` 與 `0` 相等與比較，讓我試著在 console 裡印結果，百思不得其解就開始查資料瞭解這是怎麼回事。

結果發現《现代 JavaScript 教程》我已經讀過的章節「值的比较」其實有提到這個[奇怪的部分](https://zh.javascript.info/comparison#qi-guai-de-jie-guo-nullvs0)（~~而我卻一點印象也沒有，真的欠複習~~）。

```js
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```

主要是不同類型的值在進行「比較」時，JavaScript 會將其轉化為**數字**再判定大小。

因此 `null >= 0` 裡的 `null` 會被轉化成 `0`。

另外， `null` 跟 `undefined` 並不會在相等性檢查 `==` 做任何的類型轉換，它們有獨立的比較規則。

---

- [null >=0 ? true：false - 掘金](https://juejin.im/post/59b66390f265da065e320786)