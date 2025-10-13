# Cpp

[TOC]

# 基本语法



## 基本输入输出

最基本的输入输出功能是通过 **标准库** `<iostream>` 提供的。这个库定义了四个关键对象来处理标准输入和输出流：

1.  `std::cout` - 用于向**标准输出设备**（通常是屏幕/控制台）写入数据。（**输出**）
2.  `std::cin` - 用于从**标准输入设备**（通常是键盘）读取数据。（**输入**）
3.  `std::cerr` - 用于输出错误信息。（无缓冲，立即显示）
4.  `std::clog` - 用于输出日志信息。（有缓冲）

对于初学者来说，最常用的是 `std::cout` 和 `std::cin`。

### 输出 (std::cout)

`std::cout` 与 **插入运算符** `<<` 一起使用，将数据发送到控制台。

**基本语法：**
```cpp
std::cout << 要输出的数据;
```
你可以连续使用 `<<` 来输出多个数据。

**示例：**
```cpp
#include <iostream> // 必须包含这个头文件

int main() {
    // 输出字符串和换行符 (\n)
    std::cout << "Hello, World!\n";

    // 输出变量和字符串
    int age = 25;
    std::cout << "I am " << age << " years old.\n";

    // 使用 std::endl 来换行并刷新缓冲区
    std::cout << "This is a line." << std::endl;
    std::cout << "This is another line.";

    // 输出计算结果
    int a = 10, b = 20;
    std::cout << "\nThe sum of " << a << " and " << b << " is " << a + b << std::endl;

    return 0;
}
```
**输出结果：**
```
Hello, World!
I am 25 years old.
This is a line.
This is another line.
The sum of 10 and 20 is 30
```

**`\n` 与 `std::endl` 的区别：**
*   `\n` 只是一个换行符。
*   `std::endl` 不仅插入一个换行符，还会**刷新输出缓冲区**。这确保了输出能立即显示，但可能略微影响性能。在大多数简单程序中，你可以互换使用它们。

### 输入 (std::cin)

`std::cin` 与 **提取运算符** `>>` 一起使用，从键盘读取输入数据。

**基本语法：**
```cpp
std::cin >> 变量;
```
你可以连续使用 `>>` 来读取多个输入。

**示例：**
```cpp
#include <iostream>
using namespace std; // 这样后面就不用总是写 std:: 了

int main() {
    int number;
    double price;
    string name; // string 类型需要包含 <string>，但通常 <iostream> 已间接包含

    cout << "Enter an integer: ";
    cin >> number; // 从键盘读取一个整数到变量 number

    cout << "Enter a floating-point number: ";
    cin >> price; // 读取一个浮点数到变量 price

    cout << "Enter your name: ";
    cin >> name; // 读取一个字符串（遇到空格、制表符、换行符会停止）

    cout << "Hi " << name << ", the product of " << number << " and " << price << " is " << number * price << endl;

    return 0;
}
```
**运行示例：**
```
Enter an integer: 5
Enter a floating-point number: 12.5
Enter your name: Alice
Hi Alice, the product of 5 and 12.5 is 62.5
```

**注意：**
*   `cin >>` 读取字符串时会在**第一个空白字符（空格、制表符、换行）处停止**。这意味着你无法用 `cin >>` 读取带有空格的句子。
*   上面的程序如果输入 `Alice Smith` 作为名字，`name` 变量将只包含 `"Alice"`。

### 读取一行输入 (std::getline)

为了解决 `cin` 无法读取带空格字符串的问题，我们需要使用 `std::getline` 函数。

**基本语法：**
```cpp
std::getline(std::cin, string变量);
```

**示例：**
```cpp
#include <iostream>
#include <string> // 明确包含 string 头文件是好习惯

using namespace std;

int main() {
    int age;
    string fullName;

    cout << "Enter your age: ";
    cin >> age;

    // 在混合使用 cin >> 和 getline 时，需要先清除缓冲区中残留的换行符
    cin.ignore(); // 非常重要！

    cout << "Enter your full name: ";
    getline(cin, fullName); // 读取一整行，包括空格，直到按下回车

    cout << "Hello, " << fullName << ". You are " << age << " years old." << endl;

    return 0;
}
```
**运行示例：**
```
Enter your age: 30
Enter your full name: Alice Smith
Hello, Alice Smith. You are 30 years old.
```

**关键点：**
*   `cin.ignore();` 在这里至关重要。当你用 `cin >> age` 输入年龄并按回车后，键盘缓冲区里留下了一个 `\n`（换行符）。接下来的 `getline()` 会立刻读到这个 `\n`，认为这是一个空行，然后就停止了。`cin.ignore()` 的作用就是清除掉这个残留的换行符。
*   `std::getline` 会读取所有字符，直到遇到换行符（回车键），然后将内容存入字符串变量（不包括最后的换行符）。

### 使用命名空间 (std::)

你可能已经注意到，我们在每个 `cout`, `cin`, `endl` 前面都加上了 `std::`。这是为了指明它们属于 `std` 这个**命名空间**，以避免命名冲突。

为了简化代码，一种常见的做法是在文件开头使用 `using namespace std;`。这样编译器就知道程序中使用的 `cout`, `cin` 等默认来自 `std` 命名空间，就不需要每次都写 `std::` 前缀了。

**两种写法的对比：**

| 写法一（显式指定）       | 写法二（使用 `using`） |
| :----------------------- | :--------------------- |
| `#include <iostream>`    | `#include <iostream>`  |
| `int main() {`           | `using namespace std;` |
| ` std::cout << "Hello";` | `int main() {`         |
| ` std::cin >> x;`        | ` cout << "Hello";`    |
| ` return 0;`             | ` cin >> x;`           |
| `}`                      | ` return 0;`           |
|                          | `}`                    |

*   **对于小程序和学习**，使用 `using namespace std;` 很方便。
*   **在大型项目或头文件中**，更推荐显式地写 `std::`，以避免潜在的命名冲突。



## 基本数据类型

C++ 提供了丰富的基本数据类型（也称为**内置类型**），它们用于定义变量可以存储的数据种类和大小。这些类型大致可以分为四类：
1.  **整型**：用于表示整数
2.  **浮点型**：用于表示小数
3.  **字符型**：用于表示单个字符
4.  **布尔型**：用于表示真/假值

此外，C++ 还提供了 `void` 类型和指针类型，但我们先聚焦于这四大类。

### 整型 (Integer Types)

用于存储整数（没有小数部分）。区别在于它们占用的内存大小不同，从而决定了能够表示的数值范围。

| 数据类型    | 典型大小    | 表示范围                        | 说明                             |
| :---------- | :---------- | :------------------------------ | :------------------------------- |
| `short`     | 2 字节      | -32,768 到 32,767               | 短整型                           |
| `int`       | 4 字节      | -2,147,483,648 到 2,147,483,647 | 最常用的整型                     |
| `long`      | 4 或 8 字节 |                                 | 长整型（大小取决于系统和编译器） |
| `long long` | 8 字节      | -(2^63) 到 (2^63)-1             | 超长整型（C++11 引入）           |

**修饰符：** `signed` 和 `unsigned`
*   `signed`（默认）：表示有符号数，可以包含正数和负数。
*   `unsigned`：表示无符号数，只能包含正数和零，但正数范围扩大一倍。

例如：
*   `unsigned int`：范围是 0 到 4,294,967,295
*   `unsigned short`：范围是 0 到 65,535

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    short smallNumber = 1000;
    int population = 1000000; // 最常用
    long bigNumber = 1000000000L; // 后缀 L 表示 long 类型
    long long hugeNumber = 1000000000000LL; // 后缀 LL 表示 long long 类型

    unsigned int positiveOnly = 4000000000; // 无符号，不能为负
    unsigned short us = 65000;

    cout << "smallNumber: " << smallNumber << endl;
    cout << "hugeNumber: " << hugeNumber << endl;
    cout << "positiveOnly: " << positiveOnly << endl;

    return 0;
}
```

### 浮点型 (Floating-point Types)

用于存储带小数点的实数。区别在于**精度**（有效数字位数）和范围。

| 数据类型      | 典型大小         | 精度（有效数字） | 说明                       |
| :------------ | :--------------- | :--------------- | :------------------------- |
| `float`       | 4 字节           | 约 7 位          | 单精度浮点数               |
| `double`      | 8 字节           | 约 15 位         | **双精度浮点数（最常用）** |
| `long double` | 8, 12 或 16 字节 | 高于 double      | 扩展精度浮点数             |

**示例：**
```cpp
#include <iostream>
#include <iomanip> // 用于控制输出格式，如 setprecision
using namespace std;

int main() {
    float price = 19.99f; // 后缀 f 或 F 表示 float 类型
    double pi = 3.141592653589793; // 默认的浮点常量是 double 类型
    long double veryPrecise = 2.718281828459045L; // 后缀 L 表示 long double

    // 使用 setprecision 控制输出的小数位数
    cout << fixed << setprecision(10); // 固定小数格式，显示10位小数
    cout << "price (float): " << price << endl; // 可能显示精度不足
    cout << "pi (double): " << pi << endl;
    cout << "veryPrecise: " << veryPrecise << endl;

    // 科学计数法表示
    double avogadro = 6.022e23; // 6.022 × 10^23
    cout << "Avogadro's number: " << avogadro << endl;

    return 0;
}
```
**注意：** 由于浮点数在内存中的存储方式，它们有时无法精确表示某些小数（如 0.1），在进行精确比较时需要注意。

### 字符型 (Character Type)

用于存储单个字符。字符用单引号 `''` 包围。

| 数据类型   | 典型大小    | 说明                                                    |
| :--------- | :---------- | :------------------------------------------------------ |
| `char`     | 1 字节      | 用于存储基本字符（ASCII），范围 -128 到 127 或 0 到 255 |
| `wchar_t`  | 2 或 4 字节 | 用于存储宽字符（如 Unicode）                            |
| `char16_t` | 2 字节      | 用于 UTF-16 字符（C++11 引入）                          |
| `char32_t` | 4 字节      | 用于 UTF-32 字符（C++11 引入）                          |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    char grade = 'A';
    char newline = '\n'; // 转义字符：换行
    char tab = '\t';     // 转义字符：制表符
    char nullChar = '\0'; // 转义字符：空字符（字符串结束标志）

    cout << "Your grade is: " << grade << newline;
    cout << "This is" << tab << "after a tab." << endl;

    // char 本质上存储的是整数（ASCII 码）
    char letter = 65; // ASCII 码 65 对应字符 'A'
    cout << "The letter is: " << letter << endl;

    return 0;
}
```
**常见转义字符：**
*   `\n`：换行
*   `\t`：制表符
*   `\\`：反斜杠本身
*   `\'`：单引号
*   `\"`：双引号

### 布尔型 (Boolean Type)

用于表示逻辑值，只有两个可能的值：`true`（真）或 `false`（假）。

| 数据类型 | 大小        | 值                |
| :------- | :---------- | :---------------- |
| `bool`   | 通常 1 字节 | `true` 或 `false` |

在需要整数的地方，`true` 通常转换为 `1`，`false` 转换为 `0`。

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    bool isCppFun = true;
    bool isFishTasty = false;

    cout << "Is C++ fun? " << isCppFun << endl;   // 输出 1
    cout << "Is fish tasty? " << isFishTasty << endl; // 输出 0

    // 使用 boolalpha 来输出 true/false 而不是 1/0
    cout << boolalpha;
    cout << "Is C++ fun? " << isCppFun << endl;   // 输出 true
    cout << "Is fish tasty? " << isFishTasty << endl; // 输出 false

    // 布尔值通常来自比较运算
    int x = 10, y = 20;
    bool result = (x > y); // false
    cout << "Is x greater than y? " << result << endl;

    return 0;
}
```

### `void` 类型

`void` 类型表示“无类型”或“空”。它主要有两种用途：
1.  **作为函数的返回类型**：表示函数不返回任何值。
    ```cpp
    void printHello() {
        cout << "Hello" << endl;
        // 无需 return 语句，或使用 return;
    }
    ```
2.  **作为指针的类型**：表示指向未知类型的指针，`void*`（后面会详细讲）。

### `sizeof` 操作符

`sizeof` 是一个编译时操作符，用于确定**数据类型或变量在内存中所占的字节数**。这对于了解不同系统的差异非常有用。

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Size of char: " << sizeof(char) << " byte" << endl;
    cout << "Size of int: " << sizeof(int) << " bytes" << endl;
    cout << "Size of short: " << sizeof(short) << " bytes" << endl;
    cout << "Size of long: " << sizeof(long) << " bytes" << endl;
    cout << "Size of long long: " << sizeof(long long) << " bytes" << endl;
    cout << "Size of float: " << sizeof(float) << " bytes" << endl;
    cout << "Size of double: " << sizeof(double) << " bytes" << endl;
    cout << "Size of bool: " << sizeof(bool) << " byte" << endl;

    int x = 0;
    cout << "Size of variable x is: " << sizeof(x) << " bytes" << endl;
    // 等价于 cout << "Size of variable x is: " << sizeof x << " bytes" << endl;

    return 0;
}
```
**注意：** 上述大小是**典型值**，具体大小取决于编译器和计算机架构（如 32 位 vs 64 位）。

### 总结表

| 类别       | 类型                         | 说明           | 常用程度 |
| :--------- | :--------------------------- | :------------- | :------- |
| **整型**   | `int`                        | 整数           | ⭐⭐⭐⭐⭐    |
|            | `short`, `long`, `long long` | 不同范围的整数 | ⭐⭐       |
|            | `unsigned`                   | 无符号整数     | ⭐⭐⭐      |
| **浮点型** | `double`                     | 双精度浮点数   | ⭐⭐⭐⭐⭐    |
|            | `float`                      | 单精度浮点数   | ⭐⭐⭐      |
|            | `long double`                | 高精度浮点数   | ⭐        |
| **字符型** | `char`                       | 单个字符       | ⭐⭐⭐⭐⭐    |
| **布尔型** | `bool`                       | 真假值         | ⭐⭐⭐⭐⭐    |

对于初学者，最需要熟练掌握的是 `int`, `double`, `char`, `bool` 这四种最核心的基本数据类型。



## 变量



### 声明变量 (Declaring Variables)
告诉编译器变量的存在、名称和类型。

**语法：**
```cpp
type name;
```

**示例：**

```cpp
int age;          // 声明一个整型变量 age
double salary;    // 声明一个双精度浮点型变量 salary
char grade;       // 声明一个字符型变量 grade
bool isPassed;    // 声明一个布尔型变量 isPassed
```

### 定义/初始化变量 (Defining/Initializing Variables)
给变量分配内存并赋予初始值。

**几种初始化方式：**

```cpp
// 1. 先声明，后赋值（传统C风格）
int count;
count = 10;

// 2. 声明时直接初始化（推荐）
int score = 100;
double pi = 3.14159;
char initial = 'A';

// 3. C++11 统一初始化（更现代，推荐）
int height {180};          // 使用花括号
double weight {68.5};
std::string name {"Alice"};

// 4. 构造函数初始化（对于类类型）
std::string message("Hello");
```

**统一初始化的优势：**
- 防止窄化转换（如 `int x {3.14};` 会编译报错）
- 语法更统一
- 可以初始化数组等复杂类型

### 变量的作用域 (Scope)

变量的作用域指变量在程序中的可见范围。

- **局部作用域**：在函数内部声明的变量具有局部作用域，它们只能在函数内部访问。局部变量在函数每次被调用时被创建，在函数执行完后被销毁。
- **全局作用域**：在所有函数和代码块之外声明的变量具有全局作用域，它们可以被程序中的任何函数访问。全局变量在程序开始时被创建，在程序结束时被销毁。
- **块作用域**：在代码块内部声明的变量具有块作用域，它们只能在代码块内部访问。块作用域变量在代码块每次被执行时被创建，在代码块执行完后被销毁。
- **类作用域**：在类内部声明的变量具有类作用域，它们可以被类的所有成员函数访问。类作用域变量的生命周期与类的生命周期相同。

#### 局部变量 (Local Variables)
在函数或代码块 `{}` 内部声明，只在声明它的块内有效。

