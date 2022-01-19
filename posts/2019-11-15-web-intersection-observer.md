---
title: "[Web] Intersection Observer API"
date: 2022-01-19T16:35:17+08:00
layout: layouts/post.njk
draft: true
---

## 應用

- Lazy Loading：當圖片被使用者看到才載入
- Infinite Scrolling：當使用者滾動至接近內容底部時自動載入更多內容
- Parallax Scrolling
- 廣告的曝光情形
- 在使用者看見某個區域／元素時執行任務或播放動畫（ScrollMagic）

## 概念說明

```js
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0
}

let callback =(entries, observer) => {
  entries.forEach(entry => {
    // Each entry describes an intersection change for one observed target element:
    // entry.boundingClientRect
    // entry.intersectionRatio
    // entry.intersectionRect
    // entry.isIntersecting
    // entry.rootBounds
    // entry.target
    // entry.time
  });
};

let observer = new IntersectionObserver(callback, options);

let target = document.querySelector('#listItem');
observer.observe(target);
```

- 要監控的元素 `target`（目標）
- 要比較的元素 `root`（根）
- 目標與根元素交會觸發 `callback`

`callback` 

- `entries` 是 `IntersectionObserverEntry` 陣列
  - `IntersectionObserverEntry.isIntersecting` 進入視窗時都會觸發的

`options` 參數

- `root`：默認為瀏覽器視窗
- `rootMargin`：root 元素的外邊距，類似 CSS 中的 margin 屬性
- `threshold`
  - 預設為 0，意指目標元素只要有一個像素出現在 root 元素即會觸發 callback
  - 若為 1.0，意指目標元素要完全出現在 root 元素才會觸發 callback

---

- [Intersection Observer API - Web API 接口参考 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Intersection_Observer_API)
- [[WebAPIs] Intersection Observer API | PJCHENder 未整理筆記](https://pjchender.dev/webapis/webapis-intersection-observer/)