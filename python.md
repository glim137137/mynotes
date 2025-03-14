# Python

[TOC]





# 1.字符串

所有对字符串的操作（如拼接、分割、替换、转换等）都会**创建并返回一个新的字符串对象**，而**不会修改原始字符串**。这是因为字符串在 Python 中是**不可变的（immutable）**。



## 1.1.字符串方法

1. **基本操作**
   - `str.upper()`：将字符串转换为大写。
   - `str.lower()`：将字符串转换为小写。
   - `str.capitalize()`：将字符串的首字母大写。
   - `str.title()`：将字符串中的每个单词的首字母大写。
   - `str.strip()`：移除字符串两端的空白字符。
2. **查找和替换**
   - `str.find(sub)`：查找子字符串 `sub` 的位置，如果未找到返回 `-1`。
   - `str.replace(old, new)`：将字符串中的 `old` 替换为 `new`。
   - `str.count(sub)`：返回子字符串 `sub` 在字符串中出现的次数。
3. **分割和连接**
   - `str.split(sep)`：将字符串按分隔符 `sep` 分割为列表。
   - `str.join(iterable)`：将可迭代对象中的字符串连接成一个字符串，使用指定的分隔符。
4. **格式化**
   - `str.format(*args, **kwargs)`：格式化字符串，可以插入变量。
   - `f"..."`：使用 f-string 语法格式化字符串（Python 3.6+）。
5. **检测**
   - `str.startswith(prefix)`：检查字符串是否以指定的前缀开始。
   - `str.endswith(suffix)`：检查字符串是否以指定的后缀结束。
   - `str.isdigit()`：检查字符串是否只包含数字字符。
   - `str.isalpha()`：检查字符串是否只包含字母字符。
   - `str.isalnum()`：检查字符串是否只包含字母和数字字符。





# 2.字典



## 2.1.字典方法

1. **基本操作**

   - `dict.clear()`：清空字典。
   - `dict.copy()`：返回字典的**浅复制**。
   - `dict.get(key, default=None)`：返回指定键的值，如果键不存在则返回默认值。
   - `dict.items()`：返回字典中所有键值对的**视图对象**。
   - `dict.keys()`：返回字典中所有键的**视图对象**。
   - `dict.values()`：返回字典中所有值的**视图对象**。

   #### 浅复制

   这意味着它创建了一个**新的字典对象**，但**新字典中的值仍然引用原始字典中的对象**。

   - **新字典**：`copy()` 方法返回的新字典与原始字典是两个不同的对象。你可以修改新字典而不会影响原始字典。
   - **引用相同**：如果字典的值是可变对象（如列表、字典等），那么新字典中的值仍然指向原始字典中的相同对象。因此，如果你修改这些可变对象，两个字典都会反映这个修改。

   **示例**

   ```python
   original = {'a': 1, 'b': [2, 3]}
   copy_dict = original.copy()
   
   # 修改新字典
   copy_dict['a'] = 10
   copy_dict['b'].append(4)
   
   print(original)  # 输出: {'a': 1, 'b': [2, 3, 4]}  (b的内容被修改了)
   print(copy_dict)  # 输出: {'a': 10, 'b': [2, 3, 4]}
   ```

   #### 视图对象

   视图对象是一个动态视图，提供了一种对字典内容的**实时访问方式**。

   1. **动态性**：视图对象反映了字典的当前状态。如果字典的内容发生变化（例如，添加、删除键值对），视图对象会立即更新，反映这些变化。
   2. **迭代性**：视图对象可以被迭代，你可以使用 `for` 循环遍历它来访问每个键值对。
   3. **不支持索引**：视图对象不像列表那样支持索引访问，它主要用于迭代和检查成员关系。

   **示例**

   ```python
   original = {'a': 1, 'b': 2}
   view = original.items()
   
   print(view)  # 输出: dict_items([('a', 1), ('b', 2)])
   
   # 修改字典
   original['c'] = 3
   
   print(view)  # 输出: dict_items([('a', 1), ('b', 2), ('c', 3)])
   
   # 遍历视图对象
   for key, value in view:
       print(key, value)
   ```

   

   

