---
title: 'JS 變數底層運作'
date: '2022-09-08T22:39:26+08:00'
author: 'Bryan'
tags: ['JavaScript']
categories: ['JavaScript']
isCJKLanguage: true
draft: false
---

一般的重新賦值，只要修改值就會變更
```
var a = 10
console.log(a); // 10

a = 20
console.log(a); // 20
```
但是物件狀態就不一樣了
```
var objA = {
    number: 10
}

var objB = objA 
console.log(objA, objB) // { number: 10 } { number: 10 }

objA.number = 20
console.log(objA, objB) // { number: 20 } { number: 20 }

```
發現 objA 物件修改值，兩邊就會改值

會這樣的原因跟底層有關係，物件是以一種記憶體形式方式儲存，再把變數指向這個記憶體位置。因為兩個儲存的記憶體位置是一樣的，所以一改之後就會其他的部份也改了
```
/**
 * objA 記憶體位置 0x01, objB 記憶體位置 0x02
 */

var objA = {
    number: 10
}

var objB = objA // 將 objB 指向了 objA 的記憶體位置，而不是在創建一個新的物件

console.log(objB === objA) // true 因為記憶體儲存位置一樣

```

接著看下面這例子

```
var arr = [1, 2, 3]
var arr2 = [1, 2, 3]

console.log(arr[0] === arr2[0]) // true
console.log(arr === arr2) // false
```
arr 與 arr2 是兩個不同的陣列物件，它們位於記憶體中不同的位置

arr: 0x01

arr2: 0x02

因為它們指向不同的記憶體位置，所以 `console.log(arr === arr2)` 輸出為 false

但是當比較的 arr[0] 和 arr2[0]，實際上比較的是這兩個陣列中的第一個元素，而不是記憶體位置，
所以 `console.log(arr[0] === arr2[0]` 輸出為 true