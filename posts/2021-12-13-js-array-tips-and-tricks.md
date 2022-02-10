---
title: "[JS] Array Tips and Tricks 陣列方法與實用技巧"
layout: layouts/post.njk
---

<!-- @TODO: 什麼是 Shallow Copy? -->

## Cheatsheet

| Method      | Mutation | Return value                           |
| ----------- | -------- | -------------------------------------- |
| push()      | O        | Number（Array 長度）                   |
| unshift()   | O        | Number（Array 長度）                   |
| pop()       | O        | 被移掉的值                             |
| shift()     | O        | 被移掉的值                             |
| concat()    | O        | Array                                  |
| findIndex() | X        | Number                                 |
| find()      | X        | 第一個找到的值                         |
| filter()    | X        | 符合條件的 Array                       |
| forEach()   | O        | `undefined`                            |
| map()       | X        | 長度一樣的 Array                       |
| some()      | X        | Boolean                                |
| every()     | X        | Boolean                                |
| reduce()    | X        | 計算出來的值                           |
| sort()      | O        | 長度一樣的 Array                       |
| reverse()   | O        | 長度一樣的 Array                       |
| slice()     | X        | 包含 startIndex 不含 endIndex 的 Array |
| splice()    | O        | 被移掉的值 Array                       |
| indexOf()   | X        | Number                                 |
| join()      | X        | String                                 |
| includes()  | X        | Boolean                                |

## Snippets

### 清空陣列

```js
var fruits = [
  "banana",
  "apple",
  "orange",
  "watermelon",
  "apple",
  "orange",
  "grape",
  "apple"
];

fruits.length = 0;
console.log(fruits); // returns []
```

### 複製陣列

```js
let fruits = ['Apple', 'Banana']

// Shallow Copy
let shallowCopySpread = [...fruits]
let shallowCopySlice = fruits.slice()
let shallowCopyFrom = Array.from(fruits)

// Deep Copy - array contains nested objects or arrays
let deepCopy = JSON.parse(JSON.stringify(fruits));
```



### 建立一個長度為 n 的陣列

### 元素從 0 開始

```js
Array(5)               // [empty × 5]
[...Array(5)]          // [undefined, undefined, undefined, undefined, undefined]
[...Array(5).keys()]   // [0, 1, 2, 3, 4]
Array.from({length: 5}, (v, i) => i); // [0, 1, 2, 3, 4]

Array(5).keys()         // {[ Array Iterator ]}
```

#### 元素從 1 開始

```js
Array.from({ length: 5 }, (val, index) => index + 1); // [1, 2, 3, 4, 5]
Array.from(new Array(5), (val, index) => index + 1); // [1, 2, 3, 4, 5]
```

#### 元素相同 `Array.fill()`

```js
Array(length).fill(value, startIndex, endIndex);
Array(3).fill(4); // [4, 4, 4]

// A single object, referenced by each slot of the array:
let arr = Array(3).fill({}) // [{}, {}, {}]
arr[0].hi = "hi"            // [{ hi: "hi" }, { hi: "hi" }, { hi: "hi" }]
```



### 移除陣列 falsy 的值

```js
const mixedArry = [0, "blue", "", NaN, 9, true, undefined, "white", false];
const trueArry = mixedArry.filter(Boolean);
console.log(trueArry); // ["blue", 9, true, "white"]
```

### 從陣列中隨機取一個元素

```js
var colors = ["blue","white","green","navy","pink","purple","orange","yellow","black","brown"];
var randomColor = colors[Math.floor(Math.random() * colors.length)];
```

> https://dev.to/b0nbon1/understanding-big-o-notation-with-javascript-25mc)

### 根據元素 `index` 取得下一個元素，當元素為最後一個時跳回第一個（循環）

```js
const speeds = [1,1.5,2,2.5];

const speed = 2.5;

// 不存在在 speeds 的項目與最後一個項目都會拿到 0，回到第一個
const nextSpeedIndex = (speeds.indexOf(speed) + 1) % speeds.length; // 0

// 若 speed 為 2.5
// speeds.indexOf(speed) → 3
// speeds.indexOf(speed) + 1 → 4
// 4 % 4 → 0

// 若 speed 為 3
// speeds.indexOf(speed) → -1
// speeds.indexOf(speed) + 1 → 0
// 0 % 4 → 0
```