2. **查找和删除**

   - `dict.pop(key, default=None)`：删除指定键并返回其值，如果键不存在则返回默认值。
   - `dict.popitem()`：删除并返回字典中的最后一个键值对（Python 3.7+）。

3. **更新和合并**

   - `dict.update(other)`：用其他字典的键值对更新当前字典。

4. **其他操作**

   - `dict.setdefault(key, default=None)`：返回指定键的值，如果键不存在则插入键并赋值。





# 3.元组

所有对元组的操作（如查找、计数等）都会**返回新的结果**，而**不会修改原始元组**。这是因为元组在 Python 中是**不可变的（immutable）**。

1. **基本操作**
   - `tuple.count(item)`：返回元组中指定元素的出现次数。
   - `tuple.index(item)`：返回元组中第一个匹配元素的索引。
2. **切片和迭代**
   - 支持切片操作，如 `tuple[start:end:step]`。
   - 可以使用 `for` 循环遍历元组中的元素。
3. **连接与重复**
   - `tuple1 + tuple2`：将两个元组连接成一个新元组。
   - `tuple * n`：将元组重复 `n` 次，返回一个新元组。

# 4.列表

所有对列表的操作（如添加、删除、排序、查找等）都会**直接修改原始列表**，因为列表在 Python 中是**可变的（mutable）**。

## 4.1.列表方法

1. **基本操作**

   - `list.append(item)`：在列表末尾添加一个元素。
   - `list.extend(iterable)`：通过添加可迭代对象的所有元素来扩展列表。
   - `list.insert(index, item)`：在指定位置插入一个元素。
   - `list.remove(item)`：删除列表中第一个匹配的元素。
   - `list.pop(index)`：删除并返回指定位置的元素；如果不指定位置，默认删除最后一个元素。
   - `list.clear()`：清空列表中的所有元素。

2. **查找和计数**

   - `list.index(item)`：返回列表中第一个匹配元素的索引。
   - `list.count(item)`：返回列表中指定元素的出现次数。

3. **排序和反转**

   - `list.sort(reverse=False)`：就地对列表进行排序；可选参数 `reverse` 指定是否降序。
   - `list.reverse()`：就地反转列表的元素顺序。

4. **复制**

   - `list.copy()`：返回列表的**浅复制**。

5. **切片和迭代**

   -  `list[start:end:step]`：使用切片操作创建列表的**一个完整副本**。

   **示例**

   ```python
   # 示例列表
   my_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
   
   # 提取从索引 2 到 5 的元素
   sub_list1 = my_list[2:5]   # 输出: [2, 3, 4]
   
   # 提取从开头到索引 4 的元素
   sub_list2 = my_list[:4]    # 输出: [0, 1, 2, 3]
   
   # 提取从索引 5 到结尾的元素
   sub_list3 = my_list[5:]    # 输出: [5, 6, 7, 8, 9]
   
   # 使用步长提取每隔一个元素
   sub_list4 = my_list[::2]   # 输出: [0, 2, 4, 6, 8]
   
   # 反向切片
   sub_list5 = my_list[::-1]  # 输出: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
   
   # 创建**完整副本**
   copy_list = my_list[:]  # 输出: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
   ```

   - 可以使用 `for` 循环遍历列表中的元素。





# 5.集合

## 5.1.集合方法

1. **集合的创建**

- `set(iterable)`: 创建一个新的集合，可以从任何可迭代对象（如列表、元组、字符串等）中创建。

2. **添加和移除元素**

- `add(elem)`: 向集合中添加元素 `elem`。
- `remove(elem)`: 从集合中移除元素 `elem`，如果元素不存在会引发 `KeyError`。
- `discard(elem)`: 从集合中移除元素 `elem`，如果元素不存在不会引发错误。
- `pop()`: 随机移除并返回集合中的一个元素，如果集合为空则引发 `KeyError`。