```cpp
#include <iostream>
using namespace std;

void exampleFunction() {
    int localVar = 10; // 局部变量
    cout << "Inside function: " << localVar << endl;
}

int main() {
    int mainVar = 20; // main函数的局部变量
    
    {
        int blockVar = 30; // 代码块内的局部变量
        cout << "Inside block: " << blockVar << endl;
    }
    // cout << blockVar << endl; // 错误：blockVar 在此不可见
    
    exampleFunction();
    // cout << localVar << endl; // 错误：localVar 在此不可见
    
    return 0;
}
```

#### 全局变量 (Global Variables)
在所有函数外部声明，在整个程序中可见。

```cpp
#include <iostream>
using namespace std;

int globalVar = 100; // 全局变量

void function1() {
    cout << "Function1: " << globalVar << endl;
    globalVar++; // 可以修改全局变量
}

void function2() {
    cout << "Function2: " << globalVar << endl;
}

int main() {
    cout << "Main: " << globalVar << endl;
    function1();
    function2();
    return 0;
}
```

**输出：**
```
Main: 100
Function1: 100
Function2: 101
```

### 变量的生命周期 (Lifetime)

- **局部变量**：从声明处开始，到所在代码块结束时销毁
- **全局变量**：在整个程序运行期间都存在
- **静态变量**：使用 `static` 关键字，生命周期贯穿整个程序

```cpp
void counter() {
    static int count = 0; // 静态局部变量
    count++;
    cout << "Count: " << count << endl;
}

int main() {
    counter(); // 输出 Count: 1
    counter(); // 输出 Count: 2
    counter(); // 输出 Count: 3
    return 0;
}
```

### 常量 (const)

使用 `const` 关键字声明不可修改的变量。

```cpp
#include <iostream>
using namespace std;

int main() {
    const double PI = 3.1415926;
    const int MAX_STUDENTS = 100;
    
    // PI = 3.14; // 错误：不能修改常量
    
    cout << "PI: " << PI << endl;
    cout << "Max students: " << MAX_STUDENTS << endl;
    
    return 0;
}
```

**const 的好处：**
- 提高代码可读性
- 防止意外修改
- 编译器可以进行优化



## 运算符

好的，我们来全面讲解 C++ 中的运算符。

运算符是用于执行各种操作的符号。C++ 提供了丰富的运算符，可以分为以下几大类：

### 算术运算符 (Arithmetic Operators)

用于基本的数学运算。

| 运算符 | 描述         | 示例           | 结果           |
| ------ | ------------ | -------------- | -------------- |
| `+`    | 加法         | `5 + 3`        | `8`            |
| `-`    | 减法         | `5 - 3`        | `2`            |
| `*`    | 乘法         | `5 * 3`        | `15`           |
| `/`    | 除法         | `5 / 3`        | `1` (整数除法) |
| `%`    | 取模（求余） | `5 % 3`        | `2`            |
| `++`   | 自增         | `x++` 或 `++x` | `x = x + 1`    |
| `--`   | 自减         | `x--` 或 `--x` | `x = x - 1`    |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 3;
    
    cout << "a + b = " << (a + b) << endl;  // 13
    cout << "a - b = " << (a - b) << endl;  // 7
    cout << "a * b = " << (a * b) << endl;  // 30
    cout << "a / b = " << (a / b) << endl;  // 3 (整数除法)
    cout << "a % b = " << (a % b) << endl;  // 1
    
    double x = 10.0, y = 3.0;
    cout << "x / y = " << (x / y) << endl;  // 3.33333 (浮点数除法)
    
    return 0;
}
```

**前缀 vs 后缀自增/自减：**
```cpp
int i = 5;
cout << i++ << endl;  // 输出 5，然后 i 变为 6
cout << ++i << endl;  // i 先变为 7，然后输出 7
```

### 关系运算符 (Relational Operators)

用于比较两个值，返回 `true` 或 `false`。

| 运算符 | 描述     | 示例     | 结果    |
| ------ | -------- | -------- | ------- |
| `==`   | 等于     | `5 == 3` | `false` |
| `!=`   | 不等于   | `5 != 3` | `true`  |
| `>`    | 大于     | `5 > 3`  | `true`  |
| `<`    | 小于     | `5 < 3`  | `false` |
| `>=`   | 大于等于 | `5 >= 5` | `true`  |
| `<=`   | 小于等于 | `5 <= 3` | `false` |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10, y = 20;
    
    cout << boolalpha; // 输出 true/false 而不是 1/0
    cout << "x == y: " << (x == y) << endl;  // false
    cout << "x != y: " << (x != y) << endl;  // true
    cout << "x < y: " << (x < y) << endl;    // true
    cout << "x >= y: " << (x >= y) << endl;  // false
    
    return 0;
}
```

### 逻辑运算符 (Logical Operators)

用于组合或修改布尔表达式。

| 运算符 | 描述   | 示例            | 结果    |
| ------ | ------ | --------------- | ------- |
| `&&`   | 逻辑与 | `true && false` | `false` |
| `||`   | 逻辑或 | `true || false` | `true`  |
| `!`    | 逻辑非 | `!true`         | `false` |

**真值表：**
| A     | B     | A && B | A \|\| B | !A    |
| ----- | ----- | ------ | -------- | ----- |
| true  | true  | true   | true     | false |
| true  | false | false  | true     | false |
| false | true  | false  | true     | true  |
| false | false | false  | false    | true  |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 25;
    bool hasLicense = true;
    
    cout << boolalpha;
    cout << "Can drive: " << (age >= 18 && hasLicense) << endl;  // true
    cout << "Is teenager: " << (age >= 13 && age <= 19) << endl; // false
    cout << "Cannot drive: " << !(age >= 18 && hasLicense) << endl; // false
    
    return 0;
}
```

**短路求值：**
- `A && B`：如果 A 为 false，不再计算 B
- `A || B`：如果 A 为 true，不再计算 B

### 赋值运算符 (Assignment Operators)

用于给变量赋值。

| 运算符 | 描述       | 等价于                 |
| ------ | ---------- | ---------------------- |
| `=`    | 简单赋值   | `x = y`                |
| `+=`   | 加后赋值   | `x += y` → `x = x + y` |
| `-=`   | 减后赋值   | `x -= y` → `x = x - y` |
| `*=`   | 乘后赋值   | `x *= y` → `x = x * y` |
| `/=`   | 除后赋值   | `x /= y` → `x = x / y` |
| `%=`   | 取模后赋值 | `x %= y` → `x = x % y` |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    
    x += 5;   // x = 15
    x -= 3;   // x = 12
    x *= 2;   // x = 24
    x /= 4;   // x = 6
    x %= 5;   // x = 1
    
    cout << "Final x: " << x << endl;
    
    return 0;
}
```

### 位运算符 (Bitwise Operators)

直接对二进制位进行操作。

| 运算符 | 描述     | 示例            |
| ------ | -------- | --------------- |
| `&`    | 按位与   | `5 & 3` → `1`   |
| `|`    | 按位或   | `5 | 3` → `7`   |
| `^`    | 按位异或 | `5 ^ 3` → `6`   |
| `~`    | 按位取反 | `~5` → `-6`     |
| `<<`   | 左移     | `5 << 1` → `10` |
| `>>`   | 右移     | `5 >> 1` → `2`  |

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;  // 二进制: 0101
    int b = 3;  // 二进制: 0011
    
    cout << "a & b: " << (a & b) << endl;  // 0001 → 1
    cout << "a | b: " << (a | b) << endl;  // 0111 → 7
    cout << "a ^ b: " << (a ^ b) << endl;  // 0110 → 6
    cout << "~a: " << (~a) << endl;        // 111...1010 → -6
    cout << "a << 1: " << (a << 1) << endl; // 1010 → 10
    cout << "a >> 1: " << (a >> 1) << endl; // 0010 → 2
    
    return 0;
}
```

### 条件运算符 (三元运算符)
`condition ? expression1 : expression2`

```cpp
int x = 10, y = 20;
int max = (x > y) ? x : y;  // max = 20
```

### 逗号运算符
从左到右计算所有表达式，返回最后一个表达式的值。

```cpp
int a = (x = 5, y = 10, x + y);  // a = 15
```

### sizeof 运算符
返回变量或类型的大小（字节数）。

```cpp
cout << "int size: " << sizeof(int) << " bytes" << endl;
cout << "double size: " << sizeof(double) << " bytes" << endl;
```

### 类型转换运算符
```cpp
double pi = 3.14159;
int intPi = (int)pi;          // C风格转换
int intPi2 = static_cast<int>(pi); // C++风格转换（推荐）
```

### 运算符优先级

运算符按照优先级顺序执行，优先级高的先执行。

| 优先级 | 运算符                                                  | 描述                                                         |
| ------ | ------------------------------------------------------- | ------------------------------------------------------------ |
| 1      | `::`                                                    | 作用域解析                                                   |
| 2      | `++` `--` `()` `[]` `.` `->`                            | 后缀自增/自减、函数调用、数组下标、成员访问                  |
| 3      | `++` `--` `+` `-` `!` `~` `(type)` `*` `&` `sizeof`     | 前缀自增/自减、正负号、逻辑非、按位取反、类型转换、解引用、取地址 |
| 4      | `.*` `->*`                                              | 成员指针                                                     |
| 5      | `*` `/` `%`                                             | 乘、除、取模                                                 |
| 6      | `+` `-`                                                 | 加、减                                                       |
| 7      | `<<` `>>`                                               | 位左移、位右移                                               |
| 8      | `<` `<=` `>` `>=`                                       | 关系运算符                                                   |
| 9      | `==` `!=`                                               | 相等性运算符                                                 |
| 10     | `&`                                                     | 按位与                                                       |
| 11     | `^`                                                     | 按位异或                                                     |
| 12     | `|`                                                     | 按位或                                                       |
| 13     | `&&`                                                    | 逻辑与                                                       |
| 14     | `||`                                                    | 逻辑或                                                       |
| 15     | `?:`                                                    | 条件运算符                                                   |
| 16     | `=` `+=` `-=` `*=` `/=` `%=` `<<=` `>>=` `&=` `^=` `|=` | 赋值运算符                                                   |
| 17     | `,`                                                     | 逗号运算符                                                   |

**使用括号明确优先级：**
```cpp
int result1 = 2 + 3 * 4;     // 14 (乘法优先)
int result2 = (2 + 3) * 4;   // 20 (括号优先)
```

## 控制语句

### 综合示例：简易计算器

```cpp
#include <iostream>
using namespace std;

int main() {
    char operation;
    double num1, num2;
    bool continueCalc = true;
    
    while (continueCalc) {
        cout << "\n=== Simple Calculator ===" << endl;
        cout << "Enter first number: ";
        cin >> num1;
        
        cout << "Enter operation (+, -, *, /): ";
        cin >> operation;
        
        cout << "Enter second number: ";
        cin >> num2;
        
        switch (operation) {
            case '+':
                cout << "Result: " << num1 + num2 << endl;
                break;
            case '-':
                cout << "Result: " << num1 - num2 << endl;
                break;
            case '*':
                cout << "Result: " << num1 * num2 << endl;
                break;
            case '/':
                if (num2 != 0) {
                    cout << "Result: " << num1 / num2 << endl;
                } else {
                    cout << "Error: Division by zero!" << endl;
                }
                break;
            default:
                cout << "Error: Invalid operation!" << endl;
        }
        
        char choice;
        cout << "Do you want to continue? (y/n): ";
        cin >> choice;
        
        if (choice != 'y' && choice != 'Y') {
            continueCalc = false;
        }
    }
    
    cout << "Thank you for using the calculator!" << endl;
    return 0;
}
```

## 指针

### 什么是指针？
指针是一个变量，其值是**另一个变量的内存地址**。

**内存模型理解：**
```
变量:    num    (值为 10，地址为 0x1000)
指针:    ptr    (值为 0x1000，指向 num)
```

### 指针的声明和使用

**语法：**
```cpp
数据类型* 指针变量名;  // * 表示这是一个指针
```

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int num = 10;
    int* ptr = &num;  // & 取地址运算符
    
    cout << "Value of num: " << num << endl;          // 10
    cout << "Address of num: " << &num << endl;       // 0x7ff...
    cout << "Value of ptr: " << ptr << endl;          // 0x7ff... (与 &num 相同)
    cout << "Value at ptr: " << *ptr << endl;         // 10 (* 解引用运算符)
    
    return 0;
}
```

### 指针的操作

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5, b = 10;
    int* ptr = &a;
    
    cout << "*ptr = " << *ptr << endl;  // 5
    
    // 修改指针指向的值
    *ptr = 20;
    cout << "a = " << a << endl;        // 20
    
    // 修改指针指向的地址
    ptr = &b;
    cout << "*ptr = " << *ptr << endl;  // 10
    
    // 指针的指针
    int** pptr = &ptr;
    cout << "**pptr = " << **pptr << endl;  // 10
    
    return 0;
}
```

### 指针与数组

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int* ptr = arr;  // 数组名就是首元素的地址
    
    cout << "First element: " << *ptr << endl;        // 1
    cout << "Second element: " << *(ptr + 1) << endl; // 2
    cout << "Third element: " << ptr[2] << endl;      // 3
    
    // 遍历数组
    for (int i = 0; i < 5; i++) {
        cout << *(ptr + i) << " ";  // 1 2 3 4 5
    }
    cout << endl;
    
    return 0;
}
```

### 动态内存分配

```cpp
#include <iostream>
using namespace std;

int main() {
    // 动态分配内存
    int* dynamicPtr = new int;
    *dynamicPtr = 100;
    cout << "Dynamic value: " << *dynamicPtr << endl;
    
    // 动态分配数组
    int size = 5;
    int* arrPtr = new int[size];
    for (int i = 0; i < size; i++) {
        arrPtr[i] = i * 10;
    }
    
    // 必须释放内存！
    delete dynamicPtr;
    delete[] arrPtr;
    
    return 0;
}
```

### 空指针和野指针

```cpp
int* nullPtr = nullptr;  // 空指针（C++11推荐）
int* wildPtr;           // 野指针（未初始化，危险！）
```



## 引用

### 什么是引用？
引用是**变量的别名**，一旦初始化后就不能改变引用的目标。

**语法：**
```cpp
数据类型& 引用名 = 原变量名;
```

### 引用的使用

```cpp
#include <iostream>
using namespace std;

int main() {
    int num = 10;
    int& ref = num;  // ref 是 num 的别名
    
    cout << "num = " << num << endl;    // 10
    cout << "ref = " << ref << endl;    // 10
    
    // 修改引用就是修改原变量
    ref = 20;
    cout << "num = " << num << endl;    // 20
    cout << "ref = " << ref << endl;    // 20
    
    // 引用必须初始化
    // int& invalidRef;  // 错误：必须初始化
    
    return 0;
}
```

### 引用作为函数参数

```cpp
#include <iostream>
using namespace std;

// 值传递（不修改原值）
void swapByValue(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

// 指针传递
void swapByPointer(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// 引用传递（推荐）
void swapByReference(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 5, y = 10;
    
    swapByValue(x, y);
    cout << "After swapByValue: " << x << ", " << y << endl;  // 5, 10
    
    swapByPointer(&x, &y);
    cout << "After swapByPointer: " << x << ", " << y << endl; // 10, 5
    
    swapByReference(x, y);
    cout << "After swapByReference: " << x << ", " << y << endl; // 5, 10
    
    return 0;
}
```

### 引用与 const

```cpp
#include <iostream>
using namespace std;

int main() {
    int num = 10;
    
    // 普通引用
    int& ref1 = num;
    ref1 = 20;  // 可以修改
    
    // const 引用（只读引用）
    const int& ref2 = num;
    // ref2 = 30;  // 错误：不能通过 const 引用修改值
    
    // const 引用可以绑定到临时值
    const int& ref3 = 100;  // 合法
    cout << "ref3 = " << ref3 << endl;
    
    return 0;
}
```

### 指针 vs 引用

