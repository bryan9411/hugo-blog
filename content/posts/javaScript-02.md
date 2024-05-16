---
title: 'hoisting（提升)'
date: '2022-09-12T22:19:53+08:00'
author: 'Bryan'
tags: ['JavaScript']
categories: ['JavaScript']
isCJKLanguage: true
draft: false
---

## 什麼是 hoisting（提升）？
在 vsCode 打上程式碼，如果沒有賦值會顯示錯誤如下
```
console.log(a) // a is not defined
```
但是如果給它賦值，就會變成有 undefined 而非報錯
```
console.log(a) // undefined
var a = 10
```
上述兩者結合就像是這樣：

```
var a
console.log(a) // undefined
a = 10
```

這就是變數提升，當程式碼執行時，宣告的變數會被提升到其作用域的上方

除了變數提升外 function 也可以提升

```
foo() // function 被提升，會輸出 Hello world!

function foo() {
  console.log('Hello, world!')
}
```

但有例外情況。假如是把變數賦值一個 function 的話是不能提升 function
```
foo() // foo is not a function

var foo = function () {
console.log('Hello world!')
}
```
會這樣是因為提升的部份只有 foo 的變數，所以會是 undefined，而 undefined !== function 所以才會報錯

## hoisting 的順序
hoisting 只會發生在它的範圍內

```
var a = '全域變數'
function foo() {
  console.log(a) // undefined
  var a = '範圍變數'
}
foo()

======== 上方程式碼等於下方 ========

var a = '全域變數'
function foo() {
  var a
  console.log(a) //undefined
  a = '範圍變數'
}
foo()
```

從上述程式碼可以看到 hoisting 只會發生在 function 的範圍內

###  function 有提升的優先權
```
function foo () {
  console.log(a) // [Function: a]

  function a () {}
  
  var a = '範圍變數'
}
foo()

=============================================

function foo () {
  console.log(a) // [Function: a]
  
  var a = '範圍變數'
  
  function a () {}
}
foo()
```
可以看到不管變數 a 在 function a 前面或後面，優先提升的還是 function

### 如果有重複的 function 呢？
```
function foo () {
  console.log(a) // [Function: a]
  a() // second function
  
  function a () {
    console.log('first function')
  }
  
  var a = '範圍變數'
  
  function a () {
    console.log('second function')
  }
}

foo()
```
後面的 function 會蓋掉前面的 function 

### 當傳入的變數跟內部的變數一樣時
```
function foo (a) {
  var a
  console.log(a)
  a = 456
}

foo(123) // 123
```
當函數 foo 執行時，它的參數 a 被賦值為 123，接著，由於變數提升，函式內部的 `var a` 被提升到了函數的頂部

但這個宣告對程式碼的執行沒有影響，因為參數 a 已經存在且已經賦值，所以會印出函數的參數 a 的值

### 變數跟 function 優先權比較
```
function foo(a) {
  console.log(a)
  
  var a = 10
  function a() {}
}

foo(123) // [Function a]
```

從上面程式碼可以看到 function 會蓋過變數的提升，所以 function 優先權大於變數