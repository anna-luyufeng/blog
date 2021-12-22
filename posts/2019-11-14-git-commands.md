---
title: "[Note] 常用 Git 指令"
date: 2019-11-14T07:56:27Z
layout: layouts/post.njk

---

## Branch 分支

```bash
# 查看所有 branch
git branch

# 新增 branch
git branch [BRANCH_NAME]

# 新增 branch 並切換到該 branch
git checkout -b [BRANCH_NAME] 

# 刪除本地 branch
git branch -d [BRANCH_NAME]

# 重新命名 branch
git branch -m [OLD_BRANCH_NAME] [NEW_BRANCH_NAME]	

# 重新命名當前 branch
git branch -m [NEW_BRANCH_NAME]	

# 合併 branch
git merge [BRANCH_NAME]

# 取消合併 branch
git reset --hard HEAD~

# 刪除 remote 舊的 branch
git push origin --delete [OLD_BRANCH_NAME]

# 刪除 remote 舊的 branch 並將新的 branch push 到 remote
git push origin :[OLD_BRANCH_NAME] [NEW_BRANCH_NAME]

# push 新的分支到 remote，並重設新的分支的 upstream 分支
git push origin -u [NEW_BRANCH_NAME]
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

- 與作業系統的檔案系統有關，macOS 無檔名大小寫的差別

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