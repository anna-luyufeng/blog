---
title: "[Note] 常用 Git 指令"
date: 2019-11-14T07:56:27Z
layout: layouts/post.njk

---

## 初始化

需要先初始化才能使用 git 做版本控制，會建立一個 `.git` 檔案。

若要重置 git 紀錄，刪掉此檔案即可。

若不希望部分檔案不加入版本控制，建立 `.gitignore` 並放入檔案

```bash
git init

rm -r .git # 刪掉 git 紀錄檔
```

## 查看目前狀態

```
git status
```

## 將檔案加入版本控制

`untracked` （未被追蹤的）→ `staged`

```bash
git add <filename|filepattern>
git add .	# 所有檔案
git add *.js	# 所有 js 檔案
```

## 提交一個版本

```bash
git commit	# 會開啟 vim 編輯器
git commit -m "<commit-message>"	# 提交信息
git commit -a	# 檢測出有修改的檔案（不包含新增的檔案）
```

## 檢視紀錄

```bash
git log
git log --graph
git log --oneline
```

## 移動 HEAD

```bash
git checkout . # 編輯檔案後，恢復目錄到最後一次 commit 的狀態
git checkout <commit_hash>
```



## Branch 分支

```bash
git branch	# 查看所有 branch
git branch -v # branch 名稱與最新的 commit
git branch <branch_name> # 新增 branch

git checkout -b <branch_name> # 新增 branch 並切換到該 branch

git branch -d <branch_name>	# 刪除本地 branch

git branch -m <new_branch_name>	# 重新命名當前 branch（-m 指 mv 的意思）
git branch -m <old_branch_name> <new_branch_name>	# 重新命名 branch


git merge <branch_name> # 合併 branch 至當前的 branch，會產生新的 commit
git rebase <branch_name> # 合併 branch ???，不會產生新的 commit
git reset --hard HEAD~ # 取消合併 branch


git push origin :<old_branch_name> # 刪除 remote 舊的 branch
git push origin --delete <old_branch_name> # 刪除 remote 舊的 branch
git push origin :<old_branch_name> <new_branch_name> # 刪除 remote 舊的 branch 並將新的 branch push 到 remote

git push origin -u <new_branch_name> # push 新的分支到 remote，並重設新的分支的 upstream 分支
```

## Stash 暫存進度
```bash
# 將目前的進度暫存
git stash 

# 取得 stash 列表
git stash list 

# 取回並刪除該 stash
git stash pop stash@{[STASH_NUMBER]}

# 取回但不會刪除該 stash
git stash apply stash@{[STASH_NUMBER]}

# 刪除 stash
git stash drop stash@{[STASH_NUMBER]} 
```



## 各種情境使用

### 安全的強制推送

```bash
git push --force-with-lease
```

> https://blog.walterlv.com/post/safe-push-using-force-with-lease.html

### 改變檔名的大小寫

- 與作業系統的檔案系統有關，Windows 與 Mac OSX 無檔名大小寫的差別，視為同一個檔案。

```bash
# 使用 git 的 mv 指令
git mv demoFile.html DemoFile.html

# 修改 git 設定檔
git config --local core.ignorecase false
git config --global core.ignorecase false
```

-----



- [Learn Git Branching](https://learngitbranching.js.org/index.html)
- [Git 教學 - Git 書 - 為你自己學 Git | 高見龍](https://gitbook.tw/)
- [連猴子都能懂的Git入門指南 | 貝格樂（Backlog）](https://backlog.com/git-tutorial/tw/)
- [zlargon/git-tutorial: Git Tutorial Online Book](https://zlargon.gitbooks.io/git-tutorial/content/)
- https://pjchender.dev/app/cli-git/
- https://pjchender.dev/npm/note-git-conventional-commit/