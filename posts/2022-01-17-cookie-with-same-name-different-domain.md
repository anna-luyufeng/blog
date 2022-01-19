---
title: "[Web] 讀取 Cookie 的問題"
date: 2022-01-17T18:00:45+08:00
layout: layouts/post.njk
draft: true
---

同時有 subdomain 跟 domain 設定 Cookie 遇到的問題

.domain.com

層級比 sub.domain.com 來得高

How to handle multiple cookies with the same name?

https://stackoverflow.com/questions/4056306/how-to-handle-multiple-cookies-with-the-same-name/24214538#24214538



Contrary to earlier specifications, leading dots in domain names (`.example.com`) are ignored.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie