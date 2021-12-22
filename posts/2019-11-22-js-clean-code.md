---
title: "[Note]《無瑕的程式碼 JavaScript》閱讀筆記"
date: 2019-11-22T07:24:08Z
layout: layouts/post.njk

---

> 最近有大大將 [Clean Code](https://github.com/ryanmcdermott/clean-code-javascript) 翻成了[繁中版本](https://github.com/AllJointTW/clean-code-javascript) 🇹🇼 🎉 🎉 🎉 
> 之前就有將英文版閱讀過了一遍，不過譯者有加上自己的註解，覺得獲益良多
> 想趁這個機會將整個再 go through 一遍，並將還沒內化的部分筆記下來，增強印象

## 變數（Variables）
- 函數定義的參數是 **Parameter**，調用函數時傳遞的引數稱為 **Arguments**
- 使用預設參數（Parameter）代替條件判斷（Conditionals）
   - 需注意參數為 `undeined` 才會起作用，Falsy 值不會，像是 `''`、`false`、`null`、`0`、`NaN`等



## 函數（Functions）
- 參數少於 2 個較佳，若大於 2 個可用解構 Desctructing 的語法。
   - 解構會**複製**物件的原始型態，避免 Side Effect。**注意**：「巢狀物件」與「陣列」不會被複製。
- 建議函數命名以動詞開頭，像是 `doSomething()`、`setupUserProfile()`。
- [不要使用旗標（Flag）作為參數](https://github.com/AllJointTW/clean-code-javascript#%E4%B8%8D%E8%A6%81%E4%BD%BF%E7%94%A8%E6%97%97%E6%A8%99flag%E4%BD%9C%E7%82%BA%E5%8F%83%E6%95%B8)：表示函數做不只一件事（不符合[「函數應該只做一層抽象（Abstraction）」](https://github.com/AllJointTW/clean-code-javascript#%E5%87%BD%E6%95%B8%E6%87%89%E8%A9%B2%E5%8F%AA%E5%81%9A%E4%B8%80%E5%B1%A4%E6%8A%BD%E8%B1%A1abstraction)）
```js
// 糟糕的
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}

// 適當的
function createFile(name) {
  fs.create(name);
}
function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```
- 避免副作用（Side Effects）
   - 不使用會改變原始數值的方法，如：`Array.push()`
- 【不太懂】[偏好使用函數式程式（Functional Programming）設計代替命令式程式設計（Imperative Programming）](https://github.com/AllJointTW/clean-code-javascript#%E5%81%8F%E5%A5%BD%E4%BD%BF%E7%94%A8%E5%87%BD%E6%95%B8%E5%BC%8F%E7%A8%8B%E5%BC%8Ffunctional-programming%E8%A8%AD%E8%A8%88%E4%BB%A3%E6%9B%BF%E5%91%BD%E4%BB%A4%E5%BC%8F%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88imperative-programming)
    - 函數式程式（Functional Programming）屬於宣告式程式（Declarative Paradigm）
       - 較為抽象，描述該在哪裡做什麼（what to do）以及資料流程（data flow）
       - 較依賴表達式（expression），表達式是一個單純的運算過程，並且總會返回值
    - 命令式程式設計（Imperative Programming）
       - 具體表達需要做什麼來達到目標，描述如何做什麼（how to do）以及流程控制（flow control）
       - 經常使用程式語言基本的語句（statement），例如 _for, while, if, switch_ ⋯⋯等
- 封裝狀態（Encapsulate Conditionals）
   - 狀態：當有一個以上條件判斷時，將其封裝可以透過 function 的名稱了解到其判斷的是什麼
```js
// 糟糕的
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  // ...
}

// 適當的
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```
- 避免負面狀態（Negative Conditionals）
  - 讓變數命名盡量預設是 truthy，才不會加上 `!` 後變成負負得正，容易變得難以理解
- 【不太知道怎麼應用】避免狀態（Avoid conditionals）
  - 當類別或是函數出現 `if` 或 `switch` 語法，代表你的函數做了超過一件事情
  - 什麼是多態性（Polymorphism）？
     - 給不同的對象發送同一個消息的時候，這些對象會根據這個消息分別給出不同的反饋 - [js 多態如何理解，最好能有個例子](https://segmentfault.com/q/1010000003056336)
- 避免型別（Type）檢查（1）：統一所有 API
- 避免型別檢查（2）：考慮使用 TypeScript
- 別過度優化：了解哪些是[無用的優化](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
- 移除無用的程式碼（Dead Code）

## Object 與資料結構（Data Structure）

- 使用 getters 與 setters，會比單純使用屬性（property）好
```js
// 糟糕的
function makeBankAccount() {
  // ...

  return {
    balance: 0
    // ...
  };
}

const account = makeBankAccount();
account.balance = 100;

// 適當的
function makeBankAccount() {
  // 私有變數
  let balance = 0;

  // 'getter'，經由下方的返回物件對外公開
  function getBalance() {
    return balance;
  }

  // 'setter'，經由下方的返回物件對外公開
  function setBalance(amount) {
    // ... 更新前先進行驗證
    balance = amount;
  }

  return {
    // ...
    getBalance,
    setBalance
  };
}

const account = makeBankAccount();
account.setBalance(100);
```
- 讓物件擁有私有成員（members）：透過閉包（Closure）來私有化參數