---
title: "[CSS] 避免在行動版網頁使用 100vh"
date: 2022-01-20T09:56:01+08:00
layout: layouts/post.njk
draft: true
---

`vh` 並不會計算到行動裝置瀏覽器上方的網址列的高度。

## JS "window.innerHeight"

```js
document.documentElement.style.setProperty('--vh', `${window.innerHeight/100}px`);
```

### CSS

```css
.fullheight {
    height: calc(var(--vh, 1vh) * 100);
}
```

### SCSS

```scss
@function vh($quantity) {
    @return calc(var(--vh, 1vh) * #{$quantity});
}

.fullheight {
    height: vh(100);
}
```



## CSS "-webkit-fill-available"

```css
body {
  min-height: 100vh;
  min-height: -webkit-fill-available;
}
html {
  height: -webkit-fill-available;
}
```



---

[Avoid 100vh On Mobile Web | chanind.github.io](https://chanind.github.io/javascript/2019/09/28/avoid-100vh-on-mobile-web.html)

[CSS fix for 100vh in mobile WebKit](https://css-tricks.com/css-fix-for-100vh-in-mobile-webkit/)