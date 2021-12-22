---
title: "[Note] Yarn 與 npm 指令對應"
date: 2021-12-15T01:03:19+08:00
layout: layouts/post.njk
---

> Yarn 2.x? https://yarnpkg.com/getting-started/migration 

### CLI commands comparison

| npm (v5)                                | Yarn (1.x)                                 |
| --------------------------------------- | ------------------------------------------ |
| `npm install`                           | `yarn`<br />`yarn --force`<br />`yarn add` |
| **_(N/A)_**                             | `yarn add --flat`                          |
| **_(N/A)_**                             | `yarn add --har`                           |
| `npm install --no-package-lock`         | `yarn add --no-lockfile`                   |
| **_(N/A)_**                             | `yarn add --pure-lockfile`                 |
| `npm install [package] --save`          | `yarn add [package]`                       |
| `npm install [package] --save-dev`      | `yarn add [package] --dev`                 |
| **_(N/A)_**                             | `yarn add [package] --peer`                |
| `npm install [package] --save-optional` | `yarn add [package] --optional`            |
| `npm install [package] --save-exact`    | `yarn add [package] --exact`               |
| **_(N/A)_**                             | `yarn add [package] --tilde`               |
| `npm install [package] --global`        | `yarn global add [package]`                |
| `npm update --global`                   | `yarn global upgrade`                      |
| `npm rebuild`                           | `yarn add --force`                         |
| `npm uninstall [package]`               | `yarn remove [package]`                    |
| `npm cache clean`                       | `yarn cache clean [package]`               |
| `rm -rf node_modules && npm install`    | `yarn upgrade`                             |
| `npm version major`                     | `yarn version --major`                     |
| `npm version minor`                     | `yarn version --minor`                     |
| `npm version patch`                     | `yarn version --patch`                     |



> https://classic.yarnpkg.com/en/docs/migrating-from-npm @Yarn



