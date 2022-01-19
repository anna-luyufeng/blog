---
title: "[JS] Debounce 與 Throttle 差別與應用情境"
date: 2019-11-20T07:32:01Z
layout: layouts/post.njk
---

## Debounce 防抖

強制自上次調用後經過一定時間才會再次調用函數，例如只有在沒有被調用的情況下經過一段時間之後（例如 100 毫秒）才執行該函數。
設定一個 timeout，例如輸入後過兩秒才去抓一次使用者輸入的值。

```js
function debounce(func, delay) {
  // timeout 初始值
  let timeout = null;
  return function () {
    let context = this; // 指向 myDebounce 這個 input
    let args = arguments; // KeyboardEvent
    clearTimeout(timeout);

    timeout = setTimeout(function () {
      func.apply(context, args);
    }, delay);
  };
}
debounce(function (e) {
  console.log(e.target.value);
}, 2000);
```

## Throttle 節流

強制一個函數在一段時間內可調用的最大次數，例如每 100 毫秒最多執行一次函數。
防止一下太頻繁輸入值，所以限制一個時間，在這個時間內觸發的值會被存到下一次再存。

```js
function throttle(func, delay) {
  let inThrottle;
  let timeout = null;
  return function () {
    let context = this;
    let args = arguments;
    if (!inThrottle) {
      // 輸入之後兩秒內都不會再進入這邊
      func.apply(context, args);
      inThrottle = true;
      clearTimeout(timeout);
      timeout = setTimeout(function () {
        inThrottle = false;
      }, delay);
    }
  };
}
throttle(function (e) {
  console.log(e.target.value);
}, 2000);
```





## 情境

- automcomplete
- window resize & scroll event listening

---

- 圖像化 Throttle、Debounce與默認情況的事件監聽：http://demo.nimius.net/debounce_throttle/
- [[有趣面試題] 網頁效能問題改善之 Debounce & Throttle](https://ithelp.ithome.com.tw/articles/10222749)