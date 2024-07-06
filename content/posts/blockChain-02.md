---
title: 'EVM 與智能合約'
date: '2024-07-06T17:50:40+08:00'
author: 'Bryan'
tags: [區塊鏈]
categories: [區塊鏈]
isCJKLanguage: true
draft: false
---

### EVM
EVM 是 Ethereum Virtual Machine 的縮寫，也就是以太坊虛擬機。它是以太坊區塊鏈網路中的一部分，負責執行智能合約的程式碼

### 智能合約
智能合約是一種自動執行合約，其合約是以程式碼形式寫入。當預定義的規則被滿足時，智能合約會自動執行相應的操作。智能合約是在 EVM 上運行的，並且其運行結果是透明且不可篡改的。

***這裡舉一個例子是自動販賣機:*** 

當你在自動販賣機上投入硬幣並選擇你想要的商品時，自動販賣機會根據你的選擇和投入的金額，自動給你正確的商品。

***再舉一個例子是航班延誤需要保險理賠時:***

當航班延誤時，在傳統的保險合約中，當出現需要賠付的情況時，通常需要保險持有人手動提交賠償申請，並提供航班延誤證明。然後，保險公司的工作人員會審核這些申請和證明，確認情況屬實後才會進行賠付。這個過程可能需要幾天到幾周的時間，並且可能需要多次的溝通和確認。

然而，如果使用智能合約，當航班延誤的信息被上鏈後，智能合約會自動執行，無需人工審核和確認，賠償金會立即轉入保險持有人的帳號。這樣不僅可以提高效率，還可以降低人工審核的成本和錯誤率。

上面這兩個過程就是一個智能合約，當滿足特定的條件（投入足夠的金額並選擇商品、航班延誤）時，合約就會執行(出售商品、賠償金轉入保險持有人的帳號)