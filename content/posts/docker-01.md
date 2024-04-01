---
title: 'Docker 介紹'
date: '2024-03-31T12:43:25+08:00'
author: 'Bryan'
tags: [Docker]
categories: [Docker]
isCJKLanguage: true
draft: false
---
![docker](/images/Docker/banner.jpeg)

# 什麼是 Docker ?
Docker 是一個開源的容器化平台，由 `Dockerfile` 、 `Docker Image` 、 `Docker Container` 三者組成

可將應用程式及其相關環境打包成一個獨立的容器(Container)，確保應用程式在不同的環境中能夠快速運行，而不受環境變化的影響。

**安裝 Docker**

[官方文件](<https://docs.docker.com/desktop/install/mac-install/> "官方文件")

# Docker 與虛擬機(Virtual Machine)區別
Docker 主要優勢在於部署快速、環境一致性、效能高、容易管理，可以快速地部署和啟動容器，並且容器之間可以獨立運行，互不影響。

另外可以確保在不同的開發、測試環境中程式的一致性，避免因開發環境不同而引起問題。

加上 Docker 是屬於輕量級應用，由多個容器去共享主機資源，效能比較高，而虛擬機是有自己獨立的虛擬化環境，相對來說比較效能較低。

|                | Docker                                             | 虛擬機 (Virtual Machine)     |
| -------------- | -------------------------------------------------- | ---------------------------- |
| 部署與啟動速度 | 快速，低資源消耗                                   | 較長的啟動時間，較高資源消耗 |
| 環境一致性     | 是                                                 | 擁有自己獨立的虛擬化環境     |
| 虛擬化環境     | 多個容器共享主機資源  容器之間可以獨立運行，效能高 | 獨立的虛擬化環境，效能較差   |
| 程式一致性     | 可確保不同環境中程式的一致性                       | 需要特別注意環境配置的一致性 |

# Dockerfile
包含一系列指令，用於建立 Imgae

  * FROM：指定 image
  * RUN：執行指令
  * COPY：將本地文件複製到 image 裡面
  * WORKDIR：設定工作目錄
  * CMD：定義容器啟動時運行的指令

# Docker Image
包含了運行容器所需的所有內容：程式碼、運行環境、環境變數和配置...等，這些設定都是從 Dockerfile 取得
透過 `docker build` 根據 Dockerfile 來建立新的 image

# Docker Container
一個具有自己環境變數的容器，可以在容器內部進行開發測試和部署 ... 等等

## 三者關係與流程
  1. 使用 Dockerfile 建立 image 設定
  2. 通過 `docker build` 命令根據 Dockerfile 創建新的 image
  3. 使用 `docker run` 命令根據 image 建立一個新的容器