3. **清空和复制**

- `clear()`: 清空集合中的所有元素。
- `copy()`: 返回集合的浅拷贝。

4. **集合运算**

- `union(other)`: 返回两个集合的并集。
- `intersection(other)`: 返回两个集合的交集。
- `difference(other)`: 返回当前集合与 `other` 集合的差集。
- `symmetric_difference(other)`: 返回两个集合的对称差集，即在其中一个集合中但不在两个集合交集中出现的元素。

5. **子集和超集测试**

- `issubset(other)`: 检查当前集合是否是 `other` 集合的子集。
- `issuperset(other)`: 检查当前集合是否是 `other` 集合的超集。

6. **集合运算符**

集合还支持一些操作符：

- `|`（并集）
- `&`（交集）
- `-`（差集）
- `^`（对称差集）





# 6.类

A ***class*类** allows us to group data (**attributes属性**) and methods (note that we call **methods方法** instead of functions here) together in a way that is easy to be reuse and build upon if needed.

```python
Class Student:
    pass
```



## 6.1.类的实例

A `class` is a blueprint for creating **instances**. For example, each unique student that we create using the `Student` class will be an instance of that class. In the following code snippet, we create two instances of `Student` class. Note that class instantiation uses the same function notation with **round brackets ()** after the name of the class.

```python
student_1 = Student()
student_2 = Student()
```



### 6.1.1.实例属性

```python
student_1.id = "scs00001"
student_1.name = "John Smith"
student_1.email = "johnsmith@university.com"

student_2.id = "scs00002"
student_2.name = "Mariah Susanti"
student_2.email = "msusanti@university.com"
```



### 6.1.2.实例方法

#### 实例方法

实例方法是定义在类中的普通方法，第一个参数通常是 `self`，它代表类的实例。通过 `self`，我们可以访问实例的属性和其他方法。

```python
class Dog:
    # 类属性
    species = "Canis lupus familiaris"

    # 初始化方法（构造函数）
    def __init__(self, name, age):
        self.name = name  # 实例属性
        self.age = age

    # 实例方法
    def bark(self):
        return "Woof!"

# 创建对象
my_dog = Dog("Buddy", 3)
print(my_dog.name)  # 输出: Buddy
print(my_dog.age)   # 输出: 3
print(my_dog.bark())  # 输出: Woof!

```



**类方法和实例方法区别**：

| 特点       | 实例方法                 | 类方法                         |
| ---------- | ------------------------ | ------------------------------ |
| 第一个参数 | `self`（实例）           | `cls`（类）                    |
| 访问属性   | 可以访问实例属性和类属性 | 只能访问类属性                 |
| 调用方式   | 必须通过实例调用         | 可以通过类或实例调用           |
| 装饰器     | 无需装饰器               | 需要使用 `@classmethod` 装饰器 |



#### 魔术方法 (特殊的实例方法)

魔术方法（Magic Methods），也称为特殊方法（Special Methods，因其双下划线前后而得名），是 Python 中一类具有特殊意义的方法。它们通常用于实现一些内置操作的自定义行为，比如对象的创建、比较、表示等。魔术方法通常以 `__` 开头和结尾。



以下是一些常用的魔术方法及其功能：

**1.1. 初始化和表示**

- `__init__(self, ...)`：构造方法，用于创建对象时初始化实例属性。
- `__str__(self)`：用于定义 `print()` 或 `str()` 调用时的对象字符串表示。
- `__repr__(self)`：用于定义 `repr()` 调用时的对象字符串表示，通常用于调试。

