---
title: 'Dockerfile'
date: '2024-04-07T14:33:11+08:00'
author: 'Bryan'
tags: [Docker]
categories: [Docker]
isCJKLanguage: true
draft: false
---
## 什麼是 Dockerfile？
Dockerfile 包含了一系列的指令和配置，用於自動化生成 Docker Image
Dockerfile，可以定義容器的環境和配置，可以讓 Image 的建立和部署變得更加容易

## Dockerfile 指令

### From
指定要安裝的 Image
```
From alpine:lastest
```

### ENTRYPOINT
如果要在背景執行需要一個事件讓 docker 不停地去執行
例如不停地查看 dev 資料夾底下的 null log  `docker run -d test01 tail -f /dev/null`

現在想要將這 test01 image 給別人使用，但是不想讓別人知道一定要打上這段 `tail -f /dev/null` 指令才可以背景執行的話，可以透過 `ENTRYPOINT`這語法來解決

`ENTRYPOINT` 代表這個 image 會第一個執行的命令
```
ENTRYPOINT ["tail", "-f", "/dev/null"]
```

### RUN
在 Image build 時才會執行命令
```
## 在 image build 時，echo 出文字並且列出根目錄下的檔案

RUN echo "I am in the image process"
RUN ls -l /
```

### ENV
ENV 設置環境變數變數
```
ENV DB_HOST "localhost"
RUN echo ${DB_HOST}
RUN ls -l /
```

### WORKDIR
指定預設目錄
```
## 這樣預設入口點會是在 dev 資料夾內，好處是無需再使用指令 RUN 進入 dev 資料夾才印出 echo message 
## 可以使整個 dockerfile 更為簡潔
WORKDIR /dev
RUN echo ${processMessage}
```

### ARG
跟 ENV 有點類似都是建立變數，唯一不同在於 ENV 可在 image build 時執行，而 ARG 無法

```
ARG name=bryan
```

### 建立簡易的 Dockerfile
綜合上面所說的指令來製作一個簡單的 Dockerfile

```
## 指定要安裝的 Image
From alpine

## ENV 環境變數
ENV DB_HOST="localhost"

## 指定預設目錄
WORKDIR /dev

## 在 image build 時才會執行
RUN echo ${DB_HOST}
RUN ls -l /

## 這個 image 會第一個執行的命令
ENTRYPOINT ["tail", "-f", "/dev/null"]
```

`docker build -t test01 .` 建立一個新的 image
```
[+] Building 0.2s (8/8) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                         0.0s
 => => transferring dockerfile: 318B                                                                                                                                                         0.0s
 => [internal] load .dockerignore                                                                                                                                                            0.0s
 => => transferring context: 2B                                                                                                                                                              0.0s
 => [internal] load metadata for docker.io/library/alpine:latest                                                                                                                             0.0s
 => [1/4] FROM docker.io/library/alpine                                                                                                                                                      0.0s
 => CACHED [2/4] WORKDIR /dev                                                                                                                                                                0.0s
 => CACHED [3/4] RUN echo localhost                                                                                                                                                          0.0s
 => [4/4] RUN ls -l /                                                                                                                                                                        0.1s
 => exporting to image                                                                                                                                                                       0.0s
 => => exporting layers                                                                                                                                                                      0.0s
 => => writing image sha256:478cf4f35add82783b8afc107061807439b9d391d1615e4b999089ae79ba7183                                                                                                 0.0s
 => => naming to docker.io/library/test01
```

`docker images` 查看 images
```
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
test01       latest    478cf4f35add   About a minute ago   7.73MB
```