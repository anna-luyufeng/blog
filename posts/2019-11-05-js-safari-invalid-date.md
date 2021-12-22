---
title: "[JS] Safari new Date() 產生 Invalid Date 問題"
layout: layouts/post.njk
date: 2019-11-05T08:05:39Z

---

## 問題描述

用 `new Date(dateString)` 將字串轉成日期物件時，在 Chrome 沒有問題，但在 Safari 出現 `Invalid Date`

## 原因

`dateString` 日期字串要可以被 `Date.parse()` 正確識別才能正確轉換成物件格式。

### 如何正確識別？

字串須符合 IETF-compliant RFC 2822 timestamps 或 version of ISO8601。

## 不建議使用 `new Date()` 解析日期字串

> 注意: 由於瀏覽器之間的差異與不一致性，強烈不推薦使用 `Date` 構造函數來解析日期字符串(或使用與其等價的Date.parse)。對RFC 2822格式的日期僅有約定俗稱的支持。對ISO 8601格式的支持中，僅有日期的串(例如"1970-01-01")會被處理為UTC而不是本地時間，與其他格式的串的處理不同。

## Safari 可以識別的日期字串格式

- `YYYY/MM/DD HH:mm:ss`
- `YYYY-MM-DDTHH:mm:ss`
- `MM-dd-yyyy`
- `yyyy/MM/dd`
- `MM/dd/yyyy`
- `MMMM dd, yyyy`
- `MMM dd, yyyy`

### 將 `YYYY-MM-DD HH:mm:ss` 轉成 Safari 可識別的日期字串格式

```js
new Date('2018-11-11 00:00:00'.replace(/-/g, "/")); // 2018/11/11 00:00:00
new Date('2018-11-11 00:00:00'.replace(/ /g,"T")); // 2018-11-11T00:00:00
```

> 最好的辦法就是毫秒數吧。即使加上了 T，修正了格式，Safari 還是把你提供的時間當做了格林尼治時間，new出來的時間對象，時間會往前 8 小時

## Reference 

- [Safari Invalid date 问题 yinxin630/blog#7](https://github.com/yinxin630/blog/issues/7)
- https://www.jianshu.com/p/dc83b45a9480
- https://css-tricks.com/everything-you-need-to-know-about-date-in-javascript/

