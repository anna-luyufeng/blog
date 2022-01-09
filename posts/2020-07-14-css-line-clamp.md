---
title: "[CSS] 限制文字段落行數"
date: 2022-01-05T18:35:54+08:00
layout: layouts/post.njk
draft: true
---

```
-webkit-box-orient: vertical; // postcss/autoprefixer  有可能會丟失
```

https://github.com/NervJS/taro/issues/3399

````scss

@mixin lineClamp($number: null) {
  @if $number == 1 {
    display: block;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  } @else {
    display: -webkit-box;
    overflow: hidden;
    -webkit-line-clamp: $number; // if $number is 0, means no line clamp
    /*! autoprefixer: off */
    -webkit-box-orient: vertical;
  }
}

@mixin lineClamp($maxLineNumber, $fontSize: 1rem, $fixedHeight: false) {
  $maxHeight: calc(#{$maxLineNumber} * var(--line-height--base) * #{$fontSize});
  $heightProperty: if($fixedHeight, 'height', 'max-height');

  overflow: hidden;
  #{$heightProperty}: $maxHeight;

  // for webkit better experience (showing "..." at the end)
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: $maxLineNumber;
}
````

```js
/**
 * this is workaround for line-clamp css feature
 * due to autoprefixer version used in Lemon doesn't support
 * please use this function as inline style,   i,e, style={{ ...lineClamp($lineCount)}}
 * ref: https://github.com/postcss/autoprefixer/issues/1220
 *      https://github.com/postcss/autoprefixer/commit/69ed8a0d35cd3d8445c1a713f63ccfc32db29bb9
 * @param {number} lineCount
 */
export default function lineClamp(lineCount = 3) {
  return {
    overflow: 'hidden',
    display: '-webkit-box',
    WebkitLineClamp: lineCount,
    WebkitBoxOrient: 'vertical',
  };
}

```