| 特性           | 指针                     | 引用              |
| -------------- | ------------------------ | ----------------- |
| **声明**       | `int* ptr;`              | `int& ref = var;` |
| **初始化**     | 可以稍后初始化           | 必须声明时初始化  |
| **可重新指向** | 可以指向其他变量         | 一旦绑定不能改变  |
| **空值**       | 可以有 `nullptr`         | 不能为空          |
| **多级间接**   | 支持多级指针             | 只有一级          |
| **运算符**     | `*` (解引用), `&` (取址) | 自动解引用        |
| **内存占用**   | 占用内存存储地址         | 不额外占用内存    |

**使用指针的场景：**

- 动态内存分配
- 需要指向不同对象
- 需要空值表示
- 实现数据结构（如链表、树）
- C 语言兼容

**使用引用的场景：**
- 函数参数传递（避免拷贝）
- 函数返回值（返回左值）
- 操作符重载
- 范围 for 循环

### 重要注意事项

1. **永远不要返回局部变量的引用或指针**
   ```cpp
   int* badFunction() {
       int local = 10;
       return &local; // 错误：局部变量会被销毁
   }
   ```

2. **避免野指针**
   ```cpp
   int* ptr; // 未初始化，危险！
   *ptr = 10; // 未定义行为
   ```

3. **及时释放动态内存**
   ```cpp
   int* arr = new int[100];
   // 使用数组...
   delete[] arr; // 必须释放！
   ```

4. **优先使用引用而不是指针**（当不需要重新指向或空值时）

5. **使用智能指针管理动态内存**（现代 C++ 最佳实践）

指针和引用是 C++ 中非常强大的特性，理解它们的区别和正确用法对于编写高效、安全的代码至关重要。

## 数组

好的，我们来详细讲解 C++ 中的数组。

数组是一种用于存储**相同类型**元素的**连续内存**集合。它是 C++ 中最基本的数据结构之一。

### 什么是数组？
数组是相同类型元素的集合，这些元素在内存中连续存储，每个元素可以通过索引（下标）来访问。

**内存布局：**
```
索引:    [0]    [1]    [2]    [3]    [4]
值:      10     20     30     40     50
地址:    1000   1004   1008   1012   1016
```

### 数组的声明和初始化

**语法：**
```cpp
数据类型 数组名[数组大小];
```

**示例：**
```cpp
#include <iostream>
using namespace std;

int main() {
    // 1. 声明后逐个赋值
    int numbers[5];
    numbers[0] = 10;
    numbers[1] = 20;
    numbers[2] = 30;
    numbers[3] = 40;
    numbers[4] = 50;
    
    // 2. 声明时初始化
    int scores[5] = {85, 90, 78, 92, 88};
    
    // 3. 自动推断大小
    double prices[] = {12.5, 9.99, 24.5, 15.0}; // 大小为4
    
    // 4. 部分初始化（剩余元素为0）
    int data[10] = {1, 2, 3}; // 前3个为1,2,3，后7个为0
    
    return 0;
}
```

### 数组作为函数参数

数组作为函数参数时，会退化为指针。

#### 传递数组给函数

```cpp
#include <iostream>
using namespace std;

// 方式1：使用指针
void printArray1(int* arr, int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// 方式2：使用数组语法
void printArray2(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// 方式3：使用固定大小的数组（不推荐）
void printArray3(int arr[5]) {
    for (int i = 0; i < 5; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// 修改数组内容
void modifyArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2; // 修改会影响原数组
    }
}

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    
    printArray1(numbers, size);
    printArray2(numbers, size);
    
    modifyArray(numbers, size);
    cout << "After modification: ";
    printArray1(numbers, size); // 2, 4, 6, 8, 10
    
    return 0;
}
```

#### 返回数组（通过指针）

```cpp
#include <iostream>
using namespace std;

// 返回动态分配的数组
int* createArray(int size) {
    int* arr = new int[size];
    for (int i = 0; i < size; i++) {
        arr[i] = i * 10;
    }
    return arr;
}

int main() {
    int size = 5;
    int* dynamicArray = createArray(size);
    
    cout << "Dynamic array: ";
    for (int i = 0; i < size; i++) {
        cout << dynamicArray[i] << " ";
    }
    cout << endl;
    
    // 必须释放内存
    delete[] dynamicArray;
    
    return 0;
}
```

### 标准库数组 (C++11)

现代 C++ 推荐使用 `std::array`，它更安全、功能更丰富。

```cpp
#include <iostream>
#include <array> // 必须包含这个头文件
using namespace std;

int main() {
    // 声明 std::array
    array<int, 5> arr = {1, 2, 3, 4, 5};
    
    // 访问元素（有边界检查）
    cout << "First element: " << arr[0] << endl;
    cout << "Second element: " << arr.at(1) << endl; // 带边界检查
    
    // 获取大小
    cout << "Size: " << arr.size() << endl;
    
    // 遍历
    cout << "Elements: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    // 填充数组
    arr.fill(0); // 所有元素设为0
    cout << "After fill: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

**std::array 的优势：**
- 知道自己的大小
- 不会退化为指针
- 支持迭代器
- 有边界检查（使用 `.at()`）
- 更安全

### 常见数组操作

#### 查找元素

```cpp
#include <iostream>
using namespace std;

int findElement(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i; // 返回索引
        }
    }
    return -1; // 未找到
}

int main() {
    int numbers[] = {10, 20, 30, 40, 50};
    int size = 5;
    
    int index = findElement(numbers, size, 30);
    if (index != -1) {
        cout << "Element found at index: " << index << endl;
    } else {
        cout << "Element not found" << endl;
    }
    
    return 0;
}
```

#### 求最大值/最小值

```cpp
#include <iostream>
using namespace std;

int findMax(int arr[], int size) {
    int max = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

int findMin(int arr[], int size) {
    int min = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
    }
    return min;
}

int main() {
    int numbers[] = {45, 12, 67, 23, 89, 34};
    int size = 6;
    
    cout << "Max: " << findMax(numbers, size) << endl;
    cout << "Min: " << findMin(numbers, size) << endl;
    
    return 0;
}
```

#### 数组排序（冒泡排序）

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // 交换元素
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int numbers[] = {64, 34, 25, 12, 22, 11, 90};
    int size = 7;
    
    cout << "Original: ";
    for (int i = 0; i < size; i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    bubbleSort(numbers, size);
    
    cout << "Sorted: ";
    for (int i = 0; i < size; i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    return 0;
}
```

### 重要注意事项

1. **数组越界访问是未定义行为**
   ```cpp
   int arr[5] = {1, 2, 3, 4, 5};
   cout << arr[5]; // 错误：越界访问！
   ```

2. **数组大小必须是编译时常量**
   ```cpp
   int size = 10;
   int arr[size]; // 错误：C++中不允许（C语言允许）
   
   const int SIZE = 10;
   int arr[SIZE]; // 正确
   ```

3. **数组不能直接赋值**
   ```cpp
   int a[5] = {1, 2, 3, 4, 5};
   int b[5];
   b = a; // 错误：不能直接复制数组
   ```

4. **推荐使用 std::array 或 std::vector**
   ```cpp
   #include <array>
   #include <vector>
   
   std::array<int, 5> arr1 = {1, 2, 3, 4, 5};
   std::vector<int> vec = {1, 2, 3, 4, 5}; // 动态大小
   ```

5. **计算数组大小**
   ```cpp
   int arr[] = {1, 2, 3, 4, 5};
   int size = sizeof(arr) / sizeof(arr[0]); // 计算元素个数
   ```

数组是 C++ 中非常重要的基础数据结构，理解数组的原理和用法对于学习更复杂的数据结构和算法至关重要。在现代 C++ 开发中，建议优先考虑使用 `std::array` 或 `std::vector`。

## 字符串

好的，我们来全面讲解 C++ 中的字符串。

C++ 提供了两种主要的字符串处理方式：
1. **C风格字符串**：字符数组，以空字符 `\0` 结尾
2. **C++风格字符串**：`std::string` 类，更现代、更安全

### C风格字符串

#### 基本概念
C风格字符串实际上是字符数组，以空字符 `'\0'` 作为结束标志。

**声明和初始化：**
```cpp
#include <iostream>
#include <cstring> // C风格字符串函数
using namespace std;

int main() {
    // 方式1：字符数组
    char str1[] = "Hello"; // 自动添加 '\0'
    cout << "str1: " << str1 << endl;
    
    // 方式2：指定大小
    char str2[20] = "World";
    cout << "str2: " << str2 << endl;
    
    // 方式3：逐个字符初始化
    char str3[] = {'H', 'i', '\0'};
    cout << "str3: " << str3 << endl;
    
    // 方式4：字符指针
    const char* str4 = "Hello World"; // 字符串字面量
    cout << "str4: " << str4 << endl;
    
    return 0;
}
```

#### 常用操作函数

```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main() {
    char str1[20] = "Hello";
    char str2[20] = "World";
    char str3[20];
    
    // 1. 获取字符串长度
    cout << "Length of str1: " << strlen(str1) << endl; // 5
    
    // 2. 字符串复制
    strcpy(str3, str1);
    cout << "After copy: " << str3 << endl; // Hello
    
    // 3. 字符串连接
    strcat(str1, " ");
    strcat(str1, str2);
    cout << "After concatenation: " << str1 << endl; // Hello World
    
    // 4. 字符串比较
    cout << "Compare: " << strcmp("apple", "banana") << endl; // 负数
    cout << "Compare: " << strcmp("hello", "hello") << endl;  // 0
    cout << "Compare: " << strcmp("zoo", "apple") << endl;    // 正数
    
    // 5. 字符串查找
    char* found = strstr("Hello World", "World");
    if (found) {
        cout << "Substring found: " << found << endl;
    }
    
    return 0;
}
```

#### 注意事项
```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main() {
    // 1. 缓冲区溢出风险
    char small[5];
    // strcpy(small, "Hello World"); // 危险：缓冲区溢出
    
    // 2. 使用更安全的函数
    char safe[10];
    strncpy(safe, "Hello", sizeof(safe) - 1);
    safe[sizeof(safe) - 1] = '\0'; // 确保以空字符结尾
    
    // 3. 字符串字面量不可修改
    const char* literal = "Constant";
    // literal[0] = 'X'; // 错误：试图修改字符串字面量
    
    return 0;
}
```

### Cpp 风格字符串 (std::string)

#### 基本用法
`std::string` 是 C++ 标准库提供的字符串类，更安全、更方便。

```cpp
#include <iostream>
#include <string> // 必须包含这个头文件
using namespace std;

int main() {
    // 1. 声明和初始化
    string str1 = "Hello";
    string str2("World");
    string str3(5, 'A'); // "AAAAA"
    string str4(str1);   // 拷贝构造
    
    cout << "str1: " << str1 << endl;
    cout << "str2: " << str2 << endl;
    cout << "str3: " << str3 << endl;
    cout << "str4: " << str4 << endl;
    
    return 0;
}
```

#### 常用操作

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "Hello";
    
    // 1. 获取长度
    cout << "Length: " << str.length() << endl;     // 5
    cout << "Size: " << str.size() << endl;         // 5
    cout << "Empty? " << str.empty() << endl;       // 0 (false)
    
    // 2. 访问字符
    cout << "First char: " << str[0] << endl;       // H
    cout << "First char: " << str.at(0) << endl;    // H (带边界检查)
    
    // 3. 修改字符串
    str += " World";           // 追加
    str.append("!");           // 追加
    str.insert(5, " C++");     // 插入
    str.replace(6, 5, "Earth"); // 替换
    
    cout << "Modified: " << str << endl; // Hello C++ Earth!
    
    // 4. 查找和子串
    size_t pos = str.find("C++");
    if (pos != string::npos) {
        cout << "Found at position: " << pos << endl;
        string sub = str.substr(pos, 3); // 提取子串
        cout << "Substring: " << sub << endl;
    }
    
    return 0;
}
```

#### 字符串比较和操作

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1 = "apple";
    string s2 = "banana";
    string s3 = "apple";
    
    // 比较
    if (s1 == s3) {
        cout << "s1 equals s3" << endl;
    }
    if (s1 < s2) {
        cout << "apple comes before banana" << endl;
    }
    
    // 转换大小写（需要算法头文件）
    #include <algorithm>
    string text = "Hello World";
    transform(text.begin(), text.end(), text.begin(), ::toupper);
    cout << "Uppercase: " << text << endl;
    
    transform(text.begin(), text.end(), text.begin(), ::tolower);
    cout << "Lowercase: " << text << endl;
    
    return 0;
}
```

### 字符串输入输出

#### 读取字符串

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    string fullName;
    
    // 1. 使用 cin（遇到空格停止）
    cout << "Enter your first name: ";
    cin >> name;
    cout << "Hello, " << name << endl;
    
    // 清除输入缓冲区
    cin.ignore(); // 重要！
    
    // 2. 使用 getline 读取整行
    cout << "Enter your full name: ";
    getline(cin, fullName);
    cout << "Hello, " << fullName << endl;
    
    // 3. 读取多个值
    string firstName, lastName;
    cout << "Enter first and last name: ";
    cin >> firstName >> lastName;
    cout << "Hello, " << firstName << " " << lastName << endl;
    
    return 0;
}
```

#### 字符串流

```cpp
#include <iostream>
#include <string>
#include <sstream> // 字符串流
using namespace std;

int main() {
    // 将数字转换为字符串
    int age = 25;
    double salary = 50000.50;
    
    stringstream ss;
    ss << "Age: " << age << ", Salary: " << salary;
    string info = ss.str();
    cout << info << endl;
    
    // 从字符串提取数据
    string data = "John 25 50000.50";
    string name;
    int age2;
    double salary2;
    
    stringstream ss2(data);
    ss2 >> name >> age2 >> salary2;
    cout << "Name: " << name << ", Age: " << age2 << ", Salary: " << salary2 << endl;
    
    return 0;
}
```

### 字符串与数值转换

#### C++11 现代方法

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // 字符串转数值
    string numStr = "123";
    int num1 = stoi(numStr);        // string to int
    double num2 = stod("45.67");    // string to double
    long num3 = stol("1000000");    // string to long
    
    cout << "Integer: " << num1 << endl;
    cout << "Double: " << num2 << endl;
    cout << "Long: " << num3 << endl;
    
    // 数值转字符串
    string str1 = to_string(123);       // int to string
    string str2 = to_string(45.67);     // double to string
    string str3 = to_string(1000000L);  // long to string
    
    cout << "String1: " << str1 << endl;
    cout << "String2: " << str2 << endl;
    cout << "String3: " << str3 << endl;
    
    return 0;
}
```

#### 传统方法

```cpp
#include <iostream>
#include <cstdlib> // atoi, atof
#include <sstream>
using namespace std;

int main() {
    // 传统转换方法
    const char* numStr = "123";
    int num1 = atoi(numStr);        // ASCII to integer
    double num2 = atof("45.67");    // ASCII to float
    
    cout << "atoi: " << num1 << endl;
    cout << "atof: " << num2 << endl;
    
    return 0;
}
```

### 最佳实践和建议

1. **优先使用 std::string**：更安全、更方便
2. **避免C风格字符串**：除非需要与C代码交互
3. **使用getline读取整行**：避免cin的空格问题
4. **注意字符串编码**：处理中文等需要宽字符或UTF-8
5. **使用现代转换函数**：stoi(), stod() 等

```cpp
#include <iostream>
#include <string>
using namespace std;

// 宽字符串（处理中文等）
#include <locale>
#include <codecvt>

void wideStringExample() {
    wstring_convert<codecvt_utf8<wchar_t>> converter;
    wstring wide = L"你好世界";
    string utf8 = converter.to_bytes(wide);
    cout << "UTF-8: " << utf8 << endl;
}

int main() {
    // 始终使用 std::string
    string name;
    cout << "Enter your name: ";
    getline(cin, name);
    
    // 安全的字符串操作
    string greeting = "Hello, " + name + "!";
    cout << greeting << endl;
    
    // 使用现代转换
    try {
        int age = stoi("25");
        cout << "Age: " << age << endl;
    } catch (const exception& e) {
        cout << "Invalid number" << endl;
    }
    
    return 0;
}
```

字符串处理是编程中的基本技能，掌握好字符串操作对于任何 C++ 程序员都至关重要。在现代 C++ 开发中，强烈推荐使用 `std::string` 而不是 C风格字符串。

