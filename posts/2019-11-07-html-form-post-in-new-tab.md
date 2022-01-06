---
title: "[HTML] form 發送 POST 請求至分頁"
date: 2019-11-07T08:50:27Z
layout: layouts/post.njk
---

預設為當前頁面，在 `<form>` 加上 `target="_blank"` 屬性

```html
<form action="POST_URL" method="post" target="_blank">
  <label for="post-name">Name:</label>
  <input id="post-name" type="text" name="name">
  <input type="submit" value="Save">
</form>
```

> [form - HTML（超文本标记语言） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form#attr-target)