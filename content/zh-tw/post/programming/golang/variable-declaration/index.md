---
date: "2025-04-26T14:50:39+08:00"
draft: false
title: "Let's GO 哥布林 - 宣告變數"
description: "認識宣告 Go 變數的方式、海象運算符短宣告、const 常數"
categories:
  - 程式學習
tags:
  - Golang
image: "variable-declaration.png"
---

一般變數需要透過關鍵字 `var` 進行宣告，後面接上變數名稱，最後別忘了加上變數的型別。

```go
var mySkillIssues int
mySkillIssues = 42
```

\
當然我們也可以一行解決變數宣告和賦值。

```go
var mySkillIssues int = 42
```

---

## 海象運算符短宣告

如果是在函式作用域裡面，建議改用**海象運算符**來宣告並賦值函式。海象運算符長這樣：`:=`。對，我沒有開玩笑，所以才叫 **warlus operator**。

```go
mySkillIssues := 42
```

\
除了宣告和賦值一行處理之外，Go 還會進行[**型別推論 (Type Inference)**](https://zh.wikipedia.org/wiki/%E7%B1%BB%E5%9E%8B%E6%8E%A8%E8%AE%BA)，所以省去了手動定義型別的麻煩。注意上述程式碼並未提示 `mySkillIssues` 為 `int` 型別。

> **海象運算符僅限函式作用域使用**，所以函式之外，只能用 `var` 或是 `const` 宣告變數。

Go 和 Python 一樣，可以在一行內宣告多個變數。由於 Go 會自動推論型別，所以一次宣告多個不同型別的變數完全沒問題。我們只需要注意變數和值的對應順序即可。

```go
name, age := "goblin", 28
```

---

## Constants

`const` 變數被宣告後，其值就無法更改。要注意 `const` 的限制如下：

- 無法透過海象運算符進行短宣告。

- 只能是原始型別 (整數、字串、布林值……)

- 不能是複合型別 (slice、map、struct)

```go
const home = "The Cave"
```

Go 必須在編譯階段就知道 `const` 變數，所以我們**無法宣告在 run-time 才計算的** `const`：

```go
// currentTime 為函式回傳值，所以要等到 run-time 才會知道是多少
const currentTime = time.Now()
```

相對來說，如果是在編譯階段就運算完成，那就沒問題：

```go
const firstName = "Xavier"
const title = "The Goblin"
const fullName = firstName + " " + title
```
