---
title: "[SEO] 為什麼台灣的使用者會搜尋到英文版網站？"
date: 2022-01-04T21:19:22+08:00
layout: layouts/post.njk
---

## 針對不同地區或語言使用不同網址

- 國家／地區專屬網域（ccTLD）：`example.de`
- 有 gTLD 的子網域：`de.example.com`
- 有 gTLD 的子目錄：`example.com/de/`

> ccTLD：一般國家/地區代碼頂層網域
> gTLD：一般頂層網域（.com/.org/.edu/.gov）

## 使用 hreflang 指明網頁的替代語言版本

- 讓 Google 搜尋結果可以根據語言或地區將使用者導向最適當的版本
- 若是沒有明確指定其替代語言或地區，Google 有可能會將其視為[重複網頁](https://developers.google.com/search/docs/advanced/crawling/consolidate-duplicate-urls)

有三種方法

- [HTML](#方法一：html)
- [HTTP Response Header](#方法二：http)
- [Sitemap](#方法三：sitemap)

### 不論使用哪種方法都需要

- 必須列出本身**以及所有其他**語言版本
- 替代網址必須是完整的網址：包含 http/https，如 `https://example.com/foo`
- 替代網址不一定要相同網域
- 如果有相同語言但不同地區，建議同時提供一個總括性的語言網址
  - 例如有 `en-ie`、`en-ca`、`en-au`，提供 `en` 給其他同樣英語系地區的搜尋者使用
- 不同語言的網頁間需建立**雙向**連結
  - 如果網頁 X 連結至網頁 Y，網頁 Y 也必須連結回網頁 X
  - 如果任何一個使用 `hreflang` 註解的網頁缺少傳回連結，則可能導致系統忽略所有註解，或無法正確解讀註解
- 新增的語言務必與現有／主要的語言建立雙向連結
- 當沒有匹配使用者瀏覽器所設定的語言／地區的網頁版本，會導向  `hreflang="x-default"` 所設定通用首頁

### 方法一：HTML

```html
<head>
  <!-- 盡可能靠近 <head> 以避免被其他元素中斷 Google 爬取網頁資訊 -->
	<link rel="alternate" hreflang="lang_code" href="url_of_page" />
</head>
```

- lang_code：此網頁版本鎖定的[支援語言/地區代碼](#支援語言%2F地區代碼)，或使用 `x-default` 比對網頁上 `hreflang` 標記未明確列出的任何語言
- url_of_page：此網頁專屬語言/地區版本的**完整網址**

範例：

```html
<head>
    <title>Widgets, Inc</title>
    <link rel="alternate" hreflang="en-gb" href="https://en-gb.example.com/page.html" />
    <link rel="alternate" hreflang="en-us" href="https://en-us.example.com/page.html" />
    <link rel="alternate" hreflang="en" href="https://en.example.com/page.html" />
    <link rel="alternate" hreflang="de" href="https://de.example.com/page.html" />
    <link rel="alternate" hreflang="x-default" href="https://www.example.com/" />
</head>
```



### 方法二：HTTP

適用於非 HTML 檔案（如 PDF）

```nginx
Link: <url1>; rel="alternate"; hreflang="lang_code_1", <url2>; rel="alternate"; hreflang="lang_code_2", ...
```

範例：

```nginx
Link: <https://example.com/file.pdf>; rel="alternate"; hreflang="en",
      <https://de-ch.example.com/file.pdf>; rel="alternate"; hreflang="de-ch",
      <https://de.example.com/file.pdf>; rel="alternate"; hreflang="de"
```



### 方法三：Sitemap

- 每個語言版本網址都要一組 `<url>` 元素
- 每個 `<url>` 都須包含子元素 `<loc>` 對應網頁網址
- 每個 `<url>` 都須包含子元素 `<xhtml:link rel="alternate" hreflang="supported_language-code">`，包含網頁本身在內的每個替代網頁版本

範例：

- `www.example.com/english/page.html` ：英文使用者
- `www.example.com/deutsch/page.html`：德文使用者
- `www.example.com/schweiz-deutsch/page.html`：瑞士地區的德文使用者

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
    xmlns:xhtml="http://www.w3.org/1999/xhtml">
    <url>
        <loc>https://www.example.com/english/page.html</loc>
        <xhtml:link rel="alternate" hreflang="de" href="https://www.example.com/deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="de-ch" href="https://www.example.com/schweiz-deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="en" href="https://www.example.com/english/page.html"/>
    </url>
    <url>
        <loc>https://www.example.com/deutsch/page.html</loc>
        <xhtml:link rel="alternate" hreflang="de" href="https://www.example.com/deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="de-ch" href="https://www.example.com/schweiz-deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="en" href="https://www.example.com/english/page.html"/>
    </url>
    <url>
        <loc>https://www.example.com/schweiz-deutsch/page.html</loc>
        <xhtml:link rel="alternate" hreflang="de" href="https://www.example.com/deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="de-ch" href="https://www.example.com/schweiz-deutsch/page.html"/>
        <xhtml:link rel="alternate" hreflang="en" href="https://www.example.com/english/page.html"/>
    </url>
</urlset>
```

## 支援語言/地區代碼

- `hreflang` 的值可以是語言代碼（採 [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式）或是地區代碼（採 [ISO 3166-1 Alpha 2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式）
- 語言不一定要與地區相對應：如 `de-ES` 對西班牙地區使用者顯示的德文內容
- **勿單獨指定國家／地區代碼**：如 `tw`，Google 並不會根據國家／地區代碼自動推測網頁的語言
- 同種語言不同文字版本，系統會根據國家／地區自動判斷正確的文字版本
  - 台灣的使用者 `zh-TW` 會自動判斷相應的語言文字版本為繁體中文
  - 也可以用 [ISO 15924](https://unicode.org/iso15924/iso15924-codes.html) 格式指定文字版本
  - 或組合文字版本與地區 `zh-Hans-TW` 對台灣使用者指定簡體中文

### 針對不相符的語言使用 `x-default` 標記

如果沒有其他語言/地區符合使用者的瀏覽器設定，保留 `hreflang="x-default"` 值就會派上用場。可以在沒有相符語言時控制網頁，讓使用者自行選擇所在的國家/地區。

無須為 `x-default` 值指定語言代碼；網頁鎖定的是**瀏覽器設定語言**與您網站不同的使用者，與網頁本身的語言無關。

```html
<link rel="alternate" href="https://example.com/" hreflang="x-default" />
```



---

- [多地區和多語言版本的網站 | Google 搜尋中心  |  Google Developers](https://developers.google.com/search/docs/advanced/crawling/managing-multi-regional-sites)
- [網頁本地化版本 | Google 搜尋中心  |  Google Developers](https://developers.google.com/search/docs/advanced/crawling/localized-versions)