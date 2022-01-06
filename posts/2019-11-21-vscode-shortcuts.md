---
title: "[VS Code] 常用與實用快捷鍵"
layout: layouts/post.njk
date: 2019-11-21T14:36:14Z
---

> ⌥ alt
> ⇧ shift
> ⌃ control
>
> 👍 個人常用推薦

- ⇧ ⌘ P：顯示所有命令（有些 Extension 安裝後會有對應的指令）
   - 轉換大小寫（Transform to Uppercase/Lowercase）
   - 遞減／遞增排序行（Sort Lines Ascending/Descending）
- 👍 ⌘ P：搜尋檔名並打開檔案
- ⌘ L：變更檔案語言（**自訂的**，預設為 ⌘ K M，因為覺得 language 設為 L 比較直覺）
- ⌘ X：剪下游標所在的那一行（Empty Selection，不用選取）
- ⌘ C：複製游標所在的那一行（Empty Selection，不用選取），若已有選取則複製選取的範圍非行
- 👍 ⇧⌥↓ / ⇧⌥↑：複製選取的行數至下方／下方 
- 👍 ⇧ ⌘ K：刪除游標所在的那一行
- ⌘ Enter / ⇧ ⌘ Enter：插入新的一行在游標所在的那一行之下／之上（不用將游標移到行的最後面才 Enter）
- 👍  ⇧ ⌘ L：快速選取檔案內所有相同的文字

## 折疊

- ⌘ K ⌘ 0
- ⌘ K ⌘ L

## 註解
- ⌘ /：切換行註解
- ⇧ ⌥ A：切換區塊註解：需要先選取要註解的字
- ⌘ K ⌘ /：折疊全部區塊註解
- ⌘ K ⌘ C：加入行註解
- ⌘ K ⌘ U：移除行註解

## 編輯器
- ⌘ \：分割編輯器

## 檔案
- 👍 ⌥  ⌘ S：儲存所有為儲存的檔案（尤其重構的開了很多分頁要一次儲存的時候）
- 👍 ⌘ ⇧ F：在所有檔案中尋找選取的字（打開側邊搜尋欄）
- ⌥ ⌘ C：切換大小寫須相符條件
- ⌥ ⌘ W：切換全字拼寫須相符
- 👍 ⌘ K ⌘ W：關閉所有檔案
- ⌘ K Enter：保持編輯器打開（⌘ P 打開檔案時就不會被取代）

## 顯示
- ⌘ B：切換側邊欄顯示
- ⌘ K Z：切換成無干擾模式
- Escape Escape：離開無干擾模式

## 終端機
- ⌃ `：開啟終端機
- ⌃⇧`：新增新的終端機
- ⌘ \ ：分割終端機

---
- [keyboard-shortcuts-macos.pdf](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
- [VS Code Top-Ten Pro Tips - YouTube](https://www.youtube.com/watch?v=u21W_tfPVrY)
- VScode extensions and shortcuts to improve your productivity