---
title: 'JS 字串函數'
date: '2022-10-10T23:36:33+08:00'
author: 'Bryan'
tags: [JavaScript]
categories: [JavaScript]
isCJKLanguage: true
draft: false
---
介紹工作上常使用到的字串函數方法

### `trim` 移除字串的開頭和結尾的空白字元
```
const str = '   Hello, World!   '
const trimStr = str.trim()

console.log(trimStr) // 'Hello, World!'
```

### `indexOf` 找出指定字串出現位置的 index
```
const str = 'Hello, World!'
const index = str.indexOf('World')

console.log(index) // 7
```

### `lastIndexOf` 找出指定字串最後一個出現位置的 index
```
const str = 'Hello, World!'
const lastIndex = str.lastIndexOf('o')

console.log(lastIndex) // 8
```

### `charAt` 取得指定位置的 index
```
const str = 'Hello, World!'
const char = str.charAt(4)
console.log(char) // 'o'
```

### `slice` 從字串中擷取一個子字串
```
const str = 'Hello, World!'
const slicedStr = str.slice(7, 12)
console.log(slicedStr) // 'World'
```

### `concat` 將多個字串連接在一起
```
const str1 = 'Hello'
const str2 = 'World'
const concatenatedStr = str1.concat(', ', str2, '!')
console.log(concatenatedStr) // 'Hello, World!'
```

### `replace` 將指定字串替換
```
const str = 'Hello, World!'
const replacedStr = str.replace('World', 'Everyone')
console.log(replacedStr) // 'Hello, Everyone!'
```

### `split` 將字串分割成字串陣列
```
const str = 'Hello, World!'
const splittedStr = str.split(', ')
console.log(splittedStr) // ['Hello', 'World!']
```

### `join` 將字串陣列中的所有元素連接成一個字串
```
const arr = ['Hello', 'World!']
const joinedStr = arr.join(', ')
console.log(joinedStr) // 'Hello, World!'
```