## 结构体

结构体（struct）是一种用户自定义的数据类型，它允许将**不同类型的数据**组合成一个单一的类型。结构体是 C++ 中实现复合数据类型的基础。

### 定义结构体

**语法：**
```cpp
struct 结构体名称 {
    数据类型 成员1;
    数据类型 成员2;
    // ...
};
```

**示例：**
```cpp
#include <iostream>
#include <string>
using namespace std;

// 定义学生结构体
struct Student {
    int id;          // 学号
    string name;     // 姓名
    int age;         // 年龄
    double score;    // 成绩
};

// 定义点坐标结构体
struct Point {
    double x;
    double y;
};

// 定义日期结构体
struct Date {
    int year;
    int month;
    int day;
};
```

### 结构体的声明和初始化

#### 声明结构体变量

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int id;
    string name;
    int age;
    double score;
};

int main() {
    // 方式1：先定义后声明
    Student student1;
    
    // 方式2：定义时声明
    struct Book {
        string title;
        string author;
        double price;
    } book1, book2; // 同时声明两个变量
    
    // 方式3：使用typedef（C风格，C++中可用using）
    typedef struct {
        double width;
        double height;
    } Rectangle;
    
    Rectangle rect1;
    
    return 0;
}
```

#### 初始化结构体

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int id;
    string name;
    int age;
    double score;
};

int main() {
    // 1. 逐个成员初始化（不推荐，麻烦）
    Student s1;
    s1.id = 1001;
    s1.name = "Alice";
    s1.age = 20;
    s1.score = 95.5;
    
    // 2. 初始化列表（推荐）
    Student s2 = {1002, "Bob", 21, 88.5};
    
    // 3. C++11 统一初始化
    Student s3 {1003, "Charlie", 22, 92.0};
    
    // 4. 指定成员初始化（C++20）
    // Student s4 {.id = 1004, .name = "David", .age = 23, .score = 85.5};
    
    cout << "Student 1: " << s1.name << ", Score: " << s1.score << endl;
    cout << "Student 2: " << s2.name << ", Score: " << s2.score << endl;
    cout << "Student 3: " << s3.name << ", Score: " << s3.score << endl;
    
    return 0;
}
```

---

### 访问结构体成员

使用**成员访问运算符** `.` 来访问结构体的成员。



### 结构体与指针

#### 指向结构体的指针

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int id;
    string name;
    double score;
};

int main() {
    Student student = {1001, "Alice", 95.5};
    Student* ptr = &student;
    
    // 使用 -> 运算符访问成员
    cout << "ID: " << ptr->id << endl;
    cout << "Name: " << ptr->name << endl;
    cout << "Score: " << ptr->score << endl;
    
    // 等价于 (*ptr).member
    cout << "ID: " << (*ptr).id << endl;
    
    // 通过指针修改成员
    ptr->score = 97.0;
    cout << "Updated Score: " << student.score << endl;
    
    return 0;
}
```

#### 动态分配结构体

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int id;
    string name;
    double score;
};

int main() {
    // 动态分配单个结构体
    Student* studentPtr = new Student;
    studentPtr->id = 1001;
    studentPtr->name = "Bob";
    studentPtr->score = 88.5;
    
    cout << "Dynamic Student: " << studentPtr->name << endl;
    
    // 必须释放内存
    delete studentPtr;
    
    // 动态分配结构体数组
    Student* students = new Student[3];
    students[0] = {1001, "Alice", 95.5};
    students[1] = {1002, "Bob", 88.5};
    students[2] = {1003, "Charlie", 92.0};
    
    for (int i = 0; i < 3; i++) {
        cout << students[i].name << ": " << students[i].score << endl;
    }
    
    delete[] students;
    
    return 0;
}
```

### 结构体嵌套

结构体可以包含其他结构体作为成员。

```cpp
// 日期结构体
struct Date {
    int year;
    int month;
    int day;
};

// 学生结构体包含日期
struct Student {
    int id;
    string name;
    Date birthday;  // 嵌套结构体
    double score;
};
```

### 结构体高级特性

#### 结构体中的函数（C++特性）

```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

// 结构体可以包含成员函数
struct Point {
    double x;
    double y;
    
    // 成员函数
    void display() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
    
    double distanceToOrigin() {
        return sqrt(x*x + y*y);
    }
    
    // 可以重载运算符等
};

int main() {
    Point p = {3.0, 4.0};
    p.display();
    cout << "Distance to origin: " << p.distanceToOrigin() << endl;
    
    return 0;
}
```

#### 结构体大小和对齐

```cpp
#include <iostream>
using namespace std;

struct Example1 {
    char a;     // 1字节
    int b;      // 4字节
    double c;   // 8字节
};

struct Example2 {
    int a;      // 4字节
    char b;     // 1字节
    double c;   // 8字节
};

int main() {
    cout << "Size of Example1: " << sizeof(Example1) << " bytes" << endl;
    cout << "Size of Example2: " << sizeof(Example2) << " bytes" << endl;
    
    // 由于内存对齐，大小可能不同
    return 0;
}
```

### 结构体 vs 类 (struct vs class)

在 C++ 中，`struct` 和 `class` 几乎相同，唯一的区别是默认访问权限：

- `struct`：默认成员是 **public**
- `class`：默认成员是 **private**

```cpp
#include <iostream>
using namespace std;

// 使用 struct
struct PointStruct {
    double x; // 默认 public
    double y; // 默认 public
};

// 使用 class
class PointClass {
    double x; // 默认 private
    double y; // 默认 private
public:
    void setX(double x) { this->x = x; }
    double getX() { return x; }
};

int main() {
    PointStruct ps;
    ps.x = 3.0; // 可以直接访问
    
    PointClass pc;
    // pc.x = 3.0; // 错误：private成员
    pc.setX(3.0); // 必须通过公有方法
    
    return 0;
}
```



## 枚举

枚举（Enumeration）是一种用户自定义的数据类型，它允许为整数值定义有意义的名称，使代码更易读和维护。

### 什么是枚举？

枚举是一种将整数值与有意义的名称关联起来的方式。它主要用于表示一组相关的命名常量。

**使用场景：**
- 星期几（Monday, Tuesday, ...）
- 颜色（Red, Green, Blue）
- 状态（Open, Closed, Pending）
- 错误代码（Success, Error_NotFound, Error_Permission）

**枚举的优势: **

- **提高可读性**：使用名称而不是魔法数字
- **类型安全**：编译器可以检查类型
- **代码自文档化**：名称本身说明用途
- **避免错误**：防止使用无效的值

### C风格枚举 (C-style enums)

#### 基本语法

```cpp
enum 枚举名称 {
    枚举值1,
    枚举值2,
    枚举值3,
    // ...
};
```

#### 指定枚举值

```cpp
#include <iostream>
using namespace std;

// 指定枚举值
enum ErrorCode {
    Success = 0,        // 明确指定为 0
    FileNotFound = 1,   // 明确指定为 1
    PermissionDenied = 2, // 明确指定为 2
    UnknownError = 99   // 明确指定为 99
};

// 部分指定，后续自动递增
enum HttpStatus {
    OK = 200,
    Created = 201,
    Accepted = 202,
    BadRequest = 400,   // 400
    Unauthorized,       // 自动为 401
    Forbidden,          // 自动为 402
    NotFound = 404      // 明确指定
};

int main() {
    ErrorCode error = PermissionDenied;
    HttpStatus status = Unauthorized;
    
    cout << "Error code: " << error << endl;        // 2
    cout << "HTTP status: " << status << endl;      // 401
    
    return 0;
}
```

### C++11 枚举类 (enum class)

C++11 引入了更安全的枚举类（强类型枚举）。

#### 枚举类的优势
1. **强类型**：不会隐式转换为整数
2. **作用域**：枚举值在枚举的作用域内
3. **可以指定底层类型**
4. **可以前向声明**

#### 基本语法

```cpp
enum class 枚举名称 {
    枚举值1,
    枚举值2,
    // ...
};
```

#### 指定底层类型

```cpp
#include <iostream>
using namespace std;

// 指定底层类型为 char
enum class SmallEnum : char {
    Value1 = 'A',
    Value2 = 'B',
    Value3 = 'C'
};

// 指定底层类型为 short
enum class Status : short {
    Inactive = 0,
    Active = 1,
    Suspended = 2
};

int main() {
    SmallEnum e = SmallEnum::Value2;
    Status s = Status::Active;
    
    cout << "SmallEnum value: " << static_cast<char>(e) << endl; // B
    cout << "Status value: " << static_cast<short>(s) << endl;   // 1
    
    // 查看大小
    cout << "Size of SmallEnum: " << sizeof(SmallEnum) << " bytes" << endl;   // 1
    cout << "Size of Status: " << sizeof(Status) << " bytes" << endl;         // 2
    
    return 0;
}
```



# 面向对象

面向对象编程是一种编程范式，使用"对象"来设计软件。C++ 是支持 OOP 的强大语言，主要基于四大支柱：**封装、继承、多态和抽象**。



## 类与对象

### 类 (Class) vs 对象 (Object)
- **类**：蓝图或模板，定义对象的属性和行为
- **对象**：类的具体实例

### 定义类

```cpp
#include <iostream>
#include <string>
using namespace std;

// 类定义
class Person {
// 访问修饰符
private:    // 私有成员，只能在类内部访问
    string name;
    int age;

public:     // 公有成员，可以在类外部访问
    // 成员函数声明
    void setName(string n);
    void setAge(int a);
    void display();
    
protected:  // 受保护成员，与私有成员十分相似，但有一点不同，它在派生类（即子类）中是可访问的。
    double salary;
};

// 成员函数定义（可以在类外部）
void Person::setName(string n) {
    name = n;
}

void Person::setAge(int a) {
    if (a > 0 && a < 150) { // 数据验证
        age = a;
    }
}

void Person::display() {
    cout << "Name: " << name << ", Age: " << age << endl;
}

int main() {
    // 创建对象
    Person person1;
    Person person2;
    
    // 使用对象
    person1.setName("Alice");
    person1.setAge(25);
    
    person2.setName("Bob");
    person2.setAge(30);
    
    person1.display(); // Name: Alice, Age: 25
    person2.display(); // Name: Bob, Age: 30
    
    return 0;
}
```

## 构造函数与析构函数

### 构造函数
类的**构造函数**是类的一种特殊的成员函数，它会在每次创建类的新对象时执行。用于初始化对象。

```cpp
class Person {
private:
    string name;
    int age;

public:
    // 1. 默认构造函数
    Person() {
        name = "Unknown";
        age = 0;
        cout << "Default constructor called" << endl;
    }
    
    // 2. 参数化构造函数
    Person(string n, int a) {
        name = n;
        age = a;
        cout << "Parameterized constructor called" << endl;
    }
    
    // 3. 拷贝构造函数
    Person(const Person& other) {
        name = other.name;
        age = other.age;
        cout << "Copy constructor called" << endl;
    }
    
    void display() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

int main() {
    Person p1;                  // 默认构造函数
    Person p2("Alice", 25);     // 参数化构造函数
    Person p3 = p2;             // 拷贝构造函数
    Person p4(p2);              // 拷贝构造函数
    
    p1.display(); // Name: Unknown, Age: 0
    p2.display(); // Name: Alice, Age: 25
    p3.display(); // Name: Alice, Age: 25
    
    return 0;
}
```

### 析构函数
类的**析构函数**是类的一种特殊的成员函数，它会在每次删除所创建的对象时执行。

析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。

```cpp
class DatabaseConnection {
private:
    string connectionString;
    
public:
    DatabaseConnection(string connStr) : connectionString(connStr) {
        cout << "Connected to: " << connectionString << endl;
    }
    
    // 析构函数
    ~DatabaseConnection() {
        cout << "Disconnected from: " << connectionString << endl;
    }
    
    void query(string sql) {
        cout << "Executing: " << sql << endl;
    }
};

int main() {
    {
        DatabaseConnection db("localhost:3306/mydb");
        db.query("SELECT * FROM users");
    } // 析构函数自动调用
    
    cout << "Database connection closed" << endl;
    return 0;
}
```

### 初始化列表
更高效的初始化方式

```cpp
class Point {
private:
    double x;
    double y;
    const int id; // const成员必须用初始化列表
    
public:
    Point(double xVal, double yVal, int idVal) 
        : x(xVal), y(yVal), id(idVal) { // 初始化列表
        // 构造函数体
    }
    
    void display() {
        cout << "Point " << id << ": (" << x << ", " << y << ")" << endl;
    }
};
```

## 封装 (Encapsulation)

将数据和行为包装在一起，隐藏实现细节

```cpp
class BankAccount {
private:
    string accountNumber;
    double balance;
    string ownerName;
    
    // 私有方法，内部使用
    bool validateAmount(double amount) {
        return amount > 0;
    }
    
public:
    BankAccount(string accNum, string owner, double initialBalance = 0)
        : accountNumber(accNum), ownerName(owner), balance(initialBalance) {}
    
    // 公有接口
    void deposit(double amount) {
        if (validateAmount(amount)) {
            balance += amount;
            cout << "Deposited: $" << amount << endl;
        }
    }
    
    bool withdraw(double amount) {
        if (validateAmount(amount) && balance >= amount) {
            balance -= amount;
            cout << "Withdrew: $" << amount << endl;
            return true;
        }
        cout << "Withdrawal failed" << endl;
        return false;
    }
    
    double getBalance() const {
        return balance;
    }
    
    string getAccountInfo() const {
        return "Account: " + accountNumber + ", Owner: " + ownerName;
    }
};

int main() {
    BankAccount account("123456", "Alice", 1000);
    account.deposit(500);
    account.withdraw(200);
    cout << "Balance: $" << account.getBalance() << endl;
    cout << account.getAccountInfo() << endl;
    
    // account.balance = 1000000; // 错误：private成员
    return 0;
}
```

## 继承 (Inheritance)

### 基本继承

```cpp
#include <iostream>
#include <string>
using namespace std;

// 基类
class Animal {
protected: // 保护成员，派生类可以访问
    string name;
    int age;
    
public:
    Animal(string n, int a) : name(n), age(a) {}
    
    void eat() {
        cout << name << " is eating" << endl;
    }
    
    void sleep() {
        cout << name << " is sleeping" << endl;
    }
    
    virtual void makeSound() { // 虚函数，支持多态
        cout << name << " makes a sound" << endl;
    }
};

// 派生类
class Dog : public Animal {
private:
    string breed;
    
public:
    Dog(string n, int a, string b) : Animal(n, a), breed(b) {}
    
    void bark() {
        cout << name << " says: Woof! Woof!" << endl;
    }
    
    void makeSound() override { // 重写虚函数
        bark();
    }
    
    void displayInfo() {
        cout << name << " is a " << breed << " and is " << age << " years old" << endl;
    }
};

class Cat : public Animal {
public:
    Cat(string n, int a) : Animal(n, a) {}
    
    void meow() {
        cout << name << " says: Meow!" << endl;
    }
    
    void makeSound() override {
        meow();
    }
};

int main() {
    Dog myDog("Buddy", 3, "Golden Retriever");
    Cat myCat("Whiskers", 2);
    
    myDog.eat();        // 继承自Animal
    myDog.bark();       // Dog特有
    myDog.displayInfo();// Dog特有
    
    myCat.sleep();      // 继承自Animal
    myCat.meow();       // Cat特有
    
    return 0;
}
```

### 继承类型

当一个类派生自基类，该基类可以被继承为 **public、protected** 或 **private** 几种类型。继承类型是通过上面讲解的访问修饰符 access-specifier 来指定的。

我们几乎不使用 **protected** 或 **private** 继承，通常使用 **public** 继承。当使用不同类型的继承时，遵循以下几个规则：

```cpp
class Base {
public:
    int publicVar;
protected:
    int protectedVar;
private:
    int privateVar;
};

// 公有继承
class PublicDerived : public Base {
    // publicVar 仍然是 public
    // protectedVar 仍然是 protected
    // privateVar 不可访问
};

// 保护继承
class ProtectedDerived : protected Base {
    // publicVar 变成 protected
    // protectedVar 仍然是 protected
    // privateVar 不可访问
};

// 私有继承
class PrivateDerived : private Base {
    // publicVar 变成 private
    // protectedVar 变成 private
    // privateVar 不可访问
};
```

