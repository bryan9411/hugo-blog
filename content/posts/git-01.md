---
title: 'Git: 基本指令'
date: '2023-11-07T21:48:41+08:00'
author: 'Bryan'
tags: ['git']
categories: ['Git 版本控制']
isCJKLanguage: true
draft: false
---
![git](/static/img/git-banner.jpeg)

Git 它是一個版本控制系統，可以幫助你追蹤程式碼變化、管理版本、合作開發，是團隊協作中不可或缺的工具之一。

以下是一些基本的 git 指令與使用情境 👇

# init
當開始一個新專案時，首先需要初始化一個新的 git repository

這個指令會在當前目錄下創建一個新的 git repository，並且開始追蹤你的文件檔案

```
git init
```

# clone
當需要從遠端(通常是 gitlab or github)拉下專案到你的本機開發

上述是以 github 為範例，會從你的遠端位置拉下指定的專案到你本機環境

```
git clone https://github.com/你的使用者名稱/要拉下的專案名稱.git
```

# status
查看工作目錄和暫存區的狀態，看哪些文件已修改、哪些文件準備提交

```
git status
```

# log
查看提交記錄

```
git log
```

# add

將工作目錄中特定檔案的修改添加到暫存區
```
<!--- 這只會將 index.html 這檔案的修改添加到暫存區 -->

git add index.html
```

把全部修改得檔案添加到暫存區 👇
```
<!---
  add 後面需多加個 .
  代表把所有檔案包含剛新建的檔案或資料夾都給添加到暫存區
-->

git add .
```

只有被 git 追蹤的檔案添加到暫存區 👇
```
<!---
  -u 只會將有被加入 git 追蹤的檔案修改添加到暫存區
  新建的檔案或資料夾都不會添加到暫存區
-->

git add -u
```

# commit
將暫存區的修改提交到本地，當 commit 完後可以透過 `git log` 查看整個提交記錄

```
git commit -m 'first commit'
```

# branch
建立一個新分支

```
<!--- 建立名為 dev 分支-->
git branch dev
```

# checkout
從 A 分支切換到 B 分支

```
<!--- 假設目前在 main 分支， 切換到 dev-->
git checout dev
```

# merge
將一個分支的更改合併到另一個分支

```
<!--- 合併指定分支到當前分支 假設指定分支是 dev -->
git merge dev
```

# push
將 commit 提交到遠端

```
<!--- 假設遠端分支是 main -->
git push origin main
```
