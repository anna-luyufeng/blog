---
title: "qs 與 query-string 差異？"
date: 2022-01-27T15:47:31+08:00
layout: layouts/post.njk
draft: true
---

https://medium.com/starbugs/%E4%BD%A0%E6%89%80%E4%B8%8D%E7%9F%A5%E9%81%93%E7%9A%84-query-string-%E5%B0%8F%E7%B4%B0%E7%AF%80-56498dc0645



`qs` 跟 `query-string` 差別在 `qs` 可以處理 nesting 的值（預設至多 5 層），例如 Array of Objects (`[{}, {}]`）
因為 `query-string` 作者認為會產生很多 edge cases https://github.com/sindresorhus/query-string#nesting 所以不支援
（但我點進去是 issues board，所以⋯⋯先用 `qs` 處理）

BTW，剛剛查這幾個發現這個有趣的網站，可以比較 package
https://www.npmtrends.com/qs-vs-query-string-vs-querystring

> 其實有個 rison 格式
> https://medium.com/@takezoe/rison-uri-friendly-strucured-data-representation-74cb1feca2a7

