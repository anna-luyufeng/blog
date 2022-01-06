---
title: "[Network] HTTP Status Code 代表意義對照表"
date: 2019-11-08T04:07:09Z
layout: layouts/post.njk
---

- 1xx：Informational 資訊
- 2xx：Successful 成功：伺服器成功接收到用戶端的請求
- 3xx：Redirection 重新導向
- 4xx：Client Error 用戶端錯誤
   - 400 Bad Request
   - 401 Unauthorized 需要授權
   - 403 Forbidden 伺服器知道用戶端的身份，但用戶端無訪問權限
   - 404 Not Found 伺服器找不到請求的資源
   - 405 Method Not Allowed 
   - 444 Connection Closed Without Response (Nginx)
- 5xx：Server Error 伺服器錯誤

---

- [HTTP 狀態碼 - HTTP | MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status)
- https://httpstatuses.com/