---
title: 'Closure(閉包)'
date: '2022-09-20T22:24:48+08:00'
author: 'Bryan'
tags: ['JavaScript']
categories: ['JavaScript']
isCJKLanguage: true
draft: false
---
## 什麼是 Closure(閉包) ?
當你在一個函數中定義了另一個函式，即使外部函數已經執行完畢，這個內部函數還是能夠訪問外部函數中的變數

```
function outer () {
  var a = 10
  
  function inner() {
    a++
    console.log(a)
  }
  return inner
}

var result = outer()
result() // 11
result() // 12
result() // 13
result() // 14
```

在 outer 函數內部，我們定義了一個內部函數 inner，它可以拿到外部函數 outer 中的變數 a
當我們呼叫 outer 函數時，它回傳了 inner 函數，並且將其賦值給變數 result
此時，result 實際上指向了 inner 函數，但它仍然能夠拿到並修改 outer 函式中的變數 a
