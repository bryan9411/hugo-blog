---
title: 'GraphQL 與 RESTful API 差異'
date: '2023-11-20T21:49:00+08:00'
author: 'Bryan'
tags: ['GraphQL']
categories: ['GraphQL']
isCJKLanguage: true
draft: false
---
再介紹 GraphQL 之前要先介紹一下過去我們常用串 api 的方式 RESTful API。

### RESTful API
  RESTful API 它是一種架構風格，使用標準的 HTTP 方法 ，例如：GET、POST、PUT、DELETE 方法來做串接。優點在於簡單易懂好學且容易實現，緩存性也比較好，可以有效提升效能。

  RESTful API 還有一種特性是無狀態性（Statelessness），這表示每一個請求都是獨立且不依賴於之前的請求。這使得伺服器不需要保存客戶端的狀態，有助於提高伺服器的擴展性。

反之其缺點需要多個請求來獲取完整資料，有可能造成過度取得資料問題產生。

**例如**:

  假設有一個部落格，我們想獲取文章列表以及每篇文章的作者資訊：
  - 獲取所有文章列表: 使用 GET 方法去獲取 `/articles` 底下的所有文章
  - 獲取每篇文章的作者資訊: 使用 GET 方法去獲取 `/users/{userId}` 作者資訊

### GraphQL
  GraphQL 是一由 Facebook 開發的查詢語言，它可以允許 客戶端(client) 指定其所需的數據結構，並且僅返回這些構。
這樣的好處在於客戶端(client)可以根據自己的需求來精確地獲取資料，也可避免過度取得資料減少請求次數。
相較於 RESTful API ，GraphQL 學習成本較高相對較複雜，且在某些場景下可能存在過度複雜的查詢。
  
  雖然 GraphQL 學習成本高，但具有更大的靈活性和更精確的獲取資料。適用於對於不同資料需求的客戶端，從而減少過度取得資料的問題。

  在 GraphQL 中，要從伺服器獲取資料使用 `query` 而其他編修則是使用 `mutation`

**例如**:

  同樣使用部落格來當作舉例，可以使用 `query` 來獲取文章列表以及作者資訊：
   ```
    query {
      articles {
        title
        content
        user {
          name
          email
        }
      }
    }
   ```
在這個例子中，articles 查詢的每篇文章都有一個 user 屬性，該屬性包含作者資訊。
這與 RESTful API 中的 `/articles` 與 `/users/{userId}` 的結構相對應。

當你要編修資料時可以使用 `mutation`，例如創建新文章，可能需要標題(title)、內容(content)、作者(userId):

```
mutation {
  createArticle(input: {
    title: '哈利波特'
    content: '哈利波特與佛地魔'
    userId: '{userId}'
  }) {
    title
    content
    user {
      name
      email
    }
  }
}
```
在這個例子中，`input` 參數接收一個物件，其中裡面包含了標題、內容以及作者的 ID。
```
input: {
  title: '哈利波特'
  content: '哈利波特與佛地魔'
  userId: '{userId}'
}

```
在回傳結果中， GraphQL 可以讓我們指定希望回傳的資料，在這例子中我希望回傳給我標題、內容以及作者的名字和郵件
```
{
  title
  content
  user {
    name
    email
  }
}

```
兩段結合也就是說新增一篇標題為 '哈利波特'，內容為 '哈利波特與佛地魔' 的文章，同時將這篇文章新增到該作者底下。最後，回傳文章的標題、內容，以及作者的名字和郵件。

### 總結
最後用表格整理一下兩種不同 api 方式的差異性

|                    | RESTful API                            | GraphQL                                  |
| ------------------ | -------------------------------------- | ---------------------------------------- |
| **資料的取得方式** | 回傳整包資料，可能包含過多或不足的資訊 | 可以指定需要回傳的資料，精確獲取所需資訊 |
| **請求次數**       | 可能需要多次請求以獲取完整資訊         | 一次請求即可獲取多個資料                 |
