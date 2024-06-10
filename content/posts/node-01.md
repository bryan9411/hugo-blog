---
title: '為什麼 pnpm 速度快於 yarn ?'
date: '2024-05-22T14:10:56+08:00'
author: 'Bryan'
tags: [Nodejs]
categories: [Nodejs]
isCJKLanguage: true
draft: false
---
![why pnpm fast yarn ?](/images/Node/pnpm/why-pnpm.png)

身為前端開發者一定聽過 npm 以及 yarn 這兩項套件管理工具，但其實還有一個叫 pnpm 的套件管理工具

最近公司新專案在前端開發中，從 yarn 轉向使用 pnpm，這篇就來說一下體驗心得

假如有一個叫做「Project A」的專案，裡面安裝了 React 和 lodash，使用 yarn 和 pnpm 來安裝這些依賴項

### 使用 yarn 安裝
yarn 會將下載的 React 和 lodash 存儲在一個全局緩存目錄中，當使用 yarn 安裝時，會先檢查全局緩存中有沒有存在，如果存在就會直接使用這些緩存的檔案，而不是從網絡重新下載

但是，即時使用了全局緩存，yarn 還是會將需安裝的依賴複製到每個專案的 node_modules 裡面

也就是說，如果我們有另一個名為「Project B」的專案也一樣安裝相同版本的 React 和 lodash，yarn 會再次從全局緩存中複製一份 React 和 lodash 到 「Project B」

### 使用 pnpm 安裝
pnpm 採用全局儲存方式，會將下載的檔案存儲在一個全局目錄中，當使用 pnpm 安裝時，會先檢查全局儲存目錄中有沒有存在，如果存在就會直接使用這些檔案，而不是從網絡重新下載

與 yarn 不同的是 pnpm 不會將檔案複製到每個專案的 node_modules 裡面。相反，它會使用 link 方式直接指向全局存儲中的實際位置。這樣，每個專案的 node_modules 裡面就只包含指向全局存儲的連結，而不是整包檔案全部複製一次。

### 兩者不同安裝方式差異
根據兩者安裝的方式，最關鍵區別在於硬碟空間的使用以及安裝的速度

硬碟空間：
  * yarn: 每個專案都會重新複製一份導致空間浪費
  * pnpm: 透過 linl 連結直接找到全局儲存的位置，無需重新複製
  
安裝速度：
  * yarn: 要花時間將檔案複製到 node_modules
  * pnpm: 無需將檔案重新複製，安裝上更加快速
