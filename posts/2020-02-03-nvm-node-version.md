---
title: "[Node] nvm 切換 node 版本"
date: 2022-01-20T08:49:54+08:00
layout: layouts/post.njk
---

使用 nvm 做 node 版本切換管理

在 Shell 可以用 nvm 指令

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

`nvm: command not found`

確認自己所使用的 Shell 對應的 Profile 名稱 (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc)

```bash
touch ~/.bash_profile
source ~/.bash_profile
```

然後再安裝一次。

> 2020/7/4 官方不建議使用 Homebrew 安裝

專案內 `node -v` 取得的 node 的版本與電腦全域不相同

Instead, the proper solution is to delete `node_modules/`, `package-lock.json` & `yarn.lock` and run yarn install or npm i again.

```bash
nvm alias default {version}
```

## Troubleshooting

### `nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local" Run "npm config delete prefix" or "nvm use --delete-prefix v6.11.1 --silent" to unset it.`

Try config the $NVM_DIR reference again.

For example nvm use v7.10.0, and have the error: Run npm config· delete prefix or nvm use --delete-prefix v7.10.0 --silent to unset it.

You need overwrite nvm prefix,

```bash
npm config delete prefix 
npm config set prefix $NVM_DIR/versions/node/v9.3.0
```

https://github.com/nvm-sh/nvm#nvmrc

https://jiaming0708.github.io/2020/07/19/project-setting/