### 多继承

多继承即一个子类可以有多个父类，它继承了多个父类的特性。

C++ 类可以从多个类继承成员，语法如下：

```cpp
// 派生类
class Rectangle: public Shape, public PaintCost {
   public:
      int getArea()
      { 
         return (width * height); 
      }
};
```



## 多态 (Polymorphism)

**多态**按字面的意思就是多种形态。

当类之间存在层次结构，并且类之间是通过继承关联时，就会用到多态。

在 C++ 中，多态（Polymorphism）是面向对象编程的重要特性之一。

C++ 多态允许使用基类指针或引用来调用子类的重写方法，从而使得同一接口可以表现不同的行为。

多态使得代码更加灵活和通用，程序可以通过基类指针或引用来操作不同类型的对象，而不需要显式区分对象类型。这样可以使代码更具扩展性，在增加新的形状类时不需要修改主程序。

以下是多态的几个关键点：

**虚函数（Virtual Functions）**：

- 在基类中声明一个函数为虚函数，使用关键字`virtual`。
- 派生类可以重写（override）这个虚函数，**只有使用`virtual`的函数才可以被重写**。
- 调用虚函数时，会根据对象的实际类型来决定调用哪个版本的函数。

**动态绑定（Dynamic Binding）**：

- 也称为晚期绑定（Late Binding），在运行时确定函数调用的具体实现。
- 需要使用指向基类的指针或引用来调用虚函数，编译器在运行时根据对象的实际类型来决定调用哪个函数。

**纯虚函数（Pure Virtual Functions）**：

- 一个包含纯虚函数的类被称为抽象类（Abstract Class），它**不能被直接实例化**。
- 纯虚函数没有函数体，声明时使用`= 0`。
- 它强制派生类提供具体的实现。

**多态的实现机制**：

- 虚函数表（V-Table）：C++运行时使用虚函数表来实现多态。每个包含虚函数的类都有一个虚函数表，表中存储了指向类中所有虚函数的指针。
- 虚函数指针（V-Ptr）：对象中包含一个指向该类虚函数表的指针。

### 虚函数和重写

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Shape {
protected:
    string color;
    
public:
    Shape(string c) : color(c) {}
    
    virtual double getArea() const = 0; // 纯虚函数，抽象类
    
    virtual void draw() const {
        cout << "Drawing a " << color << " shape" << endl;
    }
    
    virtual ~Shape() {} // 虚析构函数
};

class Circle : public Shape {
private:
    double radius;
    
public:
    Circle(string c, double r) : Shape(c), radius(r) {}
    
    double getArea() const override {
        return 3.14159 * radius * radius;
    }
    
    void draw() const override {
        cout << "Drawing a " << color << " circle with area: " << getArea() << endl;
    }
};

class Rectangle : public Shape {
private:
    double width;
    double height;
    
public:
    Rectangle(string c, double w, double h) : Shape(c), width(w), height(h) {}
    
    double getArea() const override {
        return width * height;
    }
    
    void draw() const override {
        cout << "Drawing a " << color << " rectangle with area: " << getArea() << endl;
    }
};

int main() {
    // Shape shape("red"); // 错误：不能实例化抽象类
    
    vector<Shape*> shapes;
    shapes.push_back(new Circle("red", 5.0));
    shapes.push_back(new Rectangle("blue", 4.0, 6.0));
    shapes.push_back(new Circle("green", 3.0));
    
    // 多态调用
    for (Shape* shape : shapes) {
        shape->draw(); // 根据实际对象类型调用相应方法
    }
    
    // 清理内存
    for (Shape* shape : shapes) {
        delete shape;
    }
    
    return 0;
}
```

### 动态类型识别

```cpp
#include <iostream>
#include <typeinfo>
using namespace std;

class Animal {
public:
    virtual ~Animal() {}
};

class Dog : public Animal {};
class Cat : public Animal {};

int main() {
    Animal* animal = new Dog();
    
    // 使用 typeid
    if (typeid(*animal) == typeid(Dog)) {
        cout << "It's a Dog" << endl;
    } else if (typeid(*animal) == typeid(Cat)) {
        cout << "It's a Cat" << endl;
    }
    
    // 使用 dynamic_cast
    if (Dog* dog = dynamic_cast<Dog*>(animal)) {
        cout << "Successfully cast to Dog" << endl;
    }
    
    delete animal;
    return 0;
}
```

### 纯虚函数和抽象类

```cpp
class Printable {
public:
    virtual void print() const = 0; // 纯虚函数
    virtual ~Printable() {}
};

class Report : public Printable {
private:
    string content;
    
public:
    Report(string c) : content(c) {}
    
    void print() const override {
        cout << "Report: " << content << endl;
    }
};

class Invoice : public Printable {
private:
    double amount;
    
public:
    Invoice(double amt) : amount(amt) {}
    
    void print() const override {
        cout << "Invoice amount: $" << amount << endl;
    }
};

void printDocument(const Printable& doc) {
    doc.print(); // 多态调用
}

int main() {
    Report report("Quarterly Earnings");
    Invoice invoice(999.99);
    
    printDocument(report);
    printDocument(invoice);
    
    return 0;
}
```

## 静态成员

```cpp
class Employee {
private:
    string name;
    static int count; // 静态成员变量
    
public:
    Employee(string n) : name(n) {
        count++;
        cout << "Employee created. Total: " << count << endl;
    }
    
    ~Employee() {
        count--;
        cout << "Employee destroyed. Total: " << count << endl;
    }
    
    static int getCount() { // 静态成员函数
        return count;
    }
};

// 初始化静态成员
int Employee::count = 0;

int main() {
    cout << "Initial count: " << Employee::getCount() << endl;
    
    Employee e1("Alice");
    Employee e2("Bob");
    
    {
        Employee e3("Charlie");
        cout << "Current count: " << Employee::getCount() << endl;
    }
    
    cout << "Final count: " << Employee::getCount() << endl;
    return 0;
}
```

---

## 友元 (Friend)

友元是 C++ 提供的一种打破类封装性的机制，它允许一个**类、类的成员函数**或者一个**普通函数**访问另一个类的私有（`private`）和保护（`protected`）成员。

### 为什么需要友元？

面向对象编程的核心原则之一是**封装**，即隐藏对象的内部实现细节。但有些特殊场景下，严格的封装会成为障碍。例如：

1. 当两个类需要紧密协作，互相操作对方的私有数据时（如 `Tree` 和 `TreeNode` 类）。
2. 当重载某些操作符（如 `<<`, `>>`）时，操作符函数需要访问类的私有成员。
3. 当某个全局函数或另一个类的成员函数需要频繁访问某个类的内部数据时。

友元关系提供了必要的灵活性，但应谨慎使用，因为它会削弱封装性。

### 友元的三种形式

#### 友元函数（普通函数）

将一个**非成员函数**声明为类的友元，使其可以访问该类的所有成员。

**经典例子：重载 `<<` 操作符用于输出**

```cpp
#include <iostream>
using namespace std;

class Box {
private:
    double width;

public:
    Box(double w) : width(w) {}
    
    // 声明友元函数
    // 注意：这不是类的成员函数！
    friend void printWidth(const Box& box);
    friend ostream& operator<<(ostream& os, const Box& box);
};

// 友元函数的定义
void printWidth(const Box& box) {
    // 可以直接访问私有成员 width
    cout << "Width of box: " << box.width << endl;
}

// 重载 << 操作符
ostream& operator<<(ostream& os, const Box& box) {
    os << "Box(width: " << box.width << ")";
    return os;
}

int main() {
    Box b(10.0);
    printWidth(b);   // 输出: Width of box: 10
    cout << b << endl; // 输出: Box(width: 10)
    return 0;
}
```

#### 友元类（Friend Class）

将一个**整个类**声明为友元，那么该友元类的**所有成员函数**都可以访问另一个类的私有和保护成员。

**语法：** `friend class ClassName;`

**例子：**

```cpp
class Window; // 前向声明

class Monitor {
private:
    int brightness;
public:
    Monitor(int b) : brightness(b) {}
    // 声明 Window 为友元类
    friend class Window;
};

class Window {
public:
    void adjustBrightness(Monitor& mon, int level) {
        // 因为 Window 是 Monitor 的友元类，
        // 所以可以直接访问其私有成员 brightness
        mon.brightness = level;
        cout << "Brightness set to: " << mon.brightness << endl;
    }

    void showBrightness(const Monitor& mon) {
        cout << "Current brightness: " << mon.brightness << endl;
    }
};

int main() {
    Monitor myMonitor(50);
    Window settingsWindow;
    
    settingsWindow.showBrightness(myMonitor); // 输出: Current brightness: 50
    settingsWindow.adjustBrightness(myMonitor, 75); // 输出: Brightness set to: 75
    
    return 0;
}
```

#### 友元成员函数（Friend Member Function）

只将另一个类的**某一个特定成员函数**声明为友元，而不是整个类。这样，只有这个被指定的函数可以访问你的私有成员。

**语法稍复杂，需要注意声明顺序。**

**例子：**

```cpp
class Box; // 前向声明 (Forward Declaration)

class Display {
public:
    void showVolume(const Box& box); // 成员函数声明
    void showNothing(const Box& box); // 另一个成员函数
};

class Box {
private:
    double length;
    double width;
    double height;

public:
    Box(double l, double w, double h) : length(l), width(w), height(h) {}
    
    // 只将 Display::showVolume 声明为友元，而不是整个 Display 类
    friend void Display::showVolume(const Box& box);
    // 注意：Display::showNothing 不是友元，它不能访问 Box 的私有成员
};

// 现在才定义 Display 的成员函数
void Display::showVolume(const Box& box) {
    // 可以访问 Box 的私有成员，因为它是友元
    double vol = box.length * box.width * box.height;
    cout << "Volume: " << vol << endl;
}

void Display::showNothing(const Box& box) {
    // 编译错误！showNothing 不是友元，不能访问私有成员
    // cout << box.length << endl; // Error: 'double Box::length' is private
}

int main() {
    Box myBox(3, 4, 5);
    Display myDisplay;
    
    myDisplay.showVolume(myBox); // 正常工作
    // myDisplay.showNothing(myBox); // 如果取消注释，编译会失败
    
    return 0;
}
```



## 重载

### 函数重载

在同一个作用域内，可以声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同。您不能仅通过返回类型的不同来重载函数。

下面的实例中，同名函数 **print()** 被用于输出不同的数据类型

```cpp
class printData {
   public:
      void print(int i) {
        cout << "整数为: " << i << endl;
      }
 
      void print(double  f) {
        cout << "浮点数为: " << f << endl;
      }
 
      void print(char c[]) {
        cout << "字符串为: " << c << endl;
      }
};
```

### 运算符重载

您可以重定义或重载大部分 C++ 内置的运算符。这样，您就能使用自定义类型的运算符。

重载的运算符是带有特殊名称的函数，函数名是由关键字 `operator` 和其后要重载的运算符符号构成的。与其他函数一样，重载运算符有一个返回类型和一个参数列表。

```cpp
class Vector {
private:
    double x, y;
    
public:
    Vector(double x = 0, double y = 0) : x(x), y(y) {}
    
    // 运算符重载
    Vector operator+(const Vector& other) const {
        return Vector(x + other.x, y + other.y);
    }
    
    Vector operator-(const Vector& other) const {
        return Vector(x - other.x, y - other.y);
    }
    
    Vector operator*(double scalar) const {
        return Vector(x * scalar, y * scalar);
    }
    
    // 友元函数重载
    friend Vector operator*(double scalar, const Vector& vec);
    
    // 输出运算符重载
    friend ostream& operator<<(ostream& os, const Vector& vec);
    
    void display() const {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};

Vector operator*(double scalar, const Vector& vec) {
    return Vector(vec.x * scalar, vec.y * scalar);
}

ostream& operator<<(ostream& os, const Vector& vec) {
    os << "(" << vec.x << ", " << vec.y << ")";
    return os;
}

int main() {
    Vector v1(1, 2);
    Vector v2(3, 4);
    
    Vector v3 = v1 + v2;
    Vector v4 = v1 - v2;
    Vector v5 = v1 * 2;
    Vector v6 = 3 * v1;
    
    cout << "v1: " << v1 << endl;
    cout << "v2: " << v2 << endl;
    cout << "v1 + v2: " << v3 << endl;
    cout << "v1 - v2: " << v4 << endl;
    cout << "v1 * 2: " << v5 << endl;
    cout << "3 * v1: " << v6 << endl;
    
    return 0;
}
```



# 高级语法



## 模板与元编程



### 模板 (Templates)

模板是 C++ 中支持**泛型编程**的工具。它的核心思想是：**将类型参数化**。你可以把它理解为一个蓝图或一个公式，编译器会根据你使用时提供的具体类型，来生成特定版本的代码。

#### 为什么要用模板？
*   **代码复用**：编写一次逻辑，即可用于多种数据类型（`int`, `float`, `string`, 自定义类等）。
*   **类型安全**：相比使用 `void*` 的 C 风格泛型，模板在编译时进行类型检查，更安全。
*   **性能**：生成的代码是针对特定类型优化过的，没有运行时开销（不同于某些语言的泛型实现）。

#### 模板的主要种类

**a) 函数模板 (Function Templates)**

创建一个可处理多种类型的函数。

```cpp
// 模板声明，T 是一个占位符类型
template <typename T> 
T max(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    std::cout << max(10, 5) << std::endl;      // T 被推导为 int，生成 int max(int, int)
    std::cout << max(3.14, 2.99) << std::endl; // T 被推导为 double，生成 double max(double, double)
    // std::cout << max(10, 3.14) << std::endl; // 错误！编译器无法推导出唯一的 T 类型
    std::cout << max<double>(10, 3.14) << std::endl; // 正确！显式指定 T 为 double
}
```

**b) 类模板 (Class Templates)**

创建一个可包含多种类型的类。STL 中的容器（`vector`, `list`, `map` 等）都是类模板。

```cpp
// 一个简单的栈类模板
template <typename T>
class Stack {
private:
    std::vector<T> elements;
public:
    void push(const T& element) {
        elements.push_back(element);
    }
    T pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
        T top = elements.back();
        elements.pop_back();
        return top;
    }
    // ...
};

int main() {
    Stack<int> intStack;       // 一个用于 int 的栈
    Stack<std::string> strStack; // 一个用于 string 的栈

    intStack.push(42);
    strStack.push("Hello Templates");

    std::cout << intStack.pop() << std::endl;
    std::cout << strStack.pop() << std::endl;
}
```

#### 高级模板特性

*   **非类型模板参数 (Non-type Template Parameters)**：参数不仅是类型，也可以是整型值、指针或引用。
    ```cpp
    template <typename T, int Size> // `Size` 是一个非类型参数
    class Array {
    private:
        T m_data[Size]; // 编译时就知道大小的数组
    public:
        int getSize() const { return Size; }
    };
    
    Array<double, 10> myArray; // 创建一个大小为 10 的 double 数组
    ```

*   **模板特化 (Template Specialization)**：为模板的特定类型提供特殊实现。
    ```cpp
    // 通用模板
    template <typename T>
    class Printer {
    public:
        void print(const T& value) {
            std::cout << "Value: " << value << std::endl;
        }
    };
    
    // 特化版本 for std::string
    template <>
    class Printer<std::string> {
    public:
        void print(const std::string& value) {
            std::cout << "String: \"" << value << "\"" << std::endl;
        }
    };
    
    Printer<int> intPrinter;
    intPrinter.print(100); // 输出: Value: 100
    
    Printer<std::string> strPrinter;
    strPrinter.print("Hello"); // 输出: String: "Hello"
    ```

*   **默认模板参数 (Default Template Arguments)**：为模板参数指定默认值。
    ```cpp
    template <typename T = int, int Size = 100> // 默认类型是 int，默认大小是 100
    class Buffer {
        // ...
    };
    
    Buffer<> buffer1;        // 使用默认参数 Buffer<int, 100>
    Buffer<float> buffer2;   // Buffer<float, 100>
    Buffer<char, 512> buffer3; // Buffer<char, 512>
    ```

### 元编程 (Metaprogramming)

元编程指的是**在编译时执行程序**的技术。你可以编写一些代码，这些代码在编译期间运行，并生成或操纵其他代码（通常是常量和类型）。模板是 C++ 中进行元编程的主要工具，因此也称为**模板元编程 (Template Metaprogramming, TMP)**。

#### 元编程的核心思想：
利用编译器在编译时实例化模板、进行条件判断和递归计算的能力，将工作从运行时转移到编译时。

#### 经典示例：编译期计算阶乘

```cpp
// 通用模板，用于计算 N 的阶乘
template <unsigned int N>
struct Factorial {
    static const unsigned int value = N * Factorial<N - 1>::value;
};