**示例**

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, {self.age} years old"

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("Alice", 30)
print(p)          # 输出: Alice, 30 years old
print(repr(p))   # 输出: Person('Alice', 30)
```



**1.2. 运算符重载**

- `__add__(self, other)`：定义 `+` 操作符。
- `__sub__(self, other)`：定义 `-` 操作符。
- `__mul__(self, other)`：定义 `*` 操作符。
- `__truediv__(self, other)`：定义 `/` 操作符。
- `__eq__(self, other)`：定义 `==` 操作符。
- `__lt__(self, other)`：定义 `< 或 >` 操作符。
- `__le__(self, other)`：定义 `<= 或 =>` 操作符。

**示例**

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(5, 7)
v3 = v1 + v2
print(v3)  # 输出: Vector(7, 10)
```



**1.3. 集合和序列**

- `__len__(self)`：定义 `len()` 函数。
- `__getitem__(self, key)`：定义索引操作（如 `obj[key]`）。
- `__setitem__(self, key, value)`：定义索引赋值操作（如 `obj[key] = value`）。

**示例**

```python
class CustomList:
    def __init__(self):
        self.items = []

    def __len__(self):
        return len(self.items)

    def __getitem__(self, index):
        return self.items[index]

    def __setitem__(self, index, value):
        self.items[index] = value

cl = CustomList()
cl.items = [1, 2, 3]
print(len(cl))         # 输出: 3
print(cl[1])           # 输出: 2
cl[1] = 20
print(cl.items)       # 输出: [1, 20, 3]
```



**1.4.迭代器**

- `__iter__(self)` ：返回一个迭代器对象。通常可以返回自身，因为自定义类也实现了 `__next__()` 方法。

- `__next__(self)` ：返回下一个值。当没有更多值可返回时，抛出 `StopIteration` 异常，告诉迭代器停止迭代。

**示例**

```python
class NumberSequence:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        # 返回迭代器对象（通常是自身）
        return self

    def __next__(self):
        if self.current < self.end:
            number = self.current
            self.current += 1
            return number
        else:
            raise StopIteration  # 结束迭代

# 示例用法
sequence = NumberSequence(1, 5)

for num in sequence:
    print(num)  # 输出: 1, 2, 3, 4

```



## 6.2.类变量

类变量是与类本身关联的变量，而不是与类的实例关联。它们被所有实例共享，通常用于存储与类相关的属性或状态，而不是特定于某个实例的属性。



```python
class Dog:
    # 类变量
    species = "Canis familiaris"

    def __init__(self, name, age):
        self.name = name  # 实例变量
        self.age = age    # 实例变量

# 创建实例
dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

# 访问类变量
print(dog1.species)  # 输出: Canis familiaris
print(dog2.species)  # 输出: Canis familiaris

# 修改类变量
Dog.species = "Canis lupus familiaris"

print(dog1.species)  # 输出: Canis lupus familiaris
print(dog2.species)  # 输出: Canis lupus familiaris

```

**说明**

1. **定义**：类变量在类体中定义，通常在 `__init__` 方法之外。
2. **访问**：可以通过类名或实例访问类变量。
3. **共享**：所有实例共享同一个类变量的值。如果修改类变量，所有实例都能看到更改后的值。
4. **与实例变量的区别**：实例变量是与特定对象实例相关的，每个实例有自己的副本，而类变量是所有实例共享的。



## 6.3.类方法

### 类方法

类方法是与类本身关联的方法，而不是与类的实例关联。它们通常用于操作类变量或执行与类相关的操作。类方法使用 `@classmethod` 装饰器定义，并且第一个参数通常命名为 `cls`，表示类本身。

```python
class Dog:
    species = "Canis familiaris"  # 类变量

    def __init__(self, name, age):
        self.name = name  # 实例变量
        self.age = age    # 实例变量

    @classmethod
    def get_species(cls):
        return cls.species  # 访问类变量

    @classmethod
    def set_species(cls, new_species):
        cls.species = new_species  # 修改类变量

# 使用类方法
print(Dog.get_species())  # 输出: Canis familiaris

# 修改类变量通过类方法
Dog.set_species("Canis lupus familiaris")
print(Dog.get_species())  # 输出: Canis lupus familiaris

```

