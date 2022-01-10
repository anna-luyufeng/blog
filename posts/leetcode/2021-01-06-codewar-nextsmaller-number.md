---
title: ""
date: 2022-01-10T17:41:34+08:00
layout: layouts/post.njk
draft: true
---

https://www.codewars.com/kata/5659c6d896bc135c4c00021e/train/javascript

```js
function nextSmaller(n) {
  let res = -1;

  const traverse = (strNum, curStrNum) => {
    if (curStrNum[0] === "0") {
      return;
    }

    if (!strNum) {
      const num = +curStrNum;
      if (num < n) {
        res = num;
      }
      return;
    }

    for (let i = 0; i < strNum.length; i++) {
      const nextNum = +(curStrNum + strNum[i]);

      if (res > -1 && nextNum < +String(res).slice(0, curStrNum.length + 1)) {
        continue;
      }

      if (nextNum > +String(n).slice(0, curStrNum.length + 1)) {
        continue;
      }

      traverse(
        `${strNum.slice(0, i)}${strNum.slice(i + 1)}`,
        curStrNum + strNum[i]
      );
    }
  };

  traverse(String(n), "");

  return res;
}
```



907 為例，跑的過程是這樣

```
// 左邊是還有哪些數字要組 (strNum)，右邊是目前已經組進去的數字 (curStrNum)
// 起始 traverse 參數
"907", ""
  // traverse 第一層 for i = 0
  "07", "9"
    // traverse 第二層 for i = 0
    "7", "90"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "907"
    // traverse 第二層 for i = 1
    "0", "97"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "970"

  // traverse 第一層 for i = 1
  "97", "0"
    // traverse 第二層 for i = 0
    "7", "09"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "097"
    // traverse 第二層 for i = 1
    "9", "07"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "079"

  // traverse 第一層 for i = 2
  "90", "7"
    // traverse 第二層 for i = 0
    "0", "79"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "790"
    // traverse 第二層 for i = 1
    "9", "70"
      // traverse 第三層 for i = 0, strNum 沒東西要組了，檢查這個數字符不符合條件
      "", "709"
```

以 input `1234567908` 來看

1. 第一個回圈先找到最後一個大於後面的數字的位置`i1`，會找到`9` （因為只是要找小於給的數字的第一個數字）
2. 跑第二個回圈去換位置，然後break，會變成`1234567809`
3. 最後從`i1`位置切成前面跟後面，再將後面順序確保大到小，確保找到的是下一個較小的數字，會變成`12345678` +`90`
4. flag的作用就是用來判斷是否其實根本沒辦法換，已經是最小

```js
function nextSmaller(n) {
  let digitList = n.toString().split(''); 
  let i1 = 0;     
  let tmp;      
  let flag = false;   
  for (let i = 0; i < digitList.length - 1; i++) {
    if (digitList[i] > digitList[i + 1]) {
      i1 = i;
      flag = true;
    }
  }
  if (flag == false) return -1;
  for (let i = digitList.length - 1; i > 0; i--) {
    if (i === i1) i--;
    if (digitList[i] < digitList[i1]) {
      tmp = digitList[i];
      digitList[i] = digitList[i1];
      digitList[i1] = tmp;
      break;
    }
  }
  if (parseInt(digitList[0]) === 0) return -1
  return parseInt(digitList.slice(0, i1 + 1).concat(digitList.slice(i1 + 1).sort((a, b) => b - a)).join(''))
}


```

