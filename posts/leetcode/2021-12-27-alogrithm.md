---
title: "[DSA] 如何衡量程式（演算法）的好壞？"
date: 2021-12-27T11:35:53+08:00
layout: layouts/post.njk
---

演算法是用來解決問題的數學方法，而同一個問題可以有不同的解決方法，哪個方法好？

評估演算法的效能指標：

### 時間複雜度（Time Complexity）

演算法執行時，所需花費的時間。並不是以秒計算（會因電腦規格與實作方式影響），而是以**執行次數**（運算次數）計算。

### 空間複雜度（Space Complexity）

電腦執行演算法所需要耗費的**記憶體空間**。

在演算法中，我們通常使用時間複雜度與大 O 符號（Big O Notation）來描述一個演算法（函式）的好壞。

## 大 O 符號（Big O Notation）是什麼？

![image-20220109160913656](/img/image-20220109160913656.png)

用來描述一個演算法在**最壞的情況**下（花最多步驟）輸入 n 個資料量完成計算，所需執行次數與 n 的走勢。

<iframe width="560" height="315" src="https://www.youtube.com/embed/g2o22C3CRfU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 常見的時間複雜度

![截圖 2022-01-09 下午4.15.14](/img/%E6%88%AA%E5%9C%96%202022-01-09%20%E4%B8%8B%E5%8D%884.15.14.png)

