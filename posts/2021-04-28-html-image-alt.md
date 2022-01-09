---
title: "[Web] image alt 圖說內容應該要放什麼才適合？"
date: 2021-04-28T02:34:25Z
layout: layouts/post.njk
draft: true
---

圖片分成三種

- 裝飾性
- 功能性
- 包含文字的圖片

## 裝飾性 Decorative Images



### 範例一：為頁面設計的一部分

```html
<img src="topinfo_bg.png" alt="">
```



### 範例二：組成文字連結的一部分

```html
<a href="crocuspage.html">
	<img src="crocus.jpg" alt="">
	<strong> Crocus bulbs</strong>
</a>
```



### 範例三：鄰近文字已能充分說明圖片的內容

```html
<p>
	<img src="sleepingdog.jpg" alt="">
	<strong>The sleeping dog:</strong> ...
</p>
```



https://www.w3.org/WAI/tutorials/images/decision-tree/