---
date: "2025-01-18T11:54:14+08:00"
draft: false
title: "迴圈 - 以 Python 為例"
tags:
  - 電腦科學
  - Python
---

## 為什麼要有迴圈？

原因只有一個，那就是人類很懶，假設今天要輸出 100 萬筆資料，我們需要一筆一筆手刻出來嗎？在被主管開除之前，我們應該會先無聊到開始裸奔吧。

![Patrick Star wants to run naked](/img/patrick_star_nacked.png)

這個時候善用迴圈，用一組程式碼就能搞定大量的重複工作：

```python
for i in range(0, 1_000_000):
    print(i)
```

---

## 拆解 for 迴圈運作流程

上面以 `for` 關鍵字起頭的迴圈被稱為 **for 迴圈**，除了 Python 之外，Golang、JavaScript 等等眾多程式語言也都有類似的語法。本篇文章就以 Python 為例，拆解 for 迴圈的運作流程。

1. 迴圈從 i 等於 0 啟動 -> `i in range(0)`
2. 檢查若 i 不少於 1,000,000 就跳出迴圈運作 -> `range(0, 1_000_000)`，否則繼續執行以下動作:
   - 列印出 i 變數 -> `print(i)`
   - i 變數值加一 (`range` 預設會加一)
   - 回到第二步驟檢查 i 是否不少於 1,000,000

最後我們會看到 0 ~ 999,999 列印出來。

> 在 Python 中，`range(a, b)` 會包含 `a` 但不包含 `b`。所以 `range(0, 1_000_000)` 才不會列印出 1,000,000。

---

## Python 的空格很重要！

雖然可以靠 IDE 的自動矯正功能避免，但 Python 由於語法特定，for 迴圈的執行程式碼需要做好空格 (indentation)。我自己是習慣按 tab 鍵一次空四格。也要注意，執行程式碼**每一行都要空一樣的格數**，否則編譯器會顯示錯誤！

---

## `range` 的第三個參數 - step

前面提過 `range` 會預設給計數器加一，但其實透過 step 參數，我們可以指定每次遞迴要加上去的數目。

```python
for i in range(0, 10, 2):
    print(i)
# prints:
# 0
# 2
# 4
# 6
# 8
```

除了正數一路往上加之外，若帶入負數的話，等於每次遞迴都減去固定的數目。

```python
for i in range(3, 0, -1):
    print(i)
# prints:
# 3
# 2
# 1
```

---

## While 迴圈

Python 除了 for 迴圈之外，還提供了另一種迴圈叫做 while。我們會給 while 迴圈一個條件，只要該條件滿足 `True`，那迴圈就會持續執行下去，所以務必要小心陷入無限迴圈，就像我們的焦慮。

![anxitey of living](/img/anxiety.jpg)

```python
while 1:
    print("1 evaluates to True")

# prints:
# 1 evaluates to True
# 1 evaluates to True
# (...無限輪迴)
```

所以通常 while 迴圈的條件會是比較算式或變數，再次提醒，**_條件將影響到 while 迴圈何時結束，或是陷入無限輪迴當中_**。以下範例中，我們用變數當作計數器，並且在每次符合條件的遞迴中更新計數器變數，確保程式最終能脫離迴圈。

```python
num = 0
while num < 3:
    num += 1
    print(num)
# 1
# 2
# 3
# (因為 num >= 3，不符合條件，迴圈終止)
```
