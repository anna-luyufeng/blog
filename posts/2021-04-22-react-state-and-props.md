---
title: "[React] State 與 Props 的差別"
date: 2021-04-22T03:29:53Z
layout: layouts/post.njk
draft: true
---

`props` 是唯讀的

被傳遞至 component （類似 function 參數）

state 是可序列化資料

什麼是可序列化？：資料可以透過 JSON.stringfy 再 JSON.parse 100% 還原

function 就不是

https://redux.js.org/faq/organizing-state#can-i-put-functions-promises-or-other-non-serializable-items-in-my-store-state

在 component 內管理（類似被定義在 function 內的變數）

---

- https://reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props
- https://github.com/uberVU/react-guide/blob/master/props-vs-state.md

