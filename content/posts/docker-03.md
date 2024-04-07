---
title: 'Docker container'
date: '2024-04-05T19:52:53+08:00'
author: 'Bryan'
tags: [Docker]
categories: [Docker]
isCJKLanguage: true
draft: false
---

### docker run
建立並執行一個新的容器

後面可帶參數：
* -d: 在背景執行
* -e: 設置環境變數
* -p: 將 port 映射 (host port:container port)
* -it: 交互式模式
* --name: 命名容器名稱
* --restart: 重新啟動容器

### docker ps
顯示目前正在執行的容器

後面可帶參數：
* -a: 顯示所有容器
* -q: 只顯示容器 id 

### docker rm
刪除容器

後面可帶參數：
* -f: 強制刪除容器

### docker exec
進入容器裡面執行指令

後面可帶參數：
* -d: 在背景執行
* -u: 指定使用者
* -e: 設定環境變數
* -w: 指定工作目錄
* -it: 交互模式

### 以 Docker Hub 提供的 alpine image 為例

先將 image 下載下來

```
docker pull alpine
```

建立一個新的 container ，去執行這個 image

```
docker run alpine
```

這時去查看容器狀態會發現沒有任何容器正在被執行，這是因為當容器運行的主進程跑完時，容器會自己退出結束

如果想要在背景一直持續運作的話

```
docker run -d --name test01 alpine tail -f /dev/null
```
意思就是建立並執行一個容器，將該容器名稱命名為 "test01"

使用背景模式持續執行 `tail -f /dev/null` 這個命令，讓 docker 持續去查看這文件

建立好容器後，再檢查一次容器狀態

如果出現下圖代表已成功建立容器，且背景持續執行

```
CONTAINER ID   IMAGE     COMMAND               CREATED         STATUS         PORTS     NAMES
8e1989d494fe   alpine    "tail -f /dev/null"   8 seconds ago   Up 7 seconds             test01
```

### 如何將 本機 port 映射到容器的 port？
nginx 是一個 web server，這次以 nginx image 為例，將本機 port 映射到 container 的 port 

先下載 nginx image
```
docker pull nginx
```

將本地主機 port 映射到 container port
```
docker run -d -p 8081:80 --name test02 nginx
```

建立好後檢查一下容器狀態，會發現 PORTS 欄位顯示本機 8081 port 已經被映射到容器的 80 port
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                  NAMES
00e08721216d   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   0.0.0.0:8081->80/tcp   test02
```

打開瀏覽器輸入 `http://127.0.0.1:8081/` 可以成功看到 nginx server 歡迎頁面
![](/images/Docker/container/pic01.png)