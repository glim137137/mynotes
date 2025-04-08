# CMD（Command Prompt）命令提示符

[TOC]



# CMD Command

## 简介

### 什么是CMD

`cmd` 是 Windows 系统中的 **命令提示符（Command Prompt）**，用于执行各种命令、批处理脚本和系统管理任务。

作为 Windows 操作系统中内置的**命令行工具**，它提供了一种直接与计算机系统进行交互的方式。虽然现代操作系统提供了许多图形化界面和工具，但命令提示符在某些场景下仍然具有重要的作用。

### 如何打开

- 在windows系统中，按下 **`Win + R`**，输入 `cmd`，回车即可打开。
- 在文件资源管理器的地址栏直接输入 `cmd` 并回车，会在当前路径打开命令提示符。



## 常用 cmd 命令

### 文件管理

#### 文件和目录操作

`cd`

`dir`

`mkdir`

#### 文件查看和编辑

`del`

`copy`

### 系统管理

`shutdown`

#### 进程管理

`tasklist`

`taskkill`

### 网络通讯

`ping`

`ipconfig`

### 其他实用命令

`cls`

`exit`





# Batch Scripting

## 介绍

Batch 脚本（`.bat` 或 `.cmd` 文件）是 Windows 命令行（`cmd.exe`）的自动化脚本，用于执行一系列命令。它适用于系统管理、自动化任务和简单编程。

## 创建和运行 Batch 文件

- 用 **记事本** 编写脚本，保存为 `.bat` 或 `.cmd` 文件（如 `test.bat`）。
- 双击运行，或在 CMD 里输入文件名执行（如 `test.bat`）。

### 第一个Batch脚本

```bat
@echo off
echo Hello, World!
pause
```

第一行的`@echo off`是用来**关闭回显**的，即**不显示执行的命令**。在脚本运行时，执行脚本中的命令但是命令行窗口不显示出来。`pause`是**暂停**，**等待用户按键**。

## Batch Scripting 基本语法

### 注释

在`batch`中注释有两种：`rem` 和 `::`

```bat
rem this is a comment
:: this is a comment
```

### 数据类型

#### 字符串

**默认所有变量都是字符串**，即使赋值数字也会被当作字符串处理。字符串主要有两种操作，**字符串截取**和**字符串替换**。

字符串截取。 `%var:~n,k%`，其中`%var`，表示待截取字符的字符串，"`~`"取字符标志符，"`n`”表示字符截取起始位置，"`k`" 表示截取结束位置（不包含该字符）。

```bat
@echo off 
set str=superhero
echo str=%str%    	:: superhero
echo %str:~0,5%		:: super
echo %str:~3%		:: erhero
echo %str:~-3% 		:: ero
echo %str:~0,-3% 	:: superh
pause
```

字符串替换。`%var:old_str=new_str%` 

```bat
@echo off 
set str=hello world!
set temp=%str:hello=good% 
echo %temp%   		:: good world!
pause 
```

#### 整数

使用 `set /a` 进行**算术运算**，此时变量会被当作整数。`bat`支持 `+`, `-`, `*`, `/`, `%`（取模）等运算。

```BAT
@echo off
set /a num1=10
set /a num2=5
set /a sum=num1 + num2
echo Sum: %sum%
```

#### 布尔值

`Batch` 没有真正的布尔类型，通常用 `0`（成功/真）和 `1`（失败/假）表示。

`if` 语句判断 `ERRORLEVEL` 时常用这种方式。更多见“流程控制 -> if-else条件判断”。

```bat
@echo off
ping -n 1 google.com >nul
if %ERRORLEVEL%==0 (
    echo Success (True)
) else (
    echo Failed (False)
)
```

#### Batch不支持数组

`Batch` 不直接支持数组。

### 变量设置和读取

变量常常用`% variable %`括起来。

使用 `set` 设置变量：

```bat
@echo off
set name=Alice
set age=25
echo My name is %name% and I am %age% years old.
pause
```

- [ ] 你还可以使用`-p`参数来接受**用户输入**：

```bat
@echo off
set /p name=What is your name? 
echo Hello, %name%!
pause
```

#### 命令行参数

```bat
@echo off
echo First argument: %1
echo Second argument: %2
pause
> test.bat Apple Banana
```

#### 环境变量

环境变量就是 Windows 内置变量：

```bat
%CD%   			rem 获取当前目录
%PATH%  		rem 获取命令搜索路径
%DATE%  		rem 获取当前日期。
%TIME%  		rem 获取当前时间。
%RANDOM% 		rem 获取 0 和 32767 之间的任意十进制数字。
%ERRORLEVEL% 	rem 获取上一命令执行结果码
```

### 流程控制

#### if-else条件判断

```bat
@echo off
set num=10
if %num%==10 (
    echo Number is 10
) else (
    echo Number is not 10
)
pause
```

接下来介绍一下`bat`的**比较运算符**与**逻辑运算符**

- `==` 等于
- `neq` 不等于
- `lss` 小于
- `leq` 小于等于
- `gtr` 大于
- `geq` 大于等于
- `batch`的逻辑运算符只有`not`

命令执行会有成功或失败，往往执行的情况会参与到条件判断中去。`ERRORLEVEL`是最后运行的程序返回一个等于或大于指定数字的**退出代码**，`ERRORLEVEL=0`代表命令**成功**执行，`ERRORLEVEL>0` 则命令**失败**。

- [ ] 使用`ERRORLEVEL`参与条件判断

```bat
rem "if errorlevel 1 表示 errorlevel >= 1（不是 ==1）。"
rem "如果需要精确匹配，使用 if %errorlevel%==1。"
@echo off
some_command.exe
if errorlevel 1 (
    echo 命令失败！错误码: %errorlevel%
)

rem "手动设置 errorlevel"
@echo off
echo 执行某个操作...
if not exist "C:\file.txt" (
    echo 文件不存在！
    exit /b 1
)
exit /b 0
```

#### for循环

`for /param %variable in (set) do (commands)`

**默认 遍历当前目录下的文件（不包括子目录）**：

```bat
@echo off
for %%i in (*.txt) do (
    echo 找到文件: %%i
)
```

**/d 遍历目录(不递归，不包括文件)**：

```bat
@echo off
for /d %%i in (*.txt) do (
    echo File: %%i
)
pause
```

**/r 递归遍历目录和文件**：

```bat
@echo off
for /r "C:\MyFolder" %%i in (*.txt) do (
    echo 找到TXT文件: %%i
)
```

**/l 数字循环**：

```bat
@echo off
for /l %%i in (1,2,5) do (
    echo Count: %%i
)
pause
> Count: 1, 3, 5
```

**/f 解析文本文件**：

```bat
@echo off
for /f "tokens=*" %%i in (data.txt) do (
    echo Line: %%i
)
pause
```

```
eol=c 处理时跳过起始为c字符的行，通常用于跳过注释行。
skip=n  跳过文件开始的n行
delims=xxx  指定分隔符集。这个替换了空格和制表符的默认分隔符集。
tokens=x,y,m-n  被分隔各字段的处理。
usebackq   需使用双引号包含文件名时考虑，具体使用执行help for查看
```

#### Batch不支持while循环

`Batch`不支持`while`循环
