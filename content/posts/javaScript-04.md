---
title: 'JS物件函數'
date: '2024-05-19T21:12:50+08:00'
author: 'Bryan'
tags: [JavaScript]
categories: [JavaScript]
isCJKLanguage: true
draft: false
---
假如從後端拿到的 member 資料為以下格式：

```
member = {
  name: 'Bryan',
  age: 30,
  gender: 'male'
}
```

## 要拿到該物件底下所有 item 的 key

```
// 返回一個包含物件所有屬性名稱的陣列
const keys = Object.keys(member)

console.log(keys)  // ['name', 'age', 'gender']
```

## 要拿到該物件底下所有 item 的 value

```
// 返回一個包含物件所有屬性值的陣列
const values = Object.values(member)

console.log(values) // 輸出：['John', 25, 'male']
```

## 要拿到該物件底下所有 item 對應的 key 跟 value

```
// 返回一個包含物件所有屬性名稱和屬性值的陣列
const entries = Object.entries(member)

console.log(entries)

// 輸出：
// [
//   ['name', 'John'],
//   ['age', 25],
//   ['gender', 'male']
// ]
```

## 將另一個物件資料複製並加入到當前物件
```
const newMember = {
  email: 'test@gmail.com'
}

Object.assign(newMember, member)
console.log('newMember', newMember)
// 輸出：
// {
//   name: 'John',
//   age: 25,
//   gender: 'male',
//   email: 'test@gmail.com'
// }
```

## 檢查物件是否具有指定的屬性
```
console.log(member.hasOwnProperty('name')) // true
console.log(member.hasOwnProperty('height')) // false
```
