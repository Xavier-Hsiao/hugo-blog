---
date: "2025-01-20T22:30:06+08:00"
draft: false
title: "初探 Python 列表 (List) - 續"
tags:
  - Python
---

## 不靠索引也能提取列表資料

如果不需要更新列表中的資料，我們其實可以用更精簡的語法去遞迴列表。`in` 關鍵字負責宣告 `friend` 變數，儲存每一次遞迴所提取的列表資料：

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
for friend in friends:
    print(friend)

# Cute Goblin
# Big Goblin
# Small Goblin
# Taipei Goblin
```

\
這種簡潔的語法在尋找列表資料時尤其方便，因為我們只在乎列表的資料值，索引直接捨棄也不用在意，像極了哥布林的愛情：

```python
def contains_small_goblin(friends):
    found = False

    for friend in friends:
        if friend == "Small Goblin":
            found = True

    return found
```

---

## 尋找最大數

這算是個小技巧(?)，如果我們想從列表中找出最大數，可以先將初始值宣告為`float("-inf")`，這樣便能確保列表中每個數字都比它更大。接下來用遞迴陸續找出更大的數值，然後取代它就可以了。

```python
def find_max(nums):
    max_so_far = float("-inf")
    for num in nums:
        if num > max_so_far:
            max_so_far = num

    return max_so_far
```

\
同理，若是要找出最小數，將初始值變數宣告為`float("inf")`即可。

---

## 切割列表

我們可以用 `:` 切割出列表的特定區段，那回傳的會是一個新的列表。除了從哪裡開始、到哪裡結束之外，我們還能指定中間要跳過幾筆資料 (step)。

```python
my_list[ start : stop : step ]
```

\
舉個 🌰 :

```python
scores = [50, 70, 30, 20, 90, 10, 50]
print(scores[1:5:2])
# 列印出 [70, 20]
```

上述案例用中文翻譯：從索引 1 開始，切到索引 4 (不包含 5)，中間每 2 個位置跳過。

但其實**切割列表不一定要填滿三個條件**。比方說 `numbers[:3]` 代表「從頭開始切到索引 3，但不包含它」。而 `numbers[:3]` 則表示「從索引 3 開始切到尾端」。

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[:3] # [0, 1, 2]
numbers[3:] # [3, 4, 5, 6, 7, 8, 9]
```

雖然平常比較少看到，但也可以只帶入 `step`，也就是從頭切到尾，中間跳過 x 個位置。

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[::2] # [0, 2, 4, 6, 8]
```

&nbsp;

### 用負指數來切割列表

有時候我們會想**從尾端往前考慮要如何切割列表**，剛好 Python 提供了負指數滿足這個需求。舉例來說，`numbers[-1]` 會切出列表最後一筆資料，而 `numbers[-2]` 則切出倒數第二筆資料，以此類推。

負指數當然也能結合上述的切割運算式：

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[-3:] # [7, 8, 9]
```

---

## 合併列表

在 Python 合併列表超簡單，直接用 `+` 就好，我真的可以這麼幸福嗎？

```python
total = [1, 2, 3] + [4, 5, 6]
print(total)

# [1, 2, 3, 4, 5, 6]
```

---

## 查詢列表

別急，還有更幸福的。在 Python 查詢列表是否含有特定資料，直接用 `in` 關鍵字即可！回傳值為 `True` 或是 `False`。

```python
friends = ["Cute Goblin", "Big Goblin", "Small Goblin", "Taipei Goblin"]
print("Cute Goblin" in friends) # True
```

---

## 刪除列表中的資料

Python 提供了 `del` 關鍵字方便我們移除列表中的資料。我們只需要指定資料的索引位置，或是切割範圍即可。

> 注意，`del` 會直接更動 (mutate) 列表中的資料。

```python
# 第四筆資料被刪除
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

del nums[3]
print(nums)
# [1, 2, 3, 5, 6, 7, 8, 9]

# 從第二筆資料刪除到第三筆資料
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

del nums[1:3]
print(nums)
# [1, 4, 5, 6, 7, 8, 9]

# 刪除所有資料
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

del nums[:]
print(nums)
# []
```
