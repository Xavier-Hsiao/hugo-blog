---
date: "2025-02-16T13:09:10+08:00"
draft: false
title: "哥布林學 Python 物件導向 (OOP)"
description: "透過 Python 學習封裝、抽象化、繼承、多型等物件導向概念"
categories:
  - 程式學習
tags:
  - Python
  - 電腦科學
---

**物件導向 (OOP)** 是一種程式設計的規範 (paradigm)，遵循之後有助於寫出更容易管理、容易維護，且容易閱讀的程式碼。而 Python 本身借鏡了許多 OOP 的概念，雖然沒有像 Java 那樣嚴格，但諸如 `flask`、`Pygame` 等等熱門框架也以 OOP 為主旋律，多去了解絕對不吃虧。

## 一切都由物件組成

OOP 的核心概念其實很簡單，那就是將我們日常生活中的人事物「建模」成一個一個又一個的物件，而每個物件當中會包含：

- 屬性 (attribute)：類似於字典 (dictionary) 的 key-value 資料
- 方法 (method)：函式，沒錯，就是函式

舉個例子，假設我們用一個物件來代表「人」這個概念，那該物件裡面可能會有以下屬性：

- 姓名
- 年齡
- 住址
- 興趣
- 職業

除此之外，該物件也會包含人的**行為**，這些行為便是所謂的方法，所以物件將包含以下函式：

- 走路
- 跑步
- 吃飯
- 嗚啦

---

### 先有藍圖，才有物件

> 想像你是全知全能的天神，某日心血來潮想為世界增添趣味，於是決定創造名為哥布林的生物，讓他們~~自生自滅~~繁衍生息。你給自己泡了杯咖啡，創造了一隻、兩隻、三隻哥布林，漸漸發現如此單調重複的工作 **超 . 級 . 無 . 聊**，於是靈機一動，先打造了一套哥布林模型，注入神力讓模型依照既定規則自動生成哥布林......

這基本上就是我們建立物件的方式。Python 透過 `class` 關鍵字讓我們先產出**物件的藍圖**，後續依循藍圖去建立單一物件。所以物件的屬性、方法都要在 `class` 當中先定義好。

```python
class Goblin:
  health = 5
  damage = 3

Xavier = Goblin()
print(Xavier.health) # 5
```

&nbsp;

可以注意到若要從物件中提取屬性值，語法為 `<object_name>.<attribute>`。

相較於 `class` 是物件的藍圖，我們依據藍圖所生成的物件則是 `instance`，實體。真實的資料會包裹在實體中。

---

### 為物件增添函式 - method

前面提過綁定在 `class` 當中的函式被稱之為方法。方法和一般函式最大的差異，在於它能夠直接存取該物件的屬性。

```python
class Goblin:
  health = 5

  def take_damage(self, damage):
    self.health -= damage

Xavier = Goblin()
# Xaiver 會被帶入成 `take_damage` 方法的第一個參數 (self)
Xavier.take_damage(2)
print(Xavier.health) # 3
```

