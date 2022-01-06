---
title: "[Mac/Linux] CLI 命令列"
date: 2020-07-04T02:16:02Z
layout: layouts/post.njk
draft: true
---

Command Line Interface（CLI）：以**文字**的方式跟電腦溝通

Graphical User Interface（GUI）：

## 名詞釋疑

- Terminal
- Shell => ??? Bash, Zsh, Fish, https://github.com/anna-luyufeng/note/issues/82
- Console

## Terminal 視窗操作技巧

- `control+c` 取消目前指令
- `control+z` 中斷目前指令
- `control+a` 跳到指令最前面
- `control+e` 跳到指令最後面
- `control+l`／`clear` 清空畫面

## Mac/Linux 通用指令

```bash
# 
date


# manual 指令使用說明書，按 q 離開
man
```



## 檔案目錄結構和操作

```bash
# print working directory 印出從根目錄到所在位置的路徑
pwd

# list 列出檔案清單
ls
ls -l # 顯示檔案與目錄的詳細資訊
ls -a # 顯示隱藏的檔案與目錄（隱藏的檔案前面會用 . 區隔）
ls -al # 顯示隱藏檔案與目錄的詳細資訊

# change directory 切換資料夾
cd
cd ./ # 在同一層移動
cd .. # 回到上一層
cd ~ # 回到 home 目錄（Mac 是 /User/username；Linux 是 /home/username）
cd / # 回到 root 目錄

# 建立新檔案或更新現有檔案的修改時間
touch <file>

# remove 刪除檔案
rm <file|directory>
rm -r / rmdir # 刪除資料夾
rm -f # 強制刪除檔案
rm -rf # 強制刪除整個資料夾

# make directory 建立資料夾
mkdir <directory>

# copy 複製檔案
cp <file> <directory>
	cp index.html about.html # 把檔案 index.html 複製成一份 about.html
	cp -r x_folder y_folder # 把 x_folder 資料夾複製進 y_folder 資料夾中

# move 移動檔案或重新命名
mv <file-old> <file-new|directory>
  mv home.html index.html # 把 home.html 重新命名為 index.html
  mv index.html x_folder/ # 把 index.html 移動到 x_folder 資料夾中

# 檔案編輯器
vim 
```

## 管理系統程序

同 Mac 上的系統監視程式（Activity Monitor）

```bash
# 列出所有背景執行的程序（process）
ps aux
ps aux | grep ssh  # 列出正在執行 ssh 的程序

# list open files 列出目前佔用 3000 port 的程序
lsof -i tcp:3000

# 砍掉指定 PID 的程序 （process ID）
kill -9 {{PID}}

# 砍掉所有正在執行 node 的程序
killall node -9
```



## 其他好用指令

```bash
# catenate 顯示檔案所有內容
cat

# 顯示檔案最後面的內容
tail
tail -n <filename> # 最後 500 行
tail -f <filename> # -f 循環讀取，可用來觀察 log

# 印出字串
echo

# g/RE/p 正規表達式，搜尋檔案內容
grep <keyword> <file|directory>

# 下載檔案
wget <檔案網址>

# curl 送出 request，測試 API
curl -i http://www.google.com
```



## 指令組合技

```bash
# > redirect  將輸入或輸出重新導向
date > time.txt # 將 date 輸出結果放到 time.txt 內
echo "123" > number.txt # 印出 123 到 number.txt，123 會覆蓋 number.txt 內原有的內容
echo "123" >> number.txt # 123 會新增在 number.txt 內容的最後（append）

# | pipe 把前面的輸入「變成」後面的輸出
cat file.txt | grep hello world # 從 file.txt 內容印出字串 hello world 並輸出
```

---

- https://hackmd.io/@Heidi-Liu/note-cli
- https://ihower.tw/cs/cli.html

