---
date: "2025-01-15T15:16:56+08:00"
draft: false
title: "作用域 - 以 Python 為例"
tags:
  - 電腦科學
  - Python
---

## 什麼是作用域？

作用域 (Scope) 是指**變數或函示名稱可以被使用的範圍**。我自己是想像成結界，外面的世界無法接觸、取用到結界內的萬事萬物。

舉例來說，當我們在函式中建立一個變數，包含給函示參數，那這些資料就無法在函示的作用域範圍之外使用，會跑出該變數沒有定義的錯誤。

```python
def add(x, y):
    return x + y

result = add(2, 6)
print(x) # ERROR! "name 'x' is not defined"
```

\
上述範例中，`x` 和 `y` 都是 `add` 函式的參數，因此只能在 `add` 函式作用域範圍內被使用。我們在作用域之外嘗試列印 `x`，Python 的編譯器會跳出 `x` 沒有被定義的錯誤警告。

## 全域作用域

我們知道函式中所定義的變數和參數，是無法在函式作用域以外被使用的。但如果今天有多個函式都要用同一組變數該怎麼辦呢？我們可以在全域環境中定義變數，這樣每個函式都能夠取用該變數了。

以結界來比喻，我覺得就像結界內的人可以把外面世界的物品拉進去，但外部世界的人無法看透結界內發生什麼事情，自然也就無法取用結界內的物品了。

```python
outside_stuff = "pull me in baby!"

def pull_outside_stuff_into_function_scope(target):
    return outside_stuff + " - success"

print(pull_outside_stuff(outside_stuff))
```

\
上述範例中，`pull_outside_stuff_into_function_scope` 最終會成功回傳 `pull me in baby! - success`。因為 `outside_stuff` 變數是在權域作用域 (global scope) 定義的，所以能夠被函式拉到函式作用域當中使用。
