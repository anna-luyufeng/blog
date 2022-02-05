---
title: "[HTML5] Responsive Images <img>"
date: 2022-01-20T09:22:48+08:00
layout: layouts/post.njk
---

`<picture>` vs `<img>`？

- picture 根據不同裝置顯示不同張內容圖片
- img 相同圖片不同解析度或不同尺寸



## 處理圖片大小

- [sharp npm package](https://www.npmjs.com/package/sharp)
- [ImageMagick CLI 工具](https://www.imagemagick.org/script/index.php)

## 提供多個圖片版本

```html
<img src="flower-large.jpg" srcset="flower-small.jpg 480w, flower-large.jpg 1080w" sizes="50vw">
```

### "src"

- 當瀏覽器不支援 `srcset` 和 `sizes` 時會使用這個屬性
- 因此圖檔需要夠大這樣不同裝置尺寸都清晰顯示

### "srcset"

- `480w` 為圖片的實際寬度，用來表示圖片為 480 像素寬。讓瀏覽器知道圖片的寬度，不需要下載圖片才能確定其大小

### "sizes"

告訴瀏覽器圖片顯示時的寬度

若已使用 `max-width: 100%` 可省略 sizes 讓瀏覽器自己判斷

---

https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images

https://web.dev/i18n/zh/serve-responsive-images/#

https://pjchender.dev/html/html-picture-srcset/