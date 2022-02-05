---
title: "[Note] 將多個 Repository 透過 Lerna 整成 Monorepo 艱辛之旅"
date: 2022-01-10T18:37:42+08:00
layout: layouts/post.njk
draft: true
---

## 挑戰

- 各個專案的 Node 版本不一致：目標升到  `16.13.0`
- 舊架構的專案 Webpack 版本只有 3

## 遇到的問題紀錄

### 將 Node 版本升到 16.13.0

- 在根目錄新增 `.nvmrc` 鎖定 NodeJS 的版本
- 根目錄下 `yarn install`

```bash
error /Users/anna-luyufeng/Documents/snapask-lerna/packages/Kiwi/node_modules/node-sass, /Users/anna-luyufeng/Documents/snapask-lerna/packages/Lemon/node_modules/node-sass: Command failed.
```

=> `node-sass` 版本過舊，要升級到 `6.0.1` 版本（how to know？）

=> 或是改用 sass (dart sass)？

https://github.com/SnapaskProduct/DragonFruit/pull/2004

https://github.com/SnapaskProduct/Snapask-Official-Site/pull/487

```bash
[1] fs.js:47
[1] } = primordials;
[1]     ^
[1] 
[1] ReferenceError: primordials is not defined
```

=> build:i18n 出錯，改用 Shell Script，替換掉 `better-npm-run` 可參考 https://github.com/SnapaskProduct/Blueberry/pull/638

=> dotenv 設定有誤，但應該不影響

```bash
import CloudOne from './images/img_commonbg_cloud01.svg';

[1] ReferenceError: React is not defined
```

=> 無法把 svg 當作 React Component？

=> `webpack-assets.json` 內容短少（assets 沒有被正常處理）

- [webpack-isomorphic-tools](https://www.npmjs.com/package/webpack-isomorphic-tools) 用 [svg-react-loader](https://www.npmjs.com/package/svg-react-loader) 處理

<!--node v16 不會安裝 react-router 但 node v10 會，所以要自己在 package.json 加入 dependency-->

<!--又是 node-sass 的問題：Error: Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (93)-->

<!--說明一下脈絡，我升級了 style 相關的套件 例如 node-sass style-loader postcss-loader 之類的，編譯的時候會發生 this.getOptions not function 的錯誤，最後在 style-loader 的 peer dependencies 發現 webpack ^v5-->

````
 (node:73284) DeprecationWarning: loaderUtils.parseQuery() received a non-string value which can be problematic, see https://github.com/webpack/loader-utils/issues/56
[0] parseQuery() will be replaced with getOptions() in the next major version of loader-utils.
[0] (Use `node --trace-deprecation ...` to show where the warning was created)
````

## 把舊專案放進 Repo 內步驟

```bash
# 把專案改進來
lerna import 

# 改 pacakge.json 的 name


# 加根目錄 scripts
# @owo/dragonfruit 對應專案底下 package.json 的 name
{
	"scripts": {
    "start-kiwi": "yarn workspace @owo/kiwi start",
    "start-dragonfruit": "yarn workspace @owo/dragonfruit start"
  }
}
```



## Lerna

### 初始化

```bash
# 建立新的 lerna 專案或者升級舊的 lerna 專案
# 此指令是假設此目錄已是 git repo
lerna init
# => 會新增 lerna 在 package.json 的 devDependencies 裡
# => 若是沒有 package.json 會幫你建一個
# https://github.com/lerna/lerna/tree/main/commands/init#readme
```

### 安裝／刪除套件

單個 package workspace

```bash
yarn workspce packageA add axios
yarn workspace packageA remove axios
```

packageA 是需要安裝套件的 package 名稱，即 `package.json` 中的 `name` 字段，非目錄名。

root package

```bash
# root package 安装 commitizen
yarn add -W -D commitizen

# root package 移除 commitizen
yarn remove -W commitizen
```



### 改用 yarn （預設為 npm）

```json
// lerna.json
{
  ...
	"npmClient": "yarn",
  ...
}
```

### 匯入現有的 Repository，包含所有 commit 紀錄

```bash
# pathToRepo 為本機的絕對位置 ~/ = Users/YOUR-USERNAME
lerna import <pathToRepo>
#  輸入後會詢問是否確定將 commits 紀錄匯入到當前的 git branch，如果答 no 不會繼續動作。匯入時會將目標 repo 當前的 git branch 灌進 lerna repo 當前的 git branch，所以匯入之前記得 git pull 一下 target repo。 
```

https://github.com/lerna/lerna/blob/main/commands/import/README.md

### 將所有 packages link 在一起，並安裝對應的 dependencies

Enables integration with [Yarn Workspaces](https://github.com/yarnpkg/rfcs/blob/master/implemented/0000-workspaces-install-phase-1.md) (available since yarn@0.27+). The values in the array are the commands in which Lerna will delegate operation to Yarn (currently only bootstrapping). If `--use-workspaces` is true then `packages` will be overridden by the value from `package.json/workspaces.` May also be configured in `lerna.json`:

Ref: https://github.com/lerna/lerna/tree/main/commands/bootstrap#readme 

```bash
lerna bootstrap
# 將工作完全委派給 yarn
lerna bootstrap -use-workspaces 
```

```json
// lerna.json
{
  ...
	"useWorkspaces": true,
  ...
}
```



### SCC share components

[1Writing your first React UI Library - Part 1: Lerna](https://dev.to/davixyz/writing-your-first-react-ui-library-part-1-lerna-17kc)

[A step-by-step guide to building a shareable components library](https://www.devbridge.com/articles/a-step-by-step-build-to-build-a-sharable-components-library/)

https://www.velotio.com/engineering-blog/scalable-front-end-with-lerna-yarn-react

### 替換 babel

https://github.com/SnapaskProduct/Kiwi/pull/341

```bash
yarn remove babel-core
yarn remove babel-preset-env
yarn remove babel-preset-react

yarn upgrade babel-loader
yarn upgrade babel-jest

yarn upgrade @babel/core@^7.15.5
yarn upgrade @babel/preset-react@^7.14.5
yarn upgrade eslint-plugin-react@^7.26.1

babel-plugin-dynamic-import-node # https://www.npmjs.com/package/babel-plugin-dynamic-import-node
Babel plugin to transpile import() to a deferred require(), for node. Matches the proposed spec.
```

babel-polyfill

### 

為什麼 `webpack.config.js` 要設定 babel 也同時也有 `babel.config.js`？

Babel 6 -> 7

https://medium.com/@maicmi/babel-upgrade-from-babel-6-x-to-7-0-58809bd63d8

----

[结合 lerna 和 yarn workspace 管理多项目工作流](https://segmentfault.com/a/1190000025173538)

[[guide] Monorepo with React and TS](https://pjchender.dev/react/guide-mono-react-ts-template/)