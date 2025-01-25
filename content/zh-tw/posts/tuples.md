---
date: "2025-01-23T22:15:24+08:00"
draft: false
title: "初探 Python 元組 (Tuples)"
tags:
  - Python
---

## 什麼是元組 (Tuples)？

元組是 Python 其中一種資料集合的型別，具有以下兩種特色：

- 資料有序排列，可用索引提取資料
- 資料無法變更

所以基本上，我們可以將元組看作是**固定長定、無法變更的列表**。

在建立列表時，我們通常不會置入不同型別的資料，但這在元組中不成問題，因為元組的長度是固定的，所以能輕易追蹤哪個索引儲存哪種型別的資料。

和列表的 `[]` 不同，元組需要使用 `()` 來建立：

```python
my_tuple = ("this is a tuple", 45, True)
print(my_tuple[0])
# this is a tuple
print(my_tuple[1])
# 45
print(my_tuple[2])
# True
```

> 元組通常用來儲存少量、固定不變的資料。

---

## 元組和列表混用

由於元組本身就是資料的容器，所以我們**可以將多個元組儲存在列表當中**。

語法上和一般資料相同，用半形逗號區隔不同的元組，然後每個元組在列表中都有自己的索引。也就是說，當我們要提取列表中的元組資料，第一個索引代表要選取哪個元組，而第二個索引代表要選取該元組中哪筆資料。

```python
my_tuples = [("this is the first tuple in the list", 45, True),("this is the second tuple in the list", 21, False)]
print(my_tuples[0][0]) # this is the first tuple in the list
print(my_tuples[0][1]) # 45
print(my_tuples[1][0]) # this is the second tuple in the list
print(my_tuples[1][2]) # False
```

---

## 開箱元組

`Tuple Unpacking` 好像網路上有人翻譯成元組拆包，但我自己是習慣用「開箱元組」來指稱，因為開箱聽起來比較開心。

簡單來說，就是一次提取元組中所有資料，沒啥新奇的玩意：

```python
goblin = ("Cute Goblin", 28)
goblin_name, goblin_age = goblin

print(goblin_name) # Cute Goblin
print(goblin_age) # 28
```

> 事實上，當我們從函式回傳多個值的時候，等於回傳了一個元組。

---

## 何時使用元組

1. 用來代表資料量固定的實體

   - 地理經緯度：`(經度數字, 緯度數字)`
   - RGB 色票碼：`(255, 128, 0)`
   - 人員資料：`(姓名, 生日, ID)`

2. 從函式回傳多個值

3. 當作字典的 key：因為列表可以變更資料，所以不適合當作 `key`。

```python
locations = {
    (121.5598, 25.09108): "Taipei",
    (120.2513, 23.1417): "Tainan"
}
```