### 找出兩個陣列重複的元素

```js
const arrayOne = [0, 2, 4, 6, 8, 8];
const arrayTwo = [1, 2, 3, 4, 5, 6];
const duplicatedValues = [...new Set(arrayOne)].filter(item => arrayTwo.includes(item));
console.log(duplicatedValues); // [2, 4, 6]

/*
* 因 Array.prototype.includes() 是 linear，而 Set.prototype.has() 是 constant，當資料量變大時會產生巨大的差異。
*/
const firstValues = new Set(arrayOne);
const duplicatedValues = arrayTwo.filter(item => firstValues.has(item));
```

> linear 與 constant 差別是什麼？
>
> [Understanding Big-O Notation With JavaScript - DEV Community 👩‍💻👨‍💻](https://dev.to/b0nbon1/understanding-big-o-notation-with-javascript-25mc)

### 移除重複的元素

```js
var fruits = ["banana","apple","orange","watermelon","apple","orange","grape","apple"];

// 方法一
var uniqueFruits = Array.from(new Set(fruits));
console.log(uniqueFruits); // returns ["banana", "apple", "orange", "watermelon", "grape"]

// 方法二
var uniqueFruits2 = [...new Set(fruits)];
console.log(uniqueFruits2); // returns ["banana", "apple", "orange", "watermelon", "grape"]
```

### 從陣列移除指定元素

```js
const array = [1,2,3];

// splice()
function deleteBySplice (array, element) {
  const index = array.indexOf( element );
  const copiedArray = [...array]; 
  if (index !== -1) {
  	copiedArray.splice( index, 1 );
  }
  return copiedArray
}

// filter()
function deleteByFilter (array, element) {
  array = array.filter( el => el !== element );
}
```



### 將字串轉成陣列

```js
const string = 'hi there';

const usingSplit = string.split('');
const usingSpread = [...string];
const usingArrayFrom = Array.from(string);
const usingObjectAssign = Object.assign([], string);

// [ 'h', 'i', ' ', 't', 'h', 'e', 'r', 'e' ]
```



### 陣列轉物件

```js
var fruits = ["banana", "apple", "orange", "watermelon"];
var fruitsObj = { ...fruits };
console.log(fruitsObj); // returns {0: "banana", 1: "apple", 2: "orange", 3: "watermelon", 4: "apple", 5: "orange", 6: "grape", 7: "apple"}
```



## 建立 Array

```js
// 😊 
let list = [];
let list = [1,2,3];

// 💩 會產生無法預期的結果
let list = new Array();
let list = new Array(1,2,3);
```

## 判斷是否為陣列

```js
// true
Array.isArray([]);

// false
Array.isArray();
Array.isArray({});
```

## Array 的所有方法

> [Array 的所有方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) @MDN

### `Array.from()`

```js
// Arrow function
Array.from(arrayLike, (element) => { /* ... */ } )
Array.from(arrayLike, (element, index) => { /* ... */ } )

// Mapping function
Array.from(arrayLike, mapFn)
Array.from(arrayLike, mapFn, thisArg)

// Inline mapping function
Array.from(arrayLike, function mapFn(element) { /* ... */ })
Array.from(arrayLike, function mapFn(element, index) { /* ... */ })
Array.from(arrayLike, function mapFn(element) { /* ... */ }, thisArg)
Array.from(arrayLike, function mapFn(element, index) { /* ... */ }, thisArg)
```



create `Array`s from:

- array-like objects (objects with a `length` property and indexed elements)
- iterable objects (objects such as `Map` and `Set`)

```js
// String
Array.from('foo') // [ "f", "o", "o" ]

// Set：移除重複元素，shallow-copied Array instance
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set); // [ "foo", "bar", "baz" ]

// Map
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map); // [[1, 2], [2, 4], [4, 8]]

// NodeList
// Create an array based on a property of DOM Elements
const images = document.getElementsByTagName('img');
const sources = Array.from(images, image => image.src);
const insecureSources = sources.filter(link => link.startsWith('http://'));

// Array-like
function f() {
  return Array.from(arguments);
}

f(1, 2, 3); // [ 1, 2, 3 ]
```



### 原陣列會被改變

- 先 Shallow Copy 在使用方法來避免原陣列被改變

````javascript
array.push()                                    // 將元素加在原陣列的"最後面"，且回傳陣列長度
array.unshift()																	// 將元素加在原陣列"最前面"，且回傳陣列長度
array.pop()                                     // 移除原陣列"最後一個"元素，回傳被移除的元素
array.shift()                                   // 移除原陣列"第一個"元素，回傳被移除的元素

array.forEach(callbackFn<element, index, array>)	 	// 迭代陣列中的元素，並執行 callback，不會回傳任何東西

/*
原地（in place）對一個陣列所有元素進行排序
- 若是沒有 compareFunction 預設會先透過 `.toString()` 轉成字串，回傳根據 Unicode 編碼位置（code points）而定的陣列
- Chrome V8 引擎原始碼中，當陣列長度小於 10 是插入排序法（Insertion Sort）（穩定）；其他時候則是快速排序法（Quick Sort）
*/              
array.sort(compareFunction<firstEl,secondEl>)

// 回傳反過來且長度相同的陣列
array.reverse()


// 拼接陣列：移除陣列部分元素、取代部分元素抑或添加新的元素至陣列中，回傳"被移除的"元素
// deleteCount 預設為陣列的長度
// deleteCount 若為 0，則從 start 開始添加元素
// item1, item2, itemN 等添加的元素只會影響"原本"的陣列
array.splice(start, deleteCount, item1, item2, itemN)
````

> 什麼是原地（In Place）？
>
> 它的意思是陣列會在原來的位置上操作並回傳，此時就不會需要額外的記憶體空間，也就是空間複雜度為 `O(1)` ，會將操作完的值覆蓋原陣列。

#### Array.sort(compareFn)

若沒有提供 `compareFn` ，JavaScript 會把不是 `undefined` 的元素轉成字串後依照 UTF-16 Unicode 編碼**位置**進行比較排序。`undefined` 則會放在陣列的最尾端。

```js
["cherry","banana"].sort() // ["banana","cherry"]
[9, 80].sort() // [80, 9]
[0, -1, -2, 1, 3, 2].sort() // [ -1, -2, 0, 1, 2, 3 ]
```

> 什麼是穩定排序法（Stable Sorting）？
>
> 如果鍵值相同之資料，在排序後**相對位置**與排序前**相同**。

### 原陣列不會被改變

```js
array.concat()             											// 把兩個陣列合併在一起，回傳新陣列
array.findIndex(callbackFn<element, index, array>)	// 回傳"第一個"符合條件的元素 index，找不到則回傳 "-1"
array.find(callbackFn<element, index, array>)			// 回傳"第一個"符合條件的元素，找不到則回傳 "undefined"
array.filter(callbackFn<element, index, array>)		// 回傳符合條件為 true 元素的陣列，若皆無符合則回傳 "[]"（空陣列）
array.map(callbackFn<element, index, array>)				// 回傳每個元素執行 callback 處理結果且長度相等的陣列
array.some(callbackFn<element, index, array>)				// 只要有任一元素符合條件即會回傳 true，否則為 false
array.every(callbackFn<element, index, array>)				// 所有元素皆需符合條件才會回傳 true，否則為 false

// 回傳執行 reducer 運算結果的值
array.reduce(callbackFn<previousValue, currentValue, currentIndex, array>, initialValue)
 
/*
回傳擷取 startIndex 跟 endIndex 之間陣列中的元素（不包含 endIndex）
- 若數值為負數，則從陣列尾端算起
- startIndex 預設為 0，若大於陣列長度則回傳空陣列
- endIndex 預設為陣列長度，若大於陣列長度則會用陣列長度為值
*/
array.slice(startIndex, endIndex)

array.indexOf(searchElement, fromIndex)				// 回傳找到第一個目標元素所在的 index，若找不到則回傳 -1
array.join(separator)               					// 把所有陣列的值以 separator 連接成字串並回傳，預設是","
array.includes(searchElement, fromIndex)			// 檢查 searchElement 有沒有在陣列中，有的話回傳 true，否則為 false
```

----

- [陣列 Array - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10213787)
