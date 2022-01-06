---
title: "[SEO] 如何讓網頁或資源不被搜尋引擎搜尋到（noindex）？"
date: 2021-04-29T08:35:15Z
layout: layouts/post.njk
---

有兩種做法

1. 加 `<meta>` 在 `<head>` 內：僅限 HTML 資源

   ```html
   <!-- 大部分搜尋引擎 -->
   <meta name="robots" content="noindex">
   
   <!-- 指定 Google -->
   <meta name="googlebot" content="noindex">
   ```

   [Read more about the `noindex` meta tag](https://developers.google.com/search/reference/robots_meta_tag#robotsmeta)

2. 加  `X-Robots-Tag` 在 HTTP response header

   - `noindex`：不要在搜尋結果中顯示這個網頁、媒體或資源
   - `nofollow`：不要追蹤這個網頁上的連結。如果未指定這個指令，代表 Google 能追蹤網頁上的連結，找出連結的網頁。進一步瞭解 [`nofollow`](https://developers.google.com/search/docs/advanced/guidelines/qualify-outbound-links)。

   ```tex
   HTTP/1.1 200 OK
   (…)
   X-Robots-Tag: noindex, nofollow
   (…)
   ```

   [Read more about the `noindex` response header](https://developers.google.com/search/reference/robots_meta_tag#xrobotstag).

---

- [Block Search Indexing with 'noindex' | Google Search Central  |  Google Developers](https://developers.google.com/search/docs/advanced/crawling/block-indexing)

