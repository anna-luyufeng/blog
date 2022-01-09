---
title: "[VSCode] 設定 i18n Ally 支援 namespace 並以指定語言顯示翻譯內容"
date: 2022-01-05T17:52:23+08:00
layout: layouts/post.njk
---

[i18n Ally](https://marketplace.visualstudio.com/items?itemName=Lokalise.i18n-ally) 是一個 VSCode 的擴充套件

### 1. 啟用 namespace

![127826399-14373325-f8d0-4d39-959a-273261b40ffb](/img/127826399-14373325-f8d0-4d39-959a-273261b40ffb.png)

### 2. 新增 react、i18next 至 Enabled Frameworks 

在 VSCode 設定搜尋  `i18n-ally.namespace`

![127826482-59085774-d871-48b7-9241-7a2673dc79b3](/img/127826482-59085774-d871-48b7-9241-7a2673dc79b3.png)

### 3. 在 Display Language 指定顯示的翻譯語言

在 VSCode 設定搜尋 `i18n-ally.displayLanguage`

![截圖 2022-01-05 下午6.00.59](/img/%E6%88%AA%E5%9C%96%202022-01-05%20%E4%B8%8B%E5%8D%886.00.59.png)

### 4. 完成 🎉  

游標移至字串上方會顯示所有語系的翻譯內容

![截圖 2022-01-05 下午6.19.19](/img/%E6%88%AA%E5%9C%96%202022-01-05%20%E4%B8%8B%E5%8D%886.19.19.png)

當游標移開，程式碼內顯示指定的語言（`zh-tw`）

![截圖 2022-01-05 下午6.19.29](/img/%E6%88%AA%E5%9C%96%202022-01-05%20%E4%B8%8B%E5%8D%886.19.29.png)