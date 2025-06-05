# Jupyter 

**文章参考**：[Jupyter 官方文档](https://jupyter.org/documentation), [Real Python](https://realpython.com/jupyter-notebook-introduction/)

[TOC]

# Jupyter 简介

## 介绍

Jupyter 是一个开源的交互式计算环境，广泛用于数据科学、机器学习、数据分析、可视化以及交互式教学等场景。它的名称来源于支持的编程语言 **Ju**lia、**Py**thon 和 **R**，但如今它支持多种编程语言，包括 JavaScript、Go、R 等。

Jupyter 的核心组件是 **Jupyter Notebook**，它允许用户在基于 Web 的界面中编写和运行代码、展示可视化结果、添加文本说明（支持 Markdown 和 LaTeX）、嵌入图片等。Jupyter Notebook 以 `.ipynb` 文件格式保存，文件内容以单元格（cell）形式组织，支持代码单元格、Markdown 单元格和原始单元格。

Jupyter 既可以作为交互式编程工具，允许用户逐步运行代码并查看结果；也可以用于创建可分享的文档，结合代码、文本和可视化内容，适合教学、研究和报告。

### Jupyter 与其他工具的区别

- **Jupyter vs. IDE**：与传统集成开发环境（IDE，如 PyCharm、VS Code）不同，Jupyter 更注重交互性和探索式编程，适合快速原型开发和数据分析，而不是大型软件工程项目。
- **Jupyter vs. Python Shell**：相比 Python 的命令行解释器（如 `python` 或 `ipython`），Jupyter 提供更丰富的界面，支持图形化输出和文档化功能。
- **Jupyter vs. Google Colab**：Google Colab 是基于 Jupyter 的云端版本，提供了免费 GPU 支持，但需要联网且功能受限，而本地 Jupyter 更灵活，支持离线使用和更多自定义。

### Jupyter 的优势

- **交互性**：支持逐块运行代码，实时查看结果，适合数据探索和调试。
- **多语言支持**：通过内核（Kernel）机制支持多种语言。
- **文档化**：结合 Markdown、LaTeX 和代码，生成结构化的文档。
- **可视化**：无缝集成 Matplotlib、Seaborn、Plotly 等库，展示图表和可视化内容。
- **可分享**：`.ipynb` 文件易于分享，支持导出为 HTML、PDF 等格式。
- **扩展性**：支持插件（如 JupyterLab 扩展、nbextensions）增强功能。

## 安装与配置

### 安装 Jupyter

Jupyter 可以通过 Python 的包管理工具 `pip` 或 `conda` 安装。以下是安装步骤：

#### 使用 pip 安装
```bash
pip install jupyter
```

#### 使用 conda 安装（适用于 Anaconda 用户）
```bash
conda install jupyter
```

#### 验证安装
安装完成后，运行以下命令启动 Jupyter Notebook：
```bash
jupyter notebook
```

这会在默认浏览器中打开 Jupyter 的 Web 界面，通常地址为 `http://localhost:8888`。

### 配置 Jupyter

#### 设置密码
为了安全起见，可以为 Jupyter 设置访问密码：
```bash
jupyter notebook password
```
输入并确认密码后，Jupyter 会将加密后的密码存储在配置文件中。

#### 修改默认工作目录
默认情况下，Jupyter 在启动目录下工作。你可以通过以下方式修改默认目录：
1. 找到 Jupyter 配置文件（通常在 `~/.jupyter/jupyter_notebook_config.py`）。
2. 如果没有配置文件，生成一个：
   ```bash
   jupyter notebook --generate-config
   ```
3. 编辑配置文件，修改 `c.NotebookApp.notebook_dir`：
   ```python
   c.NotebookApp.notebook_dir = '/path/to/your/directory'
   ```

#### 安装其他内核
Jupyter 支持多种语言的内核，例如 R 或 Julia。安装 R 内核的示例：
```bash
# 安装 IRkernel 包
R -e "install.packages('IRkernel'); IRkernel::installspec()"
```

## 使用 Jupyter Notebook

### 启动 Jupyter Notebook

在终端运行以下命令启动 Jupyter：
```bash
jupyter notebook
```

启动后，浏览器会打开 Jupyter 的文件管理界面，显示当前目录下的文件和文件夹。

### 创建和保存 Notebook

1. **创建 Notebook**：
   - 在 Jupyter 界面点击右上角的 **New** > **Python 3**（或其他内核）。
   - 新建的 Notebook 文件以 `.ipynb` 格式保存。

2. **保存 Notebook**：
   - 点击工具栏的 **Save** 按钮（或按 `Ctrl + S`）保存。
   - 文件默认保存在当前工作目录下。

### 单元格操作

Jupyter Notebook 由单元格组成，常见的单元格类型包括：

- **代码单元格（Code Cell）**：用于编写和运行代码，默认使用选定内核（如 Python）。
- **Markdown 单元格**：用于编写格式化文本，支持 Markdown 语法和 LaTeX。
- **原始单元格（Raw Cell）**：存储未格式化的文本，通常用于特殊用途。

#### 常用快捷键
在 **命令模式**（按 `Esc` 进入，单元格边框为蓝色）：
- `A`：在上方插入新单元格。
- `B`：在下方插入新单元格。
- `DD`：删除当前单元格。
- `M`：将单元格转换为 Markdown 类型。
- `Y`：将单元格转换为代码类型。
- `Ctrl + Enter`：运行当前单元格。
- `Shift + Enter`：运行当前单元格并移到下一个单元格。

在 **编辑模式**（按 `Enter` 进入，单元格边框为绿色）：
- `Ctrl + Z`：撤销操作。
- `Ctrl + Shift + -`：分割当前单元格。

### 运行代码

在代码单元格中输入代码，按 `Shift + Enter` 执行。结果会显示在单元格下方。例如：
```python
print("Hello, Jupyter!")
```
输出：
```
Hello, Jupyter!
```

#### 显示图形
Jupyter 支持内联显示 Matplotlib 图表，需先启用内联模式：
```python
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
plt.plot(x, np.sin(x))
plt.show()
```

### 导出 Notebook

Jupyter 支持多种导出格式：
- **HTML**：适合网页分享。
- **PDF**：需要安装 `pandoc` 和 LaTeX。
- **Markdown**：导出为 `.md` 文件。
- **Python 脚本**：导出为 `.py` 文件。

导出步骤：
1. 点击 **File** > **Download as**。
2. 选择目标格式。

## Jupyter 脚本基础

### 编写交互式脚本

Jupyter Notebook 的交互性使其非常适合数据分析和探索。以下是一个简单的示例，展示如何在 Notebook 中处理数据并可视化：

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 读取数据
data = pd.read_csv("sample_data.csv")

# 数据预览
print(data.head())

# 绘制分布图
sns.histplot(data['column_name'])
plt.title("Distribution of Data")
plt.show()
```

### 使用 Markdown 增强文档

Markdown 单元格支持丰富的格式化选项，例如：
- **标题**：`# 标题1`, `## 标题2` 等。
- **列表**：
  ```markdown
  - 项目1
  - 项目2
  ```
- **代码块**：
  ```markdown
  ```python
  print("Hello")
  ```
  ```
- **LaTeX 公式**：
  ```markdown
  $$ E = mc^2 $$
  ```

### 魔法命令（Magic Commands）

Jupyter 提供内置的魔法命令，用于增强功能。分为两种：
- **行魔法命令**（以 `%` 开头）：作用于单行。
- **单元魔法命令**（以 `%%` 开头）：作用于整个单元格。

常用魔法命令：
- `%ls`：列出当前目录内容。
- `%time`：测量代码执行时间。
- `%%writefile filename`：将单元格内容写入文件。
- `%matplotlib inline`：启用 Matplotlib 内联显示。

示例：
```python
%time sum(range(1000000))
```

### 处理输入

Jupyter 支持通过 `input()` 函数获取用户输入。例如：
```python
name = input("请输入您的名字：")
print(f"你好，{name}！")
```

### 输出和可视化

Jupyter 支持多种输出格式：
- **文本输出**：通过 `print()` 或直接返回变量。
- **图形输出**：通过 Matplotlib、Seaborn 等库。
- **HTML 输出**：使用 `IPython.display` 模块。
  ```python
  from IPython.display import HTML
  HTML('<b>加粗文本</b>')
  ```

## 调试 Jupyter 脚本

### 检查异常和错误

Jupyter 会显示代码运行时的错误堆栈信息（Traceback），帮助定位问题。例如：
```python
a = 1 / 0  # 触发 ZeroDivisionError
```

### 使用调试工具

Jupyter 支持调试扩展（如 `ipdb`）。安装和使用方法：
```bash
pip install ipdb
```
在代码中添加：
```python
import ipdb; ipdb.set_trace()
```
运行到 `set_trace()` 时，代码会暂停，进入交互式调试模式。

### 日志输出

在代码中插入 `print()` 语句，检查变量值或程序流程。例如：
```python
x = 10
print(f"x 的值是: {x}")
```

### 使用 `%debug` 魔法命令

如果代码抛出异常，可以在异常发生后运行 `%debug` 进入调试模式：
```python
%debug
```

## 高级功能

### JupyterLab

JupyterLab 是 Jupyter Notebook 的下一代界面，提供更现代化的工作环境，支持多标签、文件管理器和插件系统。安装方法：
```bash
pip install jupyterlab
jupyter lab
```

### 扩展（nbextensions）

Jupyter 支持扩展以增强功能，例如代码折叠、拼写检查等。安装方法：
```bash
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```

### 远程访问

要将 Jupyter 配置为远程服务器：
1. 编辑配置文件，设置 `c.NotebookApp.ip = '0.0.0.0'`。
2. 启动 Jupyter：
   ```bash
   jupyter notebook --ip=0.0.0.0 --port=8888
   ```

### 集成其他工具

- **Git 集成**：使用 `nbdime` 进行 Notebook 的版本控制。
- **云服务**：Jupyter 可以与 AWS、Google Cloud 等云平台集成。

## 注意事项

- **性能**：Jupyter 适合交互式任务，但不适合运行长时间任务或大规模生产代码。
- **安全性**：避免在公共网络上运行未加密的 Jupyter 服务器。
- **备份**：定期保存 `.ipynb` 文件，防止数据丢失。