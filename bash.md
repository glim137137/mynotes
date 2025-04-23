# Bash

**文章参考**：[freeCodeCamp](https://www.freecodecamp.org/chinese/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/)

[TOC]

# Bash Command



## 介绍

Bash（**Bourne Again Shell**）是一个广泛使用的命令行解释器和脚本语言，主要用于类 Unix 系统（如 Linux、macOS 等）中。它是由 Brian Fox 为 GNU 项目开发的，目的是替代早期的 Bourne shell（`sh`），并在其基础上增加了许多新特性。

Bash既可以作为**命令行解释器**，允许用户输入命令并执行（这些命令可以是系统管理命令、程序执行、文件操作等）；也可以用作**脚本编程语言**，用户可以编写脚本来自动化任务、处理文本文件、进行系统管理等。

这里先介绍Bash作为命令行解释器有哪些指令。

### Bash命令与Linux命令

Bash命令和Linux命令经常被混为一谈，但它们实际上是相关但有区别的概念。

Bash命令是内置于Bash解释器中的，由Shell直接解释执行，不需要创建新进程（因为Bash本身就是一个进程），执行更快；而Linux命令本质上是操作系统提供的可执行程序，每次执行都需要创建新进程，开销较大，通常位于/bin、/usr/bin等目录。

#### 如何判断命令类型

使用`type`，`which`可以判断命令类型：

```bash
# bash
$ type -a cd
cd is a shell builtin

# linux
$ type -a ls
ls is /bin/ls
ls is /usr/bin/ls
$ which ls
/bin/ls
```

#### 所有Bash内置命令

你还可以使用`compgen -b`查看所有Bash内置命令：

```bash
$ compgen -b
.
:
[
alias
bg
bind
break
builtin
caller
cd
command
compgen
complete
compopt
continue
declare
dirs
disown
echo
enable
eval
exec
exit
export
false
fc
fg
getopts
hash
help
history
jobs
kill
let
local
logout
mapfile
popd
printf
pushd
pwd
read
readarray
readonly
return
set
shift
shopt
source
suspend
test
times
trap
true
type
typeset
ulimit
umask
unalias
unset
wait
```





## 使用Bash命令

首先值得注意的是：

**only bash** 有些常用命令并不是linux命令，如`cd`，`type`，`source`

**only linux** 但许多命令基本都只是linux命令，如`ls`，`which`，`grep`

**both bash and linux** 还有些即是linux命令又是bash命令，如`pwd`，`echo`，`printf`，`kill`，`test`

### 目录操作命令

**cd** - 改变当前目录

```bash
cd /path/to/directory
```

**pwd** - 打印当前工作目录

```bash
pwd
```

**dirs** - 显示目录栈

```bash
dirs -v
```

**pushd** - 将目录压入栈并切换

```bash
pushd /new/directory
```

**popd** - 从栈中弹出目录并切换

```bash
popd
```

### 输入输出命令

**echo** - 输出文本

```bash
echo "Hello World"
# 启用反斜杠转义字符解析
echo -e "\e[31m red word \e[0m"
# 禁用转义（默认模式）
echo -E "\e[31m no red \e[0m"
# 不输出末尾的换行符
echo -n "No newline"
```

**printf** - 格式化输出

```bash
printf "Name: %s\nAge: %d\n" "John" 25
```

**read** - 从标准输入读取

```bash
# 显示输入提示
read -p "Enter your name: " name

# 静默模式（不显示输入内容，适合密码）
read -s -p "Enter your password: " pass

# 设置超时时间（超时返回非零状态码）	
read -t 5 -p "5秒内输入: "
```

**mapfile/readarray** - 读取输入到数组

```bash
mapfile -t lines < file.txt
```

### 变量操作命令

**declare/typeset** - 声明变量属性

```bash
declare -i number=5  # 整数变量
```

**export** - 设置环境变量

```bash
export PATH=$PATH:/new/path
```

**readonly** - 创建只读变量

```bash
readonly PI=3.14159
```

**unset** - 删除变量或函数

```bash
unset VARIABLE
```

**local** - 声明局部变量(函数内使用)

```bash
function test() { local var=value; }
```

### 调试和配置命令

**set** - 设置shell选项

```bash
set -opt  # 启用选项
set +opt  # 禁用选项

# 使用未定义变量时报错
set -u nounset  

# 打印执行的每一条命令，方便调试
set -x  # 开始调试
echo "Hello"
ls /nonexistent  # 这条命令会失败
set +x  # 停止调试
```

**shopt** - 设置shell可选行为

```bash
shopt -s globstar  # 启用**递归通配
```

**trap** - 捕获信号并执行命令

```bash
trap 'echo "Interrupted!"; exit' INT
```

### 作业控制命令

**bg** - 将作业放到后台运行

```bash
bg %1
```

**fg** - 将作业带到前台运行

```bash
fg %1
```

**jobs** - 列出活动作业

```bash
jobs -l
```

**kill** - 向进程发送信号

```bash
kill -9 %1
```

### 其他实用命令

**alias** - 创建命令别名

```bash
alias ll='ls -alF'
```

**unalias** - 删除别名

```bash
unalias ll
```

**command** - 绕过函数和别名执行命令；绕过内置命令

```bash
# 忽略ls别名
command ls
# 强制使用外部echo命令而非内置echo
command echo "Hello"
```

**type** - 显示命令类型

```bash
type cd
```

**help** - 显示内置命令帮助

```bash
help cd
```

**history** - 显示命令历史

```bash
history 10
```

**source** - 在当前shell执行脚本

```bash
source config.sh
```

**eval** - 执行参数作为命令

```bash
eval "echo \$HOME"
```

**test** - 条件测试

```bash
test -f file.txt && echo "Exists"
```

**exit** - 退出shell

```bash
exit 1
```



# Bash Scripting



## 介绍

在 Linux 中，流程自动化在很大程度上依赖于 shell 脚本。这涉及到创建一个包含一系列命令的文件，这些命令可以一起执行。

### Bash 脚本的定义

Bash 脚本是一个包含一系列命令的文件，这些命令由 bash 程序逐行执行。它允许你通过命令行执行一系列操作，如导航到特定目录、创建文件夹和启动进程。

通过将这些命令保存在脚本中，你可以多次重复相同的操作，并通过运行脚本执行它们。

### Bash 脚本的优点

Bash 脚本是一种强大且灵活的工具，可以用于自动化系统管理任务、管理系统资源以及在 Unix/Linux 系统中执行其他例行任务。Shell 脚本的一些优点包括：

- **自动化**：Shell 脚本允许你自动化重复性任务和过程，节省时间并减少手动执行时可能出现的错误。
- **可移植性**：Shell 脚本可以在各种平台和操作系统上运行，包括 Unix、Linux、macOS，甚至通过使用模拟器或虚拟机在 Windows 上运行。
- **灵活性**：Shell 脚本高度可定制，可以轻松修改以满足特定需求。它们还可以与其他编程语言或实用程序结合，创建更强大的脚本。
- **易访问性**：Shell 脚本易于编写，不需要任何特殊工具或软件。它们可以使用任何文本编辑器进行编辑，并且大多数操作系统都有内置的 shell 解释器。
- **集成**：Shell 脚本可以与其他工具和应用程序集成，如数据库、Web 服务器和云服务，从而实现更复杂的自动化和系统管理任务。
- **调试**：Shell 脚本易于调试，大多数 shell 都内置调试和错误报告工具，可以帮助快速识别和修复问题。

### Bash Shell 和命令行界面的概述

"Shell" 和 "bash" 这两个术语可以互换使用。但两者之间有细微的区别。

"Shell" 这个术语是指提供命令行界面以与操作系统交互的程序。Bash（Bourne-Again SHell）是最常用的 Unix/Linux shell 之一，并且是许多 Linux 发行版中的默认 shell。

Shell 或命令行界面看起来是这样的：

![image-135](https://www.freecodecamp.org/news/content/images/2023/03/image-135.png)

Shell 接收用户的命令并显示输出。

在上述输出中，`zaira@Zaira` 是 shell 提示符。当 shell 以交互方式使用时，在等待用户命令时会显示一个 `$`。

如果 shell 以 root（具有管理权的用户）身份运行，提示符会变为 `#`。超级用户 shell 提示符看起来是这样的：

```bash
[root@host ~]#
```

Bash 是 shell 的一种，还有其他 shell 可供使用，如 Korn shell（ksh）、C shell（csh）和 Z shell（zsh）。每种 shell 都有自己的语法和功能，但它们都有一个共同的目的，那就是提供一个命令行界面来与操作系统交互。

```bash
ps
```

这是我的输出结果：

![检查 shell 类型，我使用的是 bash shell](https://www.freecodecamp.org/news/content/images/2023/03/image-134.png)

> 检查 shell 类型，我使用的是 bash shell

总结一下，“shell” 是指任何提供命令行界面的程序的一个广泛术语，“Bash” 是一种特定类型的 shell，在 Unix/Linux 系统中广泛使用。

注意：在本教程中，我们将使用 “bash" shell。

### 从命令行运行 Bash 命令

如前所述，shell 提示符看起来像这样：

```bash
[username@host ~]$
```

你可以在 `$` 符号后输入任何命令，并在终端上看到输出。

通常，命令遵循以下语法：

```
command [选项] 参数
```

让我们讨论一些基本的 bash 命令并查看它们的输出。确保跟着做哦 :)

- `date`：显示当前日期

```bash
zaira@Zaira:~/shell-tutorial$ date
Tue Mar 14 13:08:57 PKT 2023
```

- `pwd`：显示当前工作目录。

```bash
zaira@Zaira:~/shell-tutorial$ pwd
/home/zaira/shell-tutorial
```

- `ls`：列出当前目录的内容。

```bash
zaira@Zaira:~/shell-tutorial$ ls
check_plaindrome.sh  count_odd.sh  env  log  temp
```

- `echo`：打印一段文本或变量的值到终端。

```bash
zaira@Zaira:~/shell-tutorial$ echo "Hello bash"
Hello bash
```

你可以始终使用 `man` 命令查看命令手册。

例如，`ls` 的手册看起来像这样：

![你可以使用 `man` 命令详细查看命令的选项](https://www.freecodecamp.org/news/content/images/2023/03/image-138.png)

> 你可以使用 `man` 命令详细查看命令的选项





## 创建和执行 Bash 脚本

### 脚本命名约定

按照惯例，bash 脚本以 `.sh` 结尾。然而，即使没有 `sh` 扩展名，bash 脚本也可以正常运行。

### 添加 Shebang

Bash 脚本以 `shebang` 开头。Shebang 是 `bash #` 和 `bang !` 的组合，后跟 bash shell 路径。这是脚本的第一行。Shebang 告诉 shell 通过 bash shell 执行它。Shebang 指向 bash 解释器的绝对路径。

以下是 shebang 语句的示例。

```bash
#!/bin/bash
```

你可以使用以下命令找到你的 bash shell 路径（可能与上述路径不同）：

```bash
which bash
```

### 创建一个 bash 脚本

我们的第一个脚本提示用户输入路径。然后，它将列出路径的内容。

使用 `vi` 命令创建一个名为 `run_all.sh` 的文件。您可以使用任何您喜欢的编辑器。

```bash
vi run_all.sh
```

在文件中添加以下命令并保存：

```bash
#!/bin/bash
echo "今天是 " `date`

echo -e "\n请输入目录路径"
read the_path

echo -e "\n 你的路径包含以下文件和文件夹："
ls $the_path
```

打印用户提供的目录内容的脚本

让我们逐行仔细看看脚本。我将再次显示相同的脚本，但这次带有行号。

```bash
  1 #!/bin/bash
  2 echo "今天是 " `date`
  3
  4 echo -e "\n请输入目录路径"
  5 read the_path
  6
  7 echo -e "\n 你的路径包含以下文件和文件夹："
  8 ls $the_path
```

- 第 1 行：Shebang (`#!/bin/bash`) 指向 bash shell 路径。

- 第 2 行：`echo` 命令在终端显示当前日期和时间。注意 `date` 在反引号中。

    > 反引号 (`) 用于命令替换。命令替换是指将反引号内的命令执行，并将其输出替换到反引号所在的位置。

- 第 4 行：我们希望用户输入一个有效的路径。

- 第 5 行：`read` 命令读取输入并将其存储在变量 `the_path` 中。

- 第 8 行：`ls` 命令使用存储路径的变量并显示当前的文件和文件夹。

### 执行 bash 脚本

为了使脚本可执行，请使用以下命令为您的用户分配执行权限：

```bash
chmod u+x run_all.sh
```

这里，

- `chmod` 修改文件的所有权以供当前用户使用：`u`。
- `+x` 将执行权限添加到当前用户。这意味着作为所有者的用户现在可以运行该脚本。
- `run_all.sh` 是我们希望运行的文件。

您可以使用下列任何方法运行脚本：

- `sh run_all.sh`
- `bash run_all.sh`
- `./run_all.sh`

让我们看看它在运行中的样子 🚀

![run-script-bash-2](https://www.freecodecamp.org/news/content/images/2023/03/run-script-bash-2.gif)

## Bash 脚本基础

### 注释

Bash 脚本中的注释以 `#` 开头。这意味着任何以 `#` 开头的行都是注释，将被解释器忽略。

注释对于文档编写非常有帮助，并且是帮助他人理解代码的一个好习惯。

以下是注释的示例：

```bash
# 这是一个示例注释
# 这两行将被解释器忽略
```

### 变量和数据类型

变量让您存储数据。您可以在脚本中使用变量读取、访问和操作数据。

Bash 中没有数据类型。在 Bash 中，变量能够存储数值、单个字符或字符串。

在 Bash 中，您可以通过以下方式使用和设置变量值：

```bash
country=Pakistan
```

2. 根据从程序或命令获取的输出，使用命令替换赋值。请注意，`$` 是访问现有变量值所需的。

```bash
same_country=$country
```

这会将 `country` 的值赋给新变量 `same_country`

要访问变量值，请在变量名称后附加 `$`。

```bash
zaira@Zaira:~$ country=Pakistan
zaira@Zaira:~$ echo $country
Pakistan
zaira@Zaira:~$ new_country=$country
zaira@Zaira:~$ echo $new_country
Pakistan
```

赋值和打印变量值

#### 变量命名规范

在 Bash 脚本中，以下是变量命名规范：

1. 变量名称应以字母或下划线 (`_`) 开头。
2. 变量名称可以包含字母、数字和下划线 (`_`)。
3. 变量名称区分大小写。
4. 变量名称不应包含空格或特殊字符。
5. 使用能反映变量用途的描述性名称。
6. 避免使用保留关键字（如 `if`, `then`, `else`, `fi` 等）作为变量名称。

以下是一些合法变量名称的示例：

```bash
name
count
_var
myVar
MY_VAR
```

以下是一些非法变量名称的示例：

```bash
2ndvar (变量名称以数字开头)
my var (变量名称包含空格)
my-var (变量名称包含连字符)
```

遵循这些命名规范有助于使 Bash 脚本更具可读性和易于维护。

#### 字符串

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字符串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

双引号的优点：

- 双引号里可以有变量
- 双引号里可以出现转义字符

- [ ] 使用双引号拼接

```bash
your_name="Peter"
greeting="Hello, "$your_name" !"
greeting_1="Hello, ${your_name} !"
echo $greeting  $greeting_1
```

- [ ] 使用`#`获取字符串长度

```bash
string="abcd"
echo ${#string}   # 输出 4
```

- [ ] 提取子字符串

```bash
string="runoob is a great site"
echo ${string:1:4} # 输出 unoo
```





#### 数组

Bash数组中可以存放多个值，但只支持一维数组（不支持多维数组）。

- [ ] 创建一个简单的数组 my_array

```bash
my_array=(A B "C" D)
```

- [ ] 读取数组

```bash
echo "First element: ${my_array[0]}"
echo "All array's element: ${my_array[*]}"
echo "All array's element: ${my_array[@]}"
echo "Array length: ${#my_array[@]}"
```





### 输入和输出

#### 收集输入

在本节中，我们将讨论一些为脚本提供输入的方法。

1. 读取用户输入并将其存储在变量中

我们可以使用 `read` 命令读取用户输入。

```bash
#!/bin/bash 

echo "What's your name?" 

read entered_name 

echo -e "\nWelcome to bash tutorial" $entered_name
```

![name-sh](https://www.freecodecamp.org/news/content/images/2023/03/name-sh.gif)

2. 从文件读取

此代码从名为 `input.txt` 的文件中读取每一行并将其打印到终端。我们将在本文稍后学习 while 循环。

```bash
while read line
do
  echo $line
done < input.txt
```

3. 命令行参数

在 bash 脚本或函数中，`$1` 表示传递的初始参数，`$2` 表示传递的第二个参数，以此类推。

> 在 Bash 中，`\$1`、`\$2`、`\$3` 等是**位置参数**，用于表示脚本或函数中传递给脚本或函数的参数。

此脚本将名字作为命令行参数并打印个性化问候语。

```bash
echo "Hello, $1!"
```

我们将 `Zaira` 作为参数提供给脚本。

```bash
#!/bin/bash
echo "Hello, $1!"
```

脚本代码：`greeting.sh`

运行脚本，输出：

![name-sh-1](https://www.freecodecamp.org/news/content/images/2023/03/name-sh-1.gif)

另外，还有几个特殊字符用来处理参数：

| 参数处理 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数。使用时加引号，并在引号中返回每个参数。“1 2 3”（传递了一个参数） |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*稍有不同。“1”，“2”，“3”（传递了三个参数）                |
| $-       | 显示Shell使用的当前选项，与[set命令](https://www.runoob.com/linux/linux-comm-set.html)功能相同。 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

#### 显示输出

这里我们将讨论一些从脚本接收输出的方法。

1. 打印到终端：

```bash
echo "Hello, World!"
```

这会将文本 “Hello, World!” 打印到终端。

2. 写入文件：

```bash
echo "This is some text." > output.txt
```

这会将文本 "This is some text." 写入名为 `output.txt` 的文件。请注意，`>` 操作符会覆盖文件内容（如果文件已存在）。

3. 追加到文件：

```bash
echo "More text." >> output.txt
```

这会将文本 "More text." **追加**到 `output.txt` 文件的末尾。

4. 重定向输出：

```bash
ls > files.txt
```

这会列出当前目录中的文件并将输出写入名为 `files.txt` 的文件。您可以通过这种方式将任何命令的输出**重定向**到文件。

#### 使用 ANSI 颜色码

ANSI 颜色码（ANSI Escape Codes）用于在终端中更改文本的显示颜色。它们是由一系列特殊字符组成的命令，可以控制文本和背景颜色、文本动画、光标位置等。

> 使用 ANSI 颜色码时，通常通过 `\e[颜色代码m` 来改变文本的颜色，后面跟上需要显示的文本，最后使用 `\e[0m` 来重置颜色（恢复为默认颜色）。我们需要使用 `-e` 标志来告诉 Bash 解释转义字符 `\`。

```bash
# 将 PASS 显示为绿色，FAIL 显示为红色
echo -e "\e[32mPASS\e[0m"
echo -e "\e[31mFAIL\e[0m"
```

常见的颜色和对应的 ANSI 代码：

| 颜色   | ANSI 代码 | 示例代码                    |
| ------ | --------- | --------------------------- |
| 黑色   | `\e[30m`  | `echo -e "\e[30mText\e[0m"` |
| 红色   | `\e[31m`  | `echo -e "\e[31mText\e[0m"` |
| 绿色   | `\e[32m`  | `echo -e "\e[32mText\e[0m"` |
| 黄色   | `\e[33m`  | `echo -e "\e[33mText\e[0m"` |
| 蓝色   | `\e[34m`  | `echo -e "\e[34mText\e[0m"` |
| 品红色 | `\e[35m`  | `echo -e "\e[35mText\e[0m"` |
| 青色   | `\e[36m`  | `echo -e "\e[36mText\e[0m"` |
| 白色   | `\e[37m`  | `echo -e "\e[37mText\e[0m"` |

额外提示：

为了在脚本中快速替换文本的颜色，你可以使用查找和替换功能（Ctrl+F），将所有的 `echo "PASS"` 和 `echo "FAIL"` 替换为带有颜色的版本，这样可以快速调整整个脚本中的颜色。



### 基本 Bash 命令

以下是一些最常用的 bash 命令列表：

1. `cd`: 切换到不同目录。
2. `ls`: 列出当前目录的内容。
3. `mkdir`: 创建新目录。
4. `touch`: 创建新文件。
5. `rm`: 删除文件或目录。
6. `cp`: 复制文件或目录。
7. `mv`: 移动或重命名文件或目录。
8. `echo`: 将文本打印到终端。
9. `cat`: 连接并打印文件内容。
10. `grep`: 在文件中搜索模式。
11. `chmod`: 更改文件或目录的权限。
12. `sudo`: 以管理权限运行命令。
13. `df`: 显示可用磁盘空间。
14. `history`: 显示先前执行的命令列表。
15. `ps`: 显示有关正在运行的进程的信息。

### 条件语句

产生布尔结果（真或假）的表达式称为条件。有多种方法来评估条件，包括 `if`、`if-else`、`if-elif-else` 和嵌套条件。

**语法**：

```bash
if [[ condition ]];
then
	statement
elif [[ condition ]]; then
	statement 
else
	do this by default
fi
```

Bash 条件语句的语法

我们可以使用**逻辑运算符**（ 如 AND `-a` 和 OR `-o`，NOT `!` ）进行更具意义的比较。

```bash
if [ $a -gt 60 -a $b -lt 100 ]
```

> 此处使用单括号也可以实现。但`[[ ... ]]` 是 Bash 中的一种改进语法，比 `[ ... ]` 更强大、灵活，支持更多的操作符和特性。

此语句检查两个条件是否都为真：a 大于 60 且 b 小于 100。

让我们看一个使用 `if`、`if-else` 和 `if-elif-else` 语句的 Bash 脚本示例，以确定用户输入的数字是正数、负数还是零：

```bash
#!/bin/bash

echo "Please enter a number: "
read num
```

确定数字是正数、负数还是零的脚本

该脚本首先提示用户输入一个数字。然后，它使用一个 `if` 语句检查该数字是否大于 0。如果是的话，脚本输出该数字是正数。如果该数字不大于 0，脚本进入下一个语句，即 `if-elif` 语句。在这里，脚本检查该数字是否小于 0。如果是的话，脚本输出该数字是负数。最后，如果该数字既不大于 0 也不小于 0，脚本使用 `else` 语句输出该数字是零。

来看一下它的运行情况 🚀

![test-odd](https://www.freecodecamp.org/news/content/images/2023/03/test-odd.gif)

#### 0代表true

这和大多数编程语言的惯例不同。在Bash中，`0` 被认为是 **true**。

- `if` 语句检查条件，如果返回 `0`（即成功），它被视为 true，并且执行 `then` 块中的代码。
- 如果你写 `if [ 1 ]`，Bash会认为1是 false，`else` 块中的代码将被执行。

#### test命令

bash中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

数值测试：

```bash
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo 'equal'
else
    echo 'not equal'
fi
```

| 参数 | 说明           |
| :--- | :------------- |
| -eq  | 等于则为真     |
| -ne  | 不等于则为真   |
| -gt  | 大于则为真     |
| -ge  | 大于等于则为真 |
| -lt  | 小于则为真     |
| -le  | 小于等于则为真 |

字符串测试：

```bash
num1="ru1noob"
num2="runoob"
if test $num1 = $num2
then
    echo 'equal!'
else
    echo 'not equal!'
fi
```

| 参数      | 说明                     |
| :-------- | :----------------------- |
| =         | 等于则为真               |
| !=        | 不相等则为真             |
| -z 字符串 | 字符串的长度为零则为真   |
| -n 字符串 | 字符串的长度不为零则为真 |

文件测试：

```bash
cd /bin
if test -e ./bash
then
    echo '文件已存在!'
else
    echo '文件不存在!'
fi
```

| 参数      | 说明                                 |
| :-------- | :----------------------------------- |
| -e 文件名 | 如果文件存在则为真                   |
| -r 文件名 | 如果文件存在且可读则为真             |
| -w 文件名 | 如果文件存在且可写则为真             |
| -x 文件名 | 如果文件存在且可执行则为真           |
| -s 文件名 | 如果文件存在且至少有一个字符则为真   |
| -d 文件名 | 如果文件存在且为目录则为真           |
| -f 文件名 | 如果文件存在且为普通文件则为真       |
| -c 文件名 | 如果文件存在且为字符型特殊文件则为真 |
| -b 文件名 | 如果文件存在且为块特殊文件则为真     |



### 循环和分支

#### While 循环

While 循环检查一个条件，并且在条件为 `true` 时持续循环。我们需要提供一个计数器语句来增加计数器以控制循环的执行。

在下面的例子中，`(( i += 1 ))` 是增加 `i` 值的计数器语句。该循环将恰好运行 10 次。

```bash
#!/bin/bash
i=1
while [[ $i -le 10 ]] ; do
   echo "$i"
  (( i += 1 ))
done
```

While 循环迭代 10 次。

![image-187](https://www.freecodecamp.org/news/content/images/2023/03/image-187.png)

#### For 循环

`for` 循环，就像 `while` 循环一样，允许你执行特定次数的语句。每个循环在语法和用法上有所不同。

在下面的例子中，该循环将迭代 5 次。

```bash
#!/bin/bash

for i in {1..5}
do
    echo $i
done
```

For 循环迭代 5 次。

![image-186](https://www.freecodecamp.org/news/content/images/2023/03/image-186.png)

你还可以使用使用 C 风格的语法 `for((…))`：

```bash
#!/bin/bash

# 从 1 到 5 输出数字
for (( i=1; i<=5; i++ ))
do
    echo "数字: $i"
done

```

此外，如果你需要遍历数组，文件，目录也有对应的方法：

```bash
#!/bin/bash

# 定义一个列表
fruits=("apple" "banana" "cherry")

# 1.遍历列表中的元素
for fruit in "${fruits[@]}"
do
    echo "水果: $fruit"
done

# 假设有一个名为 list.txt 的文件
# 文件内容：
# apple
# banana
# cherry

# 2.遍历文件中的每一行
for fruit in $(cat list.txt)
do
    echo "水果: $fruit"
done

# 3.遍历当前目录下的所有文件
for file in *
do
    echo "文件: $file"
done
```

#### Case 语句

在 Bash 中，case 语句用于将给定值与一系列模式进行比较，并根据第一个匹配的模式执行一段代码。Bash 中 case 语句的语法如下：

```bash
case expression in
    pattern1)
        # code to execute if expression matches pattern1
        ;;
    pattern2)
        # code to execute if expression matches pattern2
        ;;
    pattern3)
        # code to execute if expression matches pattern3
        ;;
    *)
        # code to execute if none of the above patterns match expression
        ;;
esac
```

Case 语句语法

这里，“`expression`” 是我们想要比较的值，“`pattern1`”、“`pattern2`”、“`pattern3`”等是我们想要进行比较的模式。

双分号 `;;` 将要为每个模式执行的代码块分隔开来。星号 `*` 代表默认情况，当没有一个指定的模式匹配该表达式时执行。

让我们看一个例子。

```bash
fruit="apple"

case $fruit in
    "apple")
        echo "This is a red fruit."
        ;;
    "banana")
        echo "This is a yellow fruit."
        ;;
    "orange")
        echo "This is an orange fruit."
        ;;
    *)
        echo "Unknown fruit."
        ;;
esac
```

Case 语句示例

在这个例子中，由于 “fruit” 的值是 “apple”，第一个模式匹配，并且执行 echo “This is a red fruit.” 的代码块。如果 “fruit” 的值是 “banana”，第二个模式将匹配并执行 echo “This is a yellow fruit.” 的代码块，依此类推。如果 “fruit” 的值不匹配任何指定的模式，则执行默认情况，输出 “Unknown fruit.”。



### 函数

Bash函数是Bash脚本中可重复使用的一段代码块。你可以将常用的操作封装成函数，以便在脚本中多次调用。下面是一个Bash函数的基本语法和示例。

```bash
function function_name {
    # 函数内容
}
# 或者
function_name() {
    # 函数内容
}
```

#### 带参数的函数

`bash`的函数接受参数不像其他编程语言声明在`()`中，而是依旧以命令行参数的形式。

```bash
#!/bin/bash

# 定义一个带参数的函数
greet() {
    echo "Hello, \$1!"
}

# 调用函数并传递参数
greet "Alice"

```

#### 返回值

Bash函数不能直接返回值，通常使用`echo`来输出返回值并通过命令替换来接收结果。

```bash
#!/bin/bash

# 定义一个返回值的函数
add() {
    result=$(( \$1 + \$2 ))
    echo $result
}

# 调用函数并接收返回值
sum=$(add 5 10)
echo "The sum is: $sum"

```

#### 局部变量

在函数内部，你可以使用`local`关键字来定义局部变量，以防止与外部变量冲突。

```bash
#!/bin/bash

# 定义一个使用局部变量的函数
calculate_area() {
    local width=\$1
    local height=\$2
    local area=$(( width * height ))
    echo "The area is: $area"
}

# 调用函数
calculate_area 5 10

```



## 调试 Bash 脚本

调试和排除故障是任何 Bash 脚本编写者的重要技能。虽然 Bash 脚本可以非常强大，但它们也容易出现错误和意外行为。在本节中，我们将讨论一些调试和排除 Bash 脚本故障的技巧和技术。

调试 Bash 脚本最有用的技巧之一是在脚本的开头设置 `set -x` 选项。这个选项启用了调试模式，使得 Bash 会在终端中打印它执行的每个命令，并以 `+` 符号作为前缀。这对于识别脚本中出现错误的位置非常有帮助。

```bash
#!/bin/bash

set -x

# 您的脚本放在这里
```

### 检查退出码

当 Bash 遇到错误时，它会设置一个退出码来指示错误的性质。您可以使用 `$?` 变量检查最近命令的退出码。值为 `0` 表示成功，而任何其他值表示错误。

```bash
#!/bin/bash

# 您的脚本放在这里

if [ $? -ne 0 ]; then
    echo "发生错误。"
fi
```

### 使用 `echo` 语句

另一个调试 Bash 脚本的有用技巧是在代码中插入 `echo` 语句。这可以帮助您识别错误发生的位置以及变量传递的值是什么。

```bash
#!/bin/bash

# 您的脚本放在这里

echo "变量 x 的值是: $x"

# 更多代码放在这里
```

### 使用 `set -e` 选项

如果您希望在脚本中的任何命令失败时立即退出脚本，您可以使用 `set -e` 选项。这个选项会使 Bash 在脚本中的任何命令失败时退出并带有错误，这样可以更容易地识别和修复脚本中的错误。

```bash
#!/bin/bash

set -e

# 您的脚本放在这里
```