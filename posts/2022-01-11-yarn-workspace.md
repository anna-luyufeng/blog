---
title: "Yarn Workspace"
date: 2022-01-11T09:26:50+08:00
layout: layouts/post.njk
draft: true
---

Yarn Workspace 是專案檔案管理的一種架構。當今天專案成長到需要拆分多個細小專案，那麼當在開發管理時便會遇到麻煩，例如，在安裝套件時你得每個專案都跑一次安裝。

範例專案介紹：一個 common-lib, react, and vue 專案

該如何設置 yarn workspace?

```json
{
  "private": true,
  "workspaces": ["package-a", "package-b"]
}
```

在根目錄下新增 package.json 檔，這裡稱為大包 private 為 true 是為了防止意外發布大包

workspaces 陣列定義專案內有哪些子專案(小包)

此時大包的 package.json 的內容如下

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F87a9bc6b-123a-462d-b4a3-acca5eb02785%252F%E6%88%AA%E5%9C%96_2021-11-02_18.00.04.png)

Q1. 一定得在 packages 目錄底下嗎？

A1. NO, 只是慣例在命名為 packages 的目錄底下，實際上不取名作 packages 也可以，更甚者不在任何目錄底下也沒問題，只要在 workspaces 陣列裡面定義出子專案的路徑就可以。

workspaces 也可以為物件，此時會有兩個屬性 **packages** and **nohoist**

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F24321f35-16d5-46a0-bf3b-0d30d8b7fea7%252F%E6%88%AA%E5%9C%96_2021-11-02_18.21.38.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F65ff2b59-b7dd-41d5-9336-bb796e556932%252F%E6%88%AA%E5%9C%96_2021-11-02_18.30.37.png)

**nohoist**

hoist：Yarn 在安裝套件時為了減少重複的依賴安裝，進而提供效率，會盡可能地提升重複的套件至大包的 node_modules

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F8fb0404a-8443-409e-8f52-b994af2fa422%252FUntitled.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F7e844e5f-45ac-4625-868e-77dd7b27d93e%252F%E6%88%AA%E5%9C%96_2021-11-03_15.43.53.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F3dba5e3e-d2a2-44c2-91a7-1359f5ff089f%252F%E6%88%AA%E5%9C%96_2021-11-03_15.49.18.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252Fb5448cd0-1c8f-4333-acd8-9ac9daad2b13%252F%E6%88%AA%E5%9C%96_2021-11-03_15.49.56.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F3d668d50-3edc-42b8-91fd-2aa74edc629f%252F%E6%88%AA%E5%9C%96_2021-11-03_15.52.45.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252Fe9bf0374-08d7-4a90-856e-8ac47ba32815%252F%E6%88%AA%E5%9C%96_2021-11-03_16.06.26-20220111093509069.png)

![img](/img/https%253A%252F%252Fs3-us-west-2.amazonaws.com%252Fsecure.notion-static.com%252F7fbde2ff-2f96-40ea-af28-63088c039af1%252F%E6%88%AA%E5%9C%96_2021-11-03_16.06.35.png)

references:

1. https://classic.yarnpkg.com/lang/en/docs/workspaces/
2. https://classic.yarnpkg.com/blog/2018/02/15/nohoist/