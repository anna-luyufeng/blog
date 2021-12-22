---
title: "[JS] Code Readability 程式碼可讀性 - 命名"
date: 2021-12-13T15:55:29+08:00
layout: layouts/post.njk
tags:
  - JavaScript
---

> 此為閱讀 LINE Andriod 團隊 [Ishikawa Munetoshi ](https://engineering.linecorp.com/zh-hant/blog/author/munetoshi-ishikawa/) 所分享的 [Code Readabitliy 簡報](https://speakerdeck.com/munetoshi/code-readability) 之筆記

## 如何稱得上是好命名？

- 精準的 Accurate
- 描述性的 Descriptive
- 不會模稜兩可的 Unambiguous

## 命名重點

1. 名稱所表達的內容
2. 文法
3. 詞彙的選擇

## 名稱表達的內容

- ❌  Who/When/Where/Why/How 不需要表達命名對象什麼時候使用 / 在哪裡使用 / 如何使用 / 由誰使用
- ✅  What 形容是什麼 / 做什麼 → 命名對象責任明確化
  - **What** a type/value is
  - **What** a procedure/function does
- 例外：callback （抽象方法）因為還沒決定要做什麼，因此會有「在什麼時候／哪裡被呼叫」的資訊來命名

## 文法

- 接近英文文法規則，語順和語形來決定
- 不依據文法命名，則可能使名稱受到誤解
- 名詞句最後的單字應是最重要的單字
- 祈使句的第一個單字則表示該程序的動詞

### 多數情況

- value/type：名詞或名詞句型。例：已收到訊息的文字 `receivedMessageText`
- procedure/function/method：祈使句（動詞開頭）。例：儲存已收到的訊息 `saveReceivedMessage`



- 形容詞／形容詞句：性質或狀態的 type 或 value，例如 `Iterable`、`PLAYING`、`CONNECTED`
  - constant：v-ing, v-ed （Non-mutating） 不會改變原值
- 第三人稱形式的動詞／助動詞＋形容詞的疑問句：表達 Boolean 值，例如 `contains`、`isTextVisible`、`may/shouldShow`
- 包含介詞的副詞句：表達 type 變換與 callback 的程序，例如 `toInt`、`fromMemberId`、`onNewInit`、`onFinished`

## 詞彙的選擇

### 選擇不會模稜兩可的單字

採用資訊量較多的單字，可參考字典獲同意字詞典，找出最適合的單字。

也要避免難懂的專用名詞讓人難以理解。

- flag → is, was, should, can, may, will
- check → is, query, verify, measure, filter, notify, update
- good, fine → valid, completed, reliable, secure, satisfies
- old → previous, stored, expired, invalidated, deprecated
- tmp, retbval → actual name

### 避免使用令人混淆的縮寫

> Recognizing is easier than recalling

容易使閱讀程式碼的負擔變大。除非被廣泛使用，一估狗就有你的意思；若是專案獨有的縮寫，則可以利用註解讓人理解。

### 添加後綴作為補充單位／類型

- timeout: timeoutMillis, timeoutHours
- width: widthPoints, widthPx, widthInches
- color: colorInt, colorResId
- i, j, k: xxxIndex, row, col

### 正面描述（Positive affirmation），避免語意不清

- ✅ isEnabled（肯定）
- ✅ isDisabled（否定）
- ❌ isNotEnabled → isDisabled（肯定＋否定）
- ❌ isNotDisabled → isEnabled（否定＋否定）



## 實際應用／範例

-  `index` 是 zero-based，序數 `orinalNumber`



---

- https://engineering.linecorp.com/zh-hant/blog/author/munetoshi-ishikawa/
- https://google.github.io/styleguide/jsguide.html