**说明**

1. **定义**：使用 `@classmethod` 装饰器来定义类方法。
2. **第一个参数**：类方法的第一个参数是 `cls`，表示调用该方法的类。
3. **访问类变量**：可以在类方法中访问和修改类变量。
4. **通过类调用**：类方法可以通过类名直接调用，而不需要实例化对象。



### 静态方法

静态方法是与类关联的方法，但不与类的实例或类本身的状态直接相关。它们通常用于执行某些功能，但不需要访问类变量或实例变量。静态方法使用 `@staticmethod` 装饰器定义。

```python
class MathUtils:
    
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def multiply(a, b):
        return a * b

# 使用静态方法
result_add = MathUtils.add(5, 3)      # 输出: 8
result_multiply = MathUtils.multiply(5, 3)  # 输出: 15

print(result_add)      # 输出: 8
print(result_multiply) # 输出: 15

```

**说明**

1. **定义**：使用 `@staticmethod` 装饰器来定义静态方法。
2. **没有特定参数**：静态方法不需要 `self` 或 `cls` 参数，因为它们不依赖于类或实例的状态。
3. **调用方式**：可以通过类名直接调用，也可以通过实例调用，但通常通过类名调用更为清晰。

**应用场景**

- 静态方法通常用于逻辑独立于类或实例的方法，比如工具函数或帮助方法。



## 6.4.继承

继承是面向对象编程中的一个基本概念，它允许一个类（子类或派生类）继承另一个类（父类或基类）的属性和方法。这使得代码重用变得更加容易，同时也可以通过扩展父类的功能来实现更复杂的行为。

1. **父类（基类）**：被继承的类。
2. **子类（派生类）**：继承父类的类，可以增加新的属性和方法，也可以重写父类的方法。

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Some sound"

# Dog 类继承自 Animal 类, 方法重写
class Dog(Animal):
    def speak(self):
        return "Woof!"

# Cat 类继承自 Animal 类, 方法重写
class Cat(Animal):
    def speak(self):
        return "Meow!"

# 创建实例
dog = Dog("Buddy")
cat = Cat("Kitty")

# 调用方法
print(dog.name)       # 输出: Buddy
print(dog.speak())    # 输出: Woof!

print(cat.name)       # 输出: Kitty
print(cat.speak())     # 输出: Meow!

```

**说明**

1. **构造函数**：子类会继承父类的构造函数，但如果需要，可以在子类中重写构造函数。
2. **方法重写**：子类可以重写父类的方法，以实现特定的功能。
3. **多层继承**：子类还可以作为其他类的父类，形成多层继承结构。



# 7.文件操作

## 1. 文件打开与关闭

- **`open(filename, mode)`**: 打开一个文件并返回文件对象。

  | Mode | Meaning                                                      |
  | ---- | ------------------------------------------------------------ |
  | `r`  | open for reading (default)                                   |
  | `w`  | open for writing, truncating the file first                  |
  | `a`  | open for writing, appending to the end of the file ifit exists |
  | `b`  | binary mode 二进制文件                                       |
  | `t`  | text mode (default) 纯文本文件                               |
  | `+`  | open a disk file for updating (reading and writing)          |

  ```python
  # Create a new file object
  fileObject = open("my_newfile", "w")
  
  # Write a string to the file
  fileObject.write("This string will be written to the file.\n")
  
  # Close the file
  fileObject.close()
  ```

- **`file.close()`**: 关闭文件，释放资源。

  

## 2. 读取文件

- **`file.read(size)`**: 读取指定大小的内容，如果未指定，默认读取整个文件。
- **`file.readline()`**: 用于从文件中读取一行数据。每次调用 `readline()`，它会返回文件的下一行（str），包括行末的换行符（如果存在）。
- **`file.readlines()`**: 读取文件的所有行，返回一个列表。
- **`file.readable()`**: 检查文件是否可读。

## 3. 写入文件

- **`file.write(string)`**: 将字符串写入文件。
- **`file.writelines(lines)`**: 将字符串列表写入文件。
- **`file.writable()`**: 检查文件是否可写。

## 4. 文件指针

- **`file.tell()`**: 返回当前文件指针的位置。
- **`file.seek(offset, whence)`**: 移动文件指针到指定位置。

## 5. 文件属性

- **`file.flush()`**: 刷新文件的内部缓冲区，将数据写入文件。

## 6. 使用上下文管理器

- **`with open(...) as file:`**: 使用 `with` 语句可以自动管理文件的打开和关闭。

- **`with as`** ：用于简化资源管理，通常与上下文管理器一起使用，以确保在使用完资源后正确地清理它们（例如，文件）。`as` 关键字用于为上下文管理器指定一个别名。

  ```python
  # 使用 with 语句打开一个文件，并在读取完内容后自动关闭文件.
  with open('example.txt', 'r') as file:
      content = file.read()  # 读取文件内容
  
  # 文件在此处自动关闭，无需手动调用 file.close()
  print(content)
  
  ```

  **解释**

  1. **`as file`**：将打开的文件对象赋值给变量 `file`，你可以通过这个变量访问文件内容。
  2. **`with` 的作用**：当代码块结束时，无论是否发生异常，文件都会自动关闭。

## 7. 文件异常处理

- **`try` / `except`**: 用于处理文件操作中的异常（如文件未找到等）。

```python
try:
    # 尝试打开文件
    with open('data.txt', 'r') as file:
        content = file.read()
        print(content)