// 模板特化，作为递归的基准情况
template <>
struct Factorial<0> {
    static const unsigned int value = 1;
};

int main() {
    // 这个计算发生在编译期！
    // Factorial<5>::value 在编译后就是一个常量 120
    std::cout << "Factorial of 5: " << Factorial<5>::value << std::endl; // 输出 120

    // 下面这行代码等价于 int array[120];
    int array[Factorial<5>::value]; 

    return 0;
}
```
在这个例子中，`Factorial<5>::value` 在编译时就已经被计算为 `120`，运行时直接使用这个结果，没有任何计算开销。

#### 现代 C++ 中的元编程工具

**a) `constexpr` (C++11 起)**
让元编程变得更简单直观。使用 `constexpr` 函数，你可以用类似普通函数的语法进行编译期计算。

```cpp
// constexpr 函数，可在编译期运行
constexpr unsigned int factorial(unsigned int n) {
    return (n <= 1) ? 1 : (n * factorial(n - 1));
}

int main() {
    constexpr unsigned int result = factorial(5); // 编译期计算
    std::cout << result << std::endl; // 输出 120
    int my_array[factorial(3)]; // 数组大小为 6
}
```

**b) `std::enable_if` 与 SFINAE (C++11)**
一种利用模板特化和替换失败来控制编译器重载决议的技术。它非常强大但也非常复杂，常用于在模板中进行条件编译。

> **SFINAE**: "Substitution Failure Is Not An Error"（替换失败并非错误）。简单说就是，在重载解析过程中，如果模板参数替换失败，编译器不会报错，而是简单地忽略这个候选重载，继续尝试其他的。

**c) 概念 (Concepts) (C++20)**
**极大地简化了模板元编程！** 它允许你为模板参数指定约束条件，让模板的接口更清晰，错误信息更友好。

```cpp
// 使用概念定义一个约束：必须是 signed（有符号）整型
template <class T>
concept SignedIntegral = std::is_integral_v<T> && std::is_signed_v<T>;

// 使用概念，这个函数模板只接受满足 SignedIntegral 的类型 T
template <SignedIntegral T> 
void signedIntsOnly(T val) {
    // ... 函数体
}

signedIntsOnly(10);    // OK, int 是有符号整型
signedIntsOnly(10u);   // 错误！unsigned int 不满足概念约束
//signedIntsOnly("hello"); // 错误！显然不满足
```

### 总结

| 特性       | 描述                       | 目的                                                         |
| :--------- | :------------------------- | :----------------------------------------------------------- |
| **模板**   | 类型参数化的蓝图           | **代码复用**，编写通用、类型安全的代码                       |
| **元编程** | 在编译期执行计算和生成代码 | **性能优化**（将计算移至编译期）、**定制代码生成**（通过特化）、**静态检查**（通过概念和 SFINAE） |

**关系**：模板是**实现**元编程的**主要工具**。通过使用模板的特化、递归和参数推导，我们可以在 C++ 中实现强大的编译期计算和代码生成功能。现代 C++（尤其是 `constexpr` 和 `concepts`）让元编程变得更简单、更安全、更易读。



## 标准容器



### 概述

C++ 标准模板库 (STL) 提供了一套丰富的数据结构，称为容器。它们用于存储和管理数据的集合。所有容器都是**类模板**，这意味着你可以让它们存储任何数据类型。

容器主要分为三大类：
1.  **序列容器 (Sequence Containers)**：强调元素的顺序和位置。
2.  **关联容器 (Associative Containers)**：基于键 (key) 快速查找元素，通常使用二叉搜索树实现。
3.  **无序关联容器 (Unordered Associative Containers)**：基于哈希表实现，提供更快的平均查找速度，但元素无序。

### 常用标准容器

| 容器名                    | 中文名       | 类别       | 特点                                                         | 头文件            |
| :------------------------ | :----------- | :--------- | :----------------------------------------------------------- | :---------------- |
| `std::vector`             | 向量         | 序列       | **动态数组**。在尾部插入/删除快（O(1) 摊销），在中间/头部插入/删除慢（O(n)）。**随机访问**极快（O(1)）。 | `<vector>`        |
| `std::deque`              | 双端队列     | 序列       | **双端动态数组**。在头尾插入/删除都快（O(1) 摊销）。随机访问快（O(1)）。 | `<deque>`         |
| `std::list`               | 列表         | 序列       | **双向链表**。在任何位置插入/删除都快（O(1)），前提是已找到位置。**不支持随机访问**（访问需 O(n)）。 | `<list>`          |
| `std::forward_list`       | 单向链表     | 序列       | **单向链表**。比 `list` 更省空间，但只能单向遍历。           | `<forward_list>`  |
| `std::array`              | 数组         | 序列       | **固定大小数组**。大小在编译时确定。性能与 C 风格数组相同，但更安全（知道自身大小、不支持自动退化为指针）。 | `<array>`         |
| `std::set`                | 集合         | 关联       | **有序集合**（通常按键升序）。元素即键，**唯一**（不允许重复）。查找、插入、删除一般为 O(log n)。 | `<set>`           |
| `std::multiset`           | 多重集合     | 关联       | **有序集合**，但允许**重复**元素。                           | `<set>`           |
| `std::map`                | 映射         | 关联       | **有序键值对集合**。键是**唯一**的。基于键快速查找值。       | `<map>`           |
| `std::multimap`           | 多重映射     | 关联       | **有序键值对集合**，允许**重复**的键。                       | `<map>`           |
| `std::unordered_set`      | 无序集合     | 无序关联   | **哈希集合**。元素**唯一**。**平均**查找、插入、删除为 O(1)，最差为 O(n)。**元素无序**。 | `<unordered_set>` |
| `std::unordered_multiset` | 无序多重集合 | 无序关联   | **哈希集合**，允许**重复**元素。                             | `<unordered_set>` |
| `std::unordered_map`      | 无序映射     | 无序关联   | **哈希键值对集合**。键**唯一**。                             | `<unordered_map>` |
| `std::unordered_multimap` | 无序多重映射 | 无序关联   | **哈希键值对集合**，允许**重复**的键。                       | `<unordered_map>` |
| `std::stack`              | 栈           | 容器适配器 | LIFO（后进先出）结构。基于 `deque`（默认）、`list` 或 `vector` 实现。 | `<stack>`         |
| `std::queue`              | 队列         | 容器适配器 | FIFO（先进先出）结构。基于 `deque`（默认）或 `list` 实现。   | `<queue>`         |
| `std::priority_queue`     | 优先队列     | 容器适配器 | 元素按优先级出队。基于 `vector`（默认）实现，通常用堆结构。  | `<queue>`         |

**如何选择容器？**
*   需要高效随机访问：`vector`, `array`, `deque`
*   需要在头部和尾部频繁插入删除：`deque`
*   需要在中间频繁插入删除：`list`, `forward_list`
*   需要频繁查找且元素顺序不重要：`unordered_set`, `unordered_map`
*   需要频繁查找且元素需要有序：`set`, `map`
*   需要 LIFO 行为：`stack`
*   需要 FIFO 行为：`queue`

### 通用容器操作

大多数容器都提供了一套通用的成员函数接口。

#### 构造函数和赋值
```cpp
std::vector<int> v1; // 默认构造，空容器
std::vector<int> v2(5, 100); // 构造包含 5 个 100 的容器
std::vector<int> v3 = {1, 2, 3, 4, 5}; // 初始化列表构造 (C++11)
std::vector<int> v4(v3.begin(), v3.end()); // 范围构造
std::vector<int> v5(v4); // 拷贝构造

v1 = v5; // 赋值操作
v1 = {6, 7, 8, 9}; // 赋值初始化列表
```

#### 大小和容量
```cpp
std::vector<int> vec = {1, 2, 3};

bool isEmpty = vec.empty();  // 检查是否为空
size_t size = vec.size();    // 返回元素个数
vec.resize(10);              // 调整容器大小，新增元素默认初始化
vec.reserve(100);            // (vector, string) 预留容量，避免多次重新分配
size_t cap = vec.capacity(); // (vector, string) 返回当前分配的存储容量
vec.shrink_to_fit();         // (vector, string, deque) 请求移除未使用的容量
```

#### 访问元素
```cpp
std::vector<int> vec = {10, 20, 30};

// 以下操作许多容器都有，但 list/forward_list 没有 [] 和 at()
int first = vec.front();      // 访问第一个元素 (10)
int last = vec.back();        // 访问最后一个元素 (30)
int elem = vec[1];            // 下标访问 (20) - 不检查边界！
int safe_elem = vec.at(1);    // 带边界检查的下标访问，越界抛出 std::out_of_range

// 对于关联容器 (map, unordered_map)，使用 key 访问
std::map<std::string, int> ageMap = {{"Alice", 30}, {"Bob", 25}};
int aliceAge = ageMap["Alice"]; // 返回 30。如果键不存在，会创建它（值默认初始化）！
int bobAge = ageMap.at("Bob");  // 返回 25。如果键不存在，抛出 std::out_of_range。
```

#### 修改元素（插入、删除）
```cpp
std::vector<int> vec = {1, 2, 3};

// --- 插入 ---
vec.push_back(4);           // 在尾部插入 4 -> {1, 2, 3, 4}
// vec.push_front(0);       // 在头部插入 (deque, list 支持) -> {0, 1, 2, 3, 4}
auto it = vec.begin() + 1;
vec.insert(it, 99);         // 在迭代器位置前插入 -> {1, 99, 2, 3, 4}
vec.insert(vec.end(), {5, 6}); // 插入一个列表 -> {1, 99, 2, 3, 4, 5, 6}

// map 的插入
std::map<std::string, int> m;
m.insert({"Charlie", 40});
m.emplace("David", 35); // 直接在容器内构造元素，效率更高

// --- 删除 ---
vec.pop_back();             // 删除最后一个元素 -> {1, 99, 2, 3, 4, 5}
// vec.pop_front();         // 删除第一个元素 (deque, list 支持)
it = vec.begin() + 2;
vec.erase(it);              // 删除迭代器指向的元素 -> {1, 99, 3, 4, 5}
vec.erase(vec.begin(), vec.begin() + 2); // 删除一个范围内的元素 -> {3, 4, 5}
vec.clear();                // 删除所有元素 -> {}
```

#### 查找和计数
```cpp
std::set<int> mySet = {5, 2, 8, 1, 9};

// 查找元素，返回迭代器。找到则指向元素，未找到则等于 .end()
auto found = mySet.find(8);
if (found != mySet.end()) {
    std::cout << "Found: " << *found << std::endl;
}

// 计数元素出现次数 (对于 set/map，结果只能是 0 或 1；multiset/multimap 可以 >1)
size_t count = mySet.count(2); // 返回 1

// 对于无序容器，查找效率平均更高
std::unordered_set<int> myUSet = {5, 2, 8, 1, 9};
auto foundUS = myUSet.find(8);
```

### 迭代器 (Iterators)

迭代器用于遍历容器中的元素，提供了一种统一的方法来访问容器，无论其内部结构如何。

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};

// 1. 使用迭代器循环 (经典方法)
for (auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";
}
std::cout << std::endl;

// 2. 基于范围的 for 循环 (C++11) - 更简洁，底层使用迭代器
for (const auto& element : vec) { // 使用引用避免拷贝，const 避免修改
    std::cout << element << " ";
}
std::cout << std::endl;

// 迭代器类型：
// vec.begin()  -> 指向第一个元素
// vec.end()    -> 指向最后一个元素之后的“尾后”位置
// vec.rbegin() -> 反向迭代器，指向最后一个元素
// vec.rend()   -> 反向迭代器，指向第一个元素之前的位置
// vec.cbegin() -> const 迭代器，用于只读访问
```

### 总结

| 操作类别      | 常用函数                                                     |
| :------------ | :----------------------------------------------------------- |
| **构造/赋值** | 默认构造、拷贝构造、初始化列表构造、`operator=`, `assign`    |
| **大小**      | `size()`, `empty()`, `resize()`, `capacity()`, `reserve()`   |
| **访问**      | `[]`, `at()`, `front()`, `back()`, `find()`                  |
| **修改**      | `push_back()`, `push_front()`, `insert()`, `emplace()`, `pop_back()`, `pop_front()`, `erase()`, `clear()` |
| **迭代**      | `begin()`, `end()`, `rbegin()`, `rend()`, `cbegin()`, `cend()` |

掌握这些容器和它们的通用操作是有效使用 C++ 标准库的基础。始终根据你的具体需求（访问模式、插入删除频率、是否需排序）来选择合适的容器。



## 语法简化与类型优化



### 语法简化

#### `auto` 类型推导 (C++11)
让编译器根据初始化表达式自动推导变量类型。
```cpp
// 旧写法 - 类型冗长
std::vector<std::map<std::string, std::list<int>>>::iterator it = complexContainer.begin();

// 新写法 - 使用 auto
auto it = complexContainer.begin(); // 编译器知道 it 的类型
auto i = 42;                       // int
auto d = 3.14;                     // double
auto s = "hello";                  // const char*
auto vec = std::vector<int>{1, 2, 3}; // std::vector<int>

// 在基于范围的 for 循环中特别有用
for (auto& element : container) { ... }       // 可修改的引用
for (const auto& element : container) { ... } // 只读引用，避免拷贝
```

#### 基于范围的 for 循环 (Range-based for loop) (C++11)
简化容器遍历语法。
```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};

// 旧写法 - 繁琐
for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";
}

// 新写法 - 简洁直观
for (int value : vec) {
    std::cout << value << " ";
}
// 更推荐使用 auto 和引用
for (const auto& value : vec) {
    std::cout << value << " ";
}
```

#### 结构化绑定 (Structured Bindings) (C++17)
从元组、结构体或数组中直接解包多个变量。
```cpp
std::pair<int, std::string> getPerson() { return {30, "Alice"}; }
std::map<std::string, int> cityPopulations = {{"Beijing", 2154}, {"Shanghai", 2424}};

// 旧写法 - 需要 first 和 second
auto person = getPerson();
int age = person.first;
std::string name = person.second;

// 新写法 - 直接解包
auto [age, name] = getPerson(); // age=30, name="Alice"

// 遍历 map 时特别有用
for (const auto& [city, population] : cityPopulations) { // 不再是 pair
    std::cout << city << ": " << population << "万人\n";
}
```

#### 初始化列表 (Initializer Lists) (C++11)
统一的初始化语法。
```cpp
// 各种初始化方式变得统一
int x{5};                 // 直接初始化
std::vector<int> v{1, 2, 3}; // 列表初始化
std::map<std::string, int> m{{"a", 1}, {"b", 2}};

// 防止窄化转换（提高安全性）
int y{7.5}; // 编译错误！double 到 int 是窄化转换
```

#### Lambda 表达式 (C++11)
定义匿名函数对象，简化函数对象的创建。
```cpp
std::vector<int> numbers = {5, 2, 8, 1, 9};

// 旧写法 - 需要定义函数对象类
struct GreaterThanFive {
    bool operator()(int n) { return n > 5; }
};
auto it1 = std::find_if(numbers.begin(), numbers.end(), GreaterThanFive());

// 新写法 - 使用 lambda，简洁直观
auto it2 = std::find_if(numbers.begin(), numbers.end(),
                       [](int n) { return n > 5; }); // 内联定义谓词

// 排序：按绝对值降序
std::sort(numbers.begin(), numbers.end(),
          [](int a, int b) { return std::abs(a) > std::abs(b); });
```

