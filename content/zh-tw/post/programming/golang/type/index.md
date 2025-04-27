---
date: "2025-04-27T16:35:48+08:00"
draft: false
title: "Let's GO 哥布林 - 基本型別"
description: "認識 Go 常見的基本型別，以及對應的型別別名。"
categories:
  - 程式學習
tags:
  - Golang
image: "various-type.png"
---

# Go 基本型別

Golang 基本型別包含：

- bool

- string

- int、int8、int16、int32、int64

- uint、uint8、uint16、uint32、uint64、uintptr (將 pointer 轉換成 int)

- byte // uint8 的別名 (alias）

- rune // int32 的別名 (alias) 代表 [Unicode code point](https://goblin-stronger.com/p/%E4%BB%80%E9%BA%BC%E6%98%AF-unicode-%E5%92%8C-utf-8/)

- float32、float64、complex64、complex128

型別後面的大小 (8, 16, 32, 64, 128…) 代表記憶體儲存這個變數，需要佔用多少位元 (bit) 的空間。

---

## 型別預設大小

像 `int` 和 `uint` 這類型別的預設大小，則端看程式運行環境而定，可能會是 32 或 64 位元。

> `uint` 型別代表正整數，所以無法儲存負數。

如果沒有特殊效能需求，一般來會用的型別如下：

- `int`

- `uint`

- `float64`

- `complex128`

---

## 型別別名

由於 Golang 時常用在系統開發專案，所以像 `unit8` 以及 `int32`提供了別名，讓變數讀起來含義更明顯。

```go
func Read(p []byte) (n int, err error)
```

比方說看到上面的函式，我們馬上就知道是處理二進位資料。

```go
for _, r := range "Go語言" {
    fmt.Printf("%c = %U\n", r, r) // r is a rune (int32)
}
```

這個迴圈的 r 則是代表 `rune`，也就是 **[Unicode code point](https://goblin-stronger.com/p/%E4%BB%80%E9%BA%BC%E6%98%AF-unicode-%E5%92%8C-utf-8/)**。
