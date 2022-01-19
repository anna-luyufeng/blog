---
title: "[JS] Location and History"
date: 2022-01-14T10:58:51+08:00
layout: layouts/post.njk
draft: true
---

## Snippet

替換 Domain

```js
var initialPage = `${location.pathname}${location.search}`;
location.replace('http://localhost:3000' + initialPage);
```

