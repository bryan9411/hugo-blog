---
title: 'useEffect 系列'
date: '2024-06-10T15:01:57+08:00'
author: 'Bryan'
tags: [React]
categories: [React]
isCJKLanguage: true
draft: false
---

React 的 useEffect 是一個非常重要的 Hook，主要用來處理副作用（side effects）

### 什麼是副作用？
#### 副作用指的是任何影響到 React 組件外部的操作，例如：

 - 資料的讀取（API 請求）
 - 修改 DOM
 - 設定計時器或事件監聽器

### 基本用法
```
import React, { useState, useEffect } from 'react'

const Component = () => {
  const [count, setCount] = useState(0)

  // 使用 useEffect 來更新網頁標題
  useEffect(() => {
    document.title = `你點擊了 ${count} 次！`
  })

  return (
    <div>
      <p>你點擊了 {count} 次！</p>
      <button onClick={() => setCount(count + 1)}>
        點擊我
      </button>
    </div>
  )
}

export default Component
```

每次 Component 重新渲染後，useEffect 都會執行，`document.title` 就會被更新為最新的點擊次數

### 使用依賴陣列控制執行
如果只想要 useEffect 在某些特定情況下執行的話

這時可以使用 依賴陣列（Dependency Array）來控制執行時機

```
import React, { useState, useEffect } from 'react'

const Component = () => {
  const [count, setCount] = useState(0)
  const [name, setName] = useState('React')

  // 只有 count 值改變時才執行
  useEffect(() => {
    console.log(`count 已更新為 ${count}`)
  }, [count])

  return (
    <div>
      <p>count: {count}</p>
      <button onClick={() => setCount(count + 1)}>增加 count</button>

      <p>name: {name}</p>
      <button onClick={() => setName(name === 'React' ? 'Hooks' : 'React')}>
        切換名稱
      </button>
    </div>
  )
}

export default Component
```
只有當 `count` 值改變時才需要重新執行 useEffect

如果依賴陣列為空陣列的話，則 useEffect 只會在 Component 初始化時執行一次

### 清除副作用(side effects)
某些副作用需要清除，例如：事件監聽或計時器 可以在 useEffect 中 return 一個清除函數

```
import React, { useState, useEffect } from 'react'

const Timer = () => {
  const [seconds, setSeconds] = useState(0)

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prev) => prev + 1)
    }, 1000)

    // 清除計時器
    return () => clearInterval(interval)
  }, []) // 只在初始化時執行一次

  return <p>已經過了 {seconds} 秒。</p>
}

export default Timer
```

在 useEffect 中清除函數會在 component 卸載（unmount）或下一次執行 useEffect 前執行

### useEffect 的兄弟 useLayoutEffect
useEffect 和 useLayoutEffect 都是用來處理副作用的，但它們的執行時機不同：

#### useEffect:
  - 在瀏覽器完成畫面渲染後執行
  - 適合處理非同步操作（如資料請求）或不會影響 UI 的邏輯

#### useLayoutEffect: 
  - 在 DOM 更新後但在瀏覽器渲染畫面前執行
  - 適合需要在畫面更新前計算 DOM 的情境，例如測量元素的大小或位置

```
import React, { useState, useEffect, useLayoutEffect } from 'react'

const Component = () => {
  const [width, setWidth] = useState(0)

  // 使用 useLayoutEffect 來測量 DOM 寬度
  useLayoutEffect(() => {
    const element = document.getElementById('box')
    setWidth(element.offsetWidth)
  }, [])

  useEffect(() => {
    console.log('useEffect 執行：畫面已更新')
  })

  return (
    <div>
      <div id="box" style={{ width: '200px', height: '100px', background: 'lightblue' }}>
        我是測試區塊
      </div>
      <p>測量到的寬度：{width}px</p>
    </div>
  )
}

export default Component
```

`useLayoutEffect` 在 DOM 更新後立即執行，因此適合測量元素大小

`useEffect` 則是在畫面渲染出來後才執行，適合記錄 log 或執行非同步操作
