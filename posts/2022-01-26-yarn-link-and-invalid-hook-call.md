---
title: "[Note] 如何解決 Yarn link 與 Invalid hook call 問題"
date: 2022-01-26T16:44:30+08:00
layout: layouts/post.njk
draft: true
---

## 錯誤訊息

在本機開發的時候，若想在專案內使用測試同樣在開發中的套件，會用 `yarn link` 來協助我們連結本機尚未發佈的套件：

兩個專案目錄名稱，且假設 my-app 跟 my-libaray 在同個目錄底下

- 專案：`my-app`
- 套件：`my-library`

```bash
cd my-library
yarn link

cd ../my-app
yarn link "my-library"
```

而當試著起專案，會遇到下方錯誤：

```bash
Error: Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons: 
1. You might have mismatching versions of React and the renderer (such as React DOM) 
2. You might be breaking the Rules of Hooks 
3. You might have more than one copy of React in the same app See https://fb.me/react-invalid-hook-call for tips about how to debug and fix this problem.
```

## Node.js 載入模組的流程

1. 如果我們載入的是 Node.js 內建的模組，例如 `http`，直接載入
2. 如果是相對路徑，則載入相對路徑
3. 若以上都不符合，則會搜尋該目錄下的 node_modules；如果是沒有則會遞迴往上層的 `node_modules` 搜尋直到系統的根目錄

## 解決方式

```bash
cd my-library
yarn link

cd node_modules/react
yarn link

cd node_modules/react-dom
yarn link


cd ../../my-app
yarn link "my-library"
yarn link "react"
yarn link "react-dom"
```



## 為什麼使用已經發佈到 npm 的套件就不會有這樣的問題？

因為專案的 `node_modules` 裡的套件不會有自己的 `node_modules` 目錄，而 `yarn link` 參考本地的套件會有，因此會造成參考不一致的問題。



https://reactjs.org/warnings/invalid-hook-call-warning.html#duplicate-react

https://classic.yarnpkg.com/en/docs/cli/link

https://andyyou.medium.com/npm-link-%E8%88%87-invalid-hook-call-%E9%8C%AF%E8%AA%A4-7c4c204ad62e

https://andreaswilli.github.io/wiki/yarn-link-invalid-hook-call