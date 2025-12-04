# NumPy

文章参考：[NumPy 教程](https://www.runoob.com/numpy/numpy-tutorial.html)

[TOC]

NumPy(Numerical Python) 是 Python 语言的一个扩展程序库，支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。

NumPy 的前身 Numeric 最早是由 Jim Hugunin 与其它协作者共同开发，2005 年，Travis Oliphant 在 Numeric 中结合了另一个同性质的程序库 Numarray 的特色，并加入了其它扩展而开发了 NumPy。NumPy 为开放源代码并且由许多协作者共同维护开发。

`NumPy` 是一个运行速度非常快的数学库，主要用于数组计算，包含：

- 一个强大的N维数组对象 ndarray
- 广播功能函数
- 整合 C/C++/Fortran 代码的工具
- 线性代数、傅里叶变换、随机数生成等功能

## NumPy 应用

NumPy 通常与 SciPy（Scientific Python）和 Matplotlib（绘图库）一起使用， 这种组合广泛用于替代 MatLab，是一个强大的科学计算环境，有助于我们通过 Python 学习数据科学或者机器学习。

SciPy 是一个开源的 Python 算法库和数学工具包。

SciPy 包含的模块有最优化、线性代数、积分、插值、特殊函数、快速傅里叶变换、信号处理和图像处理、常微分方程求解和其他科学与工程中常用的计算。



# 核心



## 数组基础

基础包含：

- 数组创建（`array()`, `arange()`, `zeros()`, `ones()`等）
- 数组属性（`shape`, `dtype`, `ndim`）
- 数据类型转换
- 数组重塑与变形

### Ndarray 对象

**Ndarray**（N-dimensional array，N维数组）是 NumPy 中最基本、最重要的数据结构。它是一个**多维、同构**的数据容器，这意味着：

- **多维**：它可以是一维（像列表）、二维（像矩阵）、三维或更高维度的数组。
- **同构**：数组中的所有元素必须是**相同类型**的数据（如全部是整数，或全部是浮点数）。

这与 Python 的原生列表（可以包含不同类型的数据）有根本区别，也是 NumPy 高性能计算的基础。

#### 为什么 Ndarray 如此高效？

1. **连续内存存储**：数组元素在内存中连续存放，这使得访问和操作速度极快。
2. **向量化操作**：对整个数组执行操作而无需编写显式循环，底层由预编译的 C 代码高效执行。
3. **广播机制**：允许不同形状的数组进行数学运算。

#### 内部结构

ndarray 内部由以下内容组成：

- 一个指向数据（内存或内存映射文件中的一块数据）的指针。
- 数据类型或 dtype，描述在数组中的固定大小值的格子。
- 一个表示数组形状（shape）的元组，表示各维度大小的元组。
- 一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要"跨过"的字节数。

![img](images/ndarray.png)

#### 创建对象

创建一个 ndarray 只需调用 NumPy 的 array 函数即可：

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

**参数说明：**

| 名称   | 描述                                                      |
| :----- | :-------------------------------------------------------- |
| object | 数组或嵌套的数列                                          |
| dtype  | 数组元素的数据类型，可选                                  |
| copy   | 对象是否需要复制，可选                                    |
| order  | 创建数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
| subok  | 默认返回一个与基类类型一致的数组                          |
| ndmin  | 指定生成数组的最小维度                                    |

```python
import numpy as np

# 创建一个 2x3 的二维数组
arr = np.array([[1, 2, 3], [4, 5, 6]])

print("数组内容：\n", arr)
```



### 数据类型

numpy 支持的数据类型比 Python 内置的类型要多很多，基本上可以和 C 语言的数据类型对应上，其中部分类型对应为 Python 内置的类型。下表列举了常用 NumPy 基本类型。

| 名称       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| bool_      | 布尔型数据类型（True 或者 False）                            |
| int_       | 默认的整数类型（类似于 C 语言中的 long，int32 或 int64）     |
| intc       | 与 C 的 int 类型一样，一般是 int32 或 int 64                 |
| intp       | 用于索引的整数类型（类似于 C 的 ssize_t，一般情况下仍然是 int32 或 int64） |
| int8       | 字节（-128 to 127）                                          |
| int16      | 整数（-32768 to 32767）                                      |
| int32      | 整数（-2147483648 to 2147483647）                            |
| int64      | 整数（-9223372036854775808 to 9223372036854775807）          |
| uint8      | 无符号整数（0 to 255）                                       |
| uint16     | 无符号整数（0 to 65535）                                     |
| uint32     | 无符号整数（0 to 4294967295）                                |
| uint64     | 无符号整数（0 to 18446744073709551615）                      |
| float_     | float64 类型的简写                                           |
| float16    | 半精度浮点数，包括：1 个符号位，5 个指数位，10 个尾数位      |
| float32    | 单精度浮点数，包括：1 个符号位，8 个指数位，23 个尾数位      |
| float64    | 双精度浮点数，包括：1 个符号位，11 个指数位，52 个尾数位     |
| complex_   | complex128 类型的简写，即 128 位复数                         |
| complex64  | 复数，表示双 32 位浮点数（实数部分和虚数部分）               |
| complex128 | 复数，表示双 64 位浮点数（实数部分和虚数部分）               |

`numpy` 的数值类型实际上是 `dtype` 对象的实例，并对应唯一的字符，包括 `np.bool_`，`np.int32`，`np.float32`，等等。

你可以查看他们的信息，

```python
import numpy as np

print(np.finfo(np.float16))
print(np.finfo(np.float32))
print(np.finfo(np.float64))
```

#### 数据类型对象 `dtype`

数据类型对象（numpy.dtype 类的实例）用来描述与数组对应的内存区域是如何使用，它描述了数据的以下几个方面：：

- 数据的类型（整数，浮点数或者 Python 对象）

- 数据的大小（例如， 整数使用多少个字节存储）

- 数据的**字节顺序**（小端法或大端法）

    > 字节顺序是通过对数据类型预先设定 **<** 或 **>** 来决定的。 **<** 意味着小端法(最小值存储在最小的地址，即低位组放在最前面)。**>** 意味着大端法(最重要的字节存储在最小的地址，即高位组放在最前面)。

- 在结构化类型的情况下，字段的名称、每个字段的数据类型和每个字段所取的内存块的部分

- 如果数据类型是子数组，那么它的形状和数据类型是什么。



`dtype` 对象是使用以下语法构造的：

```python
numpy.dtype(object, align=False, copy=False)
```

- object - 要转换为的数据类型对象
- align - 如果为 true，填充字段使其类似 C 的结构体。
- copy - 复制 dtype 对象 ，如果为 false，则是对内置数据类型对象的引用



`object`是**唯一必需的参数**，用于指定要创建的数据类型。它非常灵活，可以有多种形式：

方式一：使用类型字符串

```python
import numpy as np

# 基本数据类型
dt1 = np.dtype('int32')        # 32位整数
dt2 = np.dtype('float64')      # 64位浮点数
dt3 = np.dtype('complex128')   # 128位复数
dt4 = np.dtype('bool')         # 布尔值

print(dt1)  # 输出：int32
print(dt2)  # 输出：float64
```

方式二：使用Python类型

```python
# 使用Python原生类型
dt5 = np.dtype(int)           # 等同于 'int64'（系统相关）
dt6 = np.dtype(float)         # 等同于 'float64'
dt7 = np.dtype(complex)       # 等同于 'complex128'
dt8 = np.dtype(bool)          # 布尔值

print(dt5)  # 输出：int64
```

方式三：使用NumPy标量类型

```python
# 使用NumPy的标量类型
dt9 = np.dtype(np.int32)
dt10 = np.dtype(np.float32)
dt11 = np.dtype(np.complex64)

print(dt9)  # 输出：int32
```

方式四：创建结构化数据类型

```python
# 结构化数组类型 - 类似C语言的结构体
dt12 = np.dtype([('name', 'U10'),  # 10个字符的Unicode字符串
                 ('age', 'i4'),     # 32位整数
                 ('height', 'f4')]) # 32位浮点数

print(dt12)
# 输出：dtype([('name', '<U10'), ('age', '<i4'), ('height', '<f4')])
```

方式五：创建子数组类型

```python
# 创建包含子数组的数据类型
dt13 = np.dtype(('i4', 3))  # 包含3个int32的数组
dt14 = np.dtype(('f8', (2, 3)))  # 包含2x3 float64数组的数组

print(dt13)  # 输出：(3,)int32
print(dt14) # 输出：(2, 3)float64
```



### 数组属性

NumPy 的数组中比较重要 ndarray 对象属性有：

| 属性               | 说明                                                         |
| :----------------- | :----------------------------------------------------------- |
| `ndarray.ndim`     | 数组的秩（rank），即数组的维度数量或轴的数量。               |
| `ndarray.shape`    | 数组的维度，表示数组在每个轴上的大小。对于二维数组（矩阵），表示其行数和列数。 |
| `ndarray.size`     | 数组中元素的总个数，等于 `ndarray.shape` 中各个轴上大小的乘积。 |
| `ndarray.dtype`    | 数组中元素的数据类型。                                       |
| `ndarray.itemsize` | 数组中每个元素的大小，以字节为单位。                         |
| `ndarray.flags`    | 包含有关内存布局的信息，如是否为 C 或 Fortran 连续存储，是否为只读等。 |
| `ndarray.real`     | 数组中每个元素的实部（如果元素类型为复数）。                 |
| `ndarray.imag`     | 数组中每个元素的虚部（如果元素类型为复数）。                 |
| `ndarray.data`     | 实际存储数组元素的缓冲区，一般通过索引访问元素，不直接使用该属性。 |



```python
import numpy as np

# 创建示例数组
arr = np.array([[1, 2, 3], [4, 5, 6]], dtype=np.float32)

print("数组:")
print(arr)
print()

# 演示五个核心属性
print(f"ndim (维度数量): {arr.ndim}")
print(f"shape (形状): {arr.shape}")
print(f"size (元素总数): {arr.size}")
print(f"dtype (数据类型): {arr.dtype}")
print(f"itemsize (元素字节数): {arr.itemsize}")

"""
数组:
[[1. 2. 3.]
 [4. 5. 6.]]

ndim (维度数量): 2
shape (形状): (2, 3)
size (元素总数): 6
dtype (数据类型): float32
itemsize (元素字节数): 4
"""
```



### 创建数组

`ndarray` 数组除了可以使用底层 `ndarray` 构造器来创建外，也可以通过以下几种方式来创建。

```python
import numpy as np

print("NumPy 数组创建方法演示")
print("=" * 40)

# 1. array() - 从Python列表或元组创建
print("1. array() - 从Python列表创建:")
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(f"一维数组: {arr1}")
print(f"二维数组:\n{arr2}")
print()

# 2. arange(start, stop, step, dtype) - 创建数值范围数组
print("2. arange() - 创建数值范围:")
arr3 = np.arange(5)           # 0到4
arr4 = np.arange(2, 8)        # 2到7
arr5 = np.arange(0, 10, 2)    # 0到10，步长为2
print(f"arange(5): {arr3}")
print(f"arange(2, 8): {arr4}")
print(f"arange(0, 10, 2): {arr5}")
print()

# 3. zeros(shape, dtype = float, order = 'C') - 创建全0数组
print("3. zeros() - 创建全0数组:")
zeros_1d = np.zeros(3)
zeros_2d = np.zeros((2, 3))
print(f"zeros(3): {zeros_1d}")
print(f"zeros((2, 3)):\n{zeros_2d}")
print()

# 4. ones(shape, dtype = float, order = 'C') - 创建全1数组
print("4. ones() - 创建全1数组:")
ones_1d = np.ones(4)
ones_2d = np.ones((2, 2))
print(f"ones(4): {ones_1d}")
print(f"ones((2, 2)):\n{ones_2d}")
print()

# 5. 其他常用创建方法
print("5. 其他创建方法:")
# empty(shape, dtype = float, order = 'C')
empty_arr = np.empty((2, 3))          # 创建未初始化数组
full_arr = np.full((2, 2), 7)         # 创建填充指定值的数组
identity_arr = np.eye(3)              # 创建单位矩阵
linspace_arr = np.linspace(0, 1, 5)   # 创建等间隔数组

print(f"empty((2, 3)):\n{empty_arr}")
print(f"full((2, 2), 7):\n{full_arr}")
print(f"eye(3):\n{identity_arr}")
print(f"linspace(0, 1, 5): {linspace_arr}")
```



## 切片和索引

### 切片

`ndarray`对象的内容可以通过索引或切片来访问和修改，与 Python 中 list 的切片操作一样。

`ndarray` 数组可以基于 0 - n 的下标进行索引，切片对象可以通过内置的 `slice` 函数，并设置 `start`, `stop` 及 `step` 参数进行，从原数组中切割出一个新数组。

```python
import numpy as np
 
a = np.arange(10)
s = slice(2,7,2)   # 从索引 2 开始到索引 7 停止，间隔为2
print (a[s])
```

我们也可以通过冒号分隔切片参数 `start:stop:step` 来进行切片操作：

```python
a = np.arange(10)  
b = a[2:7:2]   # 从索引 2 开始到索引 7 停止，间隔为 2
print(b)
```

### 索引

**整数数组索引**是指使用一个数组来访问另一个数组的元素。这个数组中的每个元素都是目标数组中某个维度上的索引值。

以下实例获取数组中 **(0,0)，(1,1)** 和 **(2,0)** 位置处的元素。

```python
import numpy as np 
 
x = np.array([
    [1,  2],  
    [3,  4],  
    [5,  6]]) 
y = x[[0,1,2],  [0,1,0]]  
print (y) # [1  4  5]
```

可以借助切片 **`:`** 或 **`…`** 与索引数组组合。如下面例子：

> 省略号 `...`（Ellipsis）在 NumPy 索引中是一个**占位符**，表示"所有剩余的维度"。

```python
import numpy as np
 
a = np.array([
    [1,2,3], 
    [4,5,6],
    [7,8,9]])

print(a[1:3, 1:3])
print(a[1:3,[1,2]])
print(a[...,1:]) # 第2列及剩下的所有元素
print (a[...,1])   # 第2列元素
print (a[1,...])   # 第2行元素

"""
[[5 6]
 [8 9]]
[[5 6]
 [8 9]]
[[2 3]
 [5 6]
 [8 9]]
"""
```

**布尔索引**通过布尔运算（如：比较运算符）来获取符合指定条件的元素的数组。

以下实例获取大于 5 的元素：

```python
import numpy as np 
 
x = np.array([[  0,  1,  2],
              [  3,  4,  5],
              [  6,  7,  8],
              [  9,  10,  11]])  
print ('我们的数组是：')
print (x)
print ('\n')
# 现在我们会打印出大于 5 的元素  
print  ('大于 5 的元素是：')
print (x[x >  5])
```



## 迭代数组

NumPy 迭代器对象 numpy.nditer 提供了一种灵活访问一个或者多个数组元素的方式。

迭代器最基本的任务的可以完成对数组元素的访问。

接下来我们使用 arange() 函数创建一个 2X3 数组，并使用 nditer 对它进行迭代。

```python
import numpy as np
 
a = np.arange(6).reshape(2,3)
print ('原始数组是：')
print (a)
print ('\n')
print ('迭代输出元素：')
for x in np.nditer(a):
    print (x, end=", " )
print ('\n')
```

#### 控制遍历顺序

- `for x in np.nditer(a, order='F'):`Fortran order，即是列序优先；
- `for x in np.nditer(a, order='C'):`C order，即是行序优先；



## 数组操作

- 数组拼接（`concatenate()`, `stack()`）
- 数组分割（`split()`）
- 维度操作（`reshape()`, `ravel()`, `transpose()`）
- 广播机制（Broadcasting）

### 数组拼接

#### `numpy.concatenate`

numpy.concatenate 函数用于沿指定轴连接**相同形状**的两个或多个数组，格式如下：

```
numpy.concatenate((a1, a2, ...), axis)
```

参数说明：

- `a1, a2, ...`：相同类型的数组
- `axis`：沿着它连接数组的轴，默认为 0

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
# 两个数组的维度相同
 
print ('沿轴 0 连接两个数组：')
print (np.concatenate((a,b)))
print ('\n')
 
print ('沿轴 1 连接两个数组：')
print (np.concatenate((a,b),axis = 1))

"""
第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


沿轴 0 连接两个数组：
[[1 2]
 [3 4]
 [5 6]
 [7 8]]


沿轴 1 连接两个数组：
[[1 2 5 6]
 [3 4 7 8]]
"""
```

#### `numpy.stack`

numpy.stack 函数用于沿新轴连接数组序列，格式如下：

```
numpy.stack(arrays, axis)
```

参数说明：

- `arrays`相同形状的数组序列
- `axis`：返回数组中的轴，输入数组沿着它来堆叠

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
 
print ('沿轴 0 堆叠两个数组：')
print (np.stack((a,b),0))
print ('\n')
 
print ('沿轴 1 堆叠两个数组：')
print (np.stack((a,b),1))

"""
第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


沿轴 0 堆叠两个数组：
[[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]


沿轴 1 堆叠两个数组：
[[[1 2]
  [5 6]]

 [[3 4]
  [7 8]]]
"""
```



### 数组分割

#### `numpy.split`

numpy.split 函数沿特定的轴将数组分割为子数组，格式如下：

```
numpy.split(ary, indices_or_sections, axis)
```

参数说明：

- `ary`：被分割的数组
- `indices_or_sections`：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭）
- `axis`：设置沿着哪个方向进行切分，默认为 0，横向切分，即水平方向。为 1 时，纵向切分，即竖直方向。

```python
import numpy as np
 
a = np.arange(9)
 
print ('第一个数组：')
print (a)
print ('\n')
 
print ('将数组分为三个大小相等的子数组：')
b = np.split(a,3)
print (b)
print ('\n')
 
print ('将数组在一维数组中表明的位置分割：')
b = np.split(a,[4,7])
print (b)

"""
第一个数组：
[0 1 2 3 4 5 6 7 8]


将数组分为三个大小相等的子数组：
[array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]


将数组在一维数组中表明的位置分割：
[array([0, 1, 2, 3]), array([4, 5, 6]), array([7, 8])]
"""
```





### 维度操作

#### `ndarray.reshape`

numpy.reshape 函数可以在不改变数据的条件下修改形状，格式如下：

```python
ndarray.reshape(arr, newshape, order='C')
```

- `arr`：要修改形状的数组
- `newshape`：整数或者整数数组，新的形状应当兼容原有形状
- `order`：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。

```python
import numpy as np
 
a = np.arange(8)
print ('原始数组：')
print (a)
print ('\n')
 
b = a.reshape(4,2)
print ('修改后的数组：')
print (b)

"""
原始数组：
[0 1 2 3 4 5 6 7]

修改后的数组：
[[0 1]
 [2 3]
 [4 5]
 [6 7]]
"""
```

#### `ndarray.flat`

numpy.ndarray.flat 是一个数组元素迭代器，实例如下:

```python
import numpy as np
 
a = np.arange(9).reshape(3,3) 
print ('原始数组：')
for row in a:
    print (row)
 
# 对数组中每个元素都进行处理，可以使用flat属性，该属性是一个数组元素迭代器：
print ('迭代后的数组：')
for element in a.flat:
    print (element)

"""
原始数组：
[0 1 2]
[3 4 5]
[6 7 8]
迭代后的数组：
0
1
2
3
4
5
6
7
8
"""
```

而 `ndarray.flatten` 返回一份数组拷贝，对拷贝所做的修改不会影响原始数组。

#### `ndarray.ravel`

ravel() 展平的数组元素，顺序通常是"C风格"，返回的是数组视图（view，有点类似 C/C++引用reference的意味），修改会影响原始数组。`ndarray.ravel(a, order='C')`

```python
import numpy as np
 
a = np.arange(8).reshape(2,4)
 
print ('原数组：')
print (a)
print ('\n')
 
print ('调用 ravel 函数之后：')
print (a.ravel())
print ('\n')
 
print ('以 F 风格顺序调用 ravel 函数之后：')
print (a.ravel(order = 'F'))
```

#### `numpy.transpose`

numpy.transpose 函数用于对换数组的维度，格式如下：

```python
numpy.transpose(arr, axes)
```

参数说明:

- `arr`：要操作的数组
- `axes`：整数列表，对应维度，通常所有维度都会对换。

```python
import numpy as np
 
a = np.arange(12).reshape(3,4)
 
print ('原数组：')
print (a )
print ('\n')
 
print ('对换数组：')
print (np.transpose(a))

"""
原数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]


对换数组：
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
"""
```

`ndarray.T` 类似 `numpy.transpose`

```python
a = np.arange(12).reshape(3,4)
 
print ('原数组：')
print (a)
print ('\n')
 
print ('转置数组：')
print (a.T)
```

### 广播

广播(Broadcast)是 numpy 对不同形状(`shape`)的数组进行数值计算的方式， 对数组的算术运算通常在相应的元素上进行。

如果两个数组 a 和 b 形状相同，即满足 **`a.shape == b.shape`**，那么 `a*b` 的结果就是 a 与 b 数组对应位相乘。这要求维数相同，且各维度的长度相同。

```python
import numpy as np 
 
a = np.array([1,2,3,4]) 
b = np.array([10,20,30,40]) 
c = a * b 
print (c) # [10  40  90 160]
```

当运算中的 2 个数组的形状不同时，numpy 将自动触发广播机制。如：

```python
import numpy as np 
 
a = np.array([[ 0, 0, 0],
           [10,10,10],
           [20,20,20],
           [30,30,30]])
b = np.array([0,1,2])
print(a + b)

"""
[[ 0  1  2]
 [10 11 12]
 [20 21 22]
 [30 31 32]]
"""
```

下面的图片展示了数组 b 如何通过广播来与数组 a 兼容。

![img](images/image0020619.gif)

**广播过程：**

- 一维数组 `(3,)` → 在左边补1 → `(1, 3)`
- 比较 `(4, 3)` 和 `(1, 3)`：
    - 第1维：4 vs 1 → 可以广播
    - 第2维：3 vs 3 → 相等
- 最终两个数组都扩展为 `(4, 3)`

#### 规则的核心

NumPy 广播遵循严格的规则，主要包含两个步骤：

**规则1：缺失维度处理**：

如果两个数组的维度数不同，在**左边**补 1，直到维度数相同

**规则2：维度对齐**：

从**最右边**的维度开始，逐维度比较两个数组的形状：

- 如果维度大小相等，可以正常操作
- 如果维度大小不相等，但其中一个为 1，则可以广播
- 如果维度大小不相等且都不为 1，则报错





# 数值计算



## 向量



### 单向量操作

```python
a = np.array([1,2,3,4])
print(f"a             : {a}")
# negate elements of a
b = -a 
print(f"b = -a        : {b}")

# sum all elements of a, returns a scalar
b = np.sum(a) 
print(f"b = np.sum(a) : {b}")

b = np.mean(a)
print(f"b = np.mean(a): {b}")

b = a**2
print(f"b = a**2      : {b}")

"""
a             : [1 2 3 4]
b = -a        : [-1 -2 -3 -4]
b = np.sum(a) : 10
b = np.mean(a): 2.5
b = a**2      : [ 1  4  9 16]
"""
```



### 向量间逐元素操作

向量向量逐元素操作是指**对两个向量的对应元素进行数学运算**，产生一个具有相同维度的新向量。

**基本概念**

- **要求**：两个向量必须具有**相同的形状**（相同数量的元素）
- **操作**：对每个对应的元素对执行相同的运算
- **结果**：产生一个与输入向量相同形状的新向量

#### 相加

下面是向量相加。
$$
\vec{a} + \vec{b} = \sum_{i=0}^{n-1} a_i + b_i
$$

```python
a = np.array([ 1, 2, 3, 4])
b = np.array([-1,-2, 3, 4])
print(f"Binary operators work element wise: {a + b}") # 或 np.add(a, b)

"""
Binary operators work element wise: [0 0 6 8]
"""
```

形状不同报错，

```python
#try a mismatched vector operation
c = np.array([1, 2])
try:
    d = a + c
except Exception as e:
    print("The error message you'll see is:")
    print(e)
```

减法同理。

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])
c = a - b  # 或 np.subtract(a, b)
print(c)  # 输出: [-4 -4 -4 -4]
```

#### 叉乘

也可以相乘，称之为**叉乘**。

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])
c = a * b  # 或 np.multiply(a, b)
print(c)  # 输出: [ 5 12 21 32]
# 计算: 1×5=5, 2×6=12, 3×7=21, 4×8=32
```

