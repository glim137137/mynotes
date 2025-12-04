# Python

文章参考：[Python3 教程 | 菜鸟教程](https://www.runoob.com/python3/python3-tutorial.html)

[TOC]

# 介绍

Python 是一门易于学习、功能强大的编程语言。它提供了高效的高级数据结构，还能简单有效地面向对象编程。Python 优雅的语法和动态类型以及解释型语言的本质，使它成为多数平台上写脚本和快速开发应用的理想语言。

Python 解释器易于扩展，使用 C 或 C++（或其他 C 能调用的语言）即可为 Python 扩展新功能和数据类型。Python 也可用作定制软件中的扩展程序语言。

# 基本语法



## 标准数据类型

Python3 中常见的数据类型有：

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。
- **序列（3个）**：String（字符串）、List（列表）、Tuple（元组）。

此外还有一些高级的数据类型，如: 字节数组类型(bytes)。



### 数字 Number

Python3 支持 **int、float、bool、complex（复数）**。

| 数据类型   | 关键字    | 大小 (字节) | 默认值  | 取值范围                     | 包装类    | 示例              |
| :--------- | :-------- | :---------- | :------ | :--------------------------- | :-------- | :---------------- |
| **整型**   | `int`     | 动态        | `0`     | 任意大小（受限于内存）       | `int`     | `i = 100000`      |
| **浮点型** | `float`   | 动态        | `0.0`   | 双精度浮点数（约 ±1.7e+308） | `float`   | `f = 3.14159`     |
| **布尔型** | `bool`    | 动态        | `False` | `True` 或 `False`            | `bool`    | `is_valid = True` |
| **复数型** | `complex` | 动态        | `0j`    | 实部和虚部均为浮点数         | `complex` | `c = 3 + 4j`      |

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 `Long`。

像大多数语言一样，数值类型的赋值和计算都是很直观的。

内置的 `type()` 函数可以用来查询变量所指的对象类型。

```python
>>> a = 111
>>> isinstance(a, int)
True
>>>
```

此外还可以用 `isinstance` 来判断：

```python
>>> a = 111
>>> isinstance(a, int)
True
>>>
```

`isinstance` 和 `type` 的区别在于：

- type()不会认为子类是一种父类类型。
- isinstance()会认为子类是一种父类类型。

```python
>>> class A:
...     pass
... 
>>> class B(A):
...     pass
... 
>>> isinstance(A(), A)
True
>>> type(A()) == A 
True
>>> isinstance(B(), A)
True
>>> type(B()) == A
False
```

> 注意：Python3 中，`bool` 是 `int` 的子类，True 和 False 可以和数字相加，`True==1、False==0` *会返回* True，但可以通过 `is` 来判断类型。
>
> ```python
> >>> issubclass(bool, int) 
> True
> >>> True==1
> True
> >>> False==0
> True
> >>> True+1
> 2
> >>> False+1
> 1
> >>> 1 is True
> <python-input-12>:1: SyntaxWarning: "is" with 'int' literal. Did you mean "=="?
>   1 is True
> False
> >>> 0 is False
> <python-input-13>:1: SyntaxWarning: "is" with 'int' literal. Did you mean "=="?
>   0 is False
> False
> 
> ```
>
> 什么会出现 `SyntaxWarning`？
>
> Python 检测到你在用 `is` 比较一个字面量整数（如 1）和 True，这通常是代码错误（因为 `is` 比较的是**身份**，即比较两个变量是否指向内存中的同一个对象，而不是值）。
>
> Python 建议你使用 `==` 来比较值是否相等，除非你确实想检查是否是同一个对象。
>



#### 布尔

**bool（布尔类型）**即 True 或 False。

在 Python 中，True 和 False 都是关键字，表示布尔值。

布尔类型特点：

- 布尔类型只有两个值：True 和 False。

- bool 是 int 的子类，因此**布尔值可以被看作整数来使用**，其中 True 等价于 1。

- 布尔类型可以和其他数据类型进行比较，比如数字、字符串等。在比较时，Python 会将 True 视为 1，False 视为 0。

- 布尔类型可以和逻辑运算符一起使用，包括 and、or 和 not。这些运算符可以用来组合多个布尔表达式，生成一个新的布尔值。

- 布尔类型也可以被转换成其他数据类型，比如整数、浮点数和字符串。

- 可以使用 `bool()` 函数**将其他类型的值转换为布尔值**。

    以下值在转换为布尔值时为 `False`：`None`、`False`、零 (`0`、`0.0`、`0j`)、空序列（如 `''`、`()`、`[]`）和空映射（如 `{}`）。其他所有值转换为布尔值时均为 `True`。





### 字符串 String

**String（字符串）**用单引号 `'` 或双引号 `"` 括起来，同时使用反斜杠 `\` 转义特殊字符。

字符串的截取`str[start:end]`，加号 **+** 是字符串的连接符， 星号 ***** 表示复制当前字符串，与之结合的数字为复制的次数。实例如下：

```python
str = 'Runoob'  # 定义一个字符串变量

print(str)           # 打印整个字符串
print(str[0:-1])     # 打印字符串第一个到倒数第二个字符（不包含倒数第一个字符）Runoo
print(str[0])        # 打印字符串的第一个字符
print(str[2:5])      # 打印字符串第三到第五个字符（不包含索引为 5 的字符）noo
print(str[2:])       # 打印字符串从第三个字符开始到末尾
print(str * 2)       # 打印字符串两次
print(str + "TEST")  # 打印字符串和"TEST"拼接在一起
```

所有对字符串的操作（如拼接、分割、替换、转换等）都会**创建并返回一个新的字符串对象**，而**不会修改原始字符串**。这是因为字符串在 Python 中是**不可变的（immutable）**。

```python
str = 'Runoob'
print("原始字符串:", str)

# 尝试修改字符串的第一个字符
try:
    str[0] = 'r'
except TypeError as e:
    print("尝试修改字符串的第一个字符时发生错误:", e)

str.replace('o', 'a')
print("修改后:", str) # Runoob

str = str[2:5]
print("修改并赋值后:", str) # noo
```

#### 转义字符

在需要在字符中使用特殊字符时，python 用反斜杠转义字符。如下表：

| 转义字符 | 描述                 | 示例                      |
| -------- | -------------------- | ------------------------- |
| `\n`     | 换行符               | `"Hello\nWorld"`          |
| `\t`     | 制表符（水平制表符） | `"Name:\tKimi"`           |
| `\\`     | 反斜杠               | `"Path: C:\\Users\\Kimi"` |
| `\'`     | 单引号               | `"It\'s a good day"`      |
| `\"`     | 双引号               | `"She said \"Hello\""`    |
| `\b`     | 退格符               | `"Hello\bWorld"`          |
| `\r`     | 回车符               | `"Hello\rWorld"`          |
| `\f`     | 换页符               | `"Page 1\fPage 2"`        |
| `\v`     | 垂直制表符           | `"Line 1\vLine 2"`        |
| `\ooo`   | 八进制数表示的字符   | `"\101"`（表示字符 `A`）  |
| `\xhh`   | 十六进制数表示的字符 | `"\x41"`（表示字符 `A`）  |



#### 格式化

Python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。

在 Python 中，字符串格式化使用与 C 中 sprintf 函数一样的语法。

```python
name = "Kimi"
age = 30
# python2
print("Hello, %s. You are %d years old." % (name, age))

# python3
print("Hello, {}. You are {} years old.".format(name, age))

# python3.6
print(f"Next year, {name} will be {age + 1} years old.")
```

python字符串格式化符号:

| 符  号 | 描述                                 |
| :----- | :----------------------------------- |
| %c     | 格式化字符及其ASCII码                |
| %s     | 格式化字符串                         |
| %d     | 格式化整数                           |
| %u     | 格式化无符号整型                     |
| %o     | 格式化无符号八进制数                 |
| %x     | 格式化无符号十六进制数               |
| %X     | 格式化无符号十六进制数（大写）       |
| %f     | 格式化浮点数字，可指定小数点后的精度 |
| %e     | 用科学计数法格式化浮点数             |
| %E     | 作用同%e，用科学计数法格式化浮点数   |
| %g     | %f和%e的简写                         |
| %G     | %f 和 %E 的简写                      |
| %p     | 用十六进制数格式化变量的地址         |

### 列表 List

**List（列表）** 是 Python 中使用最频繁的数据类型。

列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。

![img](images/list_slicing1_new1.png)

和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。

列表截取`list[start:end:step]`，加号 `+` 是列表连接运算符，星号 `*` 是重复操作。

```python
list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]  # 定义一个列表
tinylist = [123, 'runoob']

print (list)            # 打印整个列表
print (list[0])         # 打印列表的第一个元素
print (list[1:3])       # 打印列表第二到第四个元素（不包含第四个元素）
print (list[2:])        # 打印列表从第三个元素开始到末尾
print (tinylist * 2)    # 打印tinylist列表两次 [123, 'runoob', 123, 'runoob']
print (list + tinylist)  # 打印两个列表拼接在一起的结果
print(list[::2])   # 步长为2截取 ['abcd', 2.23, 70.2]
```

与Python字符串不一样的是，列表中的元素是可以改变的。



### 元组 Tuple

**元组（tuple）**与列表类似，不同之处在于元组的元素不能修改。元组写在小括号 `()` 里，元素之间用逗号隔开。

```python
>>> tup = (1, 2, 3, 4, 5, 6)
>>> print(tup[0])
1
>>> print(tup[1:5])
(2, 3, 4, 5)
>>> tup[0] = 11  # 修改元组元素的操作是非法的
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>>
```

元组与字符串类似，可以被索引且下标索引从0开始，-1 为从末尾开始的位置。也可以进行截取（看上面，这里不再赘述）。其实，可以**把字符串看作一种特殊的元组**。

虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。

如果你想创建只有**一个元素的元组**，需要注意在元素后面添加一个逗号，以区分它是一个元组而不是一个普通的值，这是因为在没有逗号的情况下，Python会将括号解释为数学运算中的括号，而不是元组的表示。

```python
tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```



### 集合 Set

**集合（Set）**是一种无序、可变的数据类型，用于存储唯一的元素。

集合中的元素不会重复，并且可以进行交集、并集、差集等常见的集合操作。

在 Python 中，集合使用大括号 **`{}`** 表示，元素之间用逗号 **,** 分隔。另外，也可以使用 **set(`)`** 函数创建集合。

> **注意：**创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。



### 字典 Dictionary

**字典（dictionary）**是Python中另一个非常有用的内置数据类型。

列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。

字典是一种映射类型，字典用 **{ }** 标识，它是一个无序的 **键(key) : 值(value)** 的集合。

键(key)必须使用不可变类型。

在同一个字典中，键(key)必须是唯一的。

```python
dict = {}
dict['one'] = "1 - 菜鸟教程"
dict[2]     = "2 - 菜鸟工具"

tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}

print (dict['one'])       # 输出键为 'one' 的值
print (dict[2])           # 输出键为 2 的值
print (tinydict)          # 输出完整的字典
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值
```

构造函数 dict() 可以直接从键值对序列中构建字典如下：

```python
>>> dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
>>> dict(Runoob=1, Google=2, Taobao=3)
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
```



### 数据类型转换

有时候，我们需要对数据内置的类型进行转换，数据类型的转换，一般情况下你只需要将数据类型作为函数名即可。

Python 数据类型转换可以分为两种：

- 隐式类型转换 - 自动完成
- 显式类型转换 - 需要使用类型函数来转换

#### 隐式类型转换

在隐式类型转换中，Python 会自动将一种数据类型转换为另一种数据类型，不需要我们去干预。

以下实例中，我们对两种不同类型的数据进行运算，较低数据类型（整数）就会转换为较高数据类型（浮点数）以避免数据丢失。

```python
num_int = 123
num_flo = 1.23

num_new = num_int + num_flo

print("num_int 数据类型为:",type(num_int))
print("num_flo 数据类型为:",type(num_flo))

print("num_new 值为:",num_new)
print("num_new 数据类型为:",type(num_new))
```

但是，整型和字符串类型运算结果会报错，输出 `TypeError`。

#### 显式类型转换

在显式类型转换中，用户将对象的数据类型转换为所需的数据类型。 我们使用 `int()`、`float()`、`str()` 等预定义函数来执行显式类型转换。

`int()` 强制转换为整型：

```python
num_int = 123
num_str = "456"

print("num_int 数据类型为:",type(num_int))
print("类型转换前，num_str 数据类型为:",type(num_str))

num_str = int(num_str)    # 强制转换为整型
print("类型转换后，num_str 数据类型为:",type(num_str))

num_sum = num_int + num_str

print("num_int 与 num_str 相加结果为:",num_sum)
print("sum 数据类型为:",type(num_sum))
```

以下几个内置的函数可以执行数据类型之间的转换。这些函数返回一个新的对象，表示转换的值。

| 函数                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| int(x [,base\])](https://www.runoob.com/python3/python-func-int.html) | 将x转换为一个整数                                   |
| [float(x)](https://www.runoob.com/python3/python-func-float.html) | 将x转换到一个浮点数                                 |
| complex(real [,imag\])](https://www.runoob.com/python3/python-func-complex.html) | 创建一个复数                                        |
| [str(x)](https://www.runoob.com/python3/python-func-str.html) | 将对象 x 转换为字符串                               |
| [repr(x)](https://www.runoob.com/python3/python-func-repr.html) | 将对象 x 转换为表达式字符串                         |
| [eval(str)](https://www.runoob.com/python3/python-func-eval.html) | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| [tuple(s)](https://www.runoob.com/python3/python3-func-tuple.html) | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |



## 运算符



### 算术运算符

以下假设变量 **a=10**，变量 **b=21**：

| 运算符 | 描述                                            | 实例                      |
| :----- | :---------------------------------------------- | :------------------------ |
| +      | 加 - 两个对象相加                               | a + b 输出结果 31         |
| -      | 减 - 得到负数或是一个数减去另一个数             | a - b 输出结果 -11        |
| *      | 乘 - 两个数相乘或是返回一个被重复若干次的字符串 | a * b 输出结果 210        |
| /      | 除 - x 除以 y                                   | b / a 输出结果 2.1        |
| %      | 取模 - 返回除法的余数                           | b % a 输出结果 1          |
| **     | 幂 - 返回x的y次幂                               | a**b 为10的21次方         |
| //     | 取整除 - 往小的方向取整数                       | `>>> 9//2 4 >>> -9//2 -5` |

### 比较运算符

以下假设变量 a 为 10，变量 b 为20：

| 运算符 | 描述                                                         | 实例                  |
| :----- | :----------------------------------------------------------- | :-------------------- |
| ==     | 等于 - 比较对象是否相等                                      | (a == b) 返回 False。 |
| !=     | 不等于 - 比较两个对象是否不相等                              | (a != b) 返回 True。  |
| >      | 大于 - 返回x是否大于y                                        | (a > b) 返回 False。  |
| <      | 小于 - 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。 | (a < b) 返回 True。   |
| >=     | 大于等于 - 返回x是否大于等于y。                              | (a >= b) 返回 False。 |
| <=     | 小于等于 - 返回x是否小于等于y。                              | (a <= b) 返回 True。  |



### 赋值运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| =      | 简单的赋值运算符                                             | c = a + b 将 a + b 的运算结果赋值为 c                        |
| +=     | 加法赋值运算符                                               | c += a 等效于 c = c + a                                      |
| -=     | 减法赋值运算符                                               | c -= a 等效于 c = c - a                                      |
| *=     | 乘法赋值运算符                                               | c *= a 等效于 c = c * a                                      |
| /=     | 除法赋值运算符                                               | c /= a 等效于 c = c / a                                      |
| %=     | 取模赋值运算符                                               | c %= a 等效于 c = c % a                                      |
| **=    | 幂赋值运算符                                                 | c **= a 等效于 c = c ** a                                    |
| //=    | 取整除赋值运算符                                             | c //= a 等效于 c = c // a                                    |
| :=     | 海象运算符，这个运算符的主要目的是在表达式中同时进行赋值和返回赋值的值。**Python3.8 版本新增运算符**。 | 在这个示例中，赋值表达式可以避免调用 len() 两次:```if (n := len(a)) > 10:    print(f"List is too long ({n} elements, expected <= 10)")``` |



### 位运算符

按位运算符是把数字看作二进制来进行计算的。

下表中变量 a 为 60，b 为 13二进制格式如下：

```
a = 0011 1100

b = 0000 1101

-----------------

a&b = 0000 1100

a|b = 0011 1101

a^b = 0011 0001

~a  = 1100 0011
```

| 运算符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| &      | 按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0 | (a & b) 输出结果 12 ，二进制解释： 0000 1100                 |
| \|     | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。 | (a \| b) 输出结果 61 ，二进制解释： 0011 1101                |
| ^      | 按位异或运算符：当两对应的二进位相异时，结果为1              | (a ^ b) 输出结果 49 ，二进制解释： 0011 0001                 |
| ~      | 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1。**~x** 类似于 **-x-1** | (~a ) 输出结果 -61 ，二进制解释： 1100 0011， 在一个有符号二进制数的补码形式。 |
| <<     | 左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 | a << 2 输出结果 240 ，二进制解释： 1111 0000                 |
| >>     | 右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数 | a >> 2 输出结果 15 ，二进制解释： 0000 1111                  |

### 逻辑运算符

Python语言支持逻辑运算符，以下假设变量 a 为 10, b为 20:

| 运算符 | 逻辑表达式 | 描述                                                         | 实例                    |
| :----- | :--------- | :----------------------------------------------------------- | :---------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 x 的值，否则返回 y 的计算值。 | (a and b) 返回 20。     |
| or     | x or y     | 布尔"或" - 如果 x 是 True，它返回 x 的值，否则它返回 y 的计算值。 | (a or b) 返回 10。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not(a and b) 返回 False |

### 成员运算符

除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。

| 运算符 | 描述                                                    | 实例                                              |
| :----- | :------------------------------------------------------ | :------------------------------------------------ |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False。     | x 在 y 序列中 , 如果 x 在 y 序列中返回 True。     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 | x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。 |

### 身份运算符

身份运算符用于比较两个对象的存储单元

| 运算符 | 描述                                        | 实例                                                         |
| :----- | :------------------------------------------ | :----------------------------------------------------------- |
| is     | is 是判断两个标识符是不是引用自一个对象     | **x is y**, 类似 **id(x) == id(y)** , 如果引用的是同一个对象则返回 True，否则返回 False |
| is not | is not 是判断两个标识符是不是引用自不同对象 | **x is not y** ， 类似 **id(x) != id(y)**。如果引用的不是同一个对象则返回结果 True，否则返回 False。 |

> **注：** [id()](https://www.runoob.com/python/python-func-id.html) 函数用于获取对象内存地址。



### 优先级

and 拥有更高优先级。

```python
x = True
y = False
z = False
 
print("情况1：默认优先级（先算and）")
if x or y and z:  # 等同于 x or (y and z)
    print("yes")  # 会输出
else:
    print("no")
 
print("\n情况2：强制改变优先级（先算or）")
if (x or y) and z:  # 人为添加括号改变顺序
    print("yes")  # 不会输出
else:
    print("no")  # 会输出
```



## 控制语句

### if 语句

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

### match...case

Python 3.10 增加了 **match...case** 的条件判断，不需要再使用一连串的 **if-else** 来判断了。

match 后的对象会依次与 case 后的内容进行匹配，如果匹配成功，则执行匹配到的表达式，否则直接跳过，**_** 可以匹配一切。

语法格式如下：

```python
match subject:
    case pattern_1:
        action_1
    case pattern_2:
        action_2
    case pattern_3:
        action_3
    case _:
        action_wildcard
```

**`case _`:** 类似于 C 和 Java 中的 **default:**，当其他 case 都无法匹配时，匹配这条，保证永远会匹配成功。

### while 循环

```python
n = 100
 
sum = 0
counter = 1
while counter <= n:
    sum = sum + counter
    counter += 1
 
print("1 到 %d 之和为: %d" % (n,sum))
```

#### while 循环使用 else 语句

如果 while 后面的条件语句为 false 时，则执行 else 的语句块。

语法格式如下：

```python
count = 0
while count < 5:
   print (count, " 小于 5")
   count = count + 1
else:
   print (count, " 大于或等于 5")
```

执行以上脚本，输出结果如下：

```
0  小于 5
1  小于 5
2  小于 5
3  小于 5
4  小于 5
5  大于或等于 5
```

### for 语句

```python
#  1 到 5 的所有数字：
for number in range(1, 6):
    print(number)
```

#### for...else

在 Python 中，for...else 语句用于在循环结束后执行一段代码。

语法格式如下：

```python
for item in iterable:
    # 循环主体
else:
    # 循环结束后执行的代码
```

### break continue pass 语句

![img](images/break-continue-536.png)

pass是空语句，是为了保持程序结构的完整性。pass 不做任何事情，一般用做占位语句，如下实例，

```python
for letter in 'Runoob': 
   if letter == 'o':
      pass
      print ('执行 pass 块')
   print ('当前字母 :', letter)
 
print ("Good bye!")
```



## 函数

```python
def printme( str ):
   "打印传入的字符串到标准显示设备上"
   print str
   return
```

### 参数传递

python 函数的参数传递：

- **不可变类型：**类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。
- **可变类型：**类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响

python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

```python
def ChangeInt( a ):
    a = 10
 
b = 2
ChangeInt(b)
print b # 结果是 2

def changeme( mylist ):
   "修改传入的列表"
   mylist.append([1,2,3,4])
   print "函数内取值: ", mylist
   return
 
# 调用changeme函数
mylist = [10,20,30]
changeme( mylist )
print "函数外取值: ", mylist
```

### 参数

以下是调用函数时可使用的正式参数类型：

- 必备参数
- 关键字参数
- 默认参数
- 不定长参数

#### 必备参数

必备参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样。

```python
#可写函数说明
def printme( str ):
   "打印任何传入的字符串"
   print str
   return
 
#调用printme函数
printme()

"""
Traceback (most recent call last):
  File "test.py", line 11, in <module>
    printme()
TypeError: printme() takes exactly 1 argument (0 given)

"""
```

#### 关键字参数

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。

使用关键字参数**允许函数调用时参数的顺序与声明时不一致**，因为 Python 解释器能够用参数名匹配参数值。

以下实例在函数 printme() 调用时使用参数名：

```python
def printme( str ):
   "打印任何传入的字符串"
   print str
   return
 
#调用printme函数
printme( str = "My string")
```

#### 默认参数

调用函数时，默认参数的值如果没有传入，则被认为是默认值。下例会打印默认的age，如果age没有被传入：

```python
def printinfo( name, age = 35 ):
   "打印任何传入的字符串"
   print "Name: ", name
   print "Age ", age
   return
 
#调用printinfo函数
printinfo( age=50, name="miki" )
printinfo( name="miki" )
```

#### 不定长参数

你可能需要一个函数能处理比当初声明时更多的参数。这些参数叫做不定长参数，和上述2种参数不同，声明时不会命名。基本语法如下：

```python
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print "输出: "
   print arg1
   for var in vartuple:
      print var
   return
 
# 调用printinfo 函数
printinfo( 10 )
printinfo( 70, 60, 50 )
```

##### `*args`（位置参数）

`*args` 用于接收**任意数量的位置参数**，并将它们作为一个元组存储。

```python
def my_function(*args):
    for arg in args:
        print(arg)

my_function(1, 2, 3, "hello")
```

##### `**kwargs`（关键字参数）

`**kwargs` 用于接收**任意数量的关键字参数**，并将它们作为一个字典存储。

```python
def my_function(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

my_function(a=1, b=2, name="Alice")
```

##### 解包

在函数调用时，也可以使用 `*args` 和 `**kwargs` 来解包参数。

```python
def my_function(a, b, c):
    print(f"a: {a}, b: {b}, c: {c}")

args = (1, 2)
kwargs = {"c": 3}

my_function(*args, **kwargs)
```



### 匿名函数 lambda

python 使用 lambda 来创建匿名函数。

- lambda只是一个表达式，函数体比def简单很多。
- lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
- lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
- 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

```python
sum = lambda arg1, arg2: arg1 + arg2

# 调用sum函数
print "相加后的值为 : ", sum( 10, 20 )
print "相加后的值为 : ", sum( 20, 20 )
```

- **参数**：可以有零个或多个参数。
- **表达式**：一个表达式，该表达式的值作为函数的返回值。



## 异常处理

捕捉异常可以使用try/except语句。

try/except语句用来检测try语句块中的错误，从而让except语句捕获异常信息并处理。

如果你不想在异常发生时结束你的程序，只需在try里捕获它。

```python
try:
    fh = open("testfile", "w")
    fh.write("这是一个测试文件，用于测试异常!!")
except IOError:
    print "Error: 没有找到文件或读取文件失败"
else:
    print "内容写入文件成功"
    fh.close()
```

### 使用except而不带任何异常类型

```python
try:
    # 正常的操作
    # ......................
except:
    # 发生异常，执行这块代码
    # ......................
else:
    # 如果没有异常执行这块代码

```

### try-finally 语句

```python
try:
    fh = open("testfile", "w")
    try:
        fh.write("这是一个测试文件，用于测试异常!!")
    finally:
        print "关闭文件"
        fh.close()
except IOError:
    print "Error: 没有找到文件或读取文件失败"
```

### 抛出异常

我们可以使用`raise`语句自己触发异常

raise语法格式如下：

```
raise [Exception [, args [, traceback]]]
```

语句中 Exception 是异常的类型（例如，NameError）参数标准异常中任一种，args 是自已提供的异常参数。

最后一个参数是可选的（在实践中很少使用），如果存在，是跟踪异常对象。

```python
def mye( level ):
    if lev
        raise Exception,"Invalid level!"
        # 触发异常后，后面的代码就不会再执行
try:
    mye(0)            # 触发异常
except Exception,err:
    print 1,err
else:
    print 2
```

### 用户自定义异常

通过创建一个新的异常类，程序可以命名它们自己的异常。异常应该是典型的继承自Exception类，通过直接或间接的方式。

以下为与RuntimeError相关的实例,实例中创建了一个类，基类为RuntimeError，用于在异常触发时输出更多的信息。

在try语句块中，用户自定义的异常后执行except块语句，变量 e 是用于创建Networkerror类的实例。

```python
class Networkerror(RuntimeError):
    def __init__(self, arg):
        self.args = arg
```

在你定义以上类后，你可以触发该异常，如下所示：

```python
try:
    raise Networkerror("Bad hostname")
except Networkerror,e:
    print e.args
```

### `assert` 断言

Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。

断言可以在条件不满足程序运行的情况下直接返回错误，而不必等待程序运行后出现崩溃的情况。

例如我们的代码只能在 Linux 系统下运行，可以先判断当前系统是否符合条件。

```python
import sys
assert ('linux' in sys.platform), "该代码只能在 Linux 下执行"

# 接下来要执行的代码
```





# 高级语法



## 面向对象

和其它编程语言相比，Python 在尽可能不增加新的语法和语义的情况下加入了类机制。

Python中的类提供了面向对象编程的所有基本功能：

1. 类的继承机制允许多个基类，
2. 派生类可以覆盖基类中的任何方法，
3. 方法中可以调用基类中的同名方法。

### 类

语法格式如下：

```python
class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>
```

### 对象

类对象支持两种操作：**属性引用**和**实例化**。

```python
class MyClass:
    """一个简单的类实例"""
    i = 12345
    def f(self):
        return 'hello world'
 
# 实例化类
x = MyClass()
 
# 访问类的属性和方法
print("MyClass 类的属性 i 为：", x.i)
print("MyClass 类的方法 f 输出为：", x.f())
```

### 构造方法

类有一个名为 __init__() 的特殊方法（**构造方法**），该方法在类实例化时会自动调用：

```python
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
```

#### self 代表类的实例，而非类

类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的**第一个参数名称**, 按照惯例它的名称是 self。

```python
class Test:
    def prt(self):
        print(self)
        print(self.__class__)
 
t = Test()
t.prt()
# <__main__.Test instance at 0x100771878>
# __main__.Test
```

从执行结果可以很明显的看出，self 代表的是类的实例，代表当前对象的地址，而 self.class 则指向类。

`self` 不是 python 关键字，我们把他换成 runoob 也是可以正常执行的:

```python
class Test:
    def prt(runoob):
        print(runoob)
        print(runoob.__class__)
 
t = Test()
t.prt()
```

#### 子类继承父类构造函数

如果在子类中需要父类的构造方法就需要显式地调用父类的构造方法，或者不重写父类的构造方法。

- 子类不重写 **__init__**，实例化子类时，会自动调用父类定义的 **__init__**。

- 如果重写了**__init__** 时，实例化子类，就不会调用父类已经定义的 **__init__**
- 如果重写了**__init__** 时，要继承父类的构造方法，可以使用 **super** 关键字

```python
class Father(object):
    def __init__(self, name):
        self.name=name
        print ( "name: %s" %( self.name))
    def getName(self):
        return 'Father ' + self.name
 
class Son(Father):
    def __init__(self, name):
        super(Son, self).__init__(name)
        print ("hi")
        self.name =  name
    def getName(self):
        return 'Son '+self.name
 
if __name__=='__main__':
    son=Son('runoob')
    print ( son.getName() )
    
"""
name: runoob
hi
Son runoob
"""
```

### 方法成员

在类的内部，使用 **def** 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self, 且为第一个参数，self 代表的是类的实例。

### 继承

子类（派生类 DerivedClassName）会继承父类（基类 BaseClassName）的属性和方法。

```python
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
#单继承示例
class student(people):
    grade = ''
    def __init__(self,n,a,w,g):
        #调用父类的构函
        people.__init__(self,n,a,w)
        self.grade = g
    #覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级"%(self.name,self.age,self.grade))
 
 
 
s = student('ken',10,60,3)
s.speak()
```

#### 多继承

Python同样有限的支持多继承形式。多继承的类定义形如下例:

需要注意圆括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，python从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法

```python
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
#单继承示例
class student(people):
    grade = ''
    def __init__(self,n,a,w,g):
        #调用父类的构函
        people.__init__(self,n,a,w)
        self.grade = g
    #覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级"%(self.name,self.age,self.grade))
 
#另一个类，多继承之前的准备
class speaker():
    topic = ''
    name = ''
    def __init__(self,n,t):
        self.name = n
        self.topic = t
    def speak(self):
        print("我叫 %s，我是一个演说家，我演讲的主题是 %s"%(self.name,self.topic))
 
#多继承
class sample(speaker,student):
    a =''
    def __init__(self,n,a,w,g,t):
        student.__init__(self,n,a,w,g)
        speaker.__init__(self,n,t)
 
test = sample("Tim",25,80,4,"Python")
test.speak()   #方法名同，默认调用的是在括号中参数位置排前父类的方法

# 输出：我叫 Tim，我是一个演说家，我演讲的主题是 Python
```

### 方法重写

如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法，实例如下：

```python
class Parent:        # 定义父类
   def myMethod(self):
      print ('调用父类方法')
 
class Child(Parent): # 定义子类
   def myMethod(self):
      print ('调用子类方法')
 
c = Child()          # 子类实例
c.myMethod()         # 子类调用重写方法
super(Child,c).myMethod() #用子类对象调用父类已被覆盖的方法
```

> [super() 函数](https://www.runoob.com/python/python-func-super.html)是用于调用父类(超类)的一个方法。

### 私有属性与方法

两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。

两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。

```python
#!/usr/bin/python3
 
class Site:
    def __init__(self, name, url):
        self.name = name       # public
        self.__url = url   # private
 
    def who(self):
        print('name  : ', self.name)
        print('url : ', self.__url) # 内部访问私有属性
 
    def __foo(self):          # 私有方法
        print('这是私有方法')
 
    def foo(self):            # 公共方法
        print('这是公共方法')
        self.__foo()
 
x = Site('菜鸟教程', 'www.runoob.com')
x.who()        # 正常输出
x.foo()        # 正常输出
x.__foo()      # 报错
```







## 推导式

Python 推导式是一种独特的数据处理方式，可以从一个数据序列构建另一个新的数据序列的结构体。

Python 推导式是一种强大且简洁的语法，适用于生成列表、字典、集合和生成器。

在使用推导式时，需要注意可读性，尽量保持表达式简洁，以免影响代码的可读性和可维护性。

Python 支持各种数据结构的推导式：

- 列表(list)推导式
- 字典(dict)推导式
- 集合(set)推导式
- 元组(tuple)推导式

### 列表推导式

列表推导式格式为：

```python
[表达式 for 迭代变量 in 可迭代对象]
[表达式 for 迭代变量 in 可迭代对象 if 条件]
```

如，过滤掉长度小于或等于3的字符串列表，并将剩下的转换成大写字母：

```python
names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
new_names = [name.upper()for name in names if len(name)>3]
print(new_names)
# ['ALICE', 'JERRY', 'WENDY', 'SMITH']
```

### 字典推导式

字典推导基本格式：

```python
{键表达式: 值表达式 for 迭代变量 in 可迭代对象}
{键表达式: 值表达式 for 迭代变量 in 可迭代对象 if 条件}
```

如，使用字符串及其长度创建字典：

```python
listdemo = ['Google','Runoob', 'Taobao']
# 将列表中各字符串值为键，各字符串的长度为值，组成键值对
newdict = {key:len(key) for key in listdemo}
print(newdict)
{'Google': 6, 'Runoob': 6, 'Taobao': 6}
```

### 集合推导式

集合推导基本格式：

```python
{表达式 for 迭代变量 in 可迭代对象}
{表达式 for 迭代变量 in 可迭代对象 if 条件}
```

从一个列表中提取所有唯一的元素。

```python
numbers = [1, 2, 2, 3, 4, 4, 5]
unique_numbers = {num for num in numbers}
print(unique_numbers)
# {1, 2, 3, 4, 5}
```

### 元组推导式（生成器表达式）

生成器表达式基本格式：

```python
(表达式 for 迭代变量 in 可迭代对象)
(表达式 for 迭代变量 in 可迭代对象 if 条件)
```

元组推导式和列表推导式的用法也完全相同，只是元组推导式是用 **()** 圆括号将各部分括起来，而列表推导式用的是中括号 **[]**，另外元组推导式返回的结果是一个生成器对象。

例如，我们可以使用下面的代码生成一个包含数字 1~9 的元组：

```python
>>> a = (x for x in range(1,10))
>>> a
<generator object <genexpr> at 0x7faf6ee20a50> # 返回的是生成器对象

>>> tuple(a)    # 使用 tuple() 函数，可以直接将生成器对象转换成元组
(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

## 迭代器与生成器

### 迭代器 Iterator

迭代是 Python 最强大的功能之一，是访问集合元素的一种方式。

迭代器是一个可以**记住遍历的位置的对象**。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。**迭代器只能往前不会后退**。

迭代器有两个基本的方法：**iter()** 和 **next()**。

字符串，列表或元组对象都可用于创建迭代器：

```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
>>>
```

迭代器对象可以使用常规for语句进行遍历，

```python
list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
for x in it:
    print (x, end=" ") # end关键字
# 1 2 3 4
```



### 生成器 Generator

在 Python 中，使用了 **yield** 的函数被称为生成器（generator）。

**yield** 是一个关键字，用于定义生成器函数，生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果。

跟普通函数不同的是，**生成器是一个返回迭代器的函数**，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

> 当在生成器函数中使用 **yield** 语句时，函数的执行将会暂停，并将 **yield** 后面的表达式作为当前迭代的值返回。
>
> 然后，每次调用生成器的 **next()** 方法或使用 **for** 循环进行迭代时，函数会从上次暂停的地方继续执行，直到再次遇到 **yield** 语句。这样，生成器函数可以逐步产生值，而不需要一次性计算并返回所有结果。

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1
 
# 创建生成器对象
generator = countdown(5)
 
# 通过迭代生成器获取值
print(next(generator))  # 输出: 5
print(next(generator))  # 输出: 4
print(next(generator))  # 输出: 3
 
# 使用 for 循环迭代生成器
for value in generator:
    print(value)  # 输出: 2 1
```



## 装饰器

装饰器是一种非常强大且灵活的工具，它允许用户在不修改原始函数代码的情况下，为函数添加新的功能。

装饰器本质上是一个函数，它接收一个函数作为参数，并返回一个新的函数。

### 语法

装饰器的语法形式为：
```python
@decorator_name
def function_to_be_decorated():
    pass
```
这等价于：
```python
function_to_be_decorated = decorator_name(function_to_be_decorated)
```

### 简单装饰器示例
下面是一个简单的装饰器示例，用来记录函数的调用时间：
```python
import time

def time_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Function {func.__name__} took {end_time - start_time:.4f} seconds to execute.")
        return result
    return wrapper

@time_decorator
def example_function():
    time.sleep(2)  # 模拟耗时操作

example_function()
```
在这个例子中，`time_decorator` 是一个装饰器，它接收一个函数 `func`，并返回一个新的函数 `wrapper`。`wrapper` 函数在调用 `func` 之前和之后分别记录时间，并计算执行时间。

### 带参数的装饰器
如果装饰器需要接收参数，可以再嵌套一层函数。例如，一个装饰器可以根据参数决定是否记录函数的调用时间：
```python
import time

def conditional_time_decorator(should_time):
    def decorator(func):
        def wrapper(*args, **kwargs):
            if should_time:
                start_time = time.time()
                result = func(*args, **kwargs)
                end_time = time.time()
                print(f"Function {func.__name__} took {end_time - start_time:.4f} seconds to execute.")
            else:
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@conditional_time_decorator(should_time=True)
def example_function():
    time.sleep(2)

example_function()
```

### 注意事项
- **保持函数的元信息**：在装饰器中，原始函数的元信息（如函数名、文档字符串等）会被覆盖。为了避免这种情况，可以使用 `functools.wraps` 装饰器：
  ```python
  import functools
  
  def time_decorator(func):
      @functools.wraps(func)
      def wrapper(*args, **kwargs):
          start_time = time.time()
          result = func(*args, **kwargs)
          end_time = time.time()
          print(f"Function {func.__name__} took {end_time - start_time:.4f} seconds to execute.")
          return result
      return wrapper
  ```

- **装饰器的顺序**：如果一个函数被多个装饰器装饰，装饰器的执行顺序是从最近的装饰器开始，依次向外执行。例如：
  ```python
  @decorator1
  @decorator2
  def function():
      pass
  ```
  这等价于：
  ```python
  function = decorator1(decorator2(function))
  ```

装饰器是 Python 中一个非常实用的特性，它可以让代码更加简洁和模块化，同时也可以方便地为函数添加额外的功能。



## 命名空间 & 作用域

### 命名空间

**命名空间(Namespace)**是从名称到对象的映射，大部分的命名空间都是通过 Python 字典来实现的。

> *A namespace is a mapping from names to objects.Most namespaces are currently implemented as Python dictionaries。*

命名空间提供了在项目中避免名字冲突的一种方法。各个命名空间是独立的，没有任何关系的，所以一个命名空间中不能有重名，但不同的命名空间是可以重名而没有任何影响。

一般有三种命名空间：

- **内置名称（built-in names**）， **Python 语言内置的名称**，比如函数名 abs、char 和异常名称 BaseException、Exception 等等。
- **全局名称（global names）**，**模块中定义的名称**，记录了模块的变量，包括函数、类、其它导入的模块、模块级的变量和常量。
- **局部名称（local names）**，**函数中定义的名称**，记录了函数的变量，包括函数的参数和局部定义的变量。（类中定义的也是）

![img](images/types_namespace-1.png)

Python 的查找顺序为：**局部的命名空间 -> 全局命名空间 -> 内置命名空间**。

如下图所示，相同的对象名称可以存在于多个命名空间中。

![img](images/namespaces.png)

### 作用域

**作用域**就是一个 Python 程序可以直接访问命名空间的正文区域。

> *A scope is a textual region of a Python program where a namespace is directly accessible. "Directly accessible" here means that an unqualified reference to a name attempts to find the name in the namespace.*

Python 的作用域一共有 4 种，分别是：

- **L（Local）**：最内层，包含局部变量，比如一个函数/方法内部。
- **E（Enclosing）**：包含了非局部(non-local)也非全局(non-global)的变量。比如两个嵌套函数，一个函数（或类） A 里面又包含了一个函数 B ，那么对于 B 中的名称来说 A 中的作用域就为 nonlocal。
- **G（Global）**：当前脚本的最外层，比如当前模块的全局变量。
- **B（Built-in）**： 包含了内建的变量/关键字等，最后被搜索。

**LEGB 规则**（Local, Enclosing, Global, Built-in）：Python 查找变量时的顺序是： **L –> E –> G –> B**。

在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内置中找。

```python
g_count = 0  # 全局作用域
def outer():
    o_count = 1  # 闭包函数外的函数中
    def inner():
        i_count = 2  # 局部作用域
```

内置作用域是通过一个名为 builtin 的标准模块来实现的，但是这个变量名自身并没有放入内置作用域内，所以必须导入这个文件才能够使用它。

```python
>>> import builtins
>>> dir(builtins)
```

### global 和 nonlocal 关键字



```python
num = 1

def to2():
	num = 2 # 独立的，与前面定义的无关
    print(num)

def to3():
    global num  # 需要使用 global 关键字声明
    num = 3
    print(num)
    
to2()
print(num)

to3()
print(num)
```

如果要修改嵌套作用域（enclosing 作用域，外层非全局作用域）中的变量则需要 nonlocal 关键字了，如下实例，

```python
def outer():
    num = 10
    def inner():
        nonlocal num   # nonlocal关键字声明
        num = 100
        print(num)
    inner()
    print(num)
outer()

"""
100
100
"""
```







## 模块 & 包

如果你从 Python 解释器退出再进入，那么你定义的所有的方法和变量就都消失了。

为此 Python 提供了一个办法，把这些定义存放在文件中，为一些脚本或者交互式的解释器实例使用，这个**文件被称为模块**。

Python 中的模块（Module）是一个包含 Python 定义和语句的文件，文件名就是模块名加上 **.py** 后缀。

模块可以包含函数、类、变量以及可执行的代码。通过模块，我们可以将代码组织成可重用的单元，便于管理和维护。

```python
import sys
 
print('命令行参数如下:')
for i in sys.argv:
   print(i)
 
print('\n\nPython 路径为：', sys.path, '\n')
```

- `import sys` 引入 python 标准库中的 `sys.py` 模块；这是引入某一模块的方法。
- `sys.argv` 是一个包含命令行参数的列表。
- `sys.path` 包含了一个 Python 解释器自动查找所需模块的路径的列表。

### 搜索路径

1. **当前工作目录**：即 Python 脚本被运行时的目录。
2. **PYTHONPATH 环境变量**：通过设置 `PYTHONPATH` 环境变量，可以指定额外的模块搜索路径。
3. **标准库路径**：包括 Python 的内置模块和标准库。
4. **第三方库路径**：通常位于 `site-packages` 目录下。
5. **.pth 文件**：在 `site-packages` 目录下，可以通过 `.pth` 文件指定额外的模块搜索路径。

### from … import 语句

Python 的 from 语句让你从模块中导入一个指定的部分到当前命名空间中

```python
>>> from fibo import fib, fib2
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

这个声明不会把整个fibo模块导入到当前的命名空间中，它只会将fibo里的fib函数引入进来。

### `__name__` 属性

一个模块被另一个程序第一次引入时，其主程序将运行。

如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用 **`__name__`** 属性来使该程序块仅在该模块自身运行时执行。

```python
# Filename: using_name.py

if __name__ == '__main__':
   print('程序自身在运行')
else:
   print('我来自另一模块')
```

运行输出如下：

```bash
$ python using_name.py
程序自身在运行
```

```bash
$ python
>>> import using_name
我来自另一模块
>>>
```

**说明：每个模块都有一个 __name__ 属性。**

- 如果模块是被直接运行，`__name__` 的值为 `__main__`。
- 如果模块是被导入的，`__name__` 的值为模块名。

### dir() 函数

内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回:

```python
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
```

如果没有给定参数，那么 dir() 函数会罗列出当前定义的所有名称，

```python
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir() # 得到一个当前模块中定义的属性列表
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
>>> a = 5 # 建立一个新的变量 'a'
>>> dir()
['__builtins__', '__doc__', '__name__', 'a', 'sys']
>>>
>>> del a # 删除变量名a
>>>
>>> dir()
['__builtins__', '__doc__', '__name__', 'sys']
>>>
```

### 标准模块

| 模块名        | 功能描述                                    |
| :------------ | :------------------------------------------ |
| `math`        | 数学运算（如平方根、三角函数等）            |
| `os`          | 操作系统相关功能（如文件、目录操作）        |
| `sys`         | 系统相关的参数和函数                        |
| `random`      | 生成随机数                                  |
| `datetime`    | 处理日期和时间                              |
| `json`        | 处理 JSON 数据                              |
| `re`          | 正则表达式操作                              |
| `collections` | 提供额外的数据结构（如 defaultdict、deque） |
| `itertools`   | 提供迭代器工具                              |
| `functools`   | 高阶函数工具（如 reduce、lru_cache）        |

### 包

包是一种组织和管理模块的方式，它允许将相关的模块组织在一起，形成一个层次化的结构。使用包可以避免命名冲突，并且可以方便地管理大型项目。

包本质上是一个包含 `__init__.py` 文件的目录。`__init__.py` 文件可以为空，也可以包含初始化代码。从 Python 3.3 开始，`__init__.py` 文件不再是必需的，但为了兼容性和清晰性，建议仍然使用它。

**目录结构**

```python
my_package/
    __init__.py
    module1.py
    module2.py
```

导入整个包

```python
import my_package
```

**这会执行 `my_package/__init__.py` 文件中的代码。**

导入包中的模块

```python
import my_package.module1
import my_package.module2

my_package.module1.func1()
my_package.module2.func2()
```

从包中导入特定的函数或类

```python
from my_package.module1 import func1
from my_package.module2 import func2

func1()
func2()
```



## 类型注解

类型注解就是在代码中注明数据类型的语法，它的核心目的是：

- **提高代码可读性**：让他人（以及未来的你）一眼就能看懂代码的意图
- **便于静态检查**：在运行代码前，通过工具发现潜在的类型错误
- **增强IDE支持**：让代码编辑器提供更准确的自动补全和提示

### 为什么需要类型注解？

Python 以其**动态类型**特性而闻名——你不需要提前声明变量的类型，解释器会在运行时自动推断。这虽然灵活，但也带来了问题：

1. **代码难以理解**：看到一个函数时，不清楚应该传入什么类型的数据
2. **隐藏的bug**：可能不小心传入了错误类型，直到运行时才报错
3. **开发效率低**：IDE无法提供准确的代码提示和补全

类型注解通过提供可选的类型信息来解决这些问题，让你的代码更加**健壮**和**可维护**。

### 基础类型注解

```python
# 变量注解
name: str = "Alice"  # 字符串
age: int = 30        # 整数
height: float = 1.75 # 浮点数
is_student: bool = False  # 布尔值

# 函数参数和返回值注解
def add(a: int, b: int) -> int:
    return a + b
```

### 容器类型注解

对于列表、元组、字典等容器类型，需结合 `typing` 模块或 Python 3.9+ 的内置泛型。

```python
from typing import List, Tuple, Dict, Set

# 列表（元素类型为int）
nums: List[int] = [1, 2, 3]

# 元组（固定类型和长度）
person: Tuple[str, int, float] = ("Bob", 25, 1.8)

# 字典（键为str，值为int）
scores: Dict[str, int] = {"math": 90, "english": 85}

# 集合（元素类型为str）
fruits: Set[str] = {"apple", "banana"}
```

**Python 3.9+ 简化写法**（无需导入 `typing`）：

```python
nums: list[int] = [1, 2, 3]
person: tuple[str, int, float] = ("Bob", 25, 1.8)
scores: dict[str, int] = {"math": 90}
```

### 可选类型与 Union

表示变量可以是多种类型中的一种：

```python
from typing import Optional, Union

# Optional[T] 等价于 Union[T, None]，表示可以是T类型或None
def get_name(id: int) -> Optional[str]:
    if id == 1:
        return "Alice"
    return None  # 允许返回None

# Union表示多种类型中的一种
def process_data(data: Union[int, str, float]) -> None:
    print(data)
```

**Python 3.10+ 简化写法**（用 `|` 代替 `Union`）：

```python
def process_data(data: int | str | float) -> None:
    print(data)
```







# 文件IO

### 文件打开与关闭

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

  

### 读取文件

- **`file.read(size)`**: 读取指定大小的内容，如果未指定，默认读取整个文件。
- **`file.readline()`**: 用于从文件中读取一行数据。每次调用 `readline()`，它会返回文件的下一行（str），包括行末的换行符（如果存在）。
- **`file.readlines()`**: 读取文件的所有行，返回一个列表。
- **`file.readable()`**: 检查文件是否可读。

### 写入文件

- **`file.write(string)`**: 将字符串写入文件。
- **`file.writelines(lines)`**: 将字符串列表写入文件。
- **`file.writable()`**: 检查文件是否可写。

### 文件指针

- **`file.tell()`**: 返回当前文件指针的位置。
- **`file.seek(offset, whence)`**: 移动文件指针到指定位置。

### 文件属性

- **`file.flush()`**: 刷新文件的内部缓冲区，将数据写入文件。

### 使用上下文管理器

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

### 文件异常处理

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



### CSV文件

1. 读取 CSV 文件

下面是一个读取 CSV 文件的基本示例：

```python
import csv

# 读取 CSV 文件
with open('data.csv', 'r', newline='') as csvfile:
    reader = csv.reader(csvfile)
    for row in reader:
        print(row)  # 打印每一行
```

2. 写入 CSV 文件

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

3. 使用字典读写

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





# 内置函数



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

## reversed()

`reversed()` 是一个内置函数，它返回一个反转的迭代器。这个迭代器可以遍历序列中的元素，但不会直接修改原序列。

**语法**

```python
reversed(sequence)
```

- **参数**：`sequence` 是一个可迭代对象，如列表、元组、字符串等。
- **返回值**：返回一个反转的迭代器。

**示例**

```python
# 使用 reversed() 反转列表
my_list = [1, 2, 3, 4, 5]
reversed_list = list(reversed(my_list))
print(reversed_list)  # 输出：[5, 4, 3, 2, 1]

# 使用 reversed() 反转字符串
my_string = "hello"
reversed_string = ''.join(reversed(my_string))
print(reversed_string)  # 输出：olleh
```

# 常用方法



## Number

```python
# Python数字(Number)常用操作和内置函数介绍

# 1. int() 和 float()
# 将其他类型转换为数字类型
str_num = "123"
int_num = int(str_num)  # 将字符串转换为整数
float_num = float(str_num)  # 将字符串转换为浮点数
print("Integer:", int_num)  # 输出：Integer: 123
print("Float:", float_num)  # 输出：Float: 123.0

# 2. abs()
# 返回数字的绝对值
num1 = -10
abs_num = abs(num1)  # 返回绝对值
print("Absolute value of -10:", abs_num)  # 输出：Absolute value of -10: 10

# 3. round()
# 对浮点数进行四舍五入
num2 = 3.14159
rounded_num = round(num2, 2)  # 四舍五入到小数点后两位
print("Rounded number:", rounded_num)  # 输出：Rounded number: 3.14

# 4. pow()
# 计算数字的幂
base = 2
exponent = 3
power_result = pow(base, exponent)  # 计算2的3次方
print("2 to the power of 3:", power_result)  # 输出：2 to the power of 3: 8

# 5. min() 和 max()
# 找出一组数字中的最小值和最大值
numbers = [1, 2, 3, 4, 5]
min_num = min(numbers)  # 找出最小值
max_num = max(numbers)  # 找出最大值
print("Minimum number:", min_num)  # 输出：Minimum number: 1
print("Maximum number:", max_num)  # 输出：Maximum number: 5

# 6. sum()
# 计算一组数字的总和
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)  # 计算总和
print("Sum of numbers:", total)  # 输出：Sum of numbers: 15

# 7. divmod()
# 返回商和余数
num3 = 10
num4 = 3
quotient, remainder = divmod(num3, num4)  # 返回商和余数
print("Quotient:", quotient)  # 输出：Quotient: 3
print("Remainder:", remainder)  # 输出：Remainder: 1

# 8. isinstance()
# 检查一个对象是否是特定类型的实例
num5 = 10
is_int = isinstance(num5, int)  # 检查是否是整数
is_float = isinstance(num5, float)  # 检查是否是浮点数
print("Is 10 an integer?", is_int)  # 输出：Is 10 an integer? True
print("Is 10 a float?", is_float)  # 输出：Is 10 a float? False
```



## String

```python
# Python字符串(String)常用方法介绍

# 1. len()
# 获取字符串的长度（字符数）
str1 = "Hello World"
length = len(str1)  # 返回字符串的长度
print("Length:", length)  # 输出：Length: 11

# 2. str[index]
# 获取指定索引位置的字符
str2 = "example"
ch = str2[1]  # 返回指定索引位置的字符
print("Character at index 1:", ch)  # 输出：Character at index 1: x

# 3. str[start:end]
# 获取字符串的子字符串
str3 = "Hello World"
sub_str = str3[6:11]  # 从索引6到10的子字符串
print("Substring from index 6 to 10:", sub_str)  # 输出：Substring from index 6 to 10: World

# 4. str.upper()
# 将字符串转换为大写
str4 = "hello"
upper_str = str4.upper()  # 转换为大写
print("Uppercase string:", upper_str)  # 输出：Uppercase string: HELLO

# 5. str.lower()
# 将字符串转换为小写
str5 = "HELLO"
lower_str = str5.lower()  # 转换为小写
print("Lowercase string:", lower_str)  # 输出：Lowercase string: hello

# 6. str.strip()
# 去除字符串首尾的空格
str6 = "   Hello World   "
trimmed_str = str6.strip()  # 去除首尾空格
print("Trimmed string:", trimmed_str)  # 输出：Trimmed string: Hello World

# 7. str.find(sub)
# 查找子字符串的位置
str7 = "Welcome to Python"
index = str7.find("Python")  # 查找子字符串的位置
print("Index of 'Python':", index)  # 输出：Index of 'Python': 11

# 8. str.replace(old, new)
# 替换字符串中的内容
str8 = "Hello Python, Hi Python"
new_str = str8.replace("Python", "Java")  # 替换字符串中的内容
print("Replaced string:", new_str)  # 输出：Replaced string: Hello Java, Hi Java

# 9. str.split(sep)
# 按指定分隔符分割字符串
str9 = "apple,banana,orange"
fruits = str9.split(",")  # 按逗号分割字符串
print("Fruits:", fruits)  # 输出：Fruits: ['apple', 'banana', 'orange']

# 10. str.join(iterable)
# 将可迭代对象中的元素连接成一个字符串
str10 = " "
words = ["Hello", "World"]
sentence = str10.join(words)  # 将words中的元素连接成一个字符串
print("Joined string:", sentence)  # 输出：Joined string: Hello World

# 11. str.startswith(prefix)
# 检查字符串是否以指定前缀开头
str11 = "Hello World"
starts_with_hello = str11.startswith("Hello")  # 检查是否以"Hello"开头
print("Starts with 'Hello':", starts_with_hello)  # 输出：Starts with 'Hello': True

# 12. str.endswith(suffix)
# 检查字符串是否以指定后缀结尾
str12 = "Hello World"
ends_with_world = str12.endswith("World")  # 检查是否以"World"结尾
print("Ends with 'World':", ends_with_world)  # 输出：Ends with 'World': True
```



## List

```python
# Python列表(List)常用方法介绍

# 1. append(x)
# 在列表末尾添加一个元素
my_list = [1, 2, 3]
my_list.append(4)  # 在列表末尾添加元素4
print("After append:", my_list)  # 输出：After append: [1, 2, 3, 4]

# 2. extend(iterable)
# 将一个可迭代对象的所有元素添加到列表末尾
my_list = [1, 2, 3]
another_list = [4, 5]
my_list.extend(another_list)  # 将another_list的所有元素添加到my_list
print("After extend:", my_list)  # 输出：After extend: [1, 2, 3, 4, 5]

# 3. insert(i, x)
# 在指定位置插入一个元素
my_list = [1, 2, 3]
my_list.insert(1, 'a')  # 在索引1的位置插入元素'a'
print("After insert:", my_list)  # 输出：After insert: [1, 'a', 2, 3]

# 4. remove(x)
# 移除列表中第一个值为x的元素
my_list = [1, 2, 3, 2]
my_list.remove(2)  # 移除第一个值为2的元素
print("After remove:", my_list)  # 输出：After remove: [1, 3, 2]

# 5. pop([i])
# 移除列表中指定位置的元素，并返回该元素
my_list = [1, 2, 3]
element = my_list.pop(1)  # 移除索引为1的元素，并返回该元素
print("Popped element:", element)  # 输出：Popped element: 2
print("After pop:", my_list)  # 输出：After pop: [1, 3]

# 6. clear()
# 清空列表
my_list = [1, 2, 3]
my_list.clear()  # 清空列表
print("After clear:", my_list)  # 输出：After clear: []

# 7. index(x[, start[, end]])
# 返回列表中第一个值为x的元素的索引
my_list = [1, 2, 3, 2]
index = my_list.index(2)  # 返回第一个值为2的元素的索引
print("Index of 2:", index)  # 输出：Index of 2: 1

# 8. count(x)
# 返回列表中值为x的元素的个数
my_list = [1, 2, 3, 2]
count = my_list.count(2)  # 返回值为2的元素的个数
print("Count of 2:", count)  # 输出：Count of 2: 2

# 9. sort(key=None, reverse=False)
# 对列表进行排序
my_list = [3, 1, 2]
my_list.sort()  # 对列表进行排序
print("After sort:", my_list)  # 输出：After sort: [1, 2, 3]

# 10. reverse()
# 反转列表
my_list = [1, 2, 3]
my_list.reverse()  # 反转列表
print("After reverse:", my_list)  # 输出：After reverse: [3, 2, 1]

# 11. copy()
# 返回列表的一个浅拷贝.(浅拷贝只复制对象的引用，而不是对象本身。修改浅拷贝时，原列表也会被修改)
my_list = [1, 2, [3, 4]]
new_list = my_list.copy()  # 返回列表的一个浅拷贝
print("Copied list:", new_list)  # 输出：Copied list: [1, 2, [3, 4]]
new_list[0] = 10
new_list[2][0] = 30
print("Original list:", my_list) # 输出：Original list: [1, 2, [30, 4]]
```



## Tuple

```python
# Python元组(Tuple)常用方法介绍

# 1. len()
# 获取元组的长度
my_tuple = (1, 2, 3, 4, 5)
length = len(my_tuple)  # 返回元组的长度
print("Length of tuple:", length)  # 输出：Length of tuple: 5

# 2. tuple[index]
# 访问元组中指定索引位置的元素
my_tuple = ('a', 'b', 'c', 'd')
element = my_tuple[2]  # 访问索引为2的元素
print("Element at index 2:", element)  # 输出：Element at index 2: c

# 3. tuple[start:end]
# 获取元组的子元组
my_tuple = (1, 2, 3, 4, 5)
sub_tuple = my_tuple[1:4]  # 从索引1到3的子元组
print("Subtuple from index 1 to 3:", sub_tuple)  # 输出：Subtuple from index 1 to 3: (2, 3, 4)

# 4. count(x)
# 返回元组中某个值出现的次数
my_tuple = (1, 2, 2, 3, 4, 2)
count = my_tuple.count(2)  # 返回值2出现的次数
print("Count of 2 in tuple:", count)  # 输出：Count of 2 in tuple: 3

# 5. index(x[, start[, end]])
# 返回元组中某个值第一个匹配项的索引位置
my_tuple = ('apple', 'banana', 'cherry')
index = my_tuple.index('banana')  # 返回'banana'第一个匹配项的索引位置
print("Index of 'banana':", index)  # 输出：Index of 'banana': 1

# 6. sorted()
# 对元组进行排序并返回一个新的列表
my_tuple = (3, 1, 4, 1, 5, 9, 2)
sorted_list = sorted(my_tuple)  # 对元组进行排序并返回一个新的列表
print("Sorted list from tuple:", sorted_list)  # 输出：Sorted list from tuple: [1, 1, 2, 3, 4, 5, 9]

# 7. min() 和 max()
# 找出元组中的最小值和最大值
my_tuple = (3, 1, 4, 1, 5, 9, 2)
min_value = min(my_tuple)  # 找出最小值
max_value = max(my_tuple)  # 找出最大值
print("Minimum value in tuple:", min_value)  # 输出：Minimum value in tuple: 1
print("Maximum value in tuple:", max_value)  # 输出：Maximum value in tuple: 9

# 8. sum()
# 计算元组中所有数值的总和
my_tuple = (1, 2, 3, 4, 5)
total = sum(my_tuple)  # 计算总和
print("Sum of tuple:", total)  # 输出：Sum of tuple: 15

# 9. any() 和 all()
# 检查元组中的元素是否满足某些条件
my_tuple = (True, False, True)
any_true = any(my_tuple)  # 检查是否至少有一个元素为True
all_true = all(my_tuple)  # 检查是否所有元素都为True
print("Any element is True:", any_true)  # 输出：Any element is True: True
print("All elements are True:", all_true)  # 输出：All elements are True: False
```



## Set

```python
# Python集合(Set)常用方法介绍

# 1. add(x)
# 向集合中添加一个元素
my_set = {1, 2, 3}
my_set.add(4)  # 添加元素4
print("After add:", my_set)  # 输出：After add: {1, 2, 3, 4}

# 2. update(*iterables)
# 向集合中添加多个元素
my_set = {1, 2, 3}
another_set = {4, 5}
my_set.update(another_set)  # 添加another_set中的所有元素
print("After update:", my_set)  # 输出：After update: {1, 2, 3, 4, 5}

# 3. remove(x)
# 移除集合中的一个元素，如果元素不存在会抛出KeyError
my_set = {1, 2, 3, 2}
my_set.remove(2)  # 移除第一个值为2的元素
print("After remove:", my_set)  # 输出：After remove: {1, 3}

# 4. discard(x)
# 移除集合中的一个元素，如果元素不存在不会抛出错误
my_set = {1, 2, 3}
my_set.discard(2)  # 移除值为2的元素
my_set.discard(4)  # 尝试移除不存在的元素4，不会报错
print("After discard:", my_set)  # 输出：After discard: {1, 3}

# 5. pop()
# 移除并返回集合中的一个元素，集合为空时会抛出KeyError
my_set = {1, 2, 3}
element = my_set.pop()  # 移除并返回一个元素
print("Popped element:", element)  # 输出：Popped element: 1（或2或3，具体取决于集合的内部实现）
print("After pop:", my_set)  # 输出：After pop: {2, 3}（或{1, 3}或{1, 2}）

# 6. clear()
# 清空集合
my_set = {1, 2, 3}
my_set.clear()  # 清空集合
print("After clear:", my_set)  # 输出：After clear: set()

# 7. union(*other_sets)
# 返回集合与其他集合的并集
my_set = {1, 2, 3}
another_set = {3, 4, 5}
union_set = my_set.union(another_set)  # 返回并集
print("Union set:", union_set)  # 输出：Union set: {1, 2, 3, 4, 5}

# 8. intersection(*other_sets)
# 返回集合与其他集合的交集
my_set = {1, 2, 3}
another_set = {3, 4, 5}
intersection_set = my_set.intersection(another_set)  # 返回交集
print("Intersection set:", intersection_set)  # 输出：Intersection set: {3}

# 9. difference(*other_sets)
# 返回集合与其他集合的差集
my_set = {1, 2, 3}
another_set = {3, 4, 5}
difference_set = my_set.difference(another_set)  # 返回差集
print("Difference set:", difference_set)  # 输出：Difference set: {1, 2}

# 10. symmetric_difference(other_set)
# 返回集合与其他集合的对称差集
my_set = {1, 2, 3}
another_set = {3, 4, 5}
symmetric_difference_set = my_set.symmetric_difference(another_set)  # 返回对称差集
print("Symmetric difference set:", symmetric_difference_set)  # 输出：Symmetric difference set: {1, 2, 4, 5}

# 11. issubset(other_set)
# 判断集合是否是另一个集合的子集
my_set = {1, 2}
another_set = {1, 2, 3}
is_subset = my_set.issubset(another_set)  # 判断是否是子集
print("Is my_set a subset of another_set?", is_subset)  # 输出：Is my_set a subset of another_set? True

# 12. issuperset(other_set)
# 判断集合是否是另一个集合的超集
my_set = {1, 2, 3}
another_set = {1, 2}
is_superset = my_set.issuperset(another_set)  # 判断是否是超集
print("Is my_set a superset of another_set?", is_superset)  # 输出：Is my_set a superset of another_set? True

# 13. copy()
# 返回集合的一个浅拷贝
my_set = {1, 2, 3}
new_set = my_set.copy()  # 返回集合的一个浅拷贝
print("Copied set:", new_set)  # 输出：Copied set: {1, 2, 3}
```



## Dictionary

```python
# Python字典(Dictionary)常用方法介绍

# 1. len()
# 获取字典中键值对的数量
my_dict = {'a': 1, 'b': 2, 'c': 3}
length = len(my_dict)  # 返回字典中键值对的数量
print("Length of dictionary:", length)  # 输出：Length of dictionary: 3

# 2. dict[key]
# 访问字典中指定键的值
my_dict = {'a': 1, 'b': 2, 'c': 3}
value = my_dict['b']  # 访问键'b'对应的值
print("Value of key 'b':", value)  # 输出：Value of key 'b': 2

# 3. dict.get(key, default=None)
# 获取字典中指定键的值，如果键不存在则返回默认值
my_dict = {'a': 1, 'b': 2, 'c': 3}
value = my_dict.get('d', 'Not Found')  # 获取键'd'对应的值，如果不存在则返回'Not Found'
print("Value of key 'd':", value)  # 输出：Value of key 'd': Not Found

# 4. dict.keys()
# 返回字典中所有的键
my_dict = {'a': 1, 'b': 2, 'c': 3}
keys = my_dict.keys()  # 返回所有的键
print("Keys in dictionary:", keys)  # 输出：Keys in dictionary: dict_keys(['a', 'b', 'c'])

# 5. dict.values()
# 返回字典中所有的值
my_dict = {'a': 1, 'b': 2, 'c': 3}
values = my_dict.values()  # 返回所有的值
print("Values in dictionary:", values)  # 输出：Values in dictionary: dict_values([1, 2, 3])

# 6. dict.items()
# 返回字典中所有的键值对
my_dict = {'a': 1, 'b': 2, 'c': 3}
items = my_dict.items()  # 返回所有的键值对
print("Items in dictionary:", items)  # 输出：Items in dictionary: dict_items([('a', 1), ('b', 2), ('c', 3)])

# 7. dict.update(other_dict)
# 更新字典，添加或修改键值对
my_dict = {'a': 1, 'b': 2}
another_dict = {'b': 3, 'c': 4}
my_dict.update(another_dict)  # 更新字典
print("Updated dictionary:", my_dict)  # 输出：Updated dictionary: {'a': 1, 'b': 3, 'c': 4}

# 8. dict.pop(key, default=None)
# 移除并返回字典中指定键的值，如果键不存在则返回默认值
my_dict = {'a': 1, 'b': 2, 'c': 3}
value = my_dict.pop('b', 'Not Found')  # 移除并返回键'b'对应的值
print("Popped value:", value)  # 输出：Popped value: 2
print("Dictionary after pop:", my_dict)  # 输出：Dictionary after pop: {'a': 1, 'c': 3}

# 9. dict.popitem()
# 移除并返回字典中最后一个键值对
my_dict = {'a': 1, 'b': 2, 'c': 3}
key, value = my_dict.popitem()  # 移除并返回最后一个键值对
print("Popped item:", key, value)  # 输出：Popped item: c 3
print("Dictionary after popitem:", my_dict)  # 输出：Dictionary after popitem: {'a': 1, 'b': 2}

# 10. dict.clear()
# 清空字典
my_dict = {'a': 1, 'b': 2, 'c': 3}
my_dict.clear()  # 清空字典
print("Dictionary after clear:", my_dict)  # 输出：Dictionary after clear: {}

# 11. dict.copy()
# 返回字典的一个浅拷贝
my_dict = {'a': 1, 'b': 2, 'c': 3}
new_dict = my_dict.copy()  # 返回字典的一个浅拷贝
print("Copied dictionary:", new_dict)  # 输出：Copied dictionary: {'a': 1, 'b': 2, 'c': 3}

# 12. dict.setdefault(key, default=None)
# 如果键不存在则插入键并设置为默认值
my_dict = {'a': 1, 'b': 2}
value = my_dict.setdefault('c', 3)  # 如果键'c'不存在则插入键'c'并设置为3
print("Value of key 'c':", value)  # 输出：Value of key 'c': 3
print("Dictionary after setdefault:", my_dict)  # 输出：Dictionary after setdefault: {'a': 1, 'b': 2, 'c': 3}
```



# 常用库

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