except FileNotFoundError:
    print("错误：文件未找到。请检查文件名和路径。")
except PermissionError:
    print("错误：没有权限访问该文件。")
except IOError:
    print("错误：发生了输入/输出错误。")
except Exception as e:
    print(f"发生了未知错误：{e}")

```



## 8.CSV文件

### 1. 读取 CSV 文件

下面是一个读取 CSV 文件的基本示例：

```python
import csv

# 读取 CSV 文件
with open('data.csv', 'r', newline='') as csvfile:
    reader = csv.reader(csvfile)
    for row in reader:
        print(row)  # 打印每一行
```

### 2. 写入 CSV 文件

下面是一个将数据写入 CSV 文件的示例：

```python
import csv

# 要写入的数据
data = [
    ['Name', 'Age', 'City'],
    ['Alice', 30, 'New York'],
    ['Bob', 25, 'Los Angeles'],
]

# 写入 CSV 文件
with open('output.csv', 'w', newline='') as csvfile:
    writer = csv.writer(csvfile)
    
    writer.writerows(data)  # 写入多行数据
    
    for row in data:
        writer.writerow(data)
```

### 3. 使用字典读写

`csv.DictReader` 和 `csv.DictWriter` 允许你以字典的形式处理 CSV 数据：

```python
import csv

