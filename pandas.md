# Pandas

文章参考：[Pandas 教程](https://www.runoob.com/pandas/pandas-tutorial.html)

[TOC]

**Pandas 是 Python 语言的一个扩展程序库，用于数据分析。**

Pandas 名字衍生自术语 "panel data"（面板数据）和 "**Python data analysis**"（Python 数据分析）。

Pandas 是一个开放源码、BSD 许可的库，提供高性能、易于使用的数据结构和数据分析工具。

Pandas 一个强大的分析结构化数据的工具集，基础是 [Numpy](https://www.runoob.com/numpy/numpy-tutorial.html)（提供高性能的矩阵运算）。

**Pandas 应用**

Pandas 可以从各种文件格式比如 CSV、JSON、SQL、Microsoft Excel 导入数据。

Pandas 可以对各种数据进行运算操作，比如归并、再成形、选择，还有数据清洗和数据加工特征。

Pandas 广泛应用在学术、金融、统计学等各个数据分析领域。

**Pandas 功能**

Pandas 是数据分析的利器，它不仅提供了高效、灵活的数据结构，还能帮助你以极低的成本完成复杂的数据操作和分析任务。

Pandas 提供了丰富的功能，包括：

- 数据清洗：处理缺失数据、重复数据等。
- 数据转换：改变数据的形状、结构或格式。
- 数据分析：进行统计分析、聚合、分组等。
- 数据可视化：通过整合 Matplotlib 和 Seaborn 等库，可以进行数据可视化。

**数据结构**

Pandas 的主要数据结构是 Series （一维数据）与 DataFrame（二维数据）。

- **[Series](https://www.runoob.com/pandas/pandas-series.html)** 是一种类似于一维数组的对象，它由一组数据（各种 Numpy 数据类型）以及一组与之相关的数据标签（即索引）组成。
- **[DataFrame](https://www.runoob.com/pandas/pandas-dataframe.html)** 是一个表格型的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔型值）。DataFrame 既有行索引也有列索引，它可以被看做由 Series 组成的字典（共同用一个索引）。

# 核心



## Series

Series 是 Pandas 中的一个核心数据结构，类似于一个一维的数组，具有数据和索引。

Series 可以存储任何数据类型（整数、浮点数、字符串等），并通过标签（索引）来访问元素。

Series 的数据结构是非常有用的，因为它可以处理各种数据类型，同时保持了高效的数据操作能力，比如可以通过标签来快速访问和操作数据。

**特点**：

- **一维数组：**Series 中的每个元素都有一个对应的索引值。
- **索引：** 每个数据元素都可以通过标签（索引）来访问，默认情况下索引是从 0 开始的整数，但你也可以自定义索引。
- **数据类型：** `Series` 可以容纳不同数据类型的元素，包括整数、浮点数、字符串、Python 对象等。
- **大小不变性：**Series 的大小在创建后是不变的，但可以通过某些操作（如 append 或 delete）来改变。
- **操作：**Series 支持各种操作，如数学运算、统计分析、字符串处理等。
- **缺失数据：**Series 可以包含缺失数据，Pandas 使用NaN（Not a Number）来表示缺失或无值。
- **自动对齐：**当对多个 Series 进行运算时，Pandas 会自动根据索引对齐数据，这使得数据处理更加高效。

### 创建 Series

可以使用 pd.Series() 构造函数创建一个 Series 对象，传递一个数据数组（可以是列表、NumPy 数组等）和一个可选的索引数组。

```python
pandas.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)
```

参数说明：

- `data`：Series 的数据部分，可以是列表、数组、字典、标量值等。如果不提供此参数，则创建一个空的 Series。
- `index`：Series 的索引部分，用于对数据进行标记。可以是列表、数组、索引对象等。如果不提供此参数，则创建一个默认的整数索引。
- `dtype`：指定 Series 的数据类型。可以是 NumPy 的数据类型，例如 `np.int64`、`np.float64` 等。如果不提供此参数，则根据数据自动推断数据类型。
- `name`：Series 的名称，用于标识 Series 对象。如果提供了此参数，则创建的 Series 对象将具有指定的名称。
- `copy`：是否复制数据。默认为 False，表示不复制数据。如果设置为 True，则复制输入的数据。
- `fastpath`：是否启用快速路径。默认为 False。启用快速路径可能会在某些情况下提高性能。

创建一个简单的 Series 实例，

```python
import pandas as pd

a = [1, 2, 3]

myvar = pd.Series(a)

print(myvar)
```

从上图可知，如果没有指定索引，索引值就从 0 开始，我们可以根据索引值读取数据，

```python
print(myvar[1]) # 2
```

我们可以指定索引值，如下实例，

```python
import pandas as pd

a = ["Google", "Runoob", "Wiki"]

myvar = pd.Series(a, index = ["x", "y", "z"])

print(myvar)
print(myvar["y"]) # Runoob
```

![img](images/32B49FA4-ED68-446A-9EBF-C52FCB6D0CD6.jpg)

我们也可以使用 key/value 对象，类似字典来创建 Series：

```python
import pandas as pd

sites = {1: "Google", 2: "Runoob", 3: "Wiki"}

myvar = pd.Series(sites)

print(myvar)
```

如果我们只需要字典中的一部分数据，只需要指定需要数据的索引即可，如下实例，

```python
sites = {1: "Google", 2: "Runoob", 3: "Wiki"}
myvar = pd.Series(sites, index = [1, 2])
print(myvar)
```

### 常用操作

| **方法名称**                 | **功能描述**                                           |
| :--------------------------- | :----------------------------------------------------- |
| `index`                      | 获取 Series 的索引                                     |
| `values`                     | 获取 Series 的数据部分（返回 NumPy 数组）              |
| `head(n)`                    | 返回 Series 的前 n 行（默认为 5）                      |
| `tail(n)`                    | 返回 Series 的后 n 行（默认为 5）                      |
| `dtype`                      | 返回 Series 中数据的类型                               |
| `shape`                      | 返回 Series 的形状（行数）                             |
| `describe()`                 | 返回 Series 的统计描述（如均值、标准差、最小值等）     |
| `isnull()`                   | 返回一个布尔 Series，表示每个元素是否为 NaN            |
| `notnull()`                  | 返回一个布尔 Series，表示每个元素是否不是 NaN          |
| `unique()`                   | 返回 Series 中的唯一值（去重）                         |
| `value_counts()`             | 返回 Series 中每个唯一值的出现次数                     |
| `map(func)`                  | 将指定函数应用于 Series 中的每个元素                   |
| `apply(func)`                | 将指定函数应用于 Series 中的每个元素，常用于自定义操作 |
| `astype(dtype)`              | 将 Series 转换为指定的类型                             |
| `sort_values()`              | 对 Series 中的元素进行排序（按值排序）                 |
| `sort_index()`               | 对 Series 的索引进行排序                               |
| `dropna()`                   | 删除 Series 中的缺失值（NaN）                          |
| `fillna(value)`              | 填充 Series 中的缺失值（NaN）                          |
| `replace(to_replace, value)` | 替换 Series 中指定的值                                 |
| `cumsum()`                   | 返回 Series 的累计求和                                 |
| `cumprod()`                  | 返回 Series 的累计乘积                                 |
| `shift(periods)`             | 将 Series 中的元素按指定的步数进行位移                 |
| `rank()`                     | 返回 Series 中元素的排名                               |
| `corr(other)`                | 计算 Series 与另一个 Series 的相关性（皮尔逊相关系数） |
| `cov(other)`                 | 计算 Series 与另一个 Series 的协方差                   |
| `to_list()`                  | 将 Series 转换为 Python 列表                           |
| `to_frame()`                 | 将 Series 转换为 DataFrame                             |
| `iloc[]`                     | 通过位置索引来选择数据                                 |
| `loc[]`                      | 通过标签索引来选择数据                                 |

```python
import pandas as pd

# 创建 Series
data = [1, 2, 3, 4, 5, 6]
index = ['a', 'b', 'c', 'd', 'e', 'f']
s = pd.Series(data, index=index)

# 查看基本信息
print("索引：", s.index)
print("数据：", s.values)
print("数据类型：", s.dtype)
print("前两行数据：", s.head(2))

# 使用 map 函数将每个元素加倍
s_doubled = s.map(lambda x: x * 2)
print("元素加倍后：", s_doubled)

# 计算累计和
cumsum_s = s.cumsum()
print("累计求和：", cumsum_s)

# 查找缺失值（这里没有缺失值，所以返回的全是 False）
print("缺失值判断：", s.isnull())

# 排序
sorted_s = s.sort_values()
print("排序后的 Series：", sorted_s)
```



## DataFrame

DataFrame 是 Pandas 中的另一个核心数据结构，类似于一个二维的表格或数据库中的数据表。

DataFrame 是一个表格型的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔型值）。

DataFrame 既有行索引也有列索引，它可以被看做由 Series 组成的字典（共同用一个索引）。

DataFrame 提供了各种功能来进行数据访问、筛选、分割、合并、重塑、聚合以及转换等操作。

DataFrame 是一个非常灵活且强大的数据结构，广泛用于数据分析、清洗、转换、可视化等任务。

**特点：**

- **二维结构：** `DataFrame` 是一个二维表格，可以被看作是一个 Excel 电子表格或 SQL 表，具有行和列。可以将其视为多个 `Series` 对象组成的字典。
- **列的数据类型：** 不同的列可以包含不同的数据类型，例如整数、浮点数、字符串或 Python 对象等。
- **索引**：`DataFrame` 可以拥有行索引和列索引，类似于 Excel 中的行号和列标。
- **大小可变**：可以添加和删除列，类似于 Python 中的字典。
- **自动对齐**：在进行算术运算或数据对齐操作时，`DataFrame` 会自动对齐索引。
- **处理缺失数据**：`DataFrame` 可以包含缺失数据，Pandas 使用 `NaN`（Not a Number）来表示。
- **数据操作**：支持数据切片、索引、子集分割等操作。
- **时间序列支持**：`DataFrame` 对时间序列数据有特别的支持，可以轻松地进行时间数据的切片、索引和操作。
- **丰富的数据访问功能**：通过 `.loc`、`.iloc` 和 `.query()` 方法，可以灵活地访问和筛选数据。
- **灵活的数据处理功能**：包括数据合并、重塑、透视、分组和聚合等。
- **数据可视化**：虽然 `DataFrame` 本身不是可视化工具，但它可以与 Matplotlib 或 Seaborn 等可视化库结合使用，进行数据可视化。
- **高效的数据输入输出**：可以方便地读取和写入数据，支持多种格式，如 CSV、Excel、SQL 数据库和 HDF5 格式。
- **描述性统计**：提供了一系列方法来计算描述性统计数据，如 `.describe()`、`.mean()`、`.sum()` 等。
- **灵活的数据对齐和集成**：可以轻松地与其他 `DataFrame` 或 `Series` 对象进行合并、连接或更新操作。
- **转换功能**：可以对数据集中的值进行转换，例如使用 `.apply()` 方法应用自定义函数。
- **滚动窗口和时间序列分析**：支持对数据集进行滚动窗口统计和时间序列分析。

![img](images/pandas-DataStructure.png)

![img](images/df-dp.png)

### 创建 DataFrame

DataFrame 构造方法如下：

```python
pandas.DataFrame(data=None, index=None, columns=None, dtype=None, copy=False)
```

**参数说明**：

- `data`：DataFrame 的数据部分，可以是字典、二维数组、Series、DataFrame 或其他可转换为 DataFrame 的对象。如果不提供此参数，则创建一个空的 DataFrame。
- `index`：DataFrame 的行索引，用于标识每行数据。可以是列表、数组、索引对象等。如果不提供此参数，则创建一个默认的整数索引。
- `columns`：DataFrame 的列索引，用于标识每列数据。可以是列表、数组、索引对象等。如果不提供此参数，则创建一个默认的整数索引。
- `dtype`：指定 DataFrame 的数据类型。可以是 NumPy 的数据类型，例如 `np.int64`、`np.float64` 等。如果不提供此参数，则根据数据自动推断数据类型。
- `copy`：是否复制数据。默认为 False，表示不复制数据。如果设置为 True，则复制输入的数据。

Pandas DataFrame 是一个二维的数组结构，类似二维数组。

```python
import pandas as pd

data = [['Google', 10], ['Runoob', 12], ['Wiki', 13]]

# 创建DataFrame
df = pd.DataFrame(data, columns=['Site', 'Age'])

# 使用astype方法设置每列的数据类型
df['Site'] = df['Site'].astype(str)
df['Age'] = df['Age'].astype(float)

print(df)
```

也可以使用字典来创建：

```python
import pandas as pd

data = {'Site':['Google', 'Runoob', 'Wiki'], 'Age':[10, 12, 13]}

df = pd.DataFrame(data)

print (df)
"""
     Site  Age
0  Google   10
1  Runoob   12
2    Wiki   13
"""
```

以下实例使用 ndarrays 创建，ndarray 的长度必须相同， 如果传递了 index，则索引的长度应等于数组的长度。

```python
import numpy as np
import pandas as pd

# 创建一个包含网站和年龄的二维ndarray
ndarray_data = np.array([
    ['Google', 10],
    ['Runoob', 12],
    ['Wiki', 13]
])

# 使用DataFrame构造函数创建数据帧
df = pd.DataFrame(ndarray_data, columns=['Site', 'Age'])

# 打印数据帧
print(df)
```

还可以使用字典（key/value），其中字典的 key 为列名：

```python
import pandas as pd

data = [{'a': 1, 'b': 2},{'a': 5, 'b': 10, 'c': 20}]

df = pd.DataFrame(data)

print (df)
"""
   a   b     c
0  1   2   NaN
1  5  10  20.0
"""
# 没有对应的部分数据为 NaN。
```

### 常用方法

DataFrame 的常用操作和方法如下表所示：

| **方法名称**        | **功能描述**                                                |
| :------------------ | :---------------------------------------------------------- |
| `head(n)`           | 返回 DataFrame 的前 n 行数据（默认前 5 行）                 |
| `tail(n)`           | 返回 DataFrame 的后 n 行数据（默认后 5 行）                 |
| `info()`            | 显示 DataFrame 的简要信息，包括列名、数据类型、非空值数量等 |
| `describe()`        | 返回 DataFrame 数值列的统计信息，如均值、标准差、最小值等   |
| `shape`             | 返回 DataFrame 的行数和列数（行数, 列数）                   |
| `columns`           | 返回 DataFrame 的所有列名                                   |
| `index`             | 返回 DataFrame 的行索引                                     |
| `dtypes`            | 返回每一列的数值数据类型                                    |
| `sort_values(by)`   | 按照指定列排序                                              |
| `sort_index()`      | 按行索引排序                                                |
| `dropna()`          | 删除含有缺失值（NaN）的行或列                               |
| `fillna(value)`     | 用指定的值填充缺失值                                        |
| `isnull()`          | 判断缺失值，返回一个布尔值 DataFrame                        |
| `notnull()`         | 判断非缺失值，返回一个布尔值 DataFrame                      |
| `loc[]`             | 按标签索引选择数据                                          |
| `iloc[]`            | 按位置索引选择数据                                          |
| `at[]`              | 访问 DataFrame 中单个元素（比 `loc[]` 更高效）              |
| `iat[]`             | 访问 DataFrame 中单个元素（比 `iloc[]` 更高效）             |
| `apply(func)`       | 对 DataFrame 或 Series 应用一个函数                         |
| `applymap(func)`    | 对 DataFrame 的每个元素应用函数（仅对 DataFrame）           |
| `groupby(by)`       | 分组操作，用于按某一列分组进行汇总统计                      |
| `pivot_table()`     | 创建透视表                                                  |
| `merge()`           | 合并多个 DataFrame（类似 SQL 的 JOIN 操作）                 |
| `concat()`          | 按行或按列连接多个 DataFrame                                |
| `to_csv()`          | 将 DataFrame 导出为 CSV 文件                                |
| `to_excel()`        | 将 DataFrame 导出为 Excel 文件                              |
| `to_json()`         | 将 DataFrame 导出为 JSON 格式                               |
| `to_sql()`          | 将 DataFrame 导出为 SQL 数据库                              |
| `query()`           | 使用 SQL 风格的语法查询 DataFrame                           |
| `duplicated()`      | 返回布尔值 DataFrame，指示每行是否是重复的                  |
| `drop_duplicates()` | 删除重复的行                                                |
| `set_index()`       | 设置 DataFrame 的索引                                       |
| `reset_index()`     | 重置 DataFrame 的索引                                       |
| `transpose()`       | 转置 DataFrame（行列交换）                                  |

```python
import pandas as pd

# 创建 DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Age': [25, 30, 35, 40],
    'City': ['New York', 'Los Angeles', 'Chicago', 'Houston']
}
df = pd.DataFrame(data)

# 查看前两行数据
print(df.head(2))

# 查看 DataFrame 的基本信息
print(df.info())

# 获取描述统计信息
print(df.describe())

# 按年龄排序
df_sorted = df.sort_values(by='Age', ascending=False)
print(df_sorted)

# 选择指定列
print(df[['Name', 'Age']])

# 按索引选择行
print(df.iloc[1:3])  # 选择第二到第三行（按位置）

# 按标签选择行
print(df.loc[1:2])  # 选择第二到第三行（按标签）

# 计算分组统计（按城市分组，计算平均年龄）
print(df.groupby('City')['Age'].mean())

# 处理缺失值（填充缺失值）
df['Age'] = df['Age'].fillna(30)

# 导出为 CSV 文件
df.to_csv('output.csv', index=False)
```







