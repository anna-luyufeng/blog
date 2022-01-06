---
title: "[CSS] 根據不同語系，用 `quotes` 設定引號樣式"
date: 2019-11-14T13:17:43Z
layout: layouts/post.njk
---

今天 Apple 發表了 16 吋的 Macbook Pro
想看看多強大，因此開始逛起了官網，然後不小心就開始檢查原始碼（？）

在原始碼內發現這一行

```css
:lang(zh) {
    quotes: "「" "」";
}
```

才發現原來 CSS 有這個屬性！

不過不知道為什麼值是只有打 `zh`，而字型的設定卻是打完整的 `zh-TW`

```css
[lang]:lang(zh-TW) {
    font-family: "SF Pro TC","SF Pro Text","SF Pro Icons","PingFang TC","Helvetica Neue","Helvetica","Arial", sans-serif;
}
```

---

- [:lang() - CSS | MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/:lang)
- [quotes - CSS（层叠样式表） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/quotes)