# 读取 CSV 文件为字典
with open('data.csv', 'r', newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        print(row['Name'], row['Age'])  # 按列名访问数据

# 写入字典到 CSV 文件
with open('output.csv', 'w', newline='') as csvfile:
    fieldnames = ['Name', 'Age', 'City']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()  # 写入表头
    writer.writerow({'Name': 'Alice', 'Age': 30, 'City': 'New York'})
```

**重要参数**

- **`delimiter`**：定义分隔符，默认为逗号 `,`。
- **`quotechar`**：定义用于引用字段的字符，默认为 `"`。
- **`newline=''`**：在打开文件时，建议使用此参数以避免多余的空行。

# 8.特殊函数



## isinstance()

`isinstance` 是 Python 中的一个内置函数，用于检查一个对象是否是指定类或类元组的实例。它

**语法**：

```python
isinstance(object, classinfo)
```

- **参数**
  - **object**: 你想要检查的对象。
  - **classinfo**: 一个类、类型，或一个包含多个类和类型的元组。
- **返回值**
  - 布尔值，返回 `True` 如果对象是该类（或其子类）的实例，否则返回 `False`。



## map()





## round()

`round()` 是 Python 中的一个内置函数，用于对浮点数进行四舍五入。它可以接受两个参数：

1. **number**：要四舍五入的数字。
2. **ndigits**（可选）：要保留的小数位数。如果省略，默认会四舍五入到整数。



```python
print(round(3.6))  # 输出: 4
print(round(3.4))  # 输出: 3

print(round(3.14159, 2))  # 输出: 3.14
print(round(2.675, 2))     # 输出: 2.67（结果是 2.67 而不是 2.68，这是因为浮点数的精度问题）

print(round(1234.5678, -2))  # 输出: 1200

```



## all()

`all()`是一个内置函数，用于检查可迭代对象（如列表、元组、集合或字典）中的所有元素是否都为 `True`。如果所有元素都为 `True`，则 `all()` 函数返回 `True`。如果可迭代对象为空，则 `all()` 返回 `True`。



```python
# 所有元素都为 True
print(all([True, 1, 'hello']))  # 输出：True

# 任何一个元素为 False
print(all([True, 0, 'hello']))  # 输出：False

# 空的可迭代对象
print(all([]))                 # 输出：True

# 检查列表中的所有数字是否都小于 10
numbers = [1, 2, 3, 4, 5]
print(all(number < 10 for number in numbers))  # 输出：True

# 检查列表中的所有数字是否都小于 5
numbers = [1, 2, 3, 10, 5]
print(all(number < 5 for number in numbers))  # 输出：False
```



## enumerate()

枚举`enumerate()` 是 Python 中的一个内置函数，允许你在遍历可迭代对象（如列表或元组）时，跟踪当前项的索引。它返回一个迭代器，该迭代器生成索引和相应项目的元组。

**语法**

```python
enumerate(iterable, start=0)
```

- **iterable**: 你想要迭代的集合（例如列表、元组）。
- **start**: 起始索引（默认值为 0）。

**示例**

以下是一个简单的示例，演示 `enumerate()` 的用法：

```python
fruits = ['苹果', '香蕉', '樱桃']

for index, fruit in enumerate(fruits):
    print(index, fruit)

# 输出：
# 0 苹果
# 1 香蕉
# 2 樱桃
```



# 9.库

## random

### 1.生成随机数

- 生成一个**随机浮点数**（范围在 [0.0, 1.0)）：

  ```python
  random_float = random.random()
  ```

- 生成一个**指定范围内的随机整数**：

  ```python
  random_int = random.randint(a, b)  # 包含 a 和 b
  ```

- 生成一个**指定范围内的随机浮点数**：

  ```python
  random_uniform = random.uniform(a, b)  # 包含 a，不包含 b
  ```

### 2.随机选择

- 从列表中随机选择**一个元素**：

  ```python
  random_choice = random.choice(['apple', 'banana', 'cherry'])
  ```

- 从列表中随机选择**多个元素**（**不重复**）：

  ```python
  random_sample = random.sample(['apple', 'banana', 'cherry'], k=2)
  ```

- 从列表中随机选择**多个元素**（**可能重复**）：

  ```python
  random_choices = random.choices(['apple', 'banana', 'cherry'], k=3)
  ```

### 3.洗牌

- **随机打乱一个列表**：

  ```python
  my_list = [1, 2, 3, 4, 5]
  random.shuffle(my_list)
  ```

### 4.设置随机种子

通过设置随机种子，您可以确保在调试或测试过程中每次运行程序时生成相同的随机数序列：

```python
random.seed(a)  # a 是种子值

# 生成一些随机数
print(random.randint(1, 100))  # 结果会是相同的
print(random.randint(1, 100))  # 每次运行的输出将相同
```





# 10.注意事项



## 可变类型不可变类型

- **不可变类型**：`str`、`tuple`、`int`、`float`、`bool`、`frozenset`
- **可变类型**：`list`、`dict`、`set`



# 11.关键字

## nonlocal