### 类型优化与安全

#### `nullptr` (C++11)
类型安全的空指针常量，替代容易出错的 `NULL` 宏（通常是 0）。
```cpp
void foo(int);
void foo(int*);

// 旧写法 - 有问题
foo(NULL);    // 可能调用 foo(int)，而不是预期的 foo(int*)

// 新写法 - 类型安全
foo(nullptr); // 明确调用 foo(int*)
```

#### 强类型枚举 (enum class) (C++11)
解决传统 C 风格枚举的命名污染和隐式转换问题。
```cpp
// 旧枚举 - 存在问题
enum Color { Red, Green, Blue };
enum TrafficLight { Red, Yellow, Green }; // 错误！Red 和 Green 重定义
int value = Red; // 隐式转换为 int，可能非预期

// 新枚举 - 更安全
enum class Color { Red, Green, Blue };
enum class TrafficLight { Red, Yellow, Green }; // 正确，作用域不同

Color c = Color::Red;
// int value = c; // 错误！不能隐式转换
int value = static_cast<int>(c); // 需要显式转换
```

#### 类型别名 (using) (C++11)
比 `typedef` 更清晰、更强大的类型别名语法，尤其适用于模板。
```cpp
// 旧写法 - typedef
typedef std::vector<std::map<std::string, int>> ComplexType;
typedef void (*FuncPtr)(int, double);

// 新写法 - using (更清晰)
using ComplexType = std::vector<std::map<std::string, int>>;
using FuncPtr = void (*)(int, double);

// using 可用于模板别名，typedef 不行
template <typename T>
using MyAllocatorVector = std::vector<T, MyCustomAllocator<T>>;

MyAllocatorVector<int> customVec; // std::vector<int, MyCustomAllocator<int>>
```

#### `constexpr` (C++11/14/17)
允许在编译期计算表达式和函数，将计算从运行时转移到编译时。
```cpp
// 旧写法 - 运行时计算
int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}
int array[factorial(5)]; // 错误！大小必须是编译期常量

// 新写法 - 编译期计算 (C++11 constexpr 函数限制较多，C++14 放松了限制)
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}
int array[factorial(5)]; // 正确！120 在编译期就已计算好

// if constexpr (C++17) - 编译期条件判断，简化模板元编程
template <typename T>
auto get_value(T t) {
    if constexpr (std::is_pointer_v<T>) {
        return *t; // 只有当 T 是指针时才编译这部分
    } else {
        return t;  // 只有当 T 不是指针时才编译这部分
    }
}
```

#### `std::optional` (C++17)
明确表示一个"可能不存在"的值，比使用特殊值（如 -1, nullptr）或布尔标志更安全。
```cpp
#include <optional>

// 旧写法 - 容易出错
int findIndex(const std::vector<int>& vec, int value) {
    // 返回 -1 表示未找到，但 -1 本身也是一个有效的索引！
    for (size_t i = 0; i < vec.size(); ++i) {
        if (vec[i] == value) return i;
    }
    return -1; // 歧义！
}

// 新写法 - 语义明确
std::optional<size_t> safeFindIndex(const std::vector<int>& vec, int value) {
    for (size_t i = 0; i < vec.size(); ++i) {
        if (vec[i] == value) return i;
    }
    return std::nullopt; // 明确表示"没有值"
}

// 使用
auto result = safeFindIndex(myVec, 42);
if (result.has_value()) { // 或者 if (result)
    std::cout << "Found at index: " << result.value() << std::endl;
} else {
    std::cout << "Not found" << std::endl;
}
// 或者使用 value_or 提供默认值
std::cout << "Index: " << result.value_or(999) << std::endl;
```

#### `std::variant` (C++17) 和 `std::any` (C++17)
类型安全的联合体和不限定类型的容器。
```cpp
#include <variant>
#include <any>

// std::variant - 类型安全的 union
std::variant<int, double, std::string> v;
v = 42; // 当前持有 int
v = 3.14; // 当前持有 double
// v = true; // 错误！bool 不在可选项中

// 访问 variant
std::visit([](auto&& arg) { // 使用 visit 和 lambda 处理所有可能类型
    using T = std::decay_t<decltype(arg)>;
    if constexpr (std::is_same_v<T, int>) {
        std::cout << "int: " << arg << std::endl;
    } else if constexpr (std::is_same_v<T, double>) {
        std::cout << "double: " << arg << std::endl;
    } else if constexpr (std::is_same_v<T, std::string>) {
        std::cout << "string: " << arg << std::endl;
    }
}, v);

// std::any - 可以持有任何类型的单值容器
std::any a = 42;
a = std::string("hello");
a = 3.14;

// 使用前需要检查类型
if (a.type() == typeid(int)) {
    std::cout << "int value: " << std::any_cast<int>(a) << std::endl;
} else if (a.type() == typeid(std::string)) {
    std::cout << "string value: " << std::any_cast<std::string>(a) << std::endl;
}
// 错误转换会抛出 std::bad_any_cast
```

### 总结对比表

| 传统 C++ 写法                | 现代 C++ 优化写法                 | 优点                     |
| :--------------------------- | :-------------------------------- | :----------------------- |
| `typedef long Type;`         | `using Type = long;`              | 更清晰，支持模板别名     |
| `NULL`                       | `nullptr`                         | 类型安全                 |
| `enum { Red, Blue };`        | `enum class Color { Red, Blue };` | 避免污染，强类型         |
| `int size = vec.size();`     | `auto size = vec.size();`         | 避免写冗长类型           |
| 手写循环迭代器               | 基于范围的 for 循环               | 代码简洁，不易出错       |
| `std::pair<int, string>`     | `auto [id, name] = getData();`    | 直接解包，代码清晰       |
| 返回特殊值表示错误           | `std::optional<T>`                | 语义明确，类型安全       |
| `union { int i; double d; }` | `std::variant<int, double>`       | 类型安全，易扩展         |
| `void*` 存储任意类型         | `std::any`                        | 类型安全，运行时类型信息 |

这些现代 C++ 特性共同使得代码更加：
*   **简洁**：减少样板代码。
*   **安全**：减少隐式转换错误、指针误用等问题。
*   **表达力强**：代码更能体现设计意图。
*   **高性能**：`constexpr`、移动语义等特性在保持抽象的同时不牺牲性能。



## Lambda 表达式

一个 Lambda 表达式的基本语法如下：

```cpp
[ 捕获列表 ] ( 参数列表 ) -> 返回类型 { 函数体 }
```

其中，只有 **`[捕获列表]`** 和 **`{函数体}`** 是必需的，其他部分在特定情况下可以省略。

### 捕获列表 (Capture Clause) `[...]`

捕获列表定义了 Lambda 函数体中可以访问的**外部变量**及其访问方式。这是 Lambda 与普通函数最根本的区别。

#### 值捕获 `[=]`
捕获所有外部变量的**副本**。在 Lambda 内部修改这些副本不会影响外部变量。
```cpp
int a = 1, b = 2;
auto lambda = [=] { // 按值捕获所有外部变量 (a, b)
    // a++; // 错误！按值捕获的变量默认是 const 的 (C++11/14)
    return a + b; // 可以使用副本
};
a = 10; // 修改外部变量
std::cout << lambda(); // 输出 3 (1+2)，而不是 12
```

#### 引用捕获 `[&]`
捕获所有外部变量的**引用**。在 Lambda 内部修改这些引用会直接影响外部变量。
```cpp
int a = 1, b = 2;
auto lambda = [&] { // 按引用捕获所有外部变量
    a++; // 修改会影响外部变量
    return a + b;
};
std::cout << lambda(); // 输出 4 (2+2)
std::cout << a;        // 输出 2 (已被修改)
```

#### 混合捕获与显式捕获
你可以显式指定要捕获的变量和方式。
```cpp
int x = 1, y = 2, z = 3;

auto l1 = [x, &y] { ... };     // 按值捕获 x，按引用捕获 y，不捕获 z
auto l2 = [=, &z] { ... };     // 按值捕获所有外部变量，但 z 按引用捕获
auto l3 = [&, x] { ... };      // 按引用捕获所有外部变量，但 x 按值捕获
// auto l4 = [=, x] { ... };   // 错误！x 已经包含在默认按值捕获中
```

#### `mutable` 关键字
允许修改按值捕获的变量（注意：修改的是副本，不影响外部变量）。
```cpp
int counter = 0;
auto lambda = [=]() mutable { // 允许修改按值捕获的变量
    counter++; // 修改的是副本
    return counter;
};
lambda(); // 返回 1
lambda(); // 返回 2
std::cout << counter; // 输出 0 (外部变量未被修改)
```

#### 初始化捕获 (C++14) "移动捕获"
允许在捕获列表中初始化变量，这对于捕获只能移动（不能拷贝）的类型（如 `std::unique_ptr`）非常有用。
```cpp
auto p = std::make_unique<int>(42);
// auto lambda = [p] { ... }; // 错误！unique_ptr 不能拷贝
auto lambda = [p = std::move(p)] { // C++14 初始化捕获，移动 p
    return *p;
};
```

### 参数列表 `(...)`

与普通函数的参数列表类似。如果不需要参数，可以省略。
```cpp
auto l1 = [] { return 42; };           // 无参数
auto l2 = [](int x) { return x * 2; }; // 一个 int 参数
auto l3 = [](auto x, auto y) { return x + y; }; // C++14 泛型 Lambda
```

### 返回类型 `-> type`

可以显式指定 Lambda 的返回类型。如果函数体只有一条 `return` 语句，编译器可以自动推导返回类型，此时可以省略。
```cpp
// 自动推导返回类型为 int
auto l1 = [](int x) { return x * 2; };

// 显式指定返回类型为 double
auto l2 = [](int x) -> double { return x * 2.5; };

// 函数体复杂，需要显式指定返回类型
auto l3 = [](int x) -> int {
    if (x > 0) return x * 2;
    else return -x; // 没有显式返回类型，编译器可能推导失败或报错
};
```

### 函数体 `{ ... }`

包含 Lambda 要执行的代码。

### Lambda 的底层原理

编译器会将 Lambda 表达式转换成一个**匿名类**（也叫**闭包类型**）。这个类重载了 `operator()`，使得该类的对象可以像函数一样被调用。

```cpp
// 你写的 Lambda
auto lambda = [](int x) { return x * 2; };

// 编译器大致生成的代码
class __AnonymousLambdaClass {
public:
    int operator()(int x) const {
        return x * 2;
    }
};
__AnonymousLambdaClass lambda;
```

捕获的变量会成为这个匿名类的**成员变量**：
```cpp
// 你写的 Lambda
int a = 10;
auto lambda = [a](int x) { return x + a; };

// 编译器大致生成的代码
class __AnonymousLambdaClass {
private:
    int a; // 捕获的变量成为成员变量
public:
    __AnonymousLambdaClass(int captured_a) : a(captured_a) {} // 构造函数
    int operator()(int x) const {
        return x + a;
    }
};
__AnonymousLambdaClass lambda(a); // 用 a 初始化
```



## 内存管理



### 内存布局

理解 C++ 程序的内存布局是管理内存的基础。一个典型的进程内存空间分为以下几个区域：

| 区域                | 存储内容                         | 特点                                         |
| :------------------ | :------------------------------- | :------------------------------------------- |
| **栈 (Stack)**      | 局部变量、函数参数、返回地址     | 自动分配和释放，速度快，大小有限             |
| **堆 (Heap)**       | 动态分配的内存 (`new`, `malloc`) | 手动分配和释放，大小大（受系统限制），速度慢 |
| **全局/静态存储区** | 全局变量、静态变量 (`static`)    | 在程序开始时分配，程序结束时释放             |
| **常量存储区**      | 字符串常量和其他常量             | 只读，程序结束时释放                         |
| **代码区**          | 程序的二进制代码                 | 只读                                         |

### 传统/手动内存管理

#### a) `new` 和 `delete`
C++ 的基础操作符，用于在堆上分配和释放内存。
```cpp
// 分配单个对象
int* pInt = new int;        // 分配未初始化
int* pInt2 = new int(42);   // 分配并初始化为 42
MyClass* pObj = new MyClass("arg"); // 调用构造函数

// 分配对象数组
int* pArray = new int[10];          // 分配 10 个未初始化的 int
MyClass* pObjArray = new MyClass[5]; // 调用 5 次默认构造函数

// 释放内存
delete pInt;    // 释放单个对象，调用析构函数
delete pInt2;
delete pObj;

delete[] pArray;    // 释放数组，必须使用 delete[]
delete[] pObjArray; // 调用 5 次析构函数
```

#### b) 常见问题与陷阱
1.  **内存泄漏 (Memory Leak)**：分配后忘记释放。
    ```cpp
    void leakyFunction() {
        int* p = new int[100];
        // ... 使用 p
        // 忘记 delete[] p; 内存泄漏！
    }
    ```

2.  **悬空指针 (Dangling Pointer)**：指针指向的内存已被释放。
    ```cpp
    int* p = new int(10);
    delete p;   // 内存被释放
    *p = 20;    // 错误！未定义行为，p 现在是悬空指针
    ```

3.  **重复释放 (Double Free)**：对同一块内存释放多次。
    ```cpp
    int* p = new int(10);
    delete p;
    delete p; // 错误！未定义行为
    ```

4.  **不匹配的 new/delete**：使用 `new[]` 分配但用 `delete` 释放，或反之。
    ```cpp
    int* p = new int[10];
    delete p;   // 错误！应该是 delete[] p;
    ```

### 现代/自动内存管理（智能指针）

为了解决手动管理的问题，C++11 引入了**智能指针**（在 `<memory>` 头文件中）。它们通过 **RAII** (Resource Acquisition Is Initialization)  idiom 来自动管理资源生命周期。

#### a) `std::unique_ptr`
**独占所有权**的智能指针。同一时间只能有一个 `unique_ptr` 指向一个对象。当 `unique_ptr` 被销毁时，它指向的对象也会被自动销毁。

```cpp
#include <memory>

void example() {
    // 创建 unique_ptr
    std::unique_ptr<int> p1(new int(42)); // 方式 1
    auto p2 = std::make_unique<int>(42);  // 方式 2 (C++14)，更推荐，更安全高效

    std::unique_ptr<MyClass> p3 = std::make_unique<MyClass>("arg");

    // 访问对象
    *p1 = 100;
    std::cout << *p2 << std::endl;
    p3->doSomething();

    // 所有权转移 (无法复制)
    std::unique_ptr<int> p4 = std::move(p1); // p1 现在为 nullptr
    // std::unique_ptr<int> p5 = p4; // 错误！不能拷贝

    // 释放所有权（返回原始指针并置空）
    int* rawPtr = p2.release();
    // 现在必须手动管理 rawPtr: delete rawPtr;

    // 重置指针（释放当前对象，可选地指向新对象）
    p4.reset();           // 释放 p4 指向的对象，p4 = nullptr
    p4.reset(new int(99)); // 释放旧对象，指向新分配的 int(99)

} // p2, p3, p4 离开作用域，它们指向的对象被自动删除
// 注意：p1 是空的，p2 的所有权已被 release()
```

#### b) `std::shared_ptr`
**共享所有权**的智能指针。多个 `shared_ptr` 可以指向同一个对象，通过**引用计数**机制来跟踪有多少个 `shared_ptr` 指向该对象。当最后一个 `shared_ptr` 被销毁时，对象才会被删除。

```cpp
#include <memory>

void example() {
    // 创建 shared_ptr
    auto p1 = std::make_shared<int>(42); // 推荐方式
    std::shared_ptr<int> p2(new int(100)); // 方式 2

    std::shared_ptr<MyClass> p3 = std::make_shared<MyClass>();

    // 拷贝构造，引用计数增加
    std::shared_ptr<int> p4 = p1; // p1 和 p4 共享所有权，引用计数=2
    auto p5 = p1;                 // 引用计数=3

    // 获取引用计数
    std::cout << "Use count: " << p1.use_count() << std::endl; // 输出 3

    // 赋值操作
    p2 = p1; // p2 不再指向 100（引用计数降为0，对象被删除），现在指向 42，引用计数=4

    // 重置
    p4.reset(); // p4 置空，引用计数减 1 (变为 3)
    p5.reset(new int(200)); // p5 指向新对象，原共享对象的引用计数减 1 (变为 2)

} // p1, p2, p3, p5 离开作用域，它们各自指向的对象引用计数降为 0 时被删除
```

