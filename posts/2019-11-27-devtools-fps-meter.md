---
title: "[JS] textarea 限制每行輸入字元數與總行數上限"
date: 2019-11-27T13:50:08Z
layout: layouts/post.njk
---

- 一行不能超過指定字元數
- 已輸入三行後不能新增第四行

```js
function getOverflowIndex(string, maxDigit){
    let digitCounter = 0;

    for (let index = 0; index < string.length; index++) {
      // 若是超過則回傳溢出的 index 好作字串 substring 的依據
      if (digitCounter >= maxDigit) return index;

      // 一個全形字的字元為 2 
      const isFullWidth = string.charCodeAt(index) > 255;
      digitCounter += isFullWidth ? 2 : 1;
    }

    return digitCounter;
}

/**
 * @param string 文字輸入值
 * @param maxLines 總行數上限
 * @param maxDigitPerLine 每行字元數上限
 * @returns 
 */
function trimTextarea(string, maxLines, maxDigitPerLine) {
  // 用換行符號切成以行為單位的 Array，並把
  const lines = string.split("\n").slice(0, maxLines);
  
  return lines
    .map((line) => line.substring(0, getOverflowIndex(line, maxDigitPerLine)))
    .join("\n");
}

```

