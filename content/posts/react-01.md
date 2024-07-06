---
title: 'useEffect 執行順序'
date: '2024-06-10T15:01:57+08:00'
author: 'Bryan'
tags: [React]
categories: [React]
isCJKLanguage: true
draft: false
---

### useEffect
異步函數，可以在函數組件中執行副作用操作，第二個參數為 dependences

[] 為畫面載入時只執行一次，當有填寫參數進去時，當此參數值有變化就會重新 rerender 渲染畫面

常用在資料獲取、訂閱或手動更改 React 組件的 DOM

```
useEffect(() => {
  console.log('useEffect 執行')
}, [])
```

### useLayoutEffect
同步函數，useLayoutEffect 與 useEffect 相似，但它會在所有的 DOM 變更之後同步調用副作用函數

可以在瀏覽器畫出畫面之前讀取 DOM 並同步觸發 rerender

```
useLayoutEffect(() => {
  console.log('useLayoutEffect 執行')
}, [])
```

### 執行過程
```
import { useEffect, useLayoutEffect } from 'react'

const App = () => {
  useEffect(() => {
    console.log('進入畫面第一次 useEffect 執行')

    return () => {
      console.log('清理 useEffect ')
    }
  }, [])

  useLayoutEffect(() => {
    console.log('畫面畫完之後 useLayoutEffect 執行')

    return () => {
      console.log('清理 useLayoutEffect ')
    }
  }, [])

  return <div>Hello World</div>
}

export default App
```

上述執行順序結果為
```
畫面畫完之後 useLayoutEffect 執行
進入畫面第一次 useEffect 執行
清理 useLayoutEffect 
清理 useEffect 
畫面畫完之後 useLayoutEffect 執行
進入畫面第一次 useEffect 執行
```
瀏覽器開始渲染畫面時會先執行 `useLayoutEffect` 的 func，在控制台中，會看到 "畫面畫完之後 useLayoutEffect 執行" 的 log 輸出，接著才會執行 `useEffect`並且去清理各自的副作用

#### 為什麼 useLayoutEffect 順序優先 useEffect ?
`useEffect` 是在瀏覽器畫面渲染出來後才去做執行，而 `useLayoutEffect` 不同，是在瀏覽器還沒畫出畫面出來前就先去執行

所以 `useLayoutEffect` 的回調函數會在 `useEffect` `的回調函數之前執行。同理，useLayoutEffect` 的清理函數會在 `useEffect` 的清理函數之前執行