除法同理。

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])
c = a / b  # 或 np.divide(a, b)
print(c)  # 输出: [0.2 0.33333333 0.42857143 0.5]
```

#### 幂运算

```python
a = np.array([1, 2, 3, 4])
b = np.array([2, 2, 2, 2])
c = a ** b  # 或 np.power(a, b)
print(c)  # 输出: [ 1  4  9 16]
```

#### 点乘

> 矩阵乘法是**点乘的扩展**，要求第一个矩阵的列数等于第二个矩阵的行数。
>
> 通常都是用点乘。

$$
x = \sum_{i=0}^{n-1} a_i b_i
$$

这可以用循环来实现，

```python
def my_dot(a, b): 
    """
   Compute the dot product of two vectors
 
    Args:
      a (ndarray (n,)):  input vector 
      b (ndarray (n,)):  input vector with same dimension as a
    
    Returns:
      x (scalar): 
    """
    x=0
    for i in range(a.shape[0]):
        x = x + a[i] * b[i]
    return x
```

但是向量化的并行运算要快得多。

```python
# test 1-D
a = np.array([1, 2, 3, 4])
b = np.array([-1, 4, 3, 2])
print(f"my_dot(a, b) = {my_dot(a, b)}")

# 定义两个矩阵
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

c = a @ b # 或 np.power(a, b)
print(c)
# 输出:
# [[19 22]
#  [43 50]]
```

可以从下面这个例子对比，

```python
np.random.seed(1)
a = np.random.rand(10000000)  # very large arrays
b = np.random.rand(10000000)

tic = time.time()  # capture start time
c = np.dot(a, b)
toc = time.time()  # capture end time

print(f"np.dot(a, b) =  {c:.4f}")
print(f"Vectorized version duration: {1000*(toc-tic):.4f} ms ")

tic = time.time()  # capture start time
c = my_dot(a,b)
toc = time.time()  # capture end time

print(f"my_dot(a, b) =  {c:.4f}")
print(f"loop version duration: {1000*(toc-tic):.4f} ms ")

del(a);del(b)  #remove these big arrays from memory
```



















