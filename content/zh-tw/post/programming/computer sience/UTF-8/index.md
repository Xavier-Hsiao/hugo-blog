---
date: "2025-04-25T20:34:48+08:00"
draft: false
title: "什麼是 Unicode 和 UTF 8"
description: "認識 ASCII、Unicode 和 UTF-8 的字元編碼演變，了解文件或試算表出現亂碼的原因。"
categories:
  - 程式學習
tags:
  - 電腦科學
image: "unicode.png"
---

前陣子幫同事處理文件出現亂碼的問題，因緣際會看到 Huli 大大寫的文章《[為什麼打開檔案時會看到亂碼？跟著小明一起從傳紙條學習編碼](https://life.huli.tw/2022/05/21/what-is-encoding-ascii-unicode-utf8-5fe55a98bee0/)》，對我這種技術麻瓜來說幫助很大，因此想結合查到的其他字元編碼相關資料，整理成文章。

先說結論：

> 亂碼就是在儲存跟顯示時使用了不同的編碼系統，可能導致的狀況，只要改用同一個編碼系統即可解決這個問題。

首先我們要知道電腦採取 `二進位系統` 來儲存資訊。也就是說所有資料都用一連串的 0 和 1 呈現。

- 二進位系統中最基本的單位是 `位元 (bit)`，等於單一個 0 或 1

- 下一級更大的單位是 `位元組 (byte)`，等於 8 個位元，例如：01101011

以一篇文章來說，內容由非常多 `字元` 組成，而每個字元在電腦眼中都是一連串的位元，也就是一堆 0 和 1。

---

## ASCII

`ASCII` 是美國於 1960 年代推出的標準編碼系統。

> 所謂編碼是指將人類文字轉換成電腦二進位的流程。

ASCII 支援以下符號：

- 大寫拉丁字母

- 小寫拉丁字母

- 阿拉伯數字 0 \~ 9

- 常用標點符號

ASCII 為每個符號指派一組獨一無二的 [ASCII Code](https://www.cs.cmu.edu/~pattis/15-1XX/common/handouts/ascii.html) (三位數代碼組成)，以及**一個獨一無二的位元組**。所以 ASCII 最多能儲存 2^8 = 256 個符號。

想想世界上那麼多語言使用不同的文字系統，加上 emoji 和各種顏文字，區區 256 個符號的扣打鐵定不夠，因此我們需要更先進、字元儲存量更大的編碼系統。

---

## Unicode & UTF-8

`Unicode` 使用[更複雜的機制](https://deliciousbrains.com/how-unicode-works/)，解決了 ASCII 空間不足的問題。每個符號還是會被分配到一組獨一無二的代碼，被稱為 `code point`，以十六進位紀錄，大概長這樣：`U+1F4A9`。

> **但 Unicode 本身不會將符號儲存為二進位**。也就是電腦看不懂。

所以我們需要另一套編碼方法 `UTF-8` 將 Unicode 轉換為二進位。

`UTF-8` 會將 `code point` 轉換成 1 \~ 4 個位元組：

- 常見符號，例如 C，佔據 8 位元

- 罕見符號，例如 💕，佔據 32 位元

- 其他符號則占據 16 \~ 24 位元不等

這麼做的好處是能夠更彈性地節省空間。只需要一個位元組的符號，就讓它佔據一個位元組；需要三個位元組的符號，就佔據三個整。不多也不少，快樂沒煩惱。

題外話，由於 Golang 字串預設上用 `UTF-8` 編碼，所以我們可透過遞回去取得字串中每個字元的 `code point` 以及 `byte index`。

```go
for pos, char := range "日本\x80語" { // \x80 is an illegal UTF-8 encoding
    fmt.Printf("character %#U starts at byte position %d\n", char, pos)
}

// prints
character U+65E5 '日' starts at byte position 0
character U+672C '本' starts at byte position 3
character U+FFFD '�' starts at byte position 6
character U+8A9E '語' starts at byte position 7
```
