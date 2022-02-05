---
title: "[VSCode] stylelint 在儲存的時候沒有自動校正"
date: 2021-11-18T02:23:04Z
layout: layouts/post.njk
---

開發時發現  `.scss` 等檔案本來會會自動校正格式的，突然就不會了，因此開始查是什麼問題。

查到原來是 v1.2.0 有 Bug，https://github.com/stylelint/vscode-stylelint/issues/327

```json
// settings.json
{
  "stylelint.validate": ["css", "scss"],
  "editor.codeActionsOnSave": {
      "source.fixAll.stylelint": true,
      "source.fixAll.eslint": true
  },
}
```

暫時的解決方式是先把 VSCode Stylelint 套件降版至 v1.1.0。

> 此問題已在 v1.2.1 解決