---
title: "[CSS] Grid/Flex 1fr 爆版問題與解決方式"
layout: layouts/post.njk
draft: true

---

## flexbox & "min-width"

https://makandracards.com/makandra/66994-css-flex-and-min-width

### `min-width` in `flex` context

預設 `min-width` 是 `0`，而 flex 則被設為 `min-width: auto`

min-width is defined to win against competing width and max-width



```css
grid-template-columns: 1fr;
grid-template-columns: 100%;
```







https://css-tricks.com/preventing-a-grid-blowout/

https://css-tricks.com/introduction-fr-css-unit/

如果你祖父層希望`width:88vw`，
父層用`1fr`排版的話（例如`*grid-template-columns*``: 1fr 22.5rem`），
子層(左邊內容)如果超過寬度，有時會造成不可控的寬度(如總共超過祖父層的`88vw` )

文章說這是因為1fr 預設最小寬度為auto

因為 .root 已經有用 grid-template-columns 鎖寬度和 height 鎖高度了，這邊可以不用再鎖一次

圖片會長超過區塊是因為他是 grid 的 child，grid/flex 的 child min-height/min-width 被設成 auto，所以會長出去，可以設定 min-height/min-width 來避免這種狀況
https://stackoverflow.com/a/41675912

flex 也會遇到這種問題，我之前都是用 min-width: 0 解決



QA 有時會測很長不分開的英文字串，如果這個字串的 element 是 grid/flex child，就可能會爆版，例如

```
lasjfdklasjdflaksdjflkasjdflkasjdflkaf
```

我遇到的情況則是跟 1 fr 比較相關的問題，
當 grid 內容越來越長的時候，如果只有寫 1fr ，有可能原本平均的寬度會跑掉，所以我後來也是用 minmax 解決。

https://stackoverflow.com/questions/47601564/equal-width-columns-in-css-grid

https://codepen.io/joakimc/pen/ZEbgVLZ



讚讚，這感覺可以理解，也是跟default `min-width: auto`有關。
下面沒有設定`min-width`的情況就會超過父層的寬度 (就是我遇到的情況，雖然這裡的情況 `overflow:hidden`可以解決 :smile: )
https://codepen.io/Aerobic/pen/bGROWXp 