方法的第一個參數永遠都是呼叫 `class` 的物件實體本身。其實這個參數要叫什麼名字都可以，Python 是依照參數位置區別，但慣例上使用 [`self`](https://app.heptabase.com/45a73641-738c-418c-ab35-9f2954232222/card/618f10df-56df-4f30-942c-e34ee8b29b2a) 這個名稱，淺顯易懂。

換個說法，`self` 是指向到物件實體的參數，我們需要使用它來讀取或更新 `class` 裡面所定義的屬性值。因此物件中的方法比起一般函式，比較少去回傳資料，而是直接修改資料。但方法一樣可以回傳資料的喔。

看到這裡我們發現了一個大問題，目前 `class` 的屬性都是固定值，比方說 `health = 5`，造成每個建立出來的物件實體屬性值都相同，但每隻哥布林的健康狀況理當不一樣才對。有沒有辦法把屬性值當作參數，在建立物件實體的時候丟進去生成呢？

---

### `__init__` 建構方法

既然方法都能透過 `self` 參數來存取屬性了，我們不妨也在 `class` 建立一個方法來為屬性賦值。

Python 其實提供了 `__init__()` 這個特殊函式，負責為物件實體屬性賦值。當我們建立新的物件實體，Python 便會自動去呼叫 `__init__()`，省去了我們手動為每個物件賦值的苦勞，可謂懶人救星。

```python
class Goblin:
  def __init__(self, name, health, damage):
    self.name = name + "Goby" # Computed prop!
    self.health = health
    self.damage = damage

# Xaiver will be passed into the '__init__'
# method as the first argument (self)
Xavier = Goblin("Xavier", 5, 10)
print(Xavier.name) # XaiverGoby
print(Xaviier.health) # 5
print(Xavier.damage) # 10
```

&nbsp;

我們一樣在 `__init__()` 帶入 `self` 參數，代表物件實體本身。接著陸續帶入其他屬性參數，完成賦值即可。當然如果有些屬性是透過其他屬性計算出來的，也直接在 `__init__()` 中定義。

但這又引發了另一個問題，如果某些屬性就剛好是每個物件實體都相同，該怎麼辦？只能在建立物件時重複帶入參數嗎？

---

### 實體變數 vs. class 變數

前面我們都是透過 `self` 來宣告變數，由於 `self` 代表物件實體本身，因此這些綁定 `self` 的變數，自然而然會跟著物件實體。

倘若我們是在 `class` 的範圍內宣告變數，而非 `__int__()` 建構方法的話，該變數在不同的物件實體仍會保持相同值。不過還是能以 `<class_name.<attribute>` 來變更變數值。

```python
class Bear:
    mood = "happy"  # This is a class variable

    def change_mood(self, new_mood):
        self.mood = new_mood  # This creates an instance variable

# Create two bear instances
bear1 = Bear()
bear2 = Bear()

# Access the class variable
print(Bear.mood)  # "happy"
print(bear1.mood)  # "happy"

# Modify using the instance
bear1.change_mood("grumpy")

# Now:
print(bear1.mood)  # "grumpy" (instance variable)
print(Bear.mood)  # "happy" (class variable still unchanged)
print(bear2.mood)  # "happy" (still uses the class variable)
```

---

## 封裝與抽象化

OOP 這種將屬性和行為包裹在一個物件當中的設計模式，背後蘊含了兩大原則：

- **封裝 (encapsulation)**：將相關的公開 (public) 和隱私 (private) 資料包成一個群組
- **抽象化 (abstraction)**：將複雜的邏輯藏起來，提供簡易使用的介面 (interface)。我們只需要知道車子怎麼開，不用理解引擎如何運作。

兩者乍看之下非常相似，而事實上封裝和抽象化的確只是著重面向不同而已。

> 因為有封裝，我們才能夠實現抽象化！

這邊也值得注意，封裝所提到的公開和隱私資料，和我們一般認知中 _個資、密碼、機敏資料_ 的資安概念不太一樣。封裝的意義在於更有效地管理程式碼，而非讓系統儲存的資料更加安全。在這層含義上，我們可以將封裝想像成未上鎖的檔案櫃，裡面的資料夾排列得井井有條，但知道檔案櫃所在位置的人都能自由查找資料。

唉，不對啊，如果是這樣，那還分什麼公開和隱私資料？

再想像一下，假設今天有甲、乙兩個開發團隊協作。甲團隊設計了一組 API，方便自己和乙團隊開發對應功能。如果乙團隊當中有人無心或刻意要攪亂一池春水，隨便亂調整背後邏輯的變數或函式，那大家就準備一起包包收拾滾回家去了。

因此在一般開發協作，甚或函式庫開源的情境下，我們需要將資料分成公開、隱私變數，以免天下秩序大亂。

接著底下會紀錄 Python 如何實現公開、隱私變數。爆個雷，不外乎兩個字：**信任**。

---

### 公開與隱私，一場信任所建立的遊戲

預設上所有在 `class` 宣告的屬性和方法都是公開的。也就是說任何人用 `.` 運算子即可提取資料。

你可能會想說，只要在屬性或方法前面加上 `private` 或 `non-public` 之類的關鍵字，資料就會神奇地貼上隱私標籤對吧？

我以前也是這麼以為的，但可惜事情沒有想像中那麼簡單。

由於 Python 是動態語言 (dynamic language)，且由直譯器 (interpreter) 逐行執行程式碼，因此**不會在執行前強制檢查變數的存取權限**，這使得 Python 無法像 Golang、Rust 等靜態語言那樣，透過編譯 (compilation) 時的機制來嚴格限制屬性的可視性。

因此 **Python 很吃重開發者之間[約定俗成的慣例，也就是命名方式](https://app.heptabase.com/45a73641-738c-418c-ab35-9f2954232222/card/22afa5e2-fa7d-45b4-949f-9eb4012d7a85)**來實現資料公開與隱私。

&nbsp;

### 用下底線 `_` 來搭建信任的橋樑吧

我們用以下範例來看看 Python 所謂的「慣例」長什麼模樣：

```python
class User:
    def __init__(self, name):
        self._name = name  # Convention: "this should be private"
        self.__password = "secret"  # Name mangling, not true private

user = User("Xavier")
print(user._name)  # Allowed, but conventionally discouraged
print(user.__password)  # AttributeError
print(user._User__password)  # Bypasses name mangling!
```

**單一下底線 `_`**：

- 純慣例，代表該屬性或方法僅供 `class` 內使用。
- 注意這只是慣例，所以就算在 `class` 外部仍舊能夠提取資料。

**雙底線 `__`**：

- 除了慣例之外，雙底線還會觸發 `name mangling`，也就是 Python 會自動改變該屬性、方法的名稱。
- 由於名稱被更改了，所以能預防該屬性、方法被刻意繼承到其他子 `class` 當中。
- 名稱更改的模式並非秘密，就是多加上 `class` 名稱罷了，所以能[施以小計提取資料](https://app.heptabase.com/45a73641-738c-418c-ab35-9f2954232222/card/22afa5e2-fa7d-45b4-949f-9eb4012d7a85)。

額外加映～**前後雙底線 `__keyword__`**：

- 這些是 Python 內建的*特殊方法*，像是常用的 `__repr__`、`__init__`等等。

雙底線是滿常見的隱私命名方式，如果希望其他子 `class` 繼承，可以改用單底線，或是保留雙底線然後建立 `get_something()` 之類的 getter 方法。總歸一句話，一切都源自於信任兩個字，所以和團隊或合作對象是先溝通清楚才為上策。
