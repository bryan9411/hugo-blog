---
title: 'Fetch vs Pull '
date: '2023-11-12T17:24:15+08:00'
author: 'Bryan'
tags: ['git']
categories: ['Git 版本控制']
isCJKLanguage: true
draft: false
---
![git](/images/Git/banner.jpeg)

# fetch vs pull
| 指令    | 說明                                                                                           |
| ------- | ---------------------------------------------------------------------------------------------- |
| `fetch` | 從遠端下載最新的資料，但不合併到本地分支。                                                     |
| `pull`  | 從遠端下載最新的資料並合併到本地分支，其實就是執行 `git fetch` 和 `git merge` 兩個指令的組合。 |