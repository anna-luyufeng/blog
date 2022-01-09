---
title: "[Docker] 指令"
date: 2022-01-05T17:47:39+08:00
layout: layouts/post.njk
draft: true
---

```bash
# 使用當前目錄的 Dockerfile
docker build -t [image名稱]:[版本號] .

#  把 image 跑起來
docker run --name [container名稱] -d -p 3000:3000 [image名稱]:[版本號]
# 是把 container 裡面的 3000 port 對應到外面的 3000 port，才能直接從 web 連到 container

# 進入 container
docker exec -it [container hash]  sh
```

