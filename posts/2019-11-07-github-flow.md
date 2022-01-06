---
title: "[Note] GitHub Flow 開發流程與版本控制"
date: 2019-11-07T08:42:34Z
layout: layouts/post.njk
draft: true
---

<!-- https://github.com/SnapaskProduct/web-wiki/wiki/Release-Automation-Proposal

https://github.com/SnapaskProduct/web-wiki/blob/master/guides/workflow.md -->

## [GitHub Flow](https://guides.github.com/introduction/flow/)

### 原則
- 開發都從 master branch 開分支
- 隨時都可以發 pull request
- review 過的 pull request 才可以 merge
- 隨時都可以發佈新版本

### Branch
- 開發都從 master 開分支 branch 出去
- BRANCH_NAME 命名請具有**描述性**（如 refactor-authentication、user-content-cache-key 或是 make-retina-avatars），讓其他人清楚知道分支正在進行的工作項目。

```shell
git branch [BRANCH_NAME]
git checkout -b [BRANCH_NAME]
```

### Commit 
- 遵循 [Conventional Commit](https://www.conventionalcommits.org/zh-tw/v1.0.0-beta.4/)
-  [commitlint bot](https://github.com/z0al/commitlint-bot)（待研究）

```
type(scope?): subject
body?
footer?

範例：
feat(component): add brand button
```

- type 種類
    - Bug Fixes：type 為 fix，屬於「修復問題」（＝SemVer PATCH）
    - New Features：type 為 feat，屬於「新增功能」（＝SemVer MINOR）
    - BREAKING CHANGES：當 body 或 footer 的開頭出現有 BREAKING CHANGE 這個關鍵字，屬於「會讓舊版程式無法運行的更新」（＝SemVer MAJOR）。一個 breaking change 的 type 只能是 fix、feat 或 chore。
    - 其他：除 fix: 與 feat: 以外，其他的提交 類型 也是被允許的，例如 [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) ([基於 Angular 慣例](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)) 中推薦的 chore:、docs:、style:、refactor:、perf:、test: 以及更多。


> Ｑ：為什麼要這麼麻煩？ <br>
> Ａ：為了之後版本上線以及 Changelog 能自動化處理（參考：[如何自動化 GitHub Releases 流程](https://tech.hahow.in/%E5%A6%82%E4%BD%95%E8%87%AA%E5%8B%95%E5%8C%96-github-releases-%E6%B5%81%E7%A8%8B-6e7e33b61169)）


## 版本變更（待研究補充完善）
### 變更規則 Semantic Version


### 如何變更版本編號 NPM Version？
```bash
npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease | from-git]
```
- Semantic Version
- 如何使用 Git 更新 NPM Version

### GitHub Release（Git Tag）（待研究補充完善）
- push 或 merge master 當下就應該要馬上 release Git tag
- 自動化產生 Changelog