**循环引用问题**：
`shared_ptr` 可能导致循环引用，从而无法释放内存。
```cpp
struct Node {
    std::shared_ptr<Node> next;
    // std::shared_ptr<Node> prev; // 如果用 shared_ptr，会导致循环引用
    std::weak_ptr<Node> prev;      // 解决方案：使用 weak_ptr 打破循环
    ~Node() { std::cout << "Node destroyed\n"; }
};

void circularReference() {
    auto node1 = std::make_shared<Node>();
    auto node2 = std::make_shared<Node>();
    node1->next = node2; // node2 引用计数 = 2
    node2->prev = node1; // node1 引用计数 = 2? 如果是 shared_ptr 则循环引用！
    // 函数结束，引用计数都减 1，但仍为 1，内存泄漏！
}
// 使用 weak_ptr 时，node1 和 node2 的引用计数保持为 1，函数结束时可以正确释放。
```

#### c) `std::weak_ptr`
与 `shared_ptr` 配合使用，**不增加引用计数**。它用于观察 `shared_ptr` 管理的对象，但不会阻止其被销毁。主要用于打破 `shared_ptr` 的循环引用。

```cpp
void weakPtrExample() {
    auto shared = std::make_shared<int>(42);
    std::weak_ptr<int> weak = shared; // 创建 weak_ptr，引用计数仍为 1

    std::cout << "Use count: " << shared.use_count() << std::endl; // 输出 1

    // 访问 weak_ptr 指向的对象
    if (auto locked = weak.lock()) { // 尝试获取一个 shared_ptr
        std::cout << "Object is alive: " << *locked << std::endl;
    } else {
        std::cout << "Object has been destroyed" << std::endl;
    }

    shared.reset(); // 释放对象，引用计数变为 0

    if (auto locked = weak.lock()) { // 尝试获取失败
        // 不会进入这里
    } else {
        std::cout << "Object has been destroyed" << std::endl; // 输出这里
    }
    // weak.expired() 可检查对象是否已被销毁
}
```

#### d) `std::auto_ptr` (已废弃)
C++98 的智能指针，有所有权转移的语义问题。**在 C++11 中已废弃，在 C++17 中移除**。绝对不要在新代码中使用。

### 内存管理最佳实践

1.  **优先使用栈内存**：对于生命周期局限于某个作用域的对象，直接在栈上创建。它速度快且自动管理。
    ```cpp
    void goodPractice() {
        std::vector<int> localVec; // 在栈上，自动管理
        MyClass localObj;          // 在栈上，自动管理
        // ... 使用它们
    } // 自动调用析构函数，内存被回收
    ```

2.  **优先使用智能指针**：如果必须使用堆内存，**优先使用 `std::unique_ptr`**。只有在需要共享所有权时才使用 `std::shared_ptr`。
    ```cpp
    void goodDynamicMemory() {
        auto ptr = std::make_unique<MyClass>(); // 安全！
        // 如果需要共享：
        auto sharedPtr = std::make_shared<MyClass>();
        anotherFunction(sharedPtr); // 安全地共享所有权
    } // 内存自动释放
    ```

3.  **使用 `std::make_unique` 和 `std::make_shared`**：它们更安全（避免裸 `new`）、更高效（`make_shared` 可能将引用计数和对象放在同一块内存）。
    ```cpp
    // 好
    auto p1 = std::make_unique<int>(42);
    auto p2 = std::make_shared<MyClass>(arg1, arg2);
    
    // 不如上面好
    std::unique_ptr<int> p3(new int(42));
    std::shared_ptr<MyClass> p4(new MyClass(arg1, arg2));
    ```

4.  **避免裸 `new` 和 `delete`**：在现代 C++ 业务代码中，你几乎不需要直接使用它们。将它们封装在资源管理类（如智能指针）内部。

5.  **注意对象所有权和生命周期**：明确谁拥有一个对象、谁只是使用它。使用 `unique_ptr` 表示独占所有权，`shared_ptr` 表示共享所有权，`weak_ptr` 或裸指针表示非拥有性引用/观察。

6.  **使用容器管理对象集合**：`std::vector`, `std::map` 等容器会自动管理其元素的内存。
    ```cpp
    std::vector<std::unique_ptr<MyClass>> objectPool;
    objectPool.push_back(std::make_unique<MyClass>());
    // vector 被销毁时，所有 unique_ptr 也会被销毁，从而释放所有 MyClass 对象
    ```

### 总结对比表

| 方法                  | 特点                   | 适用场景                         | 注意事项                 |
| :-------------------- | :--------------------- | :------------------------------- | :----------------------- |
| **栈对象**            | 自动管理，速度快       | 生命周期局限于作用域的对象       | 大小有限                 |
| **`new`/`delete`**    | 完全手动控制           | 需要极致的控制或与 C 接口交互    | 极易出错，易泄漏         |
| **`std::unique_ptr`** | 独占所有权，轻量       | **大多数动态分配场景的首选**     | 不能拷贝，只能移动       |
| **`std::shared_ptr`** | 共享所有权，引用计数   | 需要多个所有者共享同一对象       | 开销稍大，注意循环引用   |
| **`std::weak_ptr`**   | 不拥有对象，观察者     | 打破 `shared_ptr` 循环引用；缓存 | 使用前需用 `lock()` 检查 |
| **`std::make_xxx`**   | 创建智能指针的工厂函数 | **创建智能指针时的首选方式**     | 更安全，更高效           |

**核心原则：依靠 RAII 和智能指针，让析构函数负责资源释放，从而避免手动管理带来的错误。**



## 线程

现代 C++（C++11 起）在标准库 `<thread>` 中提供了强大的线程支持，使得编写跨平台的多线程程序变得更加简单和安全。

### 创建线程

#### 基本线程创建
使用 `std::thread` 类来创建和管理线程。构造函数接受一个**可调用对象**（函数、函数指针、Lambda、函数对象）和其参数。

```cpp
#include <iostream>
#include <thread>

// 1. 普通函数
void helloFunction() {
    std::cout << "Hello from function! Thread ID: " 
              << std::this_thread::get_id() << std::endl;
}

// 2. 函数对象（仿函数）
class HelloFunctor {
public:
    void operator()() const {
        std::cout << "Hello from functor! Thread ID: " 
                  << std::this_thread::get_id() << std::endl;
    }
};

// 3. 带参数的函数
void printMessage(const std::string& message, int count) {
    for (int i = 0; i < count; ++i) {
        std::cout << message << " (" << i + 1 << "/" << count << ")" << std::endl;
    }
}

int main() {
    std::cout << "Main thread ID: " << std::this_thread::get_id() << std::endl;

    // 方式1: 使用函数
    std::thread t1(helloFunction);

    // 方式2: 使用函数对象
    HelloFunctor functor;
    std::thread t2(functor);
    // 或者直接: std::thread t2(HelloFunctor());

    // 方式3: 使用 Lambda 表达式 (最常用)
    std::thread t3([] {
        std::cout << "Hello from lambda! Thread ID: " 
                  << std::this_thread::get_id() << std::endl;
    });

    // 方式4: 带参数的函数
    std::thread t4(printMessage, "Hello Thread", 3);
    
    // 等待所有线程完成
    t1.join();
    t2.join();
    t3.join();
    t4.join();

    std::cout << "All threads completed!" << std::endl;
    return 0;
}
```

#### 线程的 join() 和 detach()
创建线程后，你必须决定如何管理它的生命周期：

*   **`join()`**：阻塞当前线程，直到被调用的线程执行完毕。
*   **`detach()`**：将线程与 `std::thread` 对象分离，允许线程**独立地**在后台运行（守护线程）。分离后无法再与之交互。

```cpp
void backgroundTask() {
    std::this_thread::sleep_for(std::chrono::seconds(2));
    std::cout << "Background task done." << std::endl;
}

int main() {
    std::thread t(backgroundTask);
    
    // 选择一种：
    // t.join();   // 主线程等待 t 完成
    t.detach(); // t 在后台独立运行
    
    if (t.joinable()) { // 检查线程是否可 join
        // t.join(); // 如果已 detach，则 joinable() 为 false
    }
    
    // 主线程继续执行...
    std::this_thread::sleep_for(std::chrono::seconds(3)); // 确保后台线程有足够时间完成
    return 0;
}
// 注意：如果既不 join 也不 detach，std::thread 的析构函数会调用 std::terminate() 终止程序！
```

### 数据竞争与互斥锁 (Mutex)

当多个线程访问**共享数据**时，可能会发生**数据竞争**，导致未定义行为。需要使用**同步原语**来保护共享资源。

#### `std::mutex` (互斥锁)
最基本的锁，用于保护临界区。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex g_mutex; // 全局互斥锁
int sharedCounter = 0;

void incrementCounter(int numIncrements) {
    for (int i = 0; i < numIncrements; ++i) {
        g_mutex.lock();   // 进入临界区前加锁
        ++sharedCounter;  // 临界区代码
        g_mutex.unlock(); // 离开临界区后解锁
    }
}

int main() {
    std::thread t1(incrementCounter, 100000);
    std::thread t2(incrementCounter, 100000);
    
    t1.join();
    t2.join();
    
    std::cout << "Final counter value: " << sharedCounter << std::endl; // 应该是 200000
    return 0;
}
```

#### RAII 方式管理锁：`std::lock_guard` 和 `std::unique_lock`
手动管理 `lock()` 和 `unlock()` 很容易出错（例如忘记解锁）。推荐使用 **RAII** 风格的锁管理器。

*   **`std::lock_guard`**：简单高效，构造时加锁，析构时自动解锁。
    ```cpp
    void safeIncrement(int numIncrements) {
        for (int i = 0; i < numIncrements; ++i) {
            std::lock_guard<std::mutex> lock(g_mutex); // 构造函数中 lock()
            ++sharedCounter;
        } // lock 析构时自动 unlock()
    }
    ```

*   **`std::unique_lock`**：比 `lock_guard` 更灵活，但开销稍大。可以延迟加锁、手动解锁、转移所有权。
    ```cpp
    void flexibleIncrement(int numIncrements) {
        std::unique_lock<std::mutex> ulock(g_mutex, std::defer_lock); // 延迟加锁
        // ... 做一些不需要锁的操作 ...
        ulock.lock(); // 现在手动加锁
        ++sharedCounter;
        ulock.unlock(); // 可以手动提前解锁
        // ... 再做些不需要锁的操作 ...
        // 如果 ulock 仍拥有锁，析构时会自动解锁
    }
    ```

### 线程间通信

#### a) 条件变量 (`std::condition_variable`)
允许线程等待某个条件成立，常用于生产者-消费者模式。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <queue>

std::mutex mtx;
std::condition_variable cv;
std::queue<int> dataQueue;
bool finished = false;

// 生产者线程
void producer() {
    for (int i = 0; i < 5; ++i) {
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
        {
            std::lock_guard<std::mutex> lock(mtx);
            dataQueue.push(i);
            std::cout << "Produced: " << i << std::endl;
        }
        cv.notify_one(); // 通知一个等待的消费者
    }
    {
        std::lock_guard<std::mutex> lock(mtx);
        finished = true;
    }
    cv.notify_all(); // 通知所有消费者
}

// 消费者线程
void consumer() {
    while (true) {
        std::unique_lock<std::mutex> lock(mtx);
        // 等待条件：队列非空或生产结束
        cv.wait(lock, [] { return !dataQueue.empty() || finished; });
        
        if (finished && dataQueue.empty()) {
            break; // 生产结束且队列空，退出
        }
        
        while (!dataQueue.empty()) {
            int data = dataQueue.front();
            dataQueue.pop();
            lock.unlock(); // 处理数据时不需要锁，提前释放以提高并发性
            std::cout << "Consumed: " << data << " (Thread: " 
                      << std::this_thread::get_id() << ")" << std::endl;
            std::this_thread::sleep_for(std::chrono::milliseconds(50));
            lock.lock(); // 准备下一次循环前重新加锁
        }
    }
}

int main() {
    std::thread prod(producer);
    std::thread cons1(consumer);
    std::thread cons2(consumer);
    
    prod.join();
    cons1.join();
    cons2.join();
    
    return 0;
}
```

#### b) 原子操作 (`std::atomic`)
对于简单的计数器或标志位，使用原子操作无需加锁，性能更高。

```cpp
#include <atomic>

std::atomic<int> atomicCounter(0); // 原子整数

void atomicIncrement(int numIncrements) {
    for (int i = 0; i < numIncrements; ++i) {
        ++atomicCounter; // 原子操作，线程安全
        // atomicCounter.fetch_add(1, std::memory_order_relaxed); // 等效，但指定内存序
    }
}

std::atomic<bool> dataReady(false); // 原子布尔标志，常用于简单的线程间信号
```

### 异步操作 (`std::async` 和 `std::future`)

更高层次的抽象，用于启动异步任务并获取结果。

```cpp
#include <iostream>
#include <future>
#include <chrono>

// 一个耗时的计算函数
int longCalculation(int x) {
    std::this_thread::sleep_for(std::chrono::seconds(2));
    return x * x;
}

int main() {
    // 使用 std::async 启动异步任务
    // std::launch::async 保证在新线程中执行
    // std::launch::deferred 延迟执行（直到调用 get() 时才在当前线程执行）
    std::future<int> futureResult = std::async(std::launch::async, longCalculation, 12);
    
    std::cout << "Doing other work while waiting..." << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(1));
    
    // 获取结果（如果结果未就绪，会阻塞等待）
    int result = futureResult.get();
    std::cout << "The result is: " << result << std::endl; // 输出 144
    
    // 可以检查 future 的状态
    std::future_status status;
    do {
        status = futureResult.wait_for(std::chrono::milliseconds(100));
        if (status == std::future_status::timeout) {
            std::cout << "Still waiting..." << std::endl;
        }
    } while (status != std::future_status::ready);
    
    return 0;
}
```

### 线程安全的最佳实践

1.  **优先使用高级抽象**：如 `std::async` 和 `std::future`，而不是直接使用 `std::thread`。
2.  **使用 RAII 锁**：总是优先使用 `std::lock_guard` 或 `std::unique_lock`，避免手动 `lock()`/`unlock()`。
3.  **缩小临界区**：只锁保护真正共享的数据，锁的范围内代码越少越好。
4.  **避免死锁**：按固定顺序获取多个锁，或使用 `std::lock()` 一次性锁住多个互斥量。
    ```cpp
    std::mutex mtx1, mtx2;
    // 错误方式：可能死锁
    // void bad() { std::lock_guard<std::mutex> lk1(mtx1); std::lock_guard<std::mutex> lk2(mtx2); }
    // void alsoBad() { std::lock_guard<std::mutex> lk2(mtx2); std::lock_guard<std::mutex> lk1(mtx1); }
    
    // 正确方式：总是按相同顺序加锁
    void good() {
        std::lock_guard<std::mutex> lk1(mtx1);
        std::lock_guard<std::mutex> lk2(mtx2);
    }
    // 或者使用 std::lock 一次性锁住多个（避免死锁算法）
    void better() {
        std::unique_lock<std::mutex> lk1(mtx1, std::defer_lock);
        std::unique_lock<std::mutex> lk2(mtx2, std::defer_lock);
        std::lock(lk1, lk2); // 同时锁住两个，不会死锁
    }
    ```
5.  **使用线程局部存储**：对于不需要共享的数据，使用 `thread_local` 关键字。
    ```cpp
    thread_local int threadSpecificValue = 0; // 每个线程有自己的副本
    ```
6.  **谨慎使用 `volatile`**：`volatile` 用于防止编译器优化（如内存映射硬件寄存器），**它不能保证线程安全**。线程安全需要使用原子操作或互斥锁。

C++ 的多线程支持非常强大，但也需要谨慎使用。理解数据竞争、死锁等概念，并正确使用标准库提供的同步工具，是编写可靠并发程序的关键。





