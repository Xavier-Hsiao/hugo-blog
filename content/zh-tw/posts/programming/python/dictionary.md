---
date: "2025-01-25T22:47:27+08:00"
draft: false
title: "初探 Python 字典 (Dictionary)"
tags:
  - Python
---

## 什麼是字典 (Dictionary)？

在 Python 中，字典用來儲存 `key -> value` 組合的資料，和 JavaScript 的物件 (objects) 非常類似。字典使用 `{}` 來包裹住資料，每個鍵 (key) 都會對應到一個值 (value)：

```python
goblin = {
    "name": "Xavier",
    "age": 28,
    "pet": "Mimiball"
}
```

---

## 不要重複 `key`

列表利用索引 (index) 來辨別資料，而字典則是依靠鍵 (key)。所以實作上我們**不應該在字典中重複使用 key**，如果不信邪，你會發現原先的值被覆寫過去了！

```python
goblin = {
    "name": "Xavier",
    "name": "Neo-Xavier"
    "age": 28,
    "pet": "Mimiball"
}
```

上面範例中，哥布林的名字從 `Xavier` 變成了 `Neo-Xavier`，因為兩筆資料的 key 都是 `name`，而後面的資料覆寫了前面一筆 key 相同的資料。

---

## 操作字典中的資料

基本上不脫離取、增、刪、變四大操作，下面逐一說明。

### 提取字典中的資料

使用 `[]` 來提取字典中的資料。前面提過字典是靠 key 來辨別每一筆資料，所以我們需要在 `[]` 帶入特定資料的 key，而且要用字串的方式帶入，也就是前後加上 `""`。

```python
goblin = {
    "name": "Xavier",
    "age": 28,
    "pet": "Mimiball"
}

print(goblin["name"])
```

### 新增字典資料

實務上我們常常會先建立一個空字典，然後依照商業邏輯陸續新增動態資料到字典中。而新增資料到字典的方式和提取資料大同小異，一樣使用 `[key_name]` 的模式即可。

```python
goblin = {}
goblin["name"] = "Xavier"
goblin["age"] = 28
goblin["single"] = True

print(f"{goblin["name"]} is {goblin["age"]}. Single? {goblin["single"]}")
```

### 更新字典資料

不廢話，一樣透過 `[key_name]` 來更新值。

```python
goblin = {
    "name": "Xavier"
}
goblin["name"] = "Mimiball"

```

### 刪除字典資料

和列表一樣，若要刪除資料的話，字典需使用 `del` 關鍵字。如果我們執意刪除不存在的資料，Python 編譯器會跳錯誤。

```python
goblins_dict = {
    "cute": "cute_goblin",
    "small": "small_goblin",
    "big": "big_goblin"
}

del goblins_dict["big"]

print(goblins_dict)
# Prints: {'cute': 'cute_goblin', 'small': 'small_goblin'}
```

### 遞迴字典

透過 `in` 關鍵字，我們可以輕鬆遞迴字典資料的 `key`，而透過 `key` 又可以提取該筆資料的值。另外，若想知道字典的長度，一樣可以使用 `len()`。

```python
def get_most_common_enemy(enemies_dict):
    # Return the name of the enemy with the highest count
    # If there are no enemies -> return None
    # If there are multiple enemies with the same count -> return the first one found

    highest_count_so_far = float("-inf")
    most_common_enemy = None

    if len(enemies_dict) == 0:
        return None

    for name in enemies_dict:
        count = enemies_dict[name]
        if count > highest_count_so_far:
            highest_count_so_far = enemies_dict[name]
            most_common_enemy = name

    return most_common_enemy
```
