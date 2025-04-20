---
date: "2025-01-19T15:34:41+08:00"
draft: false
title: "初探 Python 列表 (List)"
tags:
  - Python
---

## 什麼是列表？

程式語言通常都會有**負責組織、儲存多筆資料**的資料型別。在 JavaScript 和 Golang 中，這種資料型別被稱為陣列 (array)，而 Python 則是列表 (list)。

Python 中的列表用 `[...]` 宣告，每項資料中間以半形逗號區隔：

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
```

> 上面的列表中清一色都是字串，但我們其實**可以在列表中加入各種型別的資料**。

若資料量持續增加，我們可以將每筆資料一行一行拆開，讓程式碼更容易閱讀。畢竟很多東西，不是越長就越好：

```python
friends = [
    "Cute Goblin",
    "Big Goblin",
    "Small Goblin",
    "Taipei Goblin"
]

goblin_age = [
    25,
    18,
    55
]
```

---

## 用索 (index) 提取列表中的資料

首先我們要知道**在程式的世界，通常都是從 0 開始計數**的，而非日常生活中直覺的 1。

列表中每一筆資料都有其索引 (index)，也就是該筆資料在列表中的位置。再提醒一次，務必要從 0 開始算起。

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
```

\
以上述列表為例，每筆資料的索引如下：

- 0：`Cute Goblin`
- 1：`Big Goblin`
- 2：`Small Goblin`
- 3：`Taipei Goblin`

再舉個例子，**索引 1 等於列表當中第二筆資料**。

我們可以運用`[索引]`來提取特定的列表資料：

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
print(friends[0])
# 列印出 "Cute Goblin"，因為我們輸入了 0 作為索引
```

## 計算列表長度

在 Python 中，我們能使用 `len(list_name)` 直接取得列表長度。

> 注意，別把「列表長度」和「列表中最後一筆資料的索引」混為一談了。由於索引是從 0 開始算起，所以「列表長度 + 1」才等於最後一筆資料的索引！

但相對來說，我們其實能利用上述兩者的關係，在不知道列表長度的情況下取得最後一筆資料的索引：

```python
def get_last_index(inventory):
    return len(inventory) - 1
```

---

## 更新列表資料

同樣運用索引，我們能夠更新列表中特定位置的資料。比方說以下就將 `Small Goblin` 更新為 `Baby Goblin`。

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
friends[0] = "Baby Goblin"
# friends: ["Cute Goblin", "Big Goblin", "Baby Goblin", "Taipei Goblin"]
```

---

## 將資料加入至列表、從列表移出

### append

append()` 方法，將資料加入至列表的最末端：

```python
teams = []
teams.append("Fubon Guardians")
teams.append("Uni Lions")

# teams = ["Fubon Guardians", "Uni Lions"]
```

\
實際上我們會時常建立空白的列表，然後透過迴圈和 `append()` 將資料加入至列表當中。比方說底下 `generate_user_list` 函式透過迴圈產生 `id`，然後在每次遞迴都將新產生的 `id` 加入至 `player_list`。

```python
def generate_user_list(num_of_users):
    player_ids = []

    for i in range(0, num_of_users):
        player_ids.append(i)

    return player_ids
```

### pop

`pop()` 的功能和 `append()` 相反，會**從列表最尾端移除資料，並回傳被移除的那筆資料**。

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
last_friend = friends.pop()

# friends = ["Cute Goblin", "Big Goblin", "Baby Goblin"]
# last_friend = "Taipei Goblin"
```

\
`pop()` 提供我們帶入參數，指定要將列表中哪個索引的資料移除。再次提醒，索引要從 0 開始算起。

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
removed_friend = friends.pop(2)

# friends = ["Cute Goblin", "Big Goblin", "Taipei Goblin"]
# removed_friend = " "Small Goblin""
```
