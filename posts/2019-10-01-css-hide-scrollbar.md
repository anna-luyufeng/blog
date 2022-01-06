---
title: "[CSS] scroll/scrollbar 滑動與捲軸"
date: 2021-12-30T18:42:07+08:00
layout: layouts/post.njk

---

### 滑順地移動至指定位置

```css
/* 有捲軸的地方 */
html {
		scroll-behavior: smooth;
}
```

> [scroll-behavior - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior)

### 避免 Anchor Scroll 選單遮住區塊標題：調整與 Scroll Snap Area 的間距

<!-- scroll snap area 是什麼？實際的定義是什麼？scroll-padding 跟 scroll-margin 的差別 -->

<!-- https://pjchender.dev/css/css-scroll/#%E8%AA%BF%E6%95%B4%E6%8D%B2%E5%8B%95%E5%88%B0%E7%9A%84%E9%82%8A%E8%B7%9Dscroll-padding -->

```css
article * {
  scroll-margin-top: 56px; /* 選單高度 */
}
```

> scroll-margin-top - CSS: Cascading Style Sheets | MDN

### 隱藏 Scrollbar

```css
/* Chrome, Safari and Opera */
::-webkit-scrollbar {
  display: none;
}
-ms-overflow-style: none; /* IE and Edge */
scrollbar-width: none; /* Firefox */
```

### <!--修改 Scrollbar 的樣式-->