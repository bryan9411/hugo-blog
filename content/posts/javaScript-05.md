---
title: 'Debounce(防抖)'
date: '2024-06-01T19:38:04+08:00'
author: 'Bryan'
tags: [JavaScript, 前端效能優化]
categories: [JavaScript, 前端效能優化]
isCJKLanguage: true
draft: false
---
防抖（Debounce）用於限制連續觸發的事件的執行頻率，當一個事件被觸發後 debounce 會延遲一段時間，如果在這段時間內再次觸發該事件，則會重新計時。只有在這段延遲時間內沒有再次觸發該事件的話才會執行。

Debounce 比較常用於以下情境：
  * 監聽表單欄位輸入，在停止輸入一段時間後才執行操作，以減少向後端發送請求的頻率
  * 監聽視窗大小變化，在窗口大小變化停止一段時間後才重新計算
  * 監聽滑鼠滾動事件，在滾動停止一段時間後才執行某些操作

## 這邊以第一個情境為例：
```
// func => 要執行的事件函數
// delay => 延遲時間
const debounce = (func, delay) => {
  let timerId

  return function (...args) {
    clearTimeout(timerId)

    timerId = setTimeout(() => {
      func.apply(this, args)
    }, delay)
  }
}

const search = debounce((keyword) => {
  console.log(`搜索關鍵字：${keyword}`)
}, 500)

search('JavaScript')
search('React')
search('Css')
search('Html')

// 執行後得出結果為 => 搜索關鍵字：Html
```
