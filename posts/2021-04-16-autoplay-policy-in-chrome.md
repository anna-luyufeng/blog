---
title: "[Chrome] 如何在網頁上自動播放影片？"
date: 2022-01-20T18:51:35+08:00
layout: layouts/post.njk
draft: true
---

你有一進到網站就被自動播放的音樂／影片聲音嚇到~~然後立刻把網頁關掉~~的經驗嗎？

這樣的使用者體驗真的很差，因此 Chrome 只讓在符合某些條件下，才能自動播放音樂與影片。

- 靜音的自動播放
- 有聲音的自動播放
  - 使用者有與網域互動過（點擊）
  - 在桌機上， Media Engagement Index (MEI)  chrome://media-engagement 使用者有在該網域有聲地播影片

https://vimeo.zendesk.com/hc/en-us/articles/115004485728-Autoplaying-and-looping-embedded-videos

> Both of these parameters will force your video to load as muted in all browsers. Videos without audio tracks (or audio tracks without sound) will not be considered muted by browsers. In order to bypass autoplay restrictions, you must use one of the embed parameters above.

https://developer.chrome.com/blog/autoplay