> 圖片來源：[Big-O Algorithm Complexity Cheat Sheet (Know Thy Complexities!) @ericdrowell](https://www.bigocheatsheet.com/)



### Cheatsheet

| Big O Notation | Name         | Example(s)                                                   |
| -------------- | ------------ | ------------------------------------------------------------ |
| O(1)           | Constant     | # Add element and print the first element from a list<br /># Odd or Even<br /># Look-up Table (on average) |
| O(log n)       | Logarithmic  | # Finding element on sorted array with binary search |
| O(n)       | Linear       | # Find max element in unsorted array<br/># Duplicate elements in array with Hash Map |
| O(n log n)   | Linearithmic | # Sorting elements in array with quicksort |
| O(n^2)  | Quadratic    | # Get the max/min value in an array<br /># Find a given element in a collection<br /># Print all the values in a list |
| O(n^3)   | Cubic        | |
| O(2^n)     | Exponential  | # Power Set: finding all the subsets on a set <br /># Fibonacci<br /># Travelling salesman problem using dynamic programming |
| O(n!) | Factorial | # Find all permutations of a given set/string |

如何衡量函式的時間複雜度？

略過常數

```js
const smallArray = [5, 3, 2, 35, 2];

const bigArray = [5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2, 5, 3, 2, 35, 2];
```

### O(1)

執行時間**不會**隨著資料量增加而增加。

#### Add element and print the first element from a list

```js
const a1 = performance.now();
smallArray.push(27);
console.log(smallArray[0]); // 5
const a2 = performance.now();
console.log(`Time: ${a2 - a1}`); // Less than 1 Millisecond


const b1 = performance.now();
bigArray.push(27);
console.log(bigArray[0]); // 5
const b2 = performance.now();
console.log(`Time: ${b2 - b1}`); // Less than 1 Millisecond
```

#### Odd or Even

```js
function isEvenOrOdd(n) {
  return n % 2 ? 'Odd' : 'Even';
}

console.log(isEvenOrOdd(10)); // Even
console.log(isEvenOrOdd(10001)); // Odd
```

#### Look-up Table

```js
const dictionary = {the: 22038615, be: 12545825, and: 10741073, of: 10343885, a: 10144200, in: 6996437, to: 6332195 /* ... */};

function getWordFrequency(dictionary, word) {
  return dictionary[word];
}

console.log(getWordFrequency(dictionary, 'the')); // 22038615
console.log(getWordFrequency(dictionary, 'in')); // 6996437
```



### O(n)

#### keywords: `一層迴圈`

隨著資料量越多，執行時間等比增加。

```js
const a1 = performance.now();
smArr.forEach(item => console.log(item));
const a2 = performance.now();
console.log(`Time: ${a2 - a1}`); // 3 Milliseconds

const b1 = performance.now();
bigArr.forEach(item => console.log(item));
const b2 = performance.now();
console.log(`Time: ${b2 - b1}`); // 13 Milliseconds
```

#### The largest item on an "unsorted" array

```js
function findMax(n) {
  let max;
  let counter = 0;

  for (let i = 0; i < n.length; i++) {
    counter++;
    if(max === undefined || max < n[i]) {
      max = n[i];
    }
  }

  console.log(`n: ${n.length}, counter: ${counter}`);
  return max;
}

findMax([3, 1, 2]);
// n: 3, counter: 3

findMax([4,5,6,1,9,2,8,3,7])
// n: 9, counter: 9
```

### O(n^2)

#### keywords: `迴圈內有迴圈`

隨著資料量越多，執行時間以指數增加。

```js
const a1 = performance.now();
smArr.forEach(() => {
    arr2.forEach(item => console.log(item));
});
const a2 = performance.now();
console.log(`Time: ${a2 - a1}`); // 8 Milliseconds


const b1 = performance.now();
bigArr.forEach(() => {
    arr2.forEach(item => console.log(item));
});
const b2 = performance.now();
console.log(`Time: ${b2 - b1}`); // 307 Milliseconds
```

#### Check if a collection has duplicated values.

```js
function hasDuplicates(n) {
  const duplicates = [];
  let counter = 0; // debug

  for (let outter = 0; outter < n.length; outter++) {
    for (let inner = 0; inner < n.length; inner++) {
      counter++; // debug

      if(outter === inner) continue;

      if(n[outter] === n[inner]) {
        return true;
      }
    }
  }

  console.log(`n: ${n.length}, counter: ${counter}`); // debug
  return false;
}
```

#### Bubble Sort

```js
function sort(n) {
  for (let outer = 0; outer < n.length; outer++) {
    let outerElement = n[outer];

    for (let inner = outer + 1; inner < n.length; inner++) {
      let innerElement = n[inner];

      if(outerElement > innerElement) {
        // swap
        n[outer] = innerElement;
        n[inner] = outerElement;
        // update references
        outerElement = n[outer];
        innerElement = n[inner];
      }
    }
  }
  return n;
}
```

### O(log n)

通常會是**搜尋**使用的演算法，會先排序後將資料切成對半。

隨著資料量增加，執行時間雖然會增加，但增加率會趨緩。能夠將資料量對半處理的通常都屬於 `O(log n)` 的演算法，因為假設一個函式資料量為 8，執行次數最多為 3 就能計算完成，資料量與執行次數即能透過 `log 8 = 3` 表示其關係。

> 💡  想像你用英文字典找「Notation」這個單字，你不會傻傻地一頁一頁找（O(n)）
>
> 而是會從中間打開，並且找到第一個字；看這個字是在 N 前面還是後面，再往 OPQ（字母的順序 N → O → P → Q）的頁面找，再將剩下的一半對半分，重複剛剛的動作，直到找到符合的字。

#### Binary Search

Find the index of an element in a **sorted** array

```js
function binarySearch(array, targetElement) {
  let low = 0;
  let high = array.length - 1;
  let mid;
  let element;

  while (low <= high) {
    mid = Math.floor((low + high) / 2, 10);
    element = array[mid];
    if (element < targetElement) {
      low = mid + 1;
    } else if (element > targetElement) {
      high = mid - 1;
    } else {
      return mid;
    }
  }
  return -1;
}

console.log(binarySearch(smallArray, 3));
console.log(binarySearch(bigArray, 3));
```

### O(n log(n))

通常是**排序**的操作。

### Quicksort

```js
const quickSort = arr => {
  if (arr.length < 2) return arr;

  let pivot = arr[0];
  let left = [];
  let right = [];

  for (let i = 1, total = arr.length; i < total; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  };
  return [
    ...sort(left),
    pivot,
    ...sort(right)
  ];
};

quickSort(smallArray); // 0 Milliseconds
quickSort(bigArray); // 1 Millisecond
```



### O(2^n)

隨著資料量增加，執行時間每次都會加倍。

### Power Set

想像你去一家披薩店，提供了多種配料：蘑菇、鳳梨、香腸、培根。你有可能什麼都不選，或者選了一種、兩種、三種或是全部都選。

Power Set 則給你所有可能性。

```js
function powerset(n = '') {
  const array = Array.from(n);
  const base = [''];

  const results = array.reduce((previous, element) => {
    const previousPlusElement = previous.map(el => {
      return `${el}${element}`;
    });
    return previous.concat(previousPlusElement);
  }, base);

  return results;
}
```



```js
powerset('') // ...
// n = 0, f(n) = 1;
powerset('a') // , a...
// n = 1, f(n) = 2;
powerset('ab') // , a, b, ab...
// n = 2, f(n) = 4;
powerset('abc') // , a, b, ab, c, ac, bc, abc...
// n = 3, f(n) = 8;
powerset('abcd') // , a, b, ab, c, ac, bc, abc, d, ad, bd, abd, cd, acd, bcd...
// n = 4, f(n) = 16;
powerset('abcde') // , a, b, ab, c, ac, bc, abc, d, ad, bd, abd, cd, acd, bcd...
// n = 5, f(n) = 32;
```



### O(n!)

每個元素都再跑一次迴圈

> Factorial: `5! = 5x4x3x2x1 = 120`

```js
const factorial = n => {
  let num = n;

  if (n === 0) return 1
  for (let i = 0; i < n; i++) {
    num = n * factorial(n - 1);
  };

  return num;
};

factorial(1); // 2 Milliseconds
factorial(5); // 3 Milliseconds
factorial(10); // 85 Milliseconds
factorial(12); //  11,942 Milliseconds
```

#### Permutations 排列組合

```js
function getPermutations(string, prefix = '') {
  if(string.length <= 1) {
    return [prefix + string];
  }

  return Array.from(string).reduce((result, char, index) => {
    const reminder = string.slice(0, index) + string.slice(index+1);
    result = result.concat(getPermutations(reminder, prefix + char));
    return result;
  }, []);
}
```

```js
getPermutations('ab') // ab, ba...
// n = 2, f(n) = 2;
getPermutations('abc') // abc, acb, bac, bca, cab, cba...
// n = 3, f(n) = 6;
getPermutations('abcd') // abcd, abdc, acbd, acdb, adbc, adcb, bacd...
// n = 4, f(n) = 24;
getPermutations('abcde') // abcde, abced, abdce, abdec, abecd, abedc, acbde...
// n = 5, f(n) = 120;
```



---

- https://ithelp.ithome.com.tw/articles/10213206
- https://pjchender.blogspot.com/2017/09/big-o-notation-time-complexity.html
- https://web.ntnu.edu.tw/~algo/
- https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course