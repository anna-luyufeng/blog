---
title: "[Editor] VIM 指令"
date: 2021-12-03
layout: layouts/post.njk

---

## 編輯

```bash
# 進入編輯模式，左下角會出現 -INSERT- 字樣
i

# 離開編輯模式
[ESC]

# 
:wq
```

## 存檔

```bash
# 退出
:q

# 不存檔退出
:q!

# 存檔並退出
:wq   
```



## 移動游標

不進入編輯模式

```bash
# 移動到單詞的開頭
w
# 移動到單詞的尾端
e

# 移動到單行的開頭
0 
# 移動到單行的尾端
$
```

---



- http://teohm.com/blog/shortcuts-to-move-faster-in-bash-command-line/
- http://linux.vbird.org/linux_basic/0310vi.php
- http://www.keyxl.com/aaa8263/290/VIM-keyboard-shortcuts.htm
- https://pjchender.dev/app/note-vim/