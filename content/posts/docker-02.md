---
title: 'Docker Image'
date: '2024-04-01T16:47:16+08:00'
author: 'Bryan'
tags: [Docker]
categories: [Docker]
isCJKLanguage: true
draft: false
---

### Docker Hub 
[Docker hub](<https://hub.docker.com/> "Docker hub")是 Docker 官方維護了一個公共倉庫，裡面放置大多數的 image 檔案，像是如果需要 ubuntu 或 Linux 環境，都可以在這網站下載到相關 image

### 下載 Image
  1. 啟動 docker
  2. 在 [Docker hub](<https://hub.docker.com/> "Docker hub") 網站註冊登入
  3. 搜尋 hello-world 這個 image 映像檔
  4. 指令 `docker pull hello-world` 把該 image 映像檔下載下來

### 查看本地 Image
啟動 docker 輸入 `docker images` 會顯示本機已有的映像檔

```
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    ee301c921b8a   11 months ago   9.14kB
```

在上述這段訊息中，可以得到幾個資訊：
  * 來自於哪個倉庫: hello-world
  * 版本資訊：latest 最新版
  * IMAGE ID
  * 建立時間
  * 該 image 大小

### 啟動 Image
image 下載完後，要起一個 docker container ，然後把 hello-world 這個 image 放進 container 裡面

```
docker container run hello-world
```

如果終端機出現以下訊息，就說明已經成功將這 image 跑起來

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

### 刪除 Image
只要知道 image 名稱，就可以透過指令做刪除

```
docker rmi hello-world
```

另外，刪除 image 時有可能會遇到以下這錯誤

```
Error response from daemon: conflict: unable to remove repository reference "hello-world" (must force) - container 68df6174ffdb is using its referenced image ee301c921b8a
```

這是因為這個 image 正在被 reference by 68df6174ffdb 這個 conatainer id

所以要先把這個 container 砍掉，沒了 container 才可以刪除 image

```
// 先刪除 container
docker rm 68df6174ffdb

// 再刪除 image
docker rmi hello-world
```

### 如果不想管有沒有被 reference 的話
如果不想管有沒有被 referenced 的話，可以使用 force 方式強制刪除
```
docker rmi -f hello-world
```
