---
title: "[JS] Array Tips and Tricks 陣列方法與實用技巧"
layout: layouts/post.njk
---

## Array 的所有方法

https://pjchender.dev/javascript/js-array

````javascript
// 原陣列不會被改變，而是回傳新陣列
arry.map(callback<element>)                  // 用來將陣列中的元素做轉換（computed），搭配 return
arry.forEach( callback<item, index, array>)   // 用來疊代陣列中的元素，並執行動作，不需搭配 return
arry.slice(begin, end)                         // 用來擷取陣列中的部分元素（不包含 end）
arry.filter(callback<item, index, array>)    // 若 callback return 為 true 時則保留該元素
arry.reduce(callback<accumulator, currentValue, currentIndex, array>, initialValue)  // 搭配 return ，return 的內容會進到 accumulator，最後回傳 accumulator
arry.join('<str>')                            // 將陣列以 <str> 連接成字串，預設是","

// 原陣列會被改變
arry.pop()                                     // 刪除最後一個元素
arry.push()                                    // 將元素塞入陣列中
arry.shift()                                   // 刪除陣列中第一個元素
arry.splice(start, deleteCount, newItem)       // 用來移除陣列中的部分元素，並可補入新元素
arry.sort(compareFunction)                     // 根據 compareFunction 來將陣列重新排序
arry.concat(value1, [value2], ...)             // 把陣列連接在一起
````

> [Array 的所有方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) @MDN

https://ithelp.ithome.com.tw/articles/10213787

### 建立一個長度為 n 且內容相同的陣列

```js
/**
 * 建立一個長度為 length ，且所有內容均為 'element' 的陣列
 * create an array with same element in given length
 **/
Array(_length_).fill(_element_);
Array(10).fill('ele');
// [ 'ele', 'ele', 'ele', 'ele', 'ele', 'ele', 'ele', 'ele', 'ele', 'ele' ]
```



### 建立一個元素從 1 ~ n 的陣列

使用 `Array(5)` （或 `new Array(5)`）可以產生一個帶有 5 個 `empty` 元素的陣列，透過解構賦值可以讓這些元素變成 `undefined`：

```js
Array(5)               // [empty × 5]
[...Array(5)]          // [undefined, undefined, undefined, undefined, undefined]
[...Array(5).keys()]   // [0, 1, 2, 3, 4]

Array(5).keys()         // Array Iterator {}
```



### 根據元素 index 取得下一個元素，當元素為最後一個時跳回第一個（循環）

```js
const speeds = [1,1.5,2,2.5];

const speed = 2.5;

// 不存在在 speeds 的項目與最後一個項目都會拿到 0，回到第一個
const nextIndex = (speeds.indexOf(speed) + 1) % speeds.length; // 0

// 若 speed 為 2.5
// speeds.indexOf(speed) → 3
// speeds.indexOf(speed) + 1 → 4
// 4 % 4 → 0

// 若 speed 為 3
// speeds.indexOf(speed) → -1
// speeds.indexOf(speed) + 1 → 0
// 0 % 4 → 0
```



### 移除重複的項目

https://github.com/anna-luyufeng/note/issues/26



### 複製 Array（Shallow Copy）

```js
let fruits = ['Apple', 'Banana']
let shallowCopy = fruits.slice() // this is how to make a copy
// ["Strawberry", "Mango"]
```





## 將字串轉成陣列

```js
const string = 'hi there';

const usingSplit = string.split('');
const usingSpread = [...string];
const usingArrayFrom = Array.from(string);
const usingObjectAssign = Object.assign([], string);

// Result
// [ 'h', 'i', ' ', 't', 'h', 'e', 'r', 'e' ]
```

