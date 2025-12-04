# Java

文章参考：[JavaGuide](https://javaguide.cn/)，[hsp](https://www.bilibili.com/video/BV1fh411y7R8/?spm_id_from=333.337.search-card.all.click&vd_source=53ce3c6946a5aed7c975753cd24f0e3f)，

[TOC]





**起源与发展**

1. **诞生**：Java由Sun Microsystems（现已被Oracle收购）的詹姆斯·高斯林（James Gosling）等人开发。项目始于1991年，最初被称为“Green Project”，目标是为智能家电（如机顶盒）创建一种通用的编程语言。
2. **命名**：最初语言名叫“Oak”（橡树），但由于商标冲突，后来改名为“Java”，灵感据说来自开发团队常喝的爪哇咖啡（Java Coffee）。
3. **首次发布**：Java 1.0于1995年正式发布，其口号“Write Once, Run Anywhere”（WORA，一次编写，到处运行）强调了其跨平台特性。

**核心特性**

- **平台无关性**：Java通过Java虚拟机（JVM）实现代码的可移植性。程序被编译成字节码（bytecode），可以在任何安装了JVM的设备上运行。
- **面向对象**：Java完全基于面向对象编程（OOP）原则，强调封装、继承和多态。
- **健壮性与安全性**：Java内置了内存管理（垃圾回收机制）和异常处理，避免了许多常见的编程错误，同时在网络环境中提供了安全保障。
- **多线程支持**：Java从一开始就支持多线程编程，适合开发高并发应用。

**演变与影响**

- **版本迭代**：Java不断更新，从Java 1.0发展到如今的Java 21（截至2025年3月，最新版本可能更高）。重要的版本包括Java 5（引入泛型）、Java 8（引入Lambda表达式和流API）等。
- **应用领域**：Java被广泛用于企业级应用（如Java EE）、安卓开发（Android SDK主要基于Java）、Web开发（如Spring框架）、大数据处理（如Hadoop）等领域。
- **社区与生态**：Java拥有庞大的开发者社区和丰富的库支持（如Apache Commons、Guava），其生态系统非常成熟。

**Java 源程序与编译型运行区别**

![img](images/ZSSDMld.png)



[TOC]

# 基本语法



## 基本数据类型

Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

![image-20250312201318955](images/image-20250312201318955.png)

| 数据类型         | 关键字    | 大小 (字节) | 默认值     | 取值范围                        | 包装类      | 示例                   |
| :--------------- | :-------- | :---------- | :--------- | :------------------------------ | :---------- | :--------------------- |
| **字节型**       | `byte`    | 1           | `0`        | -128 ~ 127                      | `Byte`      | `byte b = 100;`        |
| **短整型**       | `short`   | 2           | `0`        | -32,768 ~ 32,767                | `Short`     | `short s = 5000;`      |
| **整型**         | `int`     | 4           | `0`        | -2³¹ ~ 2³¹-1                    | `Integer`   | `int i = 100000;`      |
| **长整型**       | `long`    | 8           | `0L`       | -2⁶³ ~ 2⁶³-1                    | `Long`      | `long l = 100000L;`    |
| **单精度浮点型** | `float`   | 4           | `0.0f`     | 约 ±3.4e+38F                    | `Float`     | `float f = 3.14f;`     |
| **双精度浮点型** | `double`  | 8           | `0.0d`     | 约 ±1.7e+308                    | `Double`    | `double d = 3.14159;`  |
| **字符型**       | `char`    | 2           | `'\u0000'` | '\u0000' ~ '\uffff' (0 ~ 65535) | `Character` | `char c = 'A';`        |
| **布尔型**       | `boolean` | ~1 bit¹     | `false`    | `true` 或 `false`               | `Boolean`   | `boolean flag = true;` |

### byte

- byte 数据类型是8位、有符号的，以二进制补码表示的整数；
- 最小值是 **-128（-2^7）**；
- 最大值是 **127（2^7-1）**；
- 默认值是 **0**；
- byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
- 例子：byte a = 100，byte b = -50。

### short

- short 数据类型是 16 位、有符号的以二进制补码表示的整数
- 最小值是 **-32768（-2^15）**；
- 最大值是 **32767（2^15 - 1）**；
- Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
- 默认值是 **0**；
- 例子：short s = 1000，short r = -20000。

### int

- int 数据类型是32位、有符号的以二进制补码表示的整数；
- 最小值是 **-2,147,483,648（-2^31）**；
- 最大值是 **2,147,483,647（2^31 - 1）**；
- 一般地整型变量默认为 int 类型；
- 默认值是 **0** ；
- 例子：int a = 100000, int b = -200000。

### long

- long 数据类型是 64 位、有符号的以二进制补码表示的整数；
- 最小值是 **-9,223,372,036,854,775,808（-2^63）**；
- 最大值是 **9,223,372,036,854,775,807（2^63 -1）**；
- 这种类型主要使用在需要比较大整数的系统上；
- 默认值是 **0L**；
- 例子： **long a = 100000L**，**long b = -200000L**。
  "L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不容易分辩。所以最好大写。
- **必须加l或L**

### float

- float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
- float 在储存大型浮点数组的时候可节省内存空间；
- 默认值是 **0.0f**；
- 浮点数不能用来表示精确的值，如货币；
- 例子：float f1 = 234.5f。
- **必须加f或F**

### double

- double 数据类型是双精度、64 位、符合 IEEE 754 标准的浮点数；

- 浮点数的默认类型为 double 类型；

- double类型同样不能表示精确的值，如货币；

- 默认值是 **0.0d**；

- 例子：

  ```
  double   d1  = 7D ;
  double   d2  = 7.; 
  double   d3  =  8.0; 
  double   d4  =  8.D; 
  double   d5  =  12.9867; 
  ```

  7 是一个 int 字面量，而 7D，7. 和 8.0 是 double 字面量。

### boolean

- boolean数据类型表示一位的信息；
- 只有两个取值：true 和 false；
- 这种类型只作为一种标志来记录 true/false 情况；
- 默认值是 **false**；
- 例子：boolean one = true。

### char

- char 类型是一个单一的 16 位 Unicode 字符；
- 最小值是 **\u0000**（十进制等效值为 0）；
- 最大值是 **\uffff**（即为 65535）；
- char 数据类型可以储存任何字符；
- 例子：char letter = 'A';。



### 类型转换

Java 中的类型转换分为两种：自动类型转换（隐式转换）和强制类型转换（显式转换）。

#### 自动转换

自动类型转换是指当**小范围(低精度)**数据类型向**大范围(高精度)**数据类型转换时，Java 会自动完成转换，不需要程序员显式地指定。

转换规则如下：

```java
//          1. char -> int -> long -> float -> double
// 2. byte -> short -> int -> long -> float -> double
double d = 'd';
             
// 3. 多种类型混合运算时，系统自动全部转换为其中最高精度的类型
int i =  1;
float sum = i + 1.2; // 错误
float sum = i + 1.2f;

// 4. char, byte, short 三者可以计算，在计算时自动提升为int
byte b = 2;
short s = 1;
int sum = b + s;

byte b1 = 2;
byte b2 = 1;
byte sum = b1 + b2; // 错误
int sum = b1 + b2;
```

#### 强制转换

强制类型转换是指当**大范围(高精度)**数据类型向**小范围(低精度)**数据类型转换时，需要程序员显式地指定转换，可能会造成数据精度丢失。

```java
// 1. 精度损失
int i = (int) 1.9;

// 2. 数据溢出
int i = 2000;
byte b = (byte) i;

// 3. 强转只对最近的操作数有效
int i = (int) 10 * 3.5 + 9.3; // 错误
int i = (int) (10 * 3.5 + 9.3); // 错误

// 4. char可以保存int常量值, 不能保存int变量值(需要强转)
char c = 100;

int i = 100;
char c = i; // 错误
char c = (char) i;
```

#### 基本数据与String转换

##### 基本数据 -> String

```java
// 1. 使用 String.valueOf() 方法
int i = 123;
String s = String.valueOf(i);  // "123"

// 2. 使用基本数据类型包装类的 toString() 方法
int i = 123;
String s = Integer.toString(i);  // "123"

// 3. 使用字符串拼接
int i = 123;
double d = 45.67;
boolean b = true;
String sum = i + " " + d + " " + b;  // "123" "45.67" "true"

// 4. 使用 String.format() 方法
int i = 123;
String s = String.format("%d", i);  // "123"
```



##### String -> 基本数据

```java
// 1. 使用基本数据类型对应包装类的 parse 方法
String s = "123";

byte b = Byte.parseByte(s); // 123
int i = Integer.parseInt(s); // 123
double d = Double.parseDouble(s); // 123.0
boolean b = Boolean.parseBoolean("true"); // true
char c = s.charAt(0)
```



## 变量

### 命名规则

- **使用有意义的名字：** 变量名应该具有清晰的含义，能够准确地反映变量的用途。避免使用单个字符或无意义的缩写。
- **驼峰命名法（Camel Case）：** 在变量名中使用驼峰命名法，即将每个单词的首字母大写，除了第一个单词外，其余单词的首字母都采用大写形式。例如：`myVariableName`。
- **避免关键字：** 不要使用 Java 关键字（例如，class、int、boolean等）作为变量名。
- **区分大小写：** Java 是大小写敏感的，因此变量名中的大小写字母被视为不同的符号。例如，`myVariable` 和 `myvariable` 是两个不同的变量。
- **不以数字开头：** 变量名不能以数字开头，但可以包含数字。
- **遵循命名约定：** 对于不同类型的变量（局部变量、实例变量、静态变量等），可以采用不同的命名约定，例如使用前缀或后缀来区分。

### 格式说明

- type -- 数据类型。
- identifier -- 是变量名，可以使用逗号 **,** 隔开来声明多个同类型变量。

以下列出了一些变量的声明实例。注意有些包含了初始化过程。

```java
int a, b, c;         // 声明三个int型整数：a、 b、c
int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
byte z = 22;         // 声明并初始化 z
String s = "runoob";  // 声明并初始化字符串 s
double pi = 3.14159; // 声明了双精度浮点型变量 pi
char x = 'x';        // 声明变量 x 的值是字符 'x'。
```

### 变量类型

- **局部变量（Local Variables）：**局部变量是在方法、构造函数或块内部声明的变量，它们在声明的方法、构造函数或块执行结束后被销毁，局部变量在声明时需要初始化，否则会导致编译错误。

    ```java
    public void exampleMethod() {
        int localVar = 10; // 局部变量
        // ...
    }
    ```

- **实例变量（Instance Variables）：**实例变量是在类中声明，但在方法、构造函数或块之外，它们属于类的实例，每个类的实例都有自己的副本，如果不明确初始化，实例变量会被赋予默认值（数值类型为0，boolean类型为false，对象引用类型为null）。

    ```java
    public class ExampleClass {
        int instanceVar; // 实例变量
    }
    ```

- **静态变量或类变量（Class Variables）：**类变量是在类中用 static 关键字声明的变量，它们属于类而不是实例，所有该类的实例共享同一个类变量的值，类变量在类加载时被初始化，而且只初始化一次。

    ```java
    public class ExampleClass {
        static int classVar; // 类变量
    }
    ```

- **参数变量（Parameters）：**参数是方法或构造函数声明中的变量，用于接收调用该方法或构造函数时传递的值，参数变量的作用域只限于方法内部。

    ```java
    public void exampleMethod(int parameterVar) {
        // 参数变量
        // ...
    }
    ```





## 运算符

### 算术运算符

算术运算符用在数学表达式中，它们的作用和在数学中的作用一样。下表列出了所有的算术运算符。

表格中的实例假设整数变量A的值为10，变量B的值为20：

| 操作符 | 描述                              | 例子                               |
| :----- | :-------------------------------- | :--------------------------------- |
| +      | 加法 - 相加运算符两侧的值         | A + B 等于 30                      |
| -      | 减法 - 左操作数减去右操作数       | A – B 等于 -10                     |
| *      | 乘法 - 相乘操作符两侧的值         | A * B等于200                       |
| /      | 除法 - 左操作数除以右操作数       | B / A等于2                         |
| ％     | 取余 - 左操作数除以右操作数的余数 | B%A等于0                           |
| ++     | 自增: 操作数的值增加1             | B++ 或 ++B 等于 21（区别详见下文） |
| --     | 自减: 操作数的值减少1             | B-- 或 --B 等于 19（区别详见下文） |

### 关系运算符

下表为Java支持的关系运算符

表格中的实例整数变量A的值为10，变量B的值为20：

| 运算符 | 描述                                                         | 例子             |
| :----- | :----------------------------------------------------------- | :--------------- |
| ==     | 检查如果两个操作数的值是否相等，如果相等则条件为真。**用==比较对象是比较地址是否相同，不是比较内容。** | （A == B）为假。 |
| !=     | 检查如果两个操作数的值是否相等，如果值不相等则条件为真。     | (A != B) 为真。  |
| >      | 检查左操作数的值是否大于右操作数的值，如果是那么条件为真。   | （A> B）为假。   |
| <      | 检查左操作数的值是否小于右操作数的值，如果是那么条件为真。   | （A <B）为真。   |
| >=     | 检查左操作数的值是否大于或等于右操作数的值，如果是那么条件为真。 | （A> = B）为假。 |
| <=     | 检查左操作数的值是否小于或等于右操作数的值，如果是那么条件为真。 | （A <= B）为真。 |

### 位运算符

Java定义了位运算符，应用于整数类型(int)，长整型(long)，短整型(short)，字符型(char)，和字节型(byte)等类型。

位运算符作用在所有的位上，并且按位运算。假设a = 60，b = 13;它们的二进制格式表示将如下：

```
A = 0011 1100
B = 0000 1101
-----------------
A&B = 0000 1100
A | B = 0011 1101
A ^ B = 0011 0001
~A= 1100 0011
```

下表列出了位运算符的基本运算，假设整数变量 A 的值为 60 和变量 B 的值为 13：

| 操作符 | 描述                                                         | 例子                           |
| :----- | :----------------------------------------------------------- | :----------------------------- |
| ＆     | 如果相对应位都是1，则结果为1，否则为0                        | （A＆B），得到12，即0000 1100  |
| \|     | 如果相对应位都是 0，则结果为 0，否则为 1                     | （A \| B）得到61，即 0011 1101 |
| ^      | 如果相对应位值相同，则结果为0，否则为1                       | （A ^ B）得到49，即 0011 0001  |
| 〜     | 按位取反运算符翻转操作数的每一位，即0变成1，1变成0。         | （〜A）得到-61，即1100 0011    |
| <<     | 按位左移运算符。左操作数按位左移右操作数指定的位数。         | A << 2得到240，即 1111 0000    |
| >>     | 按位右移运算符。左操作数按位右移右操作数指定的位数。         | A >> 2得到15即 1111            |
| >>>    | 按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。 | A>>>2得到15即0000 1111         |

### 逻辑运算符

下表列出了逻辑运算符的基本运算，假设布尔变量A为真，变量B为假

| 操作符 | 描述                                                         | 例子                |
| :----- | :----------------------------------------------------------- | :------------------ |
| &&     | 短路与。第一个条件为false，则不判断第二个。（推荐）          | （A && B）为假。    |
| &      | 逻辑与。                                                     |                     |
| \| \|  | 短路或。第一个条件为true，则不判断第二个。（推荐）           | （A \| \| B）为真。 |
| \|     | 逻辑或。                                                     |                     |
| ！     | 称为逻辑非运算符。用来反转操作数的逻辑状态。如果条件为true，则逻辑非运算符将得到false。 | ！（A && B）为真。  |
| ^      | 异或。                                                       |                     |

### 赋值运算符

下面是Java语言支持的赋值运算符：

| 操作符  | 描述                                                         | 例子                                     |
| :------ | :----------------------------------------------------------- | :--------------------------------------- |
| =       | 简单的赋值运算符，将右操作数的值赋给左侧操作数               | C = A + B将把A + B得到的值赋给C          |
| + =     | 加和赋值操作符，它把左操作数和右操作数相加赋值给左操作数     | C + = A等价于C = C + A                   |
| - =     | 减和赋值操作符，它把左操作数和右操作数相减赋值给左操作数     | C - = A等价于C = C - A                   |
| * =     | 乘和赋值操作符，它把左操作数和右操作数相乘赋值给左操作数     | C * = A等价于C = C * A                   |
| / =     | 除和赋值操作符，它把左操作数和右操作数相除赋值给左操作数     | C / = A，C 与 A 同类型时等价于 C = C / A |
| （％）= | 取模和赋值操作符，它把左操作数和右操作数取模后赋值给左操作数 | C％= A等价于C = C％A                     |
| << =    | 左移位赋值运算符                                             | C << = 2等价于C = C << 2                 |
| >> =    | 右移位赋值运算符                                             | C >> = 2等价于C = C >> 2                 |
| ＆=     | 按位与赋值运算符                                             | C＆= 2等价于C = C＆2                     |
| ^ =     | 按位异或赋值操作符                                           | C ^ = 2等价于C = C ^ 2                   |
| \| =    | 按位或赋值操作符                                             | C \| = 2等价于C = C \| 2                 |

### 条件运算符

条件运算符也被称为三元运算符。该运算符有3个操作数，并且需要判断布尔表达式的值。该运算符的主要是决定哪个值应该赋值给变量。

```java
variable x = (expression) ? value if true : value if false
```

### instanceof 运算符

该运算符用于操作对象实例，检查该对象的**运行类型**是否是一个特定类型（类类型或接口类型）或特定类型的子类型。

instanceof运算符使用格式如下：

```java
( Object reference variable ) instanceof  (class/interface type)
```

下面是一个例子：

```java
String name = "James";
boolean result1 = name instanceof String; // 由于 name 是 String 类型，所以返回真
boolean result2 = name instanceof Object; // String 是 Object 的子类型。
```



## 控制语句

### while & do while

```java
// 循环10次
int i = 0;
while( i < 10 ) {
    i++;
}

// do..while 循环9次
int i = 0;
do{
    i++;
} while( i < 10 )
```

### for 遍历数组

Java5 引入了一种主要用于数组的增强型 for 循环。

Java 增强 for 循环语法格式如下:

```java
for(声明语句 : 表达式)
{
   //代码句子
}
```

**声明语句：**声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。

**表达式：**表达式是要访问的数组名，或者是返回值为数组的方法。

**示例：**

```java
public class Test {
   public static void main(String[] args){
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ){
         System.out.print( x );
         System.out.print(",");
      }
      System.out.print("\n");
      String [] names ={"James", "Larry", "Tom", "Lacy"};
      for( String name : names ) {
         System.out.print( name );
         System.out.print(",");
      }
   }
}
```

### break & continue

```java
// 标签：可以指定从哪个循环break & continue
label1:
	while( i < 10 ) {
        label2:
        while( j < 5 ) {
            if (i == 2) {
                continue label1;
            }
            j++;
        }
        i++;
    }
```



### swicth语句

```java
switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}

// 1. 表达式的值类型必须是：byte, short, int, char, enum, String
// 2. case子句的值只能是常量
// 3. break语句用于跳出switch语句块；如果没有break，程序会顺序执行到结尾
// 4. while里面嵌套switch，break有限跳出switch而不是while
```



## 数组

Java数组是存储**固定大小**的同类型元素的数据结构。数组在Java中是对象，它们提供了一种有效的方式来存储和访问多个**相同类型**的值。

数组中的元素可以是基本类型也可以是引用类型。

### 声明与创建

```java
// 1. 声明
double[] myList;         // 首选的方法
double myList[];         //  效果相同，但不是首选方法，在Java中采用是为了让 C/C++ 程序员能够快速理解java语言。

// 2. 创建
int size = 10;  					// 数组大小
double[] myList = new double[size]; // 定义数组
myList = {1.0, 2.0, 3.0} // 错误：一旦数组已经用 new 创建，就不能再用 {...} 语法重新赋值
myList[0] = 1.0;
myList[1] = 2.0;
myList[2] = 3.0;

double[] myList = {1.0, 2.0, 3.0}
```

数组创建后，没有赋值会有默认值。

```
byte, short, int, long = 0
float, double = 0.0
char = \u0000
boolean = false
String = null
```

### 多维数组

多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素都是一个一维数组，例如：

```java
String[][] str = new String[3][4];
```

### 数组 vs ArrayList

| 特性         | 数组 (`Array`)                                     | `ArrayList`                                    |
| ------------ | -------------------------------------------------- | ---------------------------------------------- |
| **大小**     | 固定大小，声明时确定，一旦创建不能更改             | 动态大小，自动扩展或收缩                       |
| **类型**     | 可以存储基本数据类型（如 `int`, `char`）和对象类型 | 只能存储对象类型（如 `Integer`, `String`）     |
| **线程安全** | 不涉及同步，多个线程访问时需要自己处理             | 不是线程安全的，多个线程操作时需要外部同步     |
| **创建方式** | `int[] arr = new int[5];`                          | `ArrayList<Integer> list = new ArrayList<>();` |
| **遍历方式** | 使用传统 `for` 循环或增强 `for` 循环               | 使用 `for` 循环或增强 `for` 循环               |

### 数组常用操作

1. **获取数组长度**

    ```java
    int length = array.length;
    ```

2. **遍历数组**

    ```java
    // 使用for循环
    for (int i = 0; i < array.length; i++) {
        System.out.println(array[i]);
    }
    
    // 使用增强for循环
    for (int num : array) {
        System.out.println(num);
    }
    ```

3. **数组排序**

    ```java
    Arrays.sort(array);
    ```

4. **数组复制**

    ```java
    int[] copy = Arrays.copyOf(original, newLength);
    
    // ❌：同一个数组
    int[] i1 = {1, 2, 3};
    int[] i2 = i1;
    
    // ✔：开劈新空间存储
    int[] i2 = new int[3];
    for(int i = 0; i < i1.length; i++) {
        i2[i] = i1[i];
    }
    ```



## 异常处理

Java 的异常处理机制用于处理程序运行过程中可能发生的错误，使程序能够更健壮地应对异常情况，而**不会直接崩溃**。

![image-20250327082213358](images/image-20250327082213358.png)

所有的异常类是从 `java.lang.Exception` 类继承的子类。

`Exception` 类是 `Throwable` 类的子类。除了`Exception`类外，`Throwable`还有一个子类`Error` 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

`Error` 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：`IOException` 类和 `RuntimeException` 类。

![Java：详解Java中的异常(Error与Exception)_exception类称为异常类，它表示程序本身可以处理的错误，在开发java ...](https://img-blog.csdnimg.cn/2019101117003396.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI5MjI5NTY3,size_16,color_FFFFFF,t_70)

### 异常的分类

#### 已检查异常（Checked Exception）

- 这些异常在**编译阶段**就会被检查，必须在代码中**显式处理**（使用 `try-catch` 或 `throws`）。
- 例如：
    - `IOException`
    - `SQLException`
    - `FileNotFoundException`

#### 运行时异常（Unchecked Exception）

- 这些异常发生在**运行时**，编译器不会强制要求开发者处理，但可以选择捕获。
- 例如：
    - `NullPointerException`
    - `ArrayIndexOutOfBoundsException`
    - `ArithmeticException`
    - `ClassCastException`
    - `NumberFormatException`

#### 错误（Error）

- 这种类型的异常通常表示**JVM 或系统层面**的问题，无法通过代码处理。
- 例如：
    - `StackOverflowError`
    - `OutOfMemoryError`

------

### 异常处理的方式

Java 提供了 **`try-catch-finally`** 机制来处理异常，以及 **`throws`** 关键字用于声明异常。

#### try-catch 语句

```java
try {
    int result = 10 / 0; // 可能会发生 ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("捕获异常：" + e.getMessage());
}
```

##### 多异常捕获

如果 `try` 代码块可能抛出多种不同类型的异常，可以使用多个 `catch` 语句：

```java
try {
    String str = null;
    System.out.println(str.length()); // NullPointerException
} catch (NullPointerException e) {
    System.out.println("空指针异常：" + e.getMessage());
} catch (Exception e) {
    System.out.println("其他异常：" + e.getMessage());
}
```

也可以使用 **`|`**（管道符）捕获多个异常：

```java
try {
    int num = Integer.parseInt("abc"); // NumberFormatException
} catch (NumberFormatException | NullPointerException e) {
    System.out.println("格式转换异常：" + e.getMessage());
}
```

#### try-catch-finally 语句

`finally` 语句块无论是否发生异常都会执行，通常用于**关闭资源**。

```java
FileReader reader = null;
BufferedReader bufferedReader = null;

try {
    reader = new FileReader("example.txt");
    bufferedReader = new BufferedReader(reader);
    
    // 使用 bufferedReader 进行文件读取
    String line = bufferedReader.readLine();
    // 处理数据...
    
} catch (IOException e) {
    // 处理 IOException 异常
    e.printStackTrace();
} finally {
    // 确保资源被关闭
    if (bufferedReader != null) {
        try {
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### try-with-resources 语句

`try-with-resources` 是 **Java 7** 引入的一种语法，用于简化资源的管理和自动关闭资源。它的核心目的是确保在 `try` 块结束时，无论是否发生异常，资源都能够被正确关闭（例如：文件流、数据库连接等）。

**关键点**

1. **资源声明在 `try` 语句括号内**：资源是在 `try` 语句的圆括号 `()` 内声明的。这些资源必须实现 `AutoCloseable` 接口（包括 `Closeable`）。
2. **自动关闭资源**：当 `try` 块执行完毕后（包括发生异常时），会自动调用这些资源的 `close()` 方法，不需要显式地在 `finally` 块中关闭。
3. **多个资源**：可以在 `try` 语句的括号中声明多个资源，资源之间用分号 `;` 分隔。

```java
try (FileReader reader = new FileReader("example.txt");
     BufferedReader bufferedReader = new BufferedReader(reader)) {
    // 使用 bufferedReader 进行文件读取
    String line = bufferedReader.readLine();
    // 处理数据...
} catch (IOException e) {
    // 处理 IOException 异常
    e.printStackTrace();
}
// 在这里，reader 和 bufferedReader 都会被自动关闭
```

#### throws 关键字

如果一个方法可能抛出异常，可以在方法声明中使用 `throws` 关键字向上抛出：

```java
public void readFile() throws IOException {
    FileReader file = new FileReader("test.txt"); // 可能抛出 FileNotFoundException
}
```

调用者必须显式处理：

```java
try {
    readFile();
} catch (IOException e) {
    System.out.println("文件读取失败：" + e.getMessage());
}
```

#### throw 关键字

`throw` 用于**手动抛出异常**：

```java
public void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("未成年人禁止入内");
    }
}
```

调用时：

```java
try {
    checkAge(16);
} catch (IllegalArgumentException e) {
    System.out.println("异常：" + e.getMessage());
}
```

### 自定义异常

如果 Java 内置异常不满足需求，可以创建自定义异常：

```java
class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}
```

使用：

```java
public void test(int value) throws MyException {
    if (value < 0) {
        throw new MyException("值不能为负数");
    }
}
```

### 异常处理最佳实践

1. **尽量捕获具体异常**，而不是直接 `catch (Exception e)`，这样可以更精确地定位问题。
2. **避免过度捕获**，如果异常无法恢复，应该让它继续传播，而不是强行捕获。
3. **正确使用 `finally` 释放资源**，如关闭数据库连接、文件流等。
4. **日志记录（Logging）**，使用 `Logger` 记录异常信息，而不是简单地 `System.out.println(e)`。

### 总结

| 关键字    | 用途                           |
| --------- | ------------------------------ |
| `try`     | 监控可能发生异常的代码块       |
| `catch`   | 捕获异常并处理                 |
| `finally` | 代码块无论是否发生异常都会执行 |
| `throw`   | 手动抛出异常                   |
| `throws`  | 方法声明抛出异常，由调用者处理 |

Java 的异常机制是保证程序稳定性的关键部分，合理地使用异常处理可以提高代码的健壮性和可维护性。



# 进阶语法



## 源文件声明规则

### 源文件声明规则

在本节的最后部分，我们将学习源文件的声明规则。当在一个源文件中定义多个类，并且还有 import 语句和 package 语句时，要特别注意这些规则。

- 一个源文件中只能有一个 public 类
- 一个源文件可以有多个非 public 类
- 源文件的名称应该和 public 类的类名保持一致。例如：源文件中 public 类的类名是 Employee，那么源文件应该命名为Employee.java。
- 如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。
- 如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。
- import 语句和 package 语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。

类有若干种访问级别，并且类也分不同的类型：抽象类和 final 类等。这些将在访问控制章节介绍。

除了上面提到的几种类型，Java 还有一些特殊的类，如：[内部类](https://www.runoob.com/java/java-inner-class.html)、[匿名类](https://www.runoob.com/java/java-anonymous-class.html)。



## Java包机制

在 Java 中，**包（package）** 是一种组织和管理代码的机制，用于将相关的类和接口分组，避免命名冲突，并提供访问控制。包是 Java 面向对象编程中的重要概念，尤其在大型项目中起到模块化的作用。以下是对 Java 包的详细说明：

### 什么是 Java 包？

包是类的命名空间（namespace），类似于文件系统中的目录。它通过将类、接口和其他资源组织到不同的包中，帮助开发者管理代码结构。

- **命名空间**：防止类名冲突。例如，两个不同的开发者可以定义名为 `Util` 的类，只要它们在不同的包中（如 `com.myapp.Util` 和 `org.lib.Util`），就不会冲突。
- **访问控制**：包与访问修饰符（如 `public`, `protected`, 默认（包级））结合，控制类和成员的可见性。
- **模块化**：将功能相似的类分组，提高代码的可维护性和可读性。

### 包的语法

#### 声明包

在 Java 文件的开头使用 `package` 关键字声明包名：

```java
package com.example.myapp;

public class MyClass {
    // 类的内容
}
```

- 包名通常使用反向域名命名约定（如 `com.company.project`），以确保全局唯一性。
- 包名必须与文件所在的目录结构一致。例如，`com.example.myapp.MyClass` 应位于 `com/example/myapp/` 目录下。

#### 默认包

如果没有显式声明 `package`，类将被放入**默认包（default package）**。但不推荐使用默认包，尤其是在大型项目中。

### 导入包

#### 使用 `import`

要使用其他包中的类，需要通过 `import` 语句引入：

```java
import java.util.ArrayList;  // 导入特定类
import java.util.*;          // 导入整个包（通配符）

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Hello");
        System.out.println(list);
    }
}
```

- `import java.util.*` 会导入 `java.util` 包中的所有公共类，但不会导入子包（如 `java.util.concurrent`）。
- **完全限定名**：也可以不使用 `import`，直接用类的全名，如 `java.util.ArrayList`。

#### 静态导入（Static Import）

从 Java 5 开始，可以导入类的静态成员：

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

public class Test {
    public static void main(String[] args) {
        System.out.println(PI);       // 直接使用 PI
        System.out.println(sqrt(16)); // 直接使用 sqrt
    }
}
```

### Java 中的常见包

Java 标准库（Java API）包含许多内置包，例如：

- **`java.lang`**：核心类（如 `String`, `Math`, `System`），无需显式导入。
- **`java.util`**：实用工具类（如 `ArrayList`, `HashMap`, `Date`, `Scanner`）。
- **`java.io`**：输入输出相关类（如 `File`, `BufferedReader`）。
- **`java.net`**：网络相关类（如 `Socket`, `URL`）。
- **`javax.swing`**：GUI 组件（如 `JFrame`, `JButton`）。

### 包的访问控制

包与 Java 的访问修饰符密切相关：

- **`public`**：类或成员对所有包可见。
- **`protected`**：对同一包内的类或子类可见。**同包可见 + 不同包的子类可见**。
- **默认（包级访问）**：如果不指定修饰符（如 `class MyClass`），类或成员只对同一包内的类可见，同一包内的类的子类不可见。**同包可见**。
- **`private`**：仅类内部可见，与包无关。

```java
package com.example;

class PackagePrivateClass {  // 默认访问权限，仅同一包可见
    void sayHello() {
        System.out.println("Hello from package-private class");
    }
}

public class PublicClass {
    public void sayHello() {
        System.out.println("Hello from public class");
    }
}
```

- `PackagePrivateClass` 只能在 `com.example` 包内访问，而 `PublicClass` 可被任何包访问。

### 包的物理结构

包名对应于文件系统的目录结构。例如：

```
src/
  com/
    example/
      myapp/
        MyClass.java
```

`MyClass.java` 的内容：

```java
package com.example.myapp;

public class MyClass {
    public void doSomething() {
        System.out.println("Doing something");
    }
}
```

编译后，生成的 `.class` 文件也会位于相同的目录结构中：

```
com/example/myapp/MyClass.class
```

#### 编译和运行

- 编译：`javac com/example/myapp/MyClass.java`
- 运行：`java com.example.myapp.MyClass`（需要在包含 `com` 的目录下执行）。

### 包的作用

1. **命名冲突解决**：
    - 不同包中的同名类不会冲突。
2. **代码组织**：
    - 将功能相关的类放在同一包中，如 `com.example.model`（数据模型）、`com.example.util`（工具类）。
3. **访问控制**：
    - 通过包级访问限制某些类的可见性。
4. **模块化开发**：
    - 大型项目中，包可以按功能模块划分（如 MVC 架构中的 `controller`, `service`, `dao`）。

### Java 9+ 的模块化（Module System）

从 Java 9 开始，引入了 **模块系统（Java Platform Module System, JPMS）**，通过 `module-info.java` 文件进一步增强包的管理：

```java
module com.example.myapp {
    exports com.example.myapp;  // 导出包供其他模块使用
    requires java.base;         // 依赖的模块
}
```

- 模块是对包的更高层次封装，提供更强的访问控制和依赖管理。
- 包仍然是模块的基础单位。

### 实际示例

假设一个简单的项目：

```
src/
  com/
    example/
      model/
        User.java
      util/
        Logger.java
```

- `User.java`：

```java
package com.example.model;

public class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

- `Logger.java`：

```java
package com.example.util;

public class Logger {
    public static void log(String message) {
        System.out.println("Log: " + message);
    }
}
```

- `Main.java`：

```java
package com.example;

import com.example.model.User;
import com.example.util.Logger;

public class Main {
    public static void main(String[] args) {
        User user = new User("Alice");
        Logger.log("User created: " + user.getName());
    }
}
```

运行结果：

```
Log: User created: Alice
```





## 对象和类

### 类（Class）

对象的蓝图或模板。它定义了对象的属性（字段）和行为（方法）。可以将类看作一个抽象的结构或数据类型，用于创建对象。

通常情况下，**每个Java文件**应该包含**一个公共类**（`public class`），且这个公共类的名称必须与文件名相同。除此之外，文件中还可以包含其他非公共类。如果一个类没有显式地声明为 `public`，那么它的访问权限默认是 **包级私有**（package-private）。

```java
// MainClass.java

public class MainClass {
    public void start() {
        HelperClass helper = new HelperClass();
        helper.sayHello();
    }
}

class HelperClass {
    void sayHello() {
        System.out.println("Hello from HelperClass!");
    }
}
```

#### 内部类（Inner Class）

**内部类（Inner Class）**指的是一个类的内部又完整嵌套了另一个类结构。

##### 局部内部类（Local Inner Class）

###### 普通局部内部类

定义在外部类局部位置上（如方法内）的类。

```java
public void method() {
    class LocalInnerClass {
        // 类的内容
        // 1.可以访问外部类的所有成员，包含私有的
        // 2.不能添加访问修饰符，因为它的地位就是一个私有变量
        // 3.如果外部类与局部内部类的成员重名时，默认就近；同名外部类成员通过（外部类名.this.成员）访问
    }
    // 实例化局部内部类
    LocalInnerClass local = new LocalInnerClass();
}
```

###### 匿名内部类（Anonymous Inner Class）

这是一种**特殊的局部内部类**，它**没有显式的类名**，直接在代码中定义并**实例化**（既是类也是对象）。

通常用于实现接口或继承[抽象]类。

```java
new InterfaceName/AbstructClassName(params) {
    // code
};
```

基于接口的匿名内部类。

```java
public class OuterClass {
    public static void test() {
        /*
        底层原理：
        class OuterClass$1 implements Animal {
            @Override
            void eat() {
                System.out.println("Eat!");
            }
        }
        OuterClass$1 usb = new OuterClass$1();
        */ 
        Animal tiger = new Animal() {
            @Override
            public void eat() {
                System.out.println("Eat!");
            }
        };
        tiger.eat();
        // 匿名内部类实际有名字，由系统分配。这里是OuterClass$1
        System.out.println(tiger.getClass());
    }

    public static void main(String[] args) {
        test();
    }
}

interface Animal {
    void eat();
}
```

基于类的匿名内部类。

```java
public class OuterClass {
    public static void test() {
        Person webb = new Person("Webb") {
            @Override
            public void introSelf() {
                System.out.println("I'm Webb!");
            }
        };
        /*
        底层原理：
        class OuterClass$2 extends Person {
        	@Override
            public void introSelf() {
                System.out.println("I'm Pete!");
            }
		}
		OuterClass$2 pete = new OuterClass$2("Pete")
        */
        Person pete = new Person("Pete") {
            @Override
            public void introSelf() {
                System.out.println("I'm Pete!");
            }
        };
        
        webb.introSelf();
        pete.introSelf();
        
        System.out.println(webb.getClass()); // OuterClass$1
        System.out.println(pete.getClass()); // OuterClass$2
    }

    public static void main(String[] args) {
        test();
    }
}

class Person {
    public Person(String name) {
    }
    public void introSelf() {
    }
}
```

##### 成员内部类（Member Inner Class）

定义在外部类成员位置上的类。

```java
public class OuterClass {
    // 成员内部类
    class InnerClass {
        // 内部类的成员
        // 1.可以访问外部类的所有成员，包含私有的。
        // 2.能添加任意访问修饰符
    }
    static class StaticInnerClass {
        // 1.可以访问外部类的所有静态成员，包含私有的。
        // 2.能添加任意访问修饰符
    }
    
}
```

###### 普通成员内部类

```java
public class TexPoke {
    class Player {
        Boolean isFall = false;
    }
    Player button = new Player();
    
    public static void main(String[] args) {
        // ❌：静态方法不能访问普通成员，这里内部类也是普通成员。
        Player button = new Player();
    }
}
```

###### 静态成员内部类

```java
public class TexPoke {
    public static int round = 4;
    
    static class Player {
        public static int round = 2;
        
        public int getSelfRound() {
            return TexPoke.round; // 2
        }
        public int getCurrRound() {
            return TexPoke.round; // 4
        }
    }
    
    public static void main(String[] args) {
        // 正确
        Player button = new Player();
    }
}

class Test {
    // 其他外部类使用内部类。
    TexPoke.Player underGun = new TexPoke.Player;
}
```

#### 类什么时候被加载？

1. 创建对象实例时（new）
2. 子类实例化时，父类也会被加载
3. 使用类的静态成员时



### 成员（Member）

成员是类中定义的变量和方法，它们代表类的属性和行为。成员可以分为五种类型：

- **字段（Fields）**：类中的变量，用来存储对象的状态或数据。
- **方法（Methods）**：类中的函数，用来定义对象的行为或操作。
- **构造器（Constructor）**：特殊的方法，用于创建和初始化对象。
- **代码块（Code Block）**：用大括号 {} 括起来的一段代码。
- **内部类（Inner Class）**：类的嵌套成员， 用于增强外部类的功能。

此外还有一些容易混淆的名称：

**成员变量**就是类的属性或者说字段。**局部变量**一般指在成员方法或者代码块中定义的变量。



### 对象（Object）

类的实例，具有状态和行为。

```java
Car myCar = new Car();
```

#### `new` 关键字

使用 `new` 关键字可以创建一个类的实例，也就是对象。它不仅仅是分配内存，还会调用类的构造方法来初始化对象。

```java
ClassName objectName = new ClassName();
```

使用 `new` 关键字可以创建数组。数组的大小必须在创建时确定，并且数组会在内存中连续存储指定类型的元素。

```java
Type[] arrayName = new Type[size];
```



### 方法（Method）

定义类的行为，包含在类中的函数。

````java
public void displayInfo() {
    System.out.println("Info"); 
}
````

#### 传参机制

- 对于基本数据类型（如 `int`, `double`, `char`, `boolean` 等），传递的是变量所存储的**实际值的副本**。
    - **特点：**
        - 方法内部对参数的修改**不会影响**原始的变量。
        - 因为方法操作的是原始值的一个拷贝。

- 对于引用数据类型（如对象、数组），传递的是变量所存储的**引用的副本**，而不是对象本身。这个引用副本和原始引用指向**堆内存中的同一个对象**。
    - **特点：**
        - 方法内部**可以通过引用的副本修改对象的状态**（例如修改对象的字段），这会影响到原始对象。
        - 但是，**如果让参数的引用指向一个新的对象，则不会影响原始的引用**。

#### 静态方法

静态方法是属于类本身的，而不是类的实例。因此，静态方法不能直接访问实例变量和实例方法，**只能访问静态变量和静态方法**。

静态方法可以通过类名或实例来调用，但**通常通过类名**来调用。

```java
class MathUtil {
    // 静态方法
    public static int square(int number) {
        return number * number;
    }

    public static void main(String[] args) {
        // 使用类名调用静态方法
        int result = MathUtil.square(5);
        System.out.println("Square of 5 is: " + result);  // 输出: Square of 5 is: 25
    }
}
```



### 方法重载（Method Overload）

重载是指**在同一个类中**，**定义多个方法名相同但参数列表不同的方法。**Java 会根据方法调用时传递的参数类型和数量来决定调用哪个具体的方法。

```java
public class MathUtils {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

// 方法名必须相同，形参列表必须不同，返回值无要求
```

#### 可变参数

可变参数（Variable Arguments，简称 Varargs）是 Java 5 引入的一个特性，它允许方法接受数量可变的同类型参数。

1. **语法**：使用三个点(`...`)表示可变参数
2. **内部实现**：在方法内部，可变参数被当作数组处理
3. **位置限制**：必须是方法参数的最后一个参数
4. **数量限制**：一个方法只能有一个可变参数

```java
public int sum(int n1, int n2) {
	return n1 + n2;
}

public int sum(int n1, int n2, int n3) {
	return n1 + n2 + n3;
}

public int sum(int n1, int n2, int n3, int n4) {
	return n1 + n2 + n3 + n4;
}

public int sum(int... nums) {
	int total = 0;
    for (int num : nums) {
        total += num;
    }
    return total;
}
```





### 方法重写（Method Override）

重写是指**子类重新定义父类中已有的方法**，以覆盖父类的实现。重写是实现运行时多态的基础，通常与继承和多态相关。

- 子类方法的参数，方法名称，要和父类方法的参数，方法名称完全一样。

    ```java
    class Parent {
    	public String getInfo() {
    		return "Parent";
    	}
    }
    
    class Child extends Parent{
        @Override
    	public String getInfo() {
            // 父类的方法只能在子类内部调用
    		return super.getInfo() + "'s Child";
    	}
    }
    
    public class Test {
    	public static void main(String[] args) {
            Child c = new Child();
            // 在外部，此时调用的是子类方法，实例化子类无法再调用父类重写之前的父类方法
            System.out.println(c.getInfo());
        } 
    }
    ```

- 子类方法的返回类型和父类返回类型一样，或者是**父类返回类型的子类**。

    ```java
    // 父类
    Object printName() {}
    // 子类
    public String printName() {}

- 子类方法**不能缩小**父类方法的访问权限。

    ```java
    // 错误：子类只能增大权限
    // 父类
    public void eat() {}
    // 子类
    void eat() {}
    ```

#### `@Override` 注解

如果使用了 `@Override` 注解，编译器会检查方法签名是否与父类中的方法匹配。如果不匹配，编译器会报错。这有助于捕获潜在的错误，避免因为签名错误导致的意外问题。

- 例如，如果你不小心拼写错误，编译器会告知你没有正确重写父类的方法。

```java
class Parent {
    public void display() {
        System.out.println("Display from Parent");
    }
}

class Child extends Parent {
    @Override
    public void display() {
        System.out.println("Display from Child");
    }
}

public class OverrideExample {
    public static void main(String[] args) {
        Parent parent = new Parent();
        Parent child = new Child();

        parent.display();  // 输出 "Display from Parent"
        child.display();   // 输出 "Display from Child"（运行时多态）
    }
}
```

### 构造器（Constructor）

#### 初始化顺序

1. 静态初始化（类加载时，仅执行一次）
2. 实例初始化（每次创建对象时）
3. 父类优先
4. 按成员定义顺序执行
5. 构造方法靠后

```java
Constructor() {
	// 父类静态成员
    // 子类静态成员
    // 父类普通成员
    // 父类构造方法 super
    // 子类普通成员
    // 子类构造方法 this
}
```

实际上，Java 编译器会将字段的直接初始化**移动到所有构造器的开头**，

```java
public class Example {
    private int val = 0;
}
// 所以，上面的等价于
public class Example {

    private int val;

    public Example() {
        val = 0; // 编译器自动添加的初始化
    }
}
```



#### 默认构造器（Default Constructor）

- 如果类中**没有显式定义任何构造器**，Java 编译器会自动提供一个无参的默认构造器。
- 默认构造器的作用是简单地创建对象，**不进行额外初始化**。
- **程序员一旦显示使用构造器，默认构造器就被覆盖掉了。** :star:

```java
class Person {
    String name;
    int age;

    // 默认构造器 (由编译器自动生成，如果没有其他构造器)
    // public Person() {} // 编译器自动提供
}
```

#### 无参构造器（No-Argument Constructor）

- 由程序员**显式定义**的无参数构造器。
- 可以用来设置字段的**默认值**。

```java
class Person {
    String name;
    int age;

    // 无参构造器（由程序员手动定义）
    public Person() {
        // 可以在无参构造器中添加自定义初始化逻辑
        this.name = "Unknown";
        this.age = 0;
    }
}

public class Main {
    public static void main(String[] args) {
        // 使用无参构造器
        Person person = new Person();
        System.out.println("Name: " + person.name + ", Age: " + person.age);
    }
}
```

#### 带参构造器（Parameterized Constructor）

- 接受参数，用于根据传入的值初始化对象。
- 支持灵活的初始化方式。

#### 重载构造器（Overloaded Constructor）

- 与普通方法类似，构造器可以被重载。重载的构造器具有相同的名称（类名），但参数列表不同。

```java
public class Person {
    String name;
    int age;

    // 无参构造器
    public Person() {
        name = "Unknown";
        age = 18;
    }

    // 带一个参数的构造器
    public Person(String n) {
        name = n;
        age = 18;
    }

    // 带两个参数的构造器
    public Person(String n, int a) {
        name = n;
        age = a;
    }
}

class Test {
    public static void main(String[] args) {
        Person p1 = new Person();           // Unknown, 18
        Person p2 = new Person("Bob");      // Bob, 18
        Person p3 = new Person("Alice", 20); // Alice, 20
        System.out.println(p1.name + ", " + p1.age);
        System.out.println(p2.name + ", " + p2.age);
        System.out.println(p3.name + ", " + p3.age);
    }
}
```

#### `this` 关键字

**访问本类的属性，没有则向上查找，找到为止。**

当局部变量（例如方法的参数）与实例变量（类的属性）同名时，可以使用 `this` 来区分实例变量和局部变量。

```java
class Person {
    String name;  // 实例变量
    
    Person(String name) {
        // 参数 name 与实例变量 name 同名，使用 this 来区分
        this.name = name;
    }
    
    void printName() {
        System.out.println("Name: " + this.name);
    }
}
```

同样，`this` 可以用来调用当前对象的实例方法。通常在**没有歧义时可以省略** `this`，但如果需要明确表示是调用当前对象的方法，可以使用 `this`。

```java
class Car {
    void start() {
        System.out.println("Car is starting...");
    }
    
    void drive() {
        // 使用 this 调用当前对象的方法
        this.start();
        System.out.println("Car is driving...");
    }
}
```

`this` 可以**作为参数**传递给方法或构造函数。当你希望传递当前对象的引用时，可以使用 `this`。

```java
class Printer {
    void print(Person person) {
        System.out.println("Printing: " + person.getName());
    }
}

class Person {
    String name;
    
    Person(String name) {
        this.name = name;
    }
    
    String getName() {
        return this.name;
    }
    
    void printDetails() {
        Printer printer = new Printer();
        // 传递当前对象（this）作为参数
        printer.print(this);
    }
}
```

> 在静态方法或静态上下文中，不能使用 `this`，因为静态方法是属于类的，而不是属于某个具体的对象实例的。
>
> ```java
> class MyClass {
>  static void myMethod() {
>      // 不能在静态方法中使用 this
>      // System.out.println(this);  // 编译错误
>  }
> }
> ```

##### 使用 `this()` 调用其他构造方法

`this()` 允许一个构造方法调用同一个类中的另一个构造方法，从而实现构造器的重载。它使得代码更加简洁，减少了冗余的代码。

值得注意的是，`this()` 只能是构造器中的第一行。

```java
class Person {
    String name;
    int age;

    // 构造器1：无参构造器
    public Person() {
        this("Unknown", 0);  // 调用构造器3，传递两个参数：String 和 int
    }

    // 构造器2：带有 name 参数的构造器
    public Person(String name) {
        this(name, 0);  // 调用构造器3，传递一个参数 name 和默认值 0 给 age
    }

    // 构造器3：带有 name 和 age 参数的构造器
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 继承（Inheritance）

一个子类可以继承另一个父类的**属性**和**方法**。但是 java 只支持单继承，也就是一个子类只能继承自一个父类。而 python 支持多继承。

**java所有类都是Object子类。**

- 示例：

    ```java
    public class Dog extends Animal { ... }
    ```

#### 继承本质

```java
class GrandPa {
    String name = "Peter";
    String hobby = "Tour";
}

class Father extends GrandPa {
    String name = "Webb";
    int age = 20;
}

class Son extends Father {
    String name = "Rob";
}

Son son = new Son();
// 自下而上的找。一直都没找到就会报错
System.out.println(son.name);  // Rob
System.out.println(son.age);   // 20
System.out.println(son.hobby); // Tour
```

#### `super` 关键字

**访问父类的属性，没有则向上查找，找到为止。**

如果子类和父类有同名的成员变量，使用 `super` 可以访问父类的成员变量，而避免与子类的同名变量产生冲突。

```java
class Animal {
    String name = "animal";
}

class Dog extends Animal {
    String name = "dog";
    
    void printName() {
        // 访问父类的成员变量
        System.out.println("父类的名字: " + super.name);
        // 访问子类的成员变量
        System.out.println("子类的名字: " + this.name);
    }
}
```

如果子类重写了父类的方法，使用 `super` 可以访问父类中被重写的方法。

```java
class Animal {
    void sound() {
        System.out.println("animal voice");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("bark");
    }
    
    void callSuperSound() {
        // 使用 super 调用父类的方法
        super.sound();
    }
}
```

##### 使用`super()`调用父类的构造函数

子类必需调用父类的构造器。

- 无论子类使用哪种构造器，子类默认情况下总会调用父类的**无参构造器（无论是默认的还是声明的）**。

```java
class Parent {
	Parent() {
		System.out.printl("first");
	}
}

class Child extends Parent {
    private int age;
	Child() {
        // 默认调用 super();
		System.out.printl("second");
	}
    Child(int age) {
        // 默认调用 super();
		this.age = age;
        System.out.printl("second");
	}
}
```

 `super()` 只能放在构造器的第一行。

- 如果父类有**无参构造器**，`super()` 会默认调用该构造函数。如果父类有**带参构造器**，子类需要显式调用父类的带参数构造函数。

- 如果父类有多个构造函数，子类可以通过 `super()` **选择性**地调用父类的某个构造函数。

```java
class Animal {
    private String name;
    
    Animal() {
        this.name = "Bee";
    }
    
    Animal(String name) {
        this.name = name;
    }
}

class Dog extends Animal {
    private int age;
    
    Dog(int age) {
        // 使用 super 调用父类的构造函数
        super();
        this.age = age;
    }
    
    Dog(String name, int age) {
        // 使用 super 调用父类的构造函数
        super(name);
        this.age = age;
    }
}
```



### 封装（Encapsulation）

- 将对象的状态（字段）私有化，通过**公共方法访问**。

- 示例：

    ```java
    private String name; 
    public String getName() { return name; }
    ```

### 多态（Polymorphism）

多态就是同一个接口，使用不同的实例而执行不同操作。

> 对象的编译类型与运行类型：
>
> ```java
> Animal animal = new Dog();
> animal = new Cat();
> ```
>
> - 编译类型（编译时确定）：`Animal`
> - 运行类型（运行时可以改变）：`Dog`，`Cat`

#### 实现多态的条件

1. **封装与继承**：两个对象存在继承关系。

2. **方法重载与方法重写**：方法名相同，但参数列表（数量、类型或顺序）不同；子类重写父类或接口中的方法。

3. **向上转型**：**父类引用指向子类对象**，使用父类或接口类型的引用指向子类对象。如 `Animal animal = new Dog();`    `Animal(getName)` ，`Dog(getName, bark)`。

    > 能否调用看编译类型：
    >
    > - 可以**调用**父类中的**所有**成员。
    >
    >     ```java
    >     animal.getName(); // 可以
    >     ```
    >
    > - 不能**调用**子类中的**特有**成员。
    >
    >     ```java
    >     animal.bark(); // 不行
    >     ```
    >
    > 能否执行看运行类型：
    >
    > - **执行**时由子类实现。
    >
    >     ```java
    >     animal.getName(); // 这里运行时还是从子类开始找。
    >     ```

    **向下转型**：将父类类型的引用转换为子类类型。如 `Dog dog = (Dog) animal;`

    > 前提：要有通过**向上转型**创建的引用。
    >
    > 作用：**调用**子类中的**特有**成员。
    >
    > 要求：父类的引用必须指向当前目标类型的对象，否则报错。`animal -> Dog -> new Dog()`

4. **动态绑定机制**：

    - 当调用**对象方法**时，该方法会和该对象的**内存地址/运行类型**绑定。
    - 当调用**对象属性**时，没有动态绑定机制，**哪里声明，哪里调用。**

    ```java
    class Calculator {
        public int a = 20;
        
        public int getA() {
            return a;
        }
        public int add() {
            return a + 3;
        }
        public int addA() {
            return getA() + 3;
        }
    }
    
    class Adder extends Calculator {
        public int a = 10;
    
        public int getA() {
            return a;
        }
    }
    
    Adder a = new Adder();
    a.add();  // 23		A: add[没有] -> C: add -> C: a(20)
    a.addA(); // 13		A: addA[没有] -> C: addA -> A: getA[] -> A: a(10)
    ```

#### 编译时多态

通过**方法重载（Overloading）**实现，即方法名相同，但参数不同。

```java
class Calculator {
    // 方法重载：不同参数的同名方法
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

public class Demo {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 10));        // 调用 int 参数的 add 方法
        System.out.println(calc.add(5.5, 10.5));    // 调用 double 参数的 add 方法
    }
}

```

#### 运行时多态

通过**方法重写（Overriding）**实现，即**子类重写父类的方法**，具体调用哪个方法由实际对象的类型决定（通常通过父类引用指向子类对象实现）。

**方法调用顺序**：在 Java 中，方法调用遵循**动态绑定**原则。如果当前类没有，JVM 会通过继承链向上查找，直到找到方法为止。

```java
// Animal.java (name, getName)
// Animal子类：Dog(bark), Cat, Pig

// Food.java (name)
// Food子类：Bone, Fish, Rice

// Master.java (name)
public void feed(Animal animal, Food food) {
    System.out.println(name + " feeds " + animal.getName() + " with " + food.getName());
}
// 不需要每种动物写一个feed方法。
public void feed(Dog dog, Bone bone) {
    System.out.println(name + " feeds " + dog.getName() + " with " + bone.getName());
}
public void feed(Cat cat, Fish fish) {
    System.out.println(name + " feeds " + cat.getName() + " with " + fish.getName());
}
...

// Daily.java
Master tom = new Master("Tom");

// 向上转型。
Animal dog = new Dog("Webb");
Animal cat = new Cat("Sands");
Animal pig = new Pig("Dave");

Food bone = new Bone("bone");
Food fish = new Fish("fish");
Food rice = new Rice("rice");

tom.feed(dog, bone);

// 向下转型。
Dog dogLower = (dog) dog;
dogLower.bark();

// 与直接创建对象的区别。
Dog dog = new Dog("Leoooooo");
Bone bone = new Bone("bone");
tom.feed(dog, bone); // 无法使用feed。不是多态。

```

#### 多态的应用

##### 多态数组

多态数组是一个数组的创建时**向上转型**，而遍历时**动态绑定**。

```java
// 父类
class Animal {
    void makeSound() {
        System.out.println("Some generic sound");
    }
}

// 子类1
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof!");
    }
    void bark() {
        System.out.println("WangWang!");
    }
}

// 子类2
class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        // 创建数组，声明类型为Animal
        Animal[] animals = new Animal[3];
        // 向上转型，存储不同子类对象
        animals[0] = new Dog();
        animals[1] = new Cat();
        animals[2] = new Dog();

        // 遍历数组，调用makeSound方法
        for (Animal animal : animals) {
            // 动态绑定，调用实际类型的makeSound
            animal.makeSound();
            if (animal instanceof Dog) {
                ((Dog) animal).bark();
            }
        }
    }
}
```

##### 多态参数

方法的形参类型是父类，但传入的实参类型是子类。通过**动态绑定**，方法内部调用参数的方法时，会根据实参类型执行对应的重写方法。

```java
// 父类
class Animal {
    void makeSound() {
        System.out.println("Some generic sound");
    }
}

// 子类1
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof!");
    }
}

// 子类2
class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow!");
    }
}

// 类包含多态参数方法
class Zoo {
    // 多态参数：参数类型为Animal
    void performSound(Animal animal) {
        animal.makeSound(); // 动态绑定，调用实际类型的makeSound
    }
}

public class Main {
    public static void main(String[] args) {
        Zoo zoo = new Zoo();

        // 创建不同子类对象
        Animal dog = new Dog();
        Animal cat = new Cat();

        // 传入多态参数
        zoo.performSound(dog); // 输出: Woof!
        zoo.performSound(cat); // 输出: Meow!

        // 直接传入子类对象（向上转型）
        zoo.performSound(new Dog()); // 输出: Woof!
        zoo.performSound(new Cat()); // 输出: Meow!
    }
}
```



### 抽象（Abstraction）

**抽象**（`abstract`）指的是将类的共同特性提取出来，放到一个抽象层面，而不关注其具体实现细节。

#### 抽象类

**抽象类**（`abstract class`）是一种**不能被实例化**的类，它是为了被继承而设计的。

类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。

抽象类可以包含**抽象方法**和**非抽象方法**。抽象方法没有方法体，只声明方法的签名，具体的实现由子类提供。

```java
abstract class Animal {
    abstract void sound();  // 抽象方法，没有方法体
    
    void eat() {  // 非抽象方法，有方法体
        System.out.println("This animal eats food.");
    }
}
```

#### 抽象方法

`abstract` 关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。抽象方法没有定义，方法名后面直接跟一个分号，而不是花括号。

声明抽象方法会造成以下两个结果：

- 如果一个类包含抽象方法，那么该类必须是抽象类。
- 任何子类必须重写父类的抽象方法，或者声明自身为抽象类。

```java
public abstract class Employee {
   private String name;
   private String address;
   private int number;
   
   public abstract double computePay();
   
   //其余代码
}
```

#### 继承抽象类

```java
public class Salary extends Employee {
   private double salary; // Annual salary
  
   public double computePay() {
      System.out.println("Computing salary pay for " + getName());
      return salary/52;
   }
 
   //其余代码
}
```





## 修饰符

### 访问修饰符（Access Modifiers）

访问修饰符控制成员的可见性，也就是定义了类、方法、字段等可以被哪些其他类访问。Java提供了四种访问修饰符：

- **`public`**：表示该成员可以被**任何类**访问，不受包限制。
- **`protected`**：表示该成员可以被**同一个包中的其他类**或**不同包中的子类**访问。
- **`private`**：表示该成员只能在**当前类**内部访问，不能被其他类访问。
- **默认（无修饰符）**：如果没有使用访问修饰符，表示该成员只能被同一个包中的其他类访问**（包内访问）**。

### 非访问修饰符（Non-access Modifiers）

非访问修饰符用于定义类、方法、字段等的其他特性，比如是否为静态、是否为常量等。常见的非访问修饰符有：

- **`static`**：表示该成员属于类，而不是某个具体的对象。可以通过类名直接访问，而不需要实例化对象。
- **`final`**：表示该成员不可改变。对于类来说，表示**该类不能被继承**；对于方法来说，表示**该方法不能被重写**；对于变量来说，表示**该变量的值不能被改变**。
- **`abstract`**：表示该类或方法是抽象的，不能实例化或者必须在子类中实现。
- **`synchronized`**：表示该方法是线程安全的，多个线程访问时会按顺序执行，确保同一时间只有一个线程访问该方法。
- **`volatile`**：表示该字段可能会被多个线程修改，确保所有线程都能看到该字段的最新值。
- **`transient`**：表示该字段不会被序列化，当对象被转换为字节流时，标记为`transient`的字段会被忽略。
- **`native`**：表示该方法是用其他语言（如C/C++）实现的，通常与Java的本地方法接口（JNI）一起使用。
- **`strictfp`**：表示严格遵循浮点运算的IEEE 754标准，确保浮点运算在不同平台上具有一致性。

### 常见使用

#### 组合使用

修饰符可以组合使用，例如：

```java
public final static int MAX_VALUE = 100;
```

#### `final`

一般来说，如果一个类已经是`final`类了，就没有必要再将方法修饰成`final`方法。

此外，`final` 与 `static` 组合使用，效率更高，**不会导致类加载**，底层编译器做了优化处理。

```java
class Player {
    public final static int count = 0;
    static {
        // 类没有加载，不会输出
        System.out.println("Class loaded!");
    }
}
public class Test { 
    public static void main(String[] args) {
        System.out.println(Player.count);
    }
}
```



## 类成员

### 类变量（Static Variable）

类变量属于类本身而非类的实例的变量。用 `static` 关键字声明。

- 类变量被同一个类的所有对象共享。
- 类变量在类加载的时候就生成了。

```java
class Student {
    static String name = "Peter";
    static int age = 12;
}

public class Test {
    public static void main(String[] args) {
        // 用类名访问（推荐）
        System.out.println(Student.name);
        Student s = new Student();
        // 用对象访问也可以。
        System.out.println(s.age);
    }
}
```

### 类方法（Static Method）

类方法属于类本身而非类的实例的方法。用 `static` 关键字声明。

- 类方法不允许使用与对象有关的关键字，如`this`，`super`…
- **类方法只能访问类成员；普通方法可以访问普通成员和类成员。**:star::star::star:

```java
class Student {
    private static String name = "Peter";
    private static int age = 12;
    
    public static String getName() {
        return name;
    }
}

public class Test {
    public static void main(String[] args) {
        System.out.println(Student.getName());
    }
}
```

### 使用场景

类变量适用于存储类级别的**共享数据**或**全局状态**。

- 计数器
- 常量
- 配置或共享状态
- 缓存：存储昂贵计算结果或共享资源，供所有实例使用。

类方法适用于实现与类相关但**不依赖实例状态**的功能。

- 访问或修改类变量

- 工具方法：`Math`，`Collections`，自定义工具类…

    ```java
    class MyTools {
        public static double calSum(double n1, double n2) {
            return n1 + n2;
        }
    }
    
    public class Test {
        public static void main(String[] args) {
            // 直接使用。
            System.out.println(MyTools.calSum(1.0, 1.1));
        }
    }

- 工厂方法：用于创建对象，替代构造函数，提供更灵活的实例化方式。

### `main` 方法

`main` 方法是一个特殊的类方法（静态方法），它是 Java 程序的入口点。

```java
public static void main(String[] args) {
    // 程序入口逻辑
}
```

说明：

1. `public`：方法是公开的，JVM（Java 虚拟机）可以从外部调用。

2. `static`：方法属于类，不需要创建类的实例即可调用。

3. `void`：方法没有返回值。

4. `main`：方法名，JVM 识别的入口点名称。

5. `String[] args`：字符串数组，用于接收命令行参数。

    ![image-20250511144653212](images/image-20250511144653212.png)

值得注意的是，`main` 方法不能直接访问本类中的普通成员，必须本类实例化才能访问。

```java
public class Baccarat { 
    public class Player {
        
    }
    private Player player;
    private Player banker;
    private int round;

    public Baccarat() {
        this.round = 0;
        this.player = new Player();
        this.banker = new Player();
    }

    public static void main(String[] args) {

        // 报错：Player不是本类，不能实例化。
        // 非静态内部类与外部类的实例绑定，必须通过外部类的实例来创建内部类的对象。直接通过 new Player() 无法实例化，因为它缺少外部类 Baccarat 的上下文。
        Player banker = new Player();
        // 报错：不能用round
        System.out.println(Baccarat.round);
        Baccarat game = new Baccarat();
    }
}
```





## 代码块

代码块是指用大括号 `{}` 括起来的语句集合，用于定义一段逻辑范围；相当于构造器的补充机制，减少构造器中重复的部分。它又称**初始化块**，属于**类成员**。

```java
修饰符 {
    // 代码
};
```

> 修饰符可选，但只能是`static`；分号可有可无。

### 普通代码块

初始化实例变量或执行对象创建时先被调用。

```java
public class MyClass extends HisClass{
    int value;
    String name;
    {
        value = 42; // 实例初始化代码块
        System.out.println("Instance block executed");
    }
    public MyClass() {
        // 1.隐式的执行要求
        // super();
        // 普通代码块{}初始化;
        // 2.显示初始化
        this.name = "aka";
    }
}
```

限定变量作用域，代码块结束后局部变量被销毁。

```java
public void example() {
    int x = 10;
    {
        int y = 20; // y 仅在此代码块内有效
        System.out.println("x = " + x + ", y = " + y);
    }
    // System.out.println(y); // 错误，y 已不可访问
}
```

### 静态代码块

初始化静态变量或执行**一次性**类初始化逻辑。

```java
public class MyClass extends HisClass {
    static int count;
    String name;
    static {
        count = 100; // 静态代码块初始化
        System.out.println("Static block executed");
    }
    public MyClass(){
        // 1.隐式的执行要求
        // 静态代码块{}初始化;
        // super();
        // 2.显示初始化
        this.name = "aka";
    }
}
```



## 接口（Interface）

**接口**（`interface`）是一种**特殊的抽象类**，它是定义一组方法声明，但**不提供实现细节**。接口主要用于定义类之间的**契约**，规定类必须实现的行为，而不关心具体的实现方式。接口强调的是"做什么"，而不是"怎么做"。

### 声明一个接口

- 接口是隐式抽象的，当声明一个接口的时候，不必使用**`abstract`**关键字。
- 接口中**每一个方法**也是隐式抽象的，声明时同样不需要**`abstract`**关键字。
- 接口中的方法都是公有的 **`public`** 。

```java
interface Animal {
    void sound();  // 接口方法，子类需要实现
    void eat();    // 接口方法，子类需要实现
}
```

### 实现接口

类使用 `implements` 关键字实现接口。当类实现接口的时候，普通类要实现接口中**所有方法**，抽象类不用。

```java
interface Animal {
    void sound();
}

interface Walkable {
    void walk();
}

// 一个类可以实现多个接口。
class Dog implements Animal, Walkable {
    public void sound() {
        System.out.println("Woof!");
    }

    public void walk() {
        System.out.println("The dog is walking.");
    }
}

```

此外，接口也是类，也具有多态特性。

```java
// 定义一个接口
interface Animal {
    void makeSound(); // 抽象方法
}

// 实现类：Dog
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("汪汪汪");
    }
}

// 实现类：Cat
class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("喵喵喵");
    }
}

// 测试类
public class Main {
    public static void main(String[] args) {
        // 使用接口类型引用指向不同实现类对象
        Animal animal1 = new Dog(); // 接口多态
        Animal animal2 = new Cat();

        animal1.makeSound(); // 输出：汪汪汪
        animal2.makeSound(); // 输出：喵喵喵
    }
}
```

### 接口的继承

接口可以继承其他接口，一个接口也可以继承多个接口，这样可以组合不同的行为。

**Java支持多重继承的接口，但不支持多重继承的类**。

```JAVA
interface Animal {
    void sound();
}

interface Walkable {
    void walk();
}

// 一个接口可以继承多个接口
interface DogActions extends Animal, Walkable {
    void fetch();
}
```





## 枚举

枚举是一个**特殊的类**，一般表示一组常量，比如一年的 4 个季节，一年的 12 个月份，一个星期的 7 天，方向有东南西北等。

Java 枚举类使用 `enum` 关键字来定义，各个常量使用逗号 **`,`** 来分割。实际上隐式继承了`java.lang.Enum`类，所以不能再继承任何类，但可以实现接口。

### 自定义枚举类

```java
public class Season {
    private String name;
    private String description;
    
    // 私有构造器：限制了外部代码直接通过 new 创建对象，强制通过特定方式（如工厂方法、单例模式）实例化。
    private Season(String n, String d) {
        name = n;
        description = d;
    }
    
    public static final Season SPRING = new Season("Spring", "Warm");
    public static final Season SUMMER = new Season("Summer", "Hot");
    public static final Season AUTUMN = new Season("Autumn", "Cool");
    public static final Season WINTER = new Season("Winter", "Cold");
    
}
```

### 声明一个枚举类

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
}
```

### 使用枚举

```java
public class Main {
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        System.out.println("Today is: " + today); // 输出: Today is: MONDAY
    }
}
```

### 遍历枚举

```java
public class Main {
    public static void main(String[] args) {
        // 遍历所有枚举值
        for (Day day : Day.values()) {
            System.out.println(day);
        }
    }
}
```

### 常用方法

| 方法                   | 说明                            |
| :--------------------- | :------------------------------ |
| 静态方法               |                                 |
| `values()`             | 返回枚举的所有值（数组）        |
| `valueOf(String name)` | 根据名称返回枚举常量            |
| 对象方法               |                                 |
| `compareTo(E o)`       | 比较枚举常量的序号              |
| `ordinal()`            | 返回枚举常量的序号（从 0 开始） |
| `name()`               | 返回枚举常量的名称（字符串）    |

```java
Day day = Day.MONDAY;
Day day = Day.valueOf("TUESDAY") // Day.TUESDAY
day.ordinal()  // 0（MONDAY 是第一个）
day.name()    // "MONDAY"
```

### 枚举类与普通类一样

枚举类与普通类一样，也可以有字段、方法和构造函数。

```java
public enum Planet {
    MERCURY(3.303e+23, 2.4397e6),  // 调用构造函数
    VENUS(4.869e+24, 6.0518e6),
    EARTH(5.976e+24, 6.37814e6);

    private final double mass;   // 枚举可以有自己的字段
    private final double radius;

    // 枚举的构造函数（必须是 private 或默认）
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    // 枚举可以有方法
    public double surfaceGravity() {
        return 6.67300E-11 * mass / (radius * radius);
    }
}
```

```java
Plant earthSurfaceGravity = Plant.EARTH.surfaceGravity()
```

枚举还可以实现接口。

```java
public interface Greetable {
    void greet();
}

public enum Greeting implements Greetable {
    HELLO {
        @Override
        public void greet() {
            System.out.println("Hello!");
        }
    },
    GOODBYE {
        @Override
        public void greet() {
            System.out.println("Goodbye!");
        }
    };
}
```

```java
Greeting.HELLO.greet(); // 输出: 你好！
```



## 注解

注解（Annotations）是Java 5引入的一种元数据机制，用于在代码中添加额外信息，供编译器、工具或运行时处理。

### 什么是Java注解

- 注解是一种特殊的元数据标记，以`@`开头，附加在代码元素（如类、方法、字段等）上。

- 注解本身不直接影响代码逻辑，但可以通过反射、编译器或工具处理来实现特定功能。

- 用途：代码文档、编译检查、运行时处理（如依赖注入、日志、测试）等。

### 标准注解

#### `@Override`

标记方法是重写父类或接口的方法。编译器检查方法是否重写，若不匹配则报错。

```java
@Override
public String toString() {
    return "Example";
}
```

源码

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {
}
```

#### `@Deprecated`

标记方法、类或字段已过时，不建议使用。编译器发出警告，提示开发者避免使用。

为版本升级做兼容过渡。

```java
@Deprecated
public void oldMethod() { ... }
```

源码

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, MODULE, PARAMETER, TYPE})
public @interface Deprecated {
    String since() default "";
    boolean forRemoval() default false;
}
```

#### `@SuppressWarnings`

抑制编译器警告（如未使用变量、类型转换等）。指定警告类型，如`@SuppressWarnings("unchecked")`。

```java
@SuppressWarnings("rawtypes")
public static void main(String[] args) {
    Person p = new Person(null);
}
```

源码

```java
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings {
    String[] value();
}
```

以下是常用的警告类型及其描述，

| 警告类型      | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| `unchecked`   | 用于原生类型（如泛型）中存在未检查的类型转换，通常是由于泛型类型的使用不当。 |
| `deprecation` | 使用了已弃用的类、方法或字段。                               |
| `rawtypes`    | 使用了原始类型（未指定泛型参数），这种用法会丧失类型安全性。 |
| `fallthrough` | 在 `switch` 语句中，某个 `case` 标签下没有 `break` 语句，可能导致控制流进入下一个 `case`。 |
| `serial`      | 未声明 `serialVersionUID`，这可能会导致 `Serializable` 类的序列化和反序列化出错。 |
| `unused`      | 变量、方法或参数声明后没有使用。                             |
| `null`        | 可能存在空指针异常，编译器无法保证某个引用是否为 `null`。    |
| `cast`        | 强制类型转换可能会导致 `ClassCastException`。                |
| `rawtypes`    | 在使用泛型时，没有提供具体的类型参数（使用原始类型）。       |
| `package`     | 包的声明与文件路径不匹配。                                   |

### 元注解

**注解的注解**。它们指定自定义注解的行为和使用范围，常用于注解的声明中。

#### `@Target`

指定注解可以应用的代码元素（如类、方法、字段等）。

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Target;

@Target({ElementType.METHOD, ElementType.FIELD})
public @interface MyAnnotation {}
```

**参数**：`ElementType`枚举值，支持以下类型：

- `TYPE`：类、接口、枚举、注解
- `FIELD`：字段（包括枚举常量）
- `METHOD`：方法
- `PARAMETER`：方法参数
- `CONSTRUCTOR`：构造方法
- `LOCAL_VARIABLE`：局部变量
- `ANNOTATION_TYPE`：注解类型
- `PACKAGE`：包
- `TYPE_PARAMETER`（Java 8+）：类型参数（如泛型）
- `TYPE_USE`（Java 8+）：类型使用（如@NonNull String）

#### `@Retention`

指定注解的生命周期，即注解在何时保留。

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {}
```

**参数**：`RetentionPolicy`枚举值：

- `SOURCE`：仅在源码中，编译后丢弃（如@Override）。
- `CLASS`：保留在字节码中，运行时不可见（默认）。
- `RUNTIME`：保留到运行时，可通过反射获取（最常用）。

#### `@Documented`

标记注解会包含在Javadoc文档中。

```java
import java.lang.annotation.Documented;

@Documented
public @interface MyAnnotation {}
```

#### `@Inherited`

允许子类自动继承父类的注解（仅适用于类注解）。

```java
import java.lang.annotation.Inherited;

@Inherited
public @interface MyAnnotation {}

@MyAnnotation
class Parent {}
class Child extends Parent {} // Child自动继承@MyAnnotation
```



## 泛型

泛型（Generics）是 Java 5 引入的重要特性，它提供了编译时类型安全检查机制，并消除了强制类型转换的需要。

泛型的本质是**参数化类型**，也就是说所操作的数据类型被指定为一个参数。

### 为什么需要泛型

```java
ArrayList l = new ArrayList ();
l.add(new People("Webb"));
l.add(new People("Peter"));
l.add(new People("Anna"));

l.add(new Dog("Leo"));

// 到Dog时出现异常，ClassCastException
for (Object o : l) {
    // 向下转型
    People p = (People) o;
    System.out.println(p);
}

// 编译只允许 Object
// ArrayList l 是原始类型，编译器只知道它存储 Object 类型，而不是 People 类型。
for (People p : l) {
    System.out.println(p);
}
```

**原始类型（Raw Type）**如 ArrayList 不使用泛型，允许添加任意 Object 类型的对象，失去了类型安全性。

所以通过使用泛型，可以在编译期确保类型安全，避免运行时的 `ClassCastException`。

### 使用泛型

#### 泛型类

泛型类允许我们创建可以操作多种数据类型的类，同时保持类型安全。

```java
public class Box<T> {
    // T 表示 content 的数据类型，在定义Box对象时指定
    private T content;
    
    public void setContent(T content) {
        this.content = content;
    }
    
    public T getContent() {
        return content;
    }
}

// 使用泛型类
// 存储String类型
Box<String> stringBox = new Box<>();
stringBox.setContent("Hello");
String str = stringBox.getContent(); // 不需要强制类型转换

// 存储Integer类型
Box<Integer> intBox = new Box<>();
intBox.setContent(123);
int num = intBox.getContent(); // 自动拆箱
```

#### 多类型参数的泛型类

```java
public class People<K, V, T> {
    private K name; // 例如 ID 或键
    private V age;      // 主要数据，如名称或属性
    private T metadata;  // 附加信息，如状态或标签

    // 构造方法
    public People(K name, V age, T metadata) {
        this.name = name;
        this.age = age;
        this.metadata = metadata;
    }

    // Getter 方法
    public String getMetadataClass() {
        return metadata.getClass().getName();
    }

    // toString 用于打印
    @Override
    public String toString() {
        return "People [Name: " + name + ", Age: " + age + ", Metadata: " + metadata + "]";
    }
}

People<String, Integer, String> person1 = new People<>("Alice", 25, "Active");
System.out.println(person1.getMetadataClass());

People<Integer, String, Boolean> person2 = new People<>(1001, "Bob", true);
System.out.println(person2.getMetadataClass());
```

#### 泛型接口

```java
public interface Network<T> {
    void add(T element);
    T get(int index);
}

// 继承接口
public interface Ethernet_1 extends Network<Integer> {
    
}

public interface Ethernet_2<M> extends Network<Integer> { // 子接口添加泛型参数 M
    void setMetadata(M metadata);
    M getMetadata();
}

// 实现接口
public class Wifi_1 implements Ethernet_2<String> { // M 设置为 String
    // 实现接口方法
}

public class Wifi_2 implements Network<Integer> { // Network中的方法类型都为Integer
    // 实现接口方法
    @Override
    void add_1(Integer element) {
        System.out.println(element + 1);
    }
}
```

#### 泛型方法

所有泛型方法声明都有一个类型参数声明部分（由尖括号`<>`分隔），该类型参数声明部分**在方法返回类型之前**。

泛型方法体的声明和其他方法一样。注意类型参数只能代表**引用型类型**，不能是原始类型（像 int、double、char 等）。

```java
class Util<U> {
    U name;
    public Util(U name) {
        this.name = name;
    }
    // 泛型方法
    public static<U> void printClass(U className) {
        System.out.println(className.getClass().getName());
    }

    // 不是一个泛型方法，而是方法使用了泛型
    public void printName() {
        System.out.println(name);
    }
}

// 使用泛型方法
Util.printClass("sss");
// 方法使用了泛型
Util<Integer> u = new Util("Tool");
u.printName();
```

### 泛型标记符

| 标记符        | 常见用途                         | 示例                |
| :------------ | :------------------------------- | :------------------ |
| `T`           | Type（任意类型）                 | `Box<T>`            |
| `E`           | Element（集合元素）              | `List<E>`           |
| `K`           | Key（键）                        | `Map<K,V>`          |
| `V`           | Value（值）                      | `Map<K,V>`          |
| `N`           | Number（数字类型）               | `Calculator<N>`     |
| `S`, `U`      | 第二、第三类型参数               | `Pair<T,U>`         |
| `?`           | 表示不确定的 java 类型（通配符） | `List<?>`           |
| `? extends T` | 表示 T 或 T 的子类（上界通配符） | `List<? extends T>` |
| `? super T`   | 表示 T 或 T 的父类（下界通配符） | `List<? super T>`   |

> 通配符 ?（包括 ? extends T 和 ? super T）只能用于**方法参数**、**变量声明**或**泛型实例化**时，而不能用于类或接口的泛型参数定义。

```java
public static void main(String[] args) {
    // 变量声明
    Util<?> n1;
    // 泛型实例化
    Util<? super Integer> n = new Util(1);
    
	Util<Integer> n3 = new Util(3);
    use(u);
}

// 方法参数
public static void use(Util<?> u) {
    u.printName();
}
```

### 一些细节

`T` 和 `E` 只能是引用类型。

```java
List<int> l = new List(); // 错误
```

在指定泛型具体类型后，可以传入该类型或者其子类类型。

```java
Animals<Frog> frog = new Animals<Frog>(new Frog());
Animals<Frog> tadpole = new Animals<Frog>(new Tadpole());

class Tadpole extends Frog {};
```

泛型可以**简写**。

```java
// 传统写法
A<Frog> frog = new A<Frog>(new Frog());
A<Frog> tadpole = new A<Frog>(new Tadpole());

// 简写，编译器自动推断
A<Frog> frog = new A<>(new Frog());
A<Frog> tadpole = new A<>(new Tadpole());
```

不写**泛型默认** `E = Object`。

```java
ArrayList arr = new ArrayList();
// 报错
for (People p : arr) {
    System.out.println(p);
}
```

**静态成员**中不能使用泛型；泛型方法可以是静态的。

```java
static T num; // 报错
public static void f(T num) {} // 报错
public static <T> void printArray(T[] array) {} // 正确
```

使用泛型的数组不能初始化。

```java
T[] arr = new T[10]; // 报错
```

泛型**没有继承性**。

```java
List<Object> l = new ArrayList<String>(); // 报错,必须一样
```



## Lambda 表达式

**Lambda 表达式**是一个匿名函数，它提供了一种清晰简洁的方式来表示一个方法接口。这是 Java 8 最重要的特性之一。

### 基本语法

```java
(parameters) -> expression
```

```java
(parameters) -> { statements; }
```

`parameters` 是参数列表，`expression` 或 `{ statements; }` 是Lambda 表达式的主体。如果只有一个参数，可以省略括号；如果没有参数，也需要空括号。

### 简单示例

```java
// 使用 Lambda 表达式计算两个数的和
MathOperation addition = (a, b) -> a + b;

// 调用 Lambda 表达式
int result = addition.operation(5, 3);
System.out.println("5 + 3 = " + result);
```

在上面的例子中，`MathOperation` 是一个**函数式接口**（只有一个抽象方法的接口），它包含一个抽象方法 `operation`，Lambda 表达式 **`(a, b) -> a + b`** 实现了这个抽象方法，表示对两个参数进行相加操作。

### 各种参数形式的 Lambda

```java
import java.util.function.*;

public class LambdaBasicForms {
    public static void main(String[] args) {
        // 1. 无参数
        Runnable noArgs = () -> System.out.println("Hello Lambda!");
        noArgs.run(); // Hello Lambda!

        // 2. 一个参数 (可省略括号)
        Function<String, Integer> oneArg = s -> s.length();
        System.out.println(oneArg.apply("Hello")); // 5

        // 3. 多个参数
        BiFunction<Integer, Integer, Integer> twoArgs = (a, b) -> a + b;
        System.out.println(twoArgs.apply(10, 20)); // 30

        // 4. 显式参数类型
        BiFunction<Integer, Integer, Integer> withTypes = (Integer a, Integer b) -> a * b;
        System.out.println(withTypes.apply(5, 6)); // 30

        // 5. 多行代码 (使用花括号)
        Function<String, String> multiLine = s -> {
            String trimmed = s.trim();
            return trimmed.toUpperCase();
        };
        System.out.println(multiLine.apply("  hello world  ")); // HELLO WORLD
    }
}
```

### 函数式接口

Lambda 表达式需要**函数式接口**（只有一个抽象方法的接口）。

#### 内置函数式接口

```java
import java.util.function.*;
import java.util.*;

public class FunctionalInterfaces {
    public static void main(String[] args) {
        // 1. Function<T, R> - 接受一个参数，返回一个结果
        Function<String, Integer> stringToInt = s -> Integer.parseInt(s);
        System.out.println(stringToInt.apply("123")); // 123

        // 2. Consumer<T> - 接受一个参数，没有返回值
        Consumer<String> printer = s -> System.out.println("消费: " + s);
        printer.accept("Hello"); // 消费: Hello

        // 3. Supplier<T> - 没有参数，返回一个结果
        Supplier<Double> randomSupplier = () -> Math.random();
        System.out.println("随机数: " + randomSupplier.get());

        // 4. Predicate<T> - 接受一个参数，返回boolean
        Predicate<String> isLong = s -> s.length() > 5;
        System.out.println(isLong.test("Hello")); // false
        System.out.println(isLong.test("Hello World")); // true

        // 5. BiFunction<T, U, R> - 接受两个参数，返回一个结果
        BiFunction<Integer, Integer, Integer> adder = (a, b) -> a + b;
        System.out.println(adder.apply(10, 20)); // 30
    }
}
```

#### 自定义函数式接口

```java
// 自定义函数式接口
@FunctionalInterface
interface StringProcessor {
    String process(String input);
    
    // 可以有默认方法
    default String defaultProcess(String input) {
        return process(input) + " (processed)";
    }
    
    // 可以有静态方法
    static StringProcessor createUpperCaseProcessor() {
        return s -> s.toUpperCase();
    }
}

public class CustomFunctionalInterface {
    public static void main(String[] args) {
        // 使用自定义函数式接口
        StringProcessor toUpper = s -> s.toUpperCase();
        StringProcessor toLower = s -> s.toLowerCase();
        StringProcessor repeater = s -> s.repeat(3);
        
        System.out.println(toUpper.process("hello")); // HELLO
        System.out.println(toLower.process("WORLD")); // world
        System.out.println(repeater.process("Java")); // JavaJavaJava
        
        // 使用默认方法
        System.out.println(toUpper.defaultProcess("test")); // TEST (processed)
        
        // 使用静态方法
        StringProcessor upper = StringProcessor.createUpperCaseProcessor();
        System.out.println(upper.process("lambda")); // LAMBDA
    }
}
```

### 方法引用

**方法引用**是 Lambda 表达式的一种简写形式，用于直接引用已有的方法。

```java
className::methodName
```

**方法引用的四种类型**：

| 类型                       | 语法                       | 等价 Lambda                               |
| :------------------------- | :------------------------- | :---------------------------------------- |
| 静态方法引用               | `Class::staticMethod`      | `(args) -> Class.staticMethod(args)`      |
| 实例方法引用               | `instance::instanceMethod` | `(args) -> instance.instanceMethod(args)` |
| 特定类型的任意对象方法引用 | `Class::instanceMethod`    | `(obj, args) -> obj.instanceMethod(args)` |
| 构造方法引用               | `Class::new`               | `() -> new Class()`                       |

```java
// 静态方法引用
Function<String, Integer> parser1 = Integer::parseInt;
System.out.println(parser1.apply("123")); // 123

// 实例方法引用
String prefix = "Hello, ";

Function<String, String> greeter = prefix::concat;
System.out.println(greeter.apply("World")); // Hello, World

// 特定类型的任意对象方法引用
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Function<String, Integer> lengthGetter = String::length; // 任意字符串的 length() 方法
names.stream()
    .map(String::length)
    .forEach(len -> System.out.print(len + " ")); // 5 3 7

// 构造方法引用
Supplier<List<String>> listSupplier = ArrayList::new;
List<String> list = listSupplier.get();
list.add("Hello");
System.out.println(list); // [Hello]
```





# 内置类



## Object

`Object`类是所有类的根类，位于`java.lang`包中。

### 常用方法

```java
// 示例类，实现Cloneable以支持clone()
class Person implements Cloneable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 重写toString
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }

    // 重写equals
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Person)) return false;
        Person other = (Person) obj;
        return this.name.equals(other.name) && this.age == other.age;
    }

    // 重写hashCode
    @Override
    public int hashCode() {
        return 31 * name.hashCode() + age;
    }

    // 重写clone
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

public class ObjectMethodsDemo {
    public static void main(String[] args) {
        try {
            // 创建测试对象
            Person p1 = new Person("Alice", 25);
            Person p2 = new Person("Alice", 25);
            Person p3 = new Person("Bob", 30);

            // 1. getClass()
            Class<?> clazz = p1.getClass(); // 获取对象的运行时类
            System.out.println("Class of p1: " + clazz.getName()); // 输出: Person

            // 2. hashCode()
            int hashCode = p1.hashCode(); // 获取对象的哈希码
            System.out.println("HashCode of p1: " + hashCode); // 输出: 哈希码（整数）

            // 3. equals(Object obj)
            boolean isEqual = p1.equals(p2); // 比较两个对象的内容是否相同 -> true
            System.out.println("Equals p2: " + isEqual); // 输出: true
            boolean notEqual = p1.equals(p3); // 比较不同对象 -> false
            System.out.println("Equals p3: " + notEqual); // 输出: false

            // 4. toString()
            String str = p1.toString(); // 获取对象的字符串表示
            System.out.println("toString of p1: " + str); // 输出: Person{name='Alice', age=25}

            // 5. clone()
            Person p1Clone = (Person) p1.clone(); // 创建p1的副本
            System.out.println("Cloned object: " + p1Clone); // 输出: Person{name='Alice', age=25}
            System.out.println("Clone equals p1: " + p1.equals(p1Clone)); // 输出: true

            // 6. wait() 和 notify()
            Object lock = new Object();
            Thread waiter = new Thread(() -> {
                synchronized (lock) {
                    try {
                        System.out.println("Thread waiting...");
                        lock.wait(); // 线程等待
                        System.out.println("Thread awakened");
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
            waiter.start();
            Thread.sleep(1000); // 确保waiter线程先运行
            synchronized (lock) {
                lock.notify(); // 唤醒等待的线程
                System.out.println("Notified waiting thread");
            }

        } catch (CloneNotSupportedException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

#### `equals()`

`Object` 类的 `equals()` 方法比较两个对象的引用地址（即是否是同一个对象）是否相同。

> 何时重写：
>
> - 需要基于内容比较相等性时（如自定义类）。如`String`，`Integer`...
> - 用于集合（如 HashSet、HashMap）时。

##### `==` vs `equals()`

| 特性         | ==                                     | equals()                                                     |
| ------------ | -------------------------------------- | ------------------------------------------------------------ |
| **类型**     | 关系运算符                             | Object 类的方法                                              |
| **适用对象** | 基本类型和引用类型                     | 仅适用于引用类型（对象）                                     |
| **默认行为** | 基本类型：比较值；引用类型：比较地址   | Object 默认实现：比较引用地址；**但许多类（如 String, Integer）重写了 equals() 以比较内容。** |
| **可自定义** | 不可重定义                             | **可重写**自定义内容比较逻辑                                 |
| **典型用途** | 检查对象是否为同一实例或基本类型值相等 | 检查是否为同一对象；检查对象的内容是否逻辑上相等             |

###### `==`

`==`可以比较基本类型和引用类型。

```java
// 1.
class Parent;
class Child extends Parent;
Child c = new Child();
Child c1 = c;
Parent p = c;
c == c1;	// true
c == p;		// true

// 2.
int a = 5; 
int b = 5; 
a == b; // true（值相等） 

Integer i1 = new Integer(1000);
Integer i2 = new Integer(1000);
i1 == i2; // false（不同对象，地址不同）

// 3.
String s1 = new String("Hello"); 
String s2 = new String("Hello"); 
s1 == s2; // false（不同对象，地址不同）
```

###### `equals()`

`equals()`仅适用于引用类型（对象）。

```java
// 1.
class Parent;
class Child extends Parent;
Child c = new Child();

Child c1 = c;
Parent p = c;

c.equals(c1);	// true
c.equals(p);	// true

// 2.
int i1 = 1;
int i2 = 2;
i1.equals(i2); // 基本类型，不能比较

Integer i1 = new Integer(1);
Integer i2 = new Integer(2);
i1.equals(i2); // false（内容不同）

// 3.
String s1 = new String("Hello"); 
String s2 = new String("Hello"); 
s1.equals(s2); // true（内容相同）
```

以下是部分类`equals`的源码。

```java
// 1. Object.java
public boolean equals(Object obj) {
    return (this == obj);
}
// 2. String.java
public boolean equals(Object anObject) {
	if (this == anObject) {
	    return true;
	}
	return (anObject instanceof String aString)
	        && (!COMPACT_STRINGS || this.coder == aString.coder)
	        && StringLatin1.equals(value, aString.value);
}
// 3. Integer.java
public boolean equals(Object obj) {
    if (obj instanceof Integer) {
        return value == ((Integer)obj).intValue();
    }
    return false;
}
```

#### `hashCode()`

`Object` 类中的 `hashCode()` 方法，用于返回对象的哈希码，即一个整数值，通常用于哈希表（如 `HashMap`、`HashSet`）等数据结构中，以优化对象的存储和查找。

> 何时重写：
>
> 重写 `equals()` 后，必须同时重写 `hashCode()`，确保相等对象有相同哈希码。

##### hashCode() 的作用

- 性能优化：

    - 在哈希表中，`hashCode()` 确定对象存储的桶位置。哈希码相等的对象会被放入同一个桶，减少查找范围。减少哈希冲突（不同对象映射到同一桶），提高哈希表性能。

    - 示例：`HashMap` 使用 `key.hashCode()` 计算键的存储位置。

- 对象比较：

    - 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的。**不同对象哈希值不一样**。

```java
A a1 = new A();
A a2 = new A();
A a3 = a1;

a1.hashCode() == a2.hashCode(); // false
a1.hashCode() == a3.hashCode(); // true
```

#### `toString()`

`Object` 类中的 `toString()` 方法，用于返回对象的字符串表示，返回格式为 `getClass().getName() + "@" + Integer.toHexString(hashCode())` 表示类名（包括包名）+ `@` + 哈希码的十六进制表示。

> 何时重写：
>
> - 当需要以人类可读的方式展示对象内容时。如`String`，`Integer`...

```java
Object obj = new Object();
System.out.println(obj.toString()); // 输出: java.lang.Object@15db9742
System.out.println(obj); // 默认调用toString()
```

#### `getClass`

`getClass()` 是 `Object` 类的一个方法，它返回当前对象的**运行类型**。这是一个 `Class` 类型的对象。

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();
        
        // 输出 Dog 类的类型
        System.out.println(myAnimal.getClass().getName()); // java.lang.Dog
    }
}
```



## 包装类

**包装类**（Wrapper Classes）是将基本数据类型（如int、double等）封装成对象的类，位于`java.lang`包中。

包装类是`final`且不可变的（`immutable`），类似`String`。对应关系如下：

| 基本类型 | 包装类    |
| -------- | --------- |
| byte     | Byte      |
| short    | Short     |
| int      | Integer   |
| long     | Long      |
| float    | Float     |
| double   | Double    |
| char     | Character |
| boolean  | Boolean   |

### 继承关系

![image-20250514150856341](images/image-20250514150856341.png)

![image-20250514150808745](images/image-20250514150808745.png)

![image-20250514150628391](images/image-20250514150628391.png)

### 包装类与基本数据转换

这里以`Integer`与`int`转换为例，

```java
// 手动装箱与拆箱.（jdk5之前）
int num = 5;
Integer integer1 = new Integer(num);
Integer integer2 = Integer.valueOf(num);

int i = integer1.intValue();

// 自动装箱与拆箱
int num = 5;
Integer integer3 = num;
int i = integer3;
```

#### Integer 缓存机制

```java
Integer a = 1;
Integer b = 1;
System.out.println(a == b); // 输出什么？true

Integer a = 128;
Integer b = 128;
System.out.println(a == b); // 输出什么？false
```

`Integer` 类内部通过 `Integer.IntegerCache` 缓存了值在 -128 到 127 范围内的 `Integer` 对象。这是 Java 的优化机制，减少对象创建。

当调用 `Integer.valueOf(1)` 时，会返回缓存中的同一个 Integer 对象（因为 1 在缓存范围内）。因此，`a` 和 `b` 引用的是**同一个 Integer 对象**。

### 包装类与 `String` 转换

这里以`Integer`与`String`转换为例，

```java
Integer i = 100;
String str1 = i + "";
String str2 = i.toString;
String str3 = String.valueOf(i);

String str = "12345";
Integer i1 = Integer.parseInt(str);
Integer i2 = new Ingeter(str);
```



## String

![image-20250514181050036](images/image-20250514181050036.png)

### 创建 `String` 对象

```java
// 1.直接创建
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
// 2.对象创建
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建

public class StringDemo {
    public static void main(String args[]) {     
        String string1 = "菜鸟教程网址：";     
        System.out.println("1、" + string1 + "www.runoob.com");  
    }
}
```

**直接创建**是先从常量池查看是否有`“Runoob”`数据空间，如果没有则创建并指向，如果有则直接指向。最终指向的是常量池的空间地址。

**对象创建**是先在堆中创建空间，里面的`value`属性指向常量池的`“Runoob”`数据空间。如果常量池没有，则先在常量池创建。

![image-20250312210526289](images/image-20250312210526289.png)

> **注意:**String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了（详看笔记部分解析）。

### 常用方法

```java
public class StringMethodsExample {
    public static void main(String[] args) {
        String str = "Hello World";
        String strObj = new String("Hello World");

        // 1. length()
        int length = str.length();  // 返回字符串的长度（字符数） -> 11
        System.out.println("Length: " + length);

        // 2. charAt(int index)
        char ch = str.charAt(1);  // 返回指定索引位置的字符 -> 'e'
        System.out.println("Character at index 1: " + ch);

        // 3. substring(int beginIndex, int endIndex)
        String sub = str.substring(0, 5);  // 返回从指定索引开始到指定结束索引（不包括 endIndex）的子字符串 -> "Hello"
        System.out.println("Substring (0, 5): " + sub);

        // 4. indexOf(String str, int fromIndex)
        int index = str.indexOf("l");  // 返回指定子字符串首次出现的索引位置 -> 2
        System.out.println("Index of 'l': " + index);

        // 7. lastIndexOf(String str)
        int lastIndex = str.lastIndexOf("l");  // 返回指定子字符串最后一次出现的索引位置 -> 9
        System.out.println("Last index of 'l': " + lastIndex);

        // 8. equals(Object obj)
        boolean isEqual = str.equals("Hello World");  // 比较两个字符串的内容是否相同 -> true
        System.out.println("Equals 'Hello World': " + isEqual);

        // 9. equalsIgnoreCase(String anotherString)
        boolean isEqualIgnoreCase = str.equalsIgnoreCase("hello world");  // 比较两个字符串的内容是否相同，忽略大小写 -> true
        System.out.println("EqualsIgnoreCase 'hello world': " + isEqualIgnoreCase);

        // 10. toLowerCase()
        String lower = str.toLowerCase();  // 返回将字符串转换为小写字母后的新字符串 -> "hello world"
        System.out.println("Lowercase: " + lower);

        // 11. toUpperCase()
        String upper = str.toUpperCase();  // 返回将字符串转换为大写字母后的新字符串 -> "HELLO WORLD"
        System.out.println("Uppercase: " + upper);

        // 12. trim()
        String trimmed = "  Hello World  ".trim();  // 返回删除前后空白字符的新字符串 -> "Hello World"
        System.out.println("Trimmed: '" + trimmed + "'");

        // 13. replace(char oldChar, char newChar)
        String replaced = str.replace('l', 'p');  // 替换字符串中所有指定字符的出现 -> "Heppo Word"
        System.out.println("Replaced 'l' with 'p': " + replaced);

        // 14. replace(String target, String replacement)
        String replacedWord = str.replace("World", "Java");  // 替换字符串中所有指定子字符串的出现 -> "Hello Java"
        System.out.println("Replaced 'World' with 'Java': " + replacedWord);

        // 15. split(String regex)
        String[] fruits = "apple,banana,orange".split(",");  // 根据指定的正则表达式分割字符串，返回一个字符串数组 -> ["apple", "banana", "orange"]
        System.out.print("Split fruits: ");
        for (String fruit : fruits) {
            System.out.print(fruit + " ");
        }
        System.out.println();

        // 16. startsWith(String prefix)
        boolean starts = str.startsWith("Hello");  // 判断字符串是否以指定的前缀开始 -> true
        System.out.println("Starts with 'Hello': " + starts);

        // 17. endsWith(String suffix)
        boolean ends = str.endsWith("World");  // 判断字符串是否以指定的后缀结尾 -> true
        System.out.println("Ends with 'World': " + ends);

        // 18. contains(CharSequence sequence)
        boolean contains = str.contains("lo");  // 判断字符串是否包含指定的子字符串 -> true
        System.out.println("Contains 'lo': " + contains);

        // 19. format(String format, Object... args)
        String formatted = String.format("Hello %s", "Java");  // 使用指定的格式字符串和参数返回格式化后的字符串 -> "Hello Java"
        System.out.println("Formatted: " + formatted);

        // 20. valueOf(int i)
        int num = 123;
        String numStr = String.valueOf(num);  // 将整数转换为字符串 -> "123"
        System.out.println("Value of num: " + numStr);

        // 21. join(CharSequence delimiter, CharSequence... elements)
        String joined = String.join(", ", "Apple", "Banana", "Orange");  // 用指定的分隔符连接多个字符串元素 -> "Apple, Banana, Orange"
        System.out.println("Joined fruits: " + joined);

        // 22. matches(String regex)
        boolean isMatch = "12345".matches("\\d+");  // 判断字符串是否与指定的正则表达式匹配 -> true
        System.out.println("Matches '\\d+': " + isMatch);
        
        // 23. intern()
        boolean isEqual = (str == strObj.intern());  // 将字符串对象放入字符串常量池（String Constant Pool）中，或者返回常量池中已存在的相同内容的字符串的引用。 -> true
        System.out.println(isEqual);
    }
}
```



## StringBuffer

`StringBuffer` 是一个可变的字符串类，用于处理需要频繁修改的字符串操作。

与 `String` 不同，`StringBuffer` 的内容可以动态改变，而不会每次修改都创建新的对象。

![image-20250514185500399](images/image-20250514185500399.png)

实际上，`StringBuffer`继承了父类`AbstractStringBuilder`，而字符串是储存在**父类的字段**中，并且字段没有`final`修饰，所以存储在**堆**中。

```java
abstract sealed class AbstractStringBuilder implements Appendable, CharSequence
    permits StringBuilder, StringBuffer {
    /**
     * The value is used for character storage.
     */
    byte[] value; // 不是final
}
```

### 创建 `StringBuffer` 对象

```java
// 1.创建一个空的 StringBuffer，初始容量为 16
StringBuffer();
// 2.指定初始容量
StringBuffer(int capacity);
// 3.包含指定字符串
StringBuffer(String str);
```

###  `StringBuffer` 与 `String` 转换

```java
// StringBuffer -> String
StringBuffer sb = new StringBuffer("test");
// 1.
String s = sb.toString();
// 2.
String s = new String(sb);

// String -> StringBuffer
String s = "test";
// 1.
StringBuffer sb = new StringBuffer(s);
// 2.
StringBuffer sb = new StringBuffer();
sb.append(s);
```

### 常用方法

```java
public class StringBufferMethodsExample {
    public static void main(String[] args) {
        // 初始化 StringBuffer 对象
        StringBuffer sb = new StringBuffer("Hello World");

        // 1. append(String str)
        sb.append("!");  // 在字符串末尾追加内容 -> "Hello World!"
        System.out.println("After append: " + sb);

        // 2. insert(int offset, String str)
        sb.insert(5, ",");  // 在指定索引位置插入字符串 -> "Hello, World!"
        System.out.println("After insert: " + sb);

        // 3. delete(int start, int end)
        sb.delete(5, 6);  // 删除指定范围的字符（start 包括，end 不包括） -> "Hello World!"
        System.out.println("After delete: " + sb);

        // 4. replace(int start, int end, String str)
        sb.replace(6, 11, "Java");  // 替换指定范围的字符为新字符串 -> "Hello Java!"
        System.out.println("After replace: " + sb);

        // 5. reverse()
        sb.reverse();  // 反转整个字符串 -> "!avaJ olleH"
        System.out.println("After reverse: " + sb);

        // 6. setCharAt(int index, char ch)
        sb.setCharAt(0, '@');  // 修改指定索引位置的字符 -> "@avaJ olleH"
        System.out.println("After setCharAt: " + sb);

        // 7. charAt(int index)
        char ch = sb.charAt(1);  // 获取指定索引位置的字符 -> 'a'
        System.out.println("Character at index 1: " + ch);

        // 8. substring(int start, int end)
        String sub = sb.substring(1, 5);  // 提取指定范围的子字符串 -> "avaJ"
        System.out.println("Substring (1, 5): " + sub);

        // 9. length()
        int length = sb.length();  // 返回字符串的长度（字符数） -> 11
        System.out.println("Length: " + length);

        // 10. capacity()
        int capacity = sb.capacity();  // 返回当前缓冲区的容量 -> 27（初始 16 + "Hello World".length()）
        System.out.println("Capacity: " + capacity);

        // 11. indexOf(String str)
        int index = sb.indexOf("a");  // 返回指定子字符串首次出现的索引位置 -> 1
        System.out.println("Index of 'a': " + index);

        // 12. lastIndexOf(String str)
        int lastIndex = sb.lastIndexOf("a");  // 返回指定子字符串最后一次出现的索引位置 -> 3
        System.out.println("Last index of 'a': " + lastIndex);

        // 13. toString()
        String result = sb.toString();  // 将 StringBuffer 转换为 String -> "@avaJ olleH"
        System.out.println("To String: " + result);

        // 14. ensureCapacity(int minimumCapacity)
        sb.ensureCapacity(50);  // 确保缓冲区容量至少为 50
        System.out.println("Capacity after ensureCapacity: " + sb.capacity()); // 输出新容量（可能 >= 50）

        // 15. setLength(int newLength)
        sb.setLength(5);  // 设置字符串长度，截断或填充空字符 -> "@avaJ"
        System.out.println("After setLength(5): " + sb);
    }
}
```



## StringBuilder

`StringBuilder` 是一个可变的字符串类，用于高效处理需要频繁修改的字符串操作。

它与 `StringBuffer` 类似，但主要区别在于 `StringBuilder` 的方法没有做互斥的处理，即没有`synchronized`关键字。

它是**非线程安全**的，因此只能在**单线程环境**中使用。

![image-20250514195215956](images/image-20250514195215956.png)

### 与 `String` 和 `StringBuffer` 的对比

| 特性         | String                       | StringBuffer               | StringBuilder              |
| ------------ | ---------------------------- | -------------------------- | -------------------------- |
| **可变性**   | 不可变（每次修改创建新对象） | 可变                       | 可变                       |
| **线程安全** | 线程安全（不可变性保证）     | 线程安全（同步方法）       | 非线程安全                 |
| **性能**     | 低（频繁修改时）             | 中等（同步开销）           | 高（无同步开销）           |
| **使用场景** | 字符串内容固定               | 多线程环境，频繁修改字符串 | 单线程环境，频繁修改字符串 |



## Character

| 序号 | 方法与描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [isLetter()](https://www.runoob.com/java/character-isletter.html) 是否是一个字母 |
| 2    | [isDigit()](https://www.runoob.com/java/character-isdigit.html) 是否是一个数字字符 |
| 3    | [isWhitespace()](https://www.runoob.com/java/character-iswhitespace.html) 是否是一个空白字符 |
| 4    | [isUpperCase()](https://www.runoob.com/java/character-isuppercase.html) 是否是大写字母 |
| 5    | [isLowerCase()](https://www.runoob.com/java/character-islowercase.html) 是否是小写字母 |
| 6    | [toUpperCase()](https://www.runoob.com/java/character-touppercase.html) 指定字母的大写形式 |
| 7    | [toLowerCase](https://www.runoob.com/java/character-tolowercase.html)() 指定字母的小写形式 |
| 8    | [toString](https://www.runoob.com/java/character-tostring.html)() 返回字符的字符串形式，字符串的长度仅为1 |
| 9    | forDigit() 将数字（指定基数）转换为相应的字符。              |
| 10   | digit() 将字符转换为数字，基于给定的基数。                   |

### 常用方法

```java
public class CharacterMethodsExample {
    public static void main(String[] args) {
        char ch1 = 'A';
        char ch2 = 'a';
        char ch3 = '5';
        char ch4 = ' ';

        // 1. isLetter() 示例
        System.out.println(Character.isLetter(ch1));  // 输出: true

        // 2. isDigit() 示例
        System.out.println(Character.isDigit(ch3));  // 输出: true

        // 3. isWhitespace() 示例
        System.out.println(Character.isWhitespace(ch4));  // 输出: true

        // 4. isUpperCase() 示例
        System.out.println(Character.isUpperCase(ch1));  // 输出: true

        // 5. isLowerCase() 示例
        System.out.println(Character.isLowerCase(ch2));  // 输出: true

        // 6. toUpperCase() 示例
        System.out.println(Character.toUpperCase(ch2));  // 输出: A

        // 7. toLowerCase() 示例
        System.out.println(Character.toLowerCase(ch1));  // 输出: a

        // 8. toString() 示例
        System.out.println(Character.toString(ch1));  // 输出: "A"
        
        // 9. forDigit() 示例
        System.out.println(Character.forDigit(10, 16)); // 输出: 'A' （十六进制中的 10 对应 A）

        // 10. digit() 示例
        System.out.println(Character.digit('A', 16)); // 输出: 10 （'A' 对应十六进制的 10）
    }
}

```

### 转义序列

前面有反斜杠（\）的字符代表转义字符，它对编译器来说是有特殊含义的。

下面列表展示了Java的转义序列：

| 转义序列 | 描述                     |
| :------- | :----------------------- |
| \t       | 在文中该处插入一个tab键  |
| \b       | 在文中该处插入一个后退键 |
| \n       | 在文中该处换行           |
| \r       | 在文中该处插入回车       |
| \f       | 在文中该处插入换页符     |
| \'       | 在文中该处插入单引号     |
| \"       | 在文中该处插入双引号     |
| \\       | 在文中该处插入反斜杠     |





## Number

| 序号 | 方法与描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [xxxValue()](https://www.runoob.com/java/number-xxxvalue.html) 将 Number 对象转换为xxx数据类型的值并返回。 |
| 2    | [compareTo()](https://www.runoob.com/java/number-compareto.html) 将number对象与参数比较。 |
| 3    | [equals()](https://www.runoob.com/java/number-equals.html) 判断number对象是否与参数相等。 |
| 4    | [valueOf()](https://www.runoob.com/java/number-valueof.html) 返回一个 Number 对象指定的内置数据类型 |
| 5    | [toString()](https://www.runoob.com/java/number-tostring.html) 以字符串形式返回值。 |
| 6    | [parseInt()](https://www.runoob.com/java/number-parseInt.html) 将字符串解析为int类型。 |

### 常用方法

```java
public class NumberMethodsExample {
    public static void main(String[] args) {
        Number num1 = new Integer(42);
        Number num2 = new Double(42.42);

        // 1. xxxValue() 示例
        System.out.println(num1.intValue());   // 输出: 42
        System.out.println(num2.doubleValue()); // 输出: 42.42

        // 2. compareTo() 示例
        System.out.println(num1.compareTo(40));   // 输出: 1 (num1 大于 40)
        System.out.println(num2.compareTo(42.42)); // 输出: 0 (相等)

        // 3. equals() 示例
        System.out.println(num1.equals(42));  // 输出: true
        System.out.println(num2.equals(42.43)); // 输出: false

        // 4. valueOf() 示例
        Integer intObj = Integer.valueOf("100");
        System.out.println(intObj);  // 输出: 100

        // 5. toString() 示例
        System.out.println(num1.toString());  // 输出: 42
        System.out.println(num2.toString());  // 输出: 42.42

        // 6. parseInt() 示例 (此方法为 Integer 类中的方法)
        int parsedValue = Integer.parseInt("123");
        System.out.println(parsedValue);  // 输出: 123
    }
}

```



## BigInteger

`BigInteger` 类位于 `java.math` 包中，用于处理任意精度的整数运算，特别适合需要处理超出 `long` 类型范围的超大整数的场景。

### 创建 `BigInteger` 对象

```java
// 1. BigInteger(String val)：从字符串表示的十进制数创建对象。
BigInteger num = new BigInteger("12345678901234567890");

// 2. BigInteger(String val, int radix)：从指定进制（2-36）的字符串创建对象。
BigInteger num = new BigInteger("FF", 16); // 十六进制 FF = 255

// 3. BigInteger.valueOf(long val)：从 long 值创建 BigInteger。
BigInteger num = BigInteger.valueOf(123);
```

### 常用方法

```java
import java.math.BigInteger;

public class BigIntegerMethodsExample {
    public static void main(String[] args) {
        // 初始化 BigInteger 对象
        BigInteger num1 = new BigInteger("12345678901234567890");
        BigInteger num2 = BigInteger.valueOf(100);

        // 1. add(BigInteger val)
        BigInteger sum = num1.add(num2);  // 相加 -> 12345678901234567990
        System.out.println("After add: " + sum);

        // 2. subtract(BigInteger val)
        BigInteger difference = num1.subtract(num2);  // 相减 -> 12345678901234567790
        System.out.println("After subtract: " + difference);

        // 3. multiply(BigInteger val)
        BigInteger product = num1.multiply(num2);  // 相乘 -> 1234567890123456789000
        System.out.println("After multiply: " + product);

        // 4. divide(BigInteger val)
        BigInteger quotient = num1.divide(num2);  // 相除（整除） -> 123456789012345678
        System.out.println("After divide: " + quotient);

        // 5. mod(BigInteger val)
        BigInteger mod = num1.mod(BigInteger.TEN);  // 取模 -> 0
        System.out.println("After mod 10: " + mod);

        // 6. pow(int exponent)
        BigInteger power = num2.pow(3);  // 幂运算 -> 100^3 = 1000000
        System.out.println("100^3: " + power);

        // 7. compareTo(BigInteger val)
        int comparison = num1.compareTo(num2);  // 比较大小 -> 1（num1 > num2）
        System.out.println("Compare num1 to num2: " + comparison);

        // 8. abs()
        BigInteger negative = new BigInteger("-123");
        BigInteger absValue = negative.abs();  // 取绝对值 -> 123
        System.out.println("Absolute value of -123: " + absValue);

        // 9. gcd(BigInteger val)
        BigInteger a = new BigInteger("48");
        BigInteger b = new BigInteger("36");
        BigInteger gcd = a.gcd(b);  // 最大公约数 -> 12
        System.out.println("GCD of 48 and 36: " + gcd);

        // 10. toString()
        String str = num1.toString();  // 转换为十进制字符串 -> "12345678901234567890"
        System.out.println("To String: " + str);

        // 11. toString(int radix)
        String hexStr = num2.toString(16);  // 转换为十六进制字符串 -> "64"
        System.out.println("100 in hex: " + hexStr);

        // 12. shiftLeft(int n)
        BigInteger shifted = num2.shiftLeft(2);  // 左移 2 位 -> 100 << 2 = 400
        System.out.println("100 shift left 2: " + shifted);

        // 13. and(BigInteger val)
        BigInteger x = new BigInteger("10");  // 1010 in binary
        BigInteger y = new BigInteger("12");  // 1100 in binary
        BigInteger andResult = x.and(y);  // 按位与 -> 1000 (8)
        System.out.println("10 AND 12: " + andResult);

        // 14. isProbablePrime(int certainty)
        BigInteger primeTest = new BigInteger("17");
        boolean isPrime = primeTest.isProbablePrime(10);  // 测试是否可能是素数 -> true
        System.out.println("Is 17 probably prime? " + isPrime);

        // 15. signum()
        int sign = num1.signum();  // 返回符号 -> 1（正数）
        System.out.println("Signum of num1: " + sign);
    }
}
```



## BigDecimal

`BigDecimal` 类位于 `java.math` 包中，用于高精度小数运算，特别适合金融、科学计算等需要精确控制精度的场景。

### 创建 `BigDecimal` 对象

```java
// 1. BigDecimal.valueOf(double val)
BigDecimal num = BigDecimal.valueOf(0.1);
System.out.println("From valueOf(double): " + num); // 输出: 0.1

// 2. 使用 String 构造
BigDecimal fromString = new BigDecimal("123.456789");

// 3. 使用静态常量
BigDecimal zero = BigDecimal.ZERO;
BigDecimal one = BigDecimal.ONE;
BigDecimal ten = BigDecimal.TEN;
```

### 常用方法

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class BigDecimalMethodsExample {
    public static void main(String[] args) {
        // 初始化 BigDecimal 对象
        BigDecimal num1 = new BigDecimal("1234567890.1234567890");
        BigDecimal num2 = new BigDecimal("100.50");

        // 1. add(BigDecimal augend)
        BigDecimal sum = num1.add(num2);  // 相加 -> 1234567990.6234567890
        System.out.println("After add: " + sum);

        // 2. subtract(BigDecimal subtrahend)
        BigDecimal difference = num1.subtract(num2);  // 相减 -> 1234567789.6234567890
        System.out.println("After subtract: " + difference);

        // 3. multiply(BigDecimal multiplicand)
        BigDecimal product = num1.multiply(num2);  // 相乘 -> 123580245813.7037039445225
        System.out.println("After multiply: " + product);

        // 4. divide(BigDecimal divisor, int scale, RoundingMode roundingMode)
        BigDecimal quotient = num1.divide(num2, 4, RoundingMode.HALF_UP);  // 相除，保留4位小数，四舍五入 -> 12282865.5626
        System.out.println("After divide: " + quotient);

        // 5. remainder(BigDecimal divisor)
        BigDecimal remainder = num1.remainder(num2);  // 取余 -> 90.1234567890
        System.out.println("After remainder: " + remainder);

        // 6. pow(int n)
        BigDecimal power = num2.pow(2);  // 幂运算 -> 100.50^2 = 10100.25
        System.out.println("100.50^2: " + power);

        // 7. compareTo(BigDecimal val)
        int comparison = num1.compareTo(num2);  // 比较大小 -> 1（num1 > num2）
        System.out.println("Compare num1 to num2: " + comparison);

        // 8. abs()
        BigDecimal negative = new BigDecimal("-123.45");
        BigDecimal absValue = negative.abs();  // 取绝对值 -> 123.45
        System.out.println("Absolute value of -123.45: " + absValue);

        // 9. setScale(int newScale, RoundingMode roundingMode)
        BigDecimal scaled = num1.setScale(2, RoundingMode.HALF_UP);  // 设置小数位数为2，四舍五入 -> 1234567890.12
        System.out.println("After setScale(2): " + scaled);

        // 10. toString()
        String str = num1.toString();  // 转换为字符串 -> "1234567890.1234567890"
        System.out.println("To String: " + str);

        // 11. stripTrailingZeros()
        BigDecimal withZeros = new BigDecimal("123.45000");
        BigDecimal stripped = withZeros.stripTrailingZeros();  // 去除尾部零 -> 123.45
        System.out.println("After stripTrailingZeros: " + stripped);

        // 12. movePointLeft(int n)
        BigDecimal movedLeft = num2.movePointLeft(2);  // 小数点左移2位 -> 1.0050
        System.out.println("100.50 move point left 2: " + movedLeft);

        // 13. movePointRight(int n)
        BigDecimal movedRight = num2.movePointRight(2);  // 小数点右移2位 -> 10050.00
        System.out.println("100.50 move point right 2: " + movedRight);

        // 14. max(BigDecimal val)
        BigDecimal max = num1.max(num2);  // 返回较大值 -> 1234567890.1234567890
        System.out.println("Max of num1 and num2: " + max);

        // 15. signum()
        int sign = num1.signum();  // 返回符号 -> 1（正数）
        System.out.println("Signum of num1: " + sign);
    }
}
```





## Arrays 工具类

`Arrays` 类是 `java.util` 包中的一个实用工具类，提供了大量静态方法来操作数组，包括排序、搜索、比较、填充、复制等操作。

### 常用方法

以下是 `java.util.Arrays` 类的主要方法及其使用示例。

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.IntStream;

public class ArraysMethodsExample {
    public static void main(String[] args) {
        // 1. 创建测试数组
        int[] intArray = {5, 2, 8, 1, 6};
        int[] intArray2 = {1, 2, 3, 4, 5};
        int[] intArrayCopy = new int[5];
        String[] strArray = {"banana", "apple", "orange", "grape"};
        int[][] deepArray1 = {{1, 2}, {3, 4}};
        int[][] deepArray2 = {{1, 2}, {3, 4}};
        
        // 2. toString(array) 打印原始数组
        System.out.println("原始int数组: " + Arrays.toString(intArray)); // [5, 2, 8, 1, 6]
        System.out.println("原始str数组: " + Arrays.toString(strArray)); // [banana, apple, orange, grape]
        
        // 3. Arrays.sort(array) 排序方法
        Arrays.sort(intArray); // 基本类型快速排序（默认升序）
        System.out.println("排序后int数组: " + Arrays.toString(intArray));
        
        Arrays.sort(strArray); // 对象类型归并排序
        System.out.println("排序后str数组: " + Arrays.toString(strArray));
        
        // Arrays.sort(array[, order])自定义排序
        Arrays.sort(strArray, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                Integer i1 = (Integer) o1;
                Integer i2 = (Integer) o2;
                return i2 - i1; // 
            }
        }); // 实现了Comparator接口的匿名内部类，要求实现compare方法。
        System.out.println("逆序排序str数组: " + Arrays.toString(strArray));
        
        Arrays.sort(strArray, Comparator.reverseOrder());
        System.out.println("逆序排序str数组: " + Arrays.toString(strArray));
        
        
        // 4. Arrays.binarySearch(array, target) 二分查找（必须先排序）
        int index = Arrays.binarySearch(intArray, 5);
        System.out.println("数字5的索引位置: " + index);
        
        // 5. Arrays.equals(arr1, arr2) 比较方法
        boolean isEqual = Arrays.equals(intArray, intArray2);
        System.out.println("数组是否相等: " + isEqual);
        
        boolean isDeepEqual = Arrays.deepEquals(deepArray1, deepArray2);
        System.out.println("多维数组是否深度相等: " + isDeepEqual);
        
        // 6. Arrays.fill(array, item) 填充方法
        Arrays.fill(intArrayCopy, 10);
        System.out.println("填充后的数组: " + Arrays.toString(intArrayCopy));
        
        // 7. Arrays.copyOf(array, num) 复制方法
        int[] copiedArray = Arrays.copyOf(intArray, 3);
        System.out.println("复制前3个元素: " + Arrays.toString(copiedArray));
        
        int[] rangeCopied = Arrays.copyOfRange(intArray, 1, 4);
        System.out.println("复制1-4索引元素: " + Arrays.toString(rangeCopied));
        
        // 8. Arrays.deepToString(array) 转换为字符串
        System.out.println("多维数组字符串表示: " + Arrays.deepToString(deepArray1));
        
        // 9. Arrays.deepHashCode(array) 哈希码方法
        int hashCode = Arrays.hashCode(intArray);
        System.out.println("数组哈希码: " + hashCode);
        
        int deepHashCode = Arrays.deepHashCode(deepArray1);
        System.out.println("多维数组深度哈希码: " + deepHashCode);
        
        // 10. 流操作 (Java 8+)
        IntStream stream = Arrays.stream(intArray);
        System.out.print("数组流中的元素: ");
        stream.forEach(n -> System.out.print(n + " "));
        System.out.println();
        
        // 11. 并行前缀计算 (Java 8+)
        int[] prefixArray = {1, 2, 3, 4, 5};
        Arrays.parallelPrefix(prefixArray, (a, b) -> a + b);
        System.out.println("并行前缀求和结果: " + Arrays.toString(prefixArray));
        
        // 12. 并行排序
        int[] bigArray = new int[10000];
        Arrays.setAll(bigArray, i -> (int)(Math.random() * 10000));
        Arrays.parallelSort(bigArray);
        System.out.println("前10个并行排序结果: " + Arrays.toString(Arrays.copyOf(bigArray, 10)));
        
        // 13. Arrays.setAll(array, callback) 设置所有元素 (Java 8+)
        Arrays.setAll(intArrayCopy, i -> i * 2);
        System.out.println("设置所有元素后的数组: " + Arrays.toString(intArrayCopy));
        
        // 14. 转换为List (注意返回的是固定大小的List)
        List<String> list = Arrays.asList(strArray);
        System.out.println("转换为List: " + list);
        
        // 15. 不匹配索引 (Java 9+)
        int mismatch = Arrays.mismatch(intArray, intArray2);
        System.out.println("第一个不匹配的索引: " + mismatch);
        
        // 16. 比较无符号 (Java 9+)
        int[] unsignedCompare1 = {0, 1, 2};
        int[] unsignedCompare2 = {0, 1, -2};
        int unsignedResult = Arrays.compareUnsigned(unsignedCompare1, unsignedCompare2);
        System.out.println("无符号比较结果: " + unsignedResult);
    }
}
```



## Math 工具类

在 Java 中，`Math` 类是一个提供了多种数学运算的方法的工具类，它位于 `java.lang` 包中。该类是 **不可实例化** 的，即不能通过 `new Math()` 来创建对象，所有方法都是静态的，直接通过类名调用。

### 常量

1. **`Math.PI`**

    - **定义**：表示圆周率 π，约等于 3.14159。
    - **用途**：常用于与圆形、周期性运动等相关的数学计算。

    **示例**：

    ```java
    System.out.println(Math.PI);  // 输出 3.141592653589793
    ```

2. **`Math.E`**

    - **定义**：表示自然对数的底数 e，约等于 2.71828。
    - **用途**：在指数运算、对数运算等数学公式中广泛使用。

    **示例**：

    ```java
    System.out.println(Math.E);  // 输出 2.718281828459045
    ```

### 常用方法

```java
// 1. 绝对值: Math.abs(double a)
System.out.println(Math.abs(-5));  // 输出: 5

// 2. 最大值: Math.max(int a, int b)
System.out.println(Math.max(10, 20));  // 输出: 20

// 3. 最小值: 
System.out.println(Math.min(10, 20));  // 输出: 10

// 4. 平方根: Math.sqrt(double a)
System.out.println(Math.sqrt(16));  // 输出: 4.0

// 5. 次方: Math.pow(double a, double b)
System.out.println(Math.pow(2, 3));  // 输出: 8.0

// 6. 随机数: Math.round(double a) 返回一个介于0.0（包括）和1.0（不包括）之间的随机数。
System.out.println(Math.random());  // 输出: 一个0到1之间的随机数

// 7. 四舍五入: 返回四舍五入后的最接近整数（long类型）。
System.out.println(Math.round(3.6));  // 输出: 4

// 8. 向上取整: Math.ceil(double a)
System.out.println(Math.ceil(3.1));  // 输出: 4.0

// 9. 向下取整: Math.floor(double a)
System.out.println(Math.floor(3.9));  // 输出: 3.0

// 10. 弧度转角度
System.out.println(Math.toDegrees(Math.PI));  // 输出: 180.0

// 11. 角度转弧度
System.out.println(Math.toRadians(180));  // 输出: 3.141592653589793

// 12. 正弦: Math.sin(double a)
System.out.println(Math.sin(Math.toRadians(30)));  // 输出: 0.49999999999999994

// 13. 余弦
System.out.println(Math.cos(Math.toRadians(60)));  // 输出: 0.5

// 14. 正切
System.out.println(Math.tan(Math.toRadians(45)));  // 输出: 1.0

// 15. 自然对数: Math.log(double a)
System.out.println(Math.log(Math.E));  // 输出: 1.0

// 16. 以10为底的对数
System.out.println(Math.log10(100));  // 输出: 2.0

```





## System

`System` 类是 `java.lang` 包中的一个核心类，提供了与系统相关的功能，包括标准输入输出、环境变量、系统属性、当前时间、数组复制、垃圾回收等。

`System` 类是 `final` 的，不能被继承，且其构造方法是私有的，因此无法实例化。所有方法均为静态，方便直接调用。

### 主要字段

```java
// 1.标准输入流，默认从键盘读取数据。可以用来接收用户输入，通常与 Scanner 类结合使用。
Scanner scanner = new Scanner(System.in);
System.out.println("输入内容：" + scanner.nextLine());

// 2.标准输出流，默认输出到控制台。用于打印信息到屏幕。
System.out.println("Hello, World!");

// 3.标准错误输出流，默认输出到控制台，通常用于输出错误信息（通常以红色显示）。
System.err.println("发生错误！");
```

### 常用方法

```java
public class SystemMethodsExample {
    public static void main(String[] args) {
        // 1. System.out.println() - 标准输出
        System.out.println("Welcome to System Class!"); // 输出到控制台 -> Welcome to System Class!

        // 2. System.err.println() - 标准错误输出
        System.err.println("This is an error message"); // 输出到错误流 -> This is an error message

        // 3. getProperty(String key) - 获取系统属性
        String osName = System.getProperty("os.name"); // 获取操作系统名称
        System.out.println("Operating System: " + osName); // 例如 -> Operating System: Windows 11

        // 4. setProperty(String key, String value) - 设置系统属性
        System.setProperty("my.app.version", "1.0.0"); // 设置自定义属性
        String appVersion = System.getProperty("systems.my.app.version"); // 获取自定义属性
        System.out.println("App Version: " + appVersion); // -> App Version: 1.0.0

        // 5. getenv(String name) - 获取环境变量
        String userHome = System.getenv("HOME"); // 获取 HOME 环境变量
        System.out.println("User Home Directory: " + userHome); // 例如 -> User Home Directory: /home/user

        // 6. currentTimeMillis() - 获取当前时间
        long currentTime = System.currentTimeMillis(); // 当前时间（毫秒）
        System.out.println("Current Time (ms): " + currentTime); // 例如 -> Current Time (ms): 1742153880000

        // 7. nanoTime() - 高精度时间
        long startTime = System.nanoTime(); // 记录开始时间
        // 模拟简单计算
        long sum = 0;
        for (int i = 0; i < 100000; i++) {
            sum += i;
        }
        long endTime = System.nanoTime(); // 记录结束时间
        System.out.println("Calculation Time (ns): " + (endTime - startTime)); // 例如 -> Calculation Time (ns): 123456

        // 8. arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
        int[] src = {10, 20, 30, 40, 50};
        int[] dest = new int[5];
        System.arraycopy(src, 2, dest, 1, 3); // 复制索引 2-4 到 dest 索引 1-3 -> [0, 30, 40, 50, 0]
        System.out.print("Copied Array: [");
        for (int i = 0; i < dest.length; i++) {
            System.out.print(dest[i] + (i < dest.length - 1 ? ", " : ""));
        }
        System.out.println("]");

        // 9. gc() - 建议垃圾回收
        System.gc(); // 建议 JVM 进行垃圾回收
        System.out.println("Garbage Collection Requested");

        // 10. identityHashCode(Object x) - 获取对象默认哈希码
        Object obj = new Object();
        int hashCode = System.identityHashCode(obj); // 默认哈希码
        System.out.println("Identity Hash Code of obj: " + hashCode); // 例如 -> Identity Hash Code of obj: 123456789

        // 11. lineSeparator() - 获取系统换行符
        String lineSep = System.lineSeparator(); // 系统换行符
        System.out.println("Line Separator: '" + lineSep + "'"); // 例如 -> Line Separator: '\n'

        // 12. exit(int status) - 终止 JVM
        System.exit(0); // 正常退出 JVM
    }
}
```







## Scanner

### 创建 Scanner 对象

- 从键盘读取数据：

    ```java
    Scanner scanner = new Scanner(System.in);
    ```

- 从文件读取数据：

    ```java
    Scanner scanner = new Scanner(new File("filename.txt"));
    ```

### 常用方法

```java
import java.util.Scanner;

public class ScannerExample {

    public static void main(String[] args) {
        // 创建 Scanner 对象
        Scanner scanner = new Scanner(System.in);

        // 1. 使用 nextLine() 读取一整行字符串
        System.out.println("Enter a line of text:");
        String line = scanner.nextLine();  // 读取一整行文本
        System.out.println("You entered: " + line);

        // 2. 使用 next() 读取单个单词
        System.out.println("Enter a word:");
        String word = scanner.next();  // 读取一个单词
        System.out.println("You entered: " + word);

        // 3. 使用 nextInt() 读取整数
        System.out.println("Enter an integer:");
        int integer = scanner.nextInt();  // 读取一个整数
        System.out.println("You entered integer: " + integer);

        // 4. 使用 nextDouble() 读取浮点数
        System.out.println("Enter a double:");
        double doubleValue = scanner.nextDouble();  // 读取一个双精度浮点数
        System.out.println("You entered double: " + doubleValue);

        // 5. 使用 nextBoolean() 读取布尔值
        System.out.println("Enter a boolean (true/false):");
        boolean boolValue = scanner.nextBoolean();  // 读取一个布尔值
        System.out.println("You entered boolean: " + boolValue);

        // 6. 使用 nextFloat() 读取浮点数
        System.out.println("Enter a float:");
        float floatValue = scanner.nextFloat();  // 读取一个浮点数
        System.out.println("You entered float: " + floatValue);

        // 7. 使用 nextLong() 读取长整型
        System.out.println("Enter a long number:");
        long longValue = scanner.nextLong();  // 读取一个长整型
        System.out.println("You entered long: " + longValue);

        // 8. 使用 hasNext() 检查是否有下一个输入项
        System.out.println("Do you want to enter another word? (yes/no):");
        if (scanner.hasNext()) {  // 检查是否有下一个单词
            String response = scanner.next();  // 读取一个单词
            System.out.println("You entered: " + response);
        }

        // 9. 使用 hasNextInt() 检查是否下一个输入是整数
        System.out.println("Enter a number (int) or a non-integer to quit:");
        if (scanner.hasNextInt()) {  // 检查下一个输入是否是整数
            int nextInt = scanner.nextInt();  // 读取整数
            System.out.println("You entered integer: " + nextInt);
        } else {
            System.out.println("You entered a non-integer. Exiting...");
        }

        // 10. 使用 skip() 跳过输入中的特定字符或模式
        scanner.nextLine();  // 清除输入缓冲区中的换行符
        System.out.println("Enter a sentence (we'll skip the first word):");
        String sentence = scanner.nextLine();
        scanner.skip(".*? ");  // 跳过句子中的第一个单词及空格
        System.out.println("Remaining sentence: " + sentence.substring(sentence.indexOf(" ") + 1));

        // 11. 使用 close() 关闭 Scanner
        scanner.close();  // 关闭 scanner，释放资源
    }
}

```



## Date

`Date` 类（位于 `java.util` 包）用于表示日期和时间，精确到毫秒。

尽管 `Date` 类在早期的 Java 版本中广泛使用，但自 Java 8 引入 `java.time` 包（如 `LocalDate`、`LocalDateTime` 等）后，`Date` 类在现代 Java 开发中已被部分替代，因为其设计存在一些局限性（如线程安全问题和 API 不够直观）。不过，`Date` 类在遗留代码和某些场景中仍然有用。

![image-20250515085127641](images/image-20250515085127641.png)

### 创建 `Date` 对象

```java
// 1. 当前系统时间
Date now = new Date();

// 2. Date(long time)：创建指定毫秒数（自 1970-01-01 00:00:00 GMT）
Date specific = new Date(1747274880000L); // 2025-05-15 08:48:00 HKT
```

### 常用方法

```java
import java.util.Date;

public class DateMethodsExample {
    public static void main(String[] args) {
        // 初始化 Date 对象（当前日期和时间）
        Date date = new Date();
        Date date2 = new Date(System.currentTimeMillis() - 24 * 60 * 60 * 1000); // 昨天

        // 1. getTime()
        long time = date.getTime();  // 返回自 1970-01-01 00:00:00 GMT 以来的毫秒数
        System.out.println("Milliseconds since epoch: " + time);

        // 2. setTime(long time)
        Date newDate = new Date();
        newDate.setTime(time - 3600 * 1000);  // 设置为一小时前
        System.out.println("After setTime (1 hour ago): " + newDate);

        // 3. before(Date when)
        boolean isBefore = date.before(date2);  // 检查 date 是否早于 date2 -> false
        System.out.println("Is date before date2? " + isBefore);

        // 4. after(Date when)
        boolean isAfter = date.after(date2);  // 检查 date 是否晚于 date2 -> true
        System.out.println("Is date after date2? " + isAfter);

        // 5. compareTo(Date anotherDate)
        int comparison = date.compareTo(date2);  // 比较两个日期 -> 1（date > date2）
        System.out.println("Compare date to date2: " + comparison);

        // 6. equals(Object obj)
        Date sameDate = new Date(date.getTime());
        boolean isEqual = date.equals(sameDate);  // 检查是否相等 -> true
        System.out.println("Is date equal to sameDate? " + isEqual);

        // 7. toString()
        String dateStr = date.toString();  // 转换为字符串，格式如 "Thu May 15 08:48:00 HKT 2025"
        System.out.println("To String: " + dateStr);

        // 8. getYear() - 已弃用
        @SuppressWarnings("deprecation")
        int year = date.getYear() + 1900;  // 返回年份（需加1900） -> 2025
        System.out.println("Year: " + year);

        // 9. getMonth() - 已弃用
        @SuppressWarnings("deprecation")
        int month = date.getMonth() + 1;  // 返回月份（0-11，需加1） -> 5
        System.out.println("Month: " + month);

        // 10. getDate() - 已弃用
        @SuppressWarnings("deprecation")
        int day = date.getDate();  // 返回日 -> 15
        System.out.println("Day of month: " + day);

        // 11. getHours() - 已弃用
        @SuppressWarnings("deprecation")
        int hours = date.getHours();  // 返回小时 -> 8
        System.out.println("Hours: " + hours);

        // 12. getMinutes() - 已弃用.dot
        @SuppressWarnings("deprecation")
        int minutes = date.getMinutes();  // 返回分钟 -> 48
        System.out.println("Minutes: " + minutes);

        // 13. getSeconds() - 已弃用
        @SuppressWarnings("deprecation")
        int seconds = date.getSeconds();  // 返回秒 -> 0
        System.out.println("Seconds: " + seconds);

        // 14. getDay() - 已弃用
        @SuppressWarnings("deprecation")
        int dayOfWeek = date.getDay();  // 返回星期几（0=周日，6=周六） -> 4（周四）
        System.out.println("Day of week (0=Sun): " + dayOfWeek);

        // 15. clone()
        Date clonedDate = (Date) date.clone();  // 创建日期副本
        System.out.println("Cloned date: " + clonedDate);
    }
}
```



## Calendar

`Calendar` 类（位于 `java.util` 包）是一个用于处理日期和时间的抽象类，常用于操作日期的年、月、日、时、分、秒等字段。

它比 `Date` 类更灵活，特别是在需要操作日期或获取特定日期组件时。

`Calendar` 是一个抽象类，不能直接实例化，通常通过 `Calendar.getInstance()` 获取实例。

```java
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.Locale;

public class Main {
    public static void main(String[] args) {
        // 获取 Calendar 实例（默认当前时间和系统时区）
        Calendar calendar = Calendar.getInstance();

        // 获取 Date 对象
        Date date = calendar.getTime();

        // 格式化日期为中文
        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd", Locale.CHINA);
        SimpleDateFormat sdf2 = new SimpleDateFormat("EEEE, MMMM dd, yyyy", Locale.CHINA);
        SimpleDateFormat sdf3 = new SimpleDateFormat("EEEE", Locale.CHINA);

        System.out.println("格式1: " + sdf1.format(date)); // 输出：2025-05-16
        System.out.println("格式2: " + sdf2.format(date)); // 输出：星期五, 五月 16, 2025
        System.out.println("格式3: " + sdf3.format(date)); // 输出：星期五

        // 示例：操作日期（加7天）
        calendar.add(Calendar.DAY_OF_MONTH, 7);
        date = calendar.getTime();
        System.out.println("7天后的日期: " + sdf2.format(date)); // 输出：星期五, 五月 23, 2025

        // 示例：获取特定字段
        int year = calendar.get(Calendar.YEAR);
        int month = calendar.get(Calendar.MONTH) + 1; // 注意：月份从0开始，需加1
        int day = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.printf("年: %d, 月: %d, 日: %d%n", year, month, day); // 输出：年: 2025, 月: 5, 日: 23
    }
}
```



## SimpleDateFormat

`SimpleDateFormat` 类（位于 `java.text` 包）用于格式化和解析日期与时间。

它允许将 `Date` 对象格式化为特定模式的字符串，或将符合特定模式的字符串解析为 `Date` 对象。`SimpleDateFormat` 常用于处理日期的显示和输入，但它不是线程安全的，在多线程环境中需小心使用。

### 创建 `SimpleDateFormat` 对象

```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");

SimpleDateFormat sdf = new SimpleDateFormat("EEEE, MMMM dd, yyyy", Locale.US);

SimpleDateFormat sdf = new SimpleDateFormat("EEEE", new DateFormatSymbols(Locale.US));
```

### 常用格式模式

以下是 `SimpleDateFormat` 中常用的格式符号：

- `yyyy`：四位年份（2025）
- `MM`：两位月份（05）
- `dd`：两位日期（15）
- `HH`：24小时制小时（09）
- `mm`：分钟（02）
- `ss`：秒（00）
- `SSS`：毫秒（000）
- `E`：星期几（Thu）
- `a`：AM/PM 标记
- `z`：时区（HKT）

### 常用方法

```java
import java.text.SimpleDateFormat;
import java.util.Date;
import java.text.ParseException;
import java.util.Locale;
import java.util.TimeZone;

public class SimpleDateFormatMethodsExample {
    public static void main(String[] args) {
        // 初始化 Date 对象（当前日期和时间：2025-05-15 09:02:00 HKT）
        Date date = new Date();
        // 初始化 SimpleDateFormat 对象
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

        // 1. format(Date date)
        String formatted = sdf.format(date);  // 将 Date 格式化为字符串 -> "2025-05-15 09:02:00"
        System.out.println("After format: " + formatted);

        // 2. parse(String source)
        try {
            Date parsedDate = sdf.parse("2025-05-15 09:02:00");  // 解析字符串为 Date
            System.out.println("After parse: " + parsedDate);
        } catch (ParseException e) {
            System.out.println("Parse error: " + e.getMessage());
        }

        // 3. setDateFormatSymbols(DateFormatSymbols symbols)
        SimpleDateFormat sdfWithSymbols = new SimpleDateFormat("EEEE, MMMM dd, yyyy");
        sdfWithSymbols.setDateFormatSymbols(new java.text.DateFormatSymbols(Locale.US));  // 设置美国英语符号
        String formattedWithSymbols = sdfWithSymbols.format(date);  // -> "Thursday, May 15, 2025"
        System.out.println("After setDateFormatSymbols (US): " + formattedWithSymbols);

        // 4. setLenient(boolean lenient)
        sdf.setLenient(false);  // 设置严格解析（非宽松）
        try {
            sdf.parse("2025-13-15 09:02:00");  // 无效月份，应抛出异常
        } catch (ParseException e) {
            System.out.println("Strict parse error (non-lenient): " + e.getMessage());
        }

        // 5. setTimeZone(TimeZone zone)
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));  // 设置时区为 UTC
        String utcFormatted = sdf.format(date);  // 转换为 UTC 时间 -> "2025-05-15 01:02:00"
        System.out.println("After setTimeZone (UTC): " + utcFormatted);

        // 6. getTimeZone()
        TimeZone timeZone = sdf.getTimeZone();  // 获取当前时区 -> UTC
        System.out.println("Current time zone: " + timeZone.getID());

        // 7. applyPattern(String pattern)
        sdf.applyPattern("dd/MM/yyyy");  // 应用新格式模式 -> "15/05/2025"
        String newPattern = sdf.format(date);
        System.out.println("After applyPattern (dd/MM/yyyy): " + newPattern);

        // 8. toPattern()
        String pattern = sdf.toPattern();  // 获取当前格式模式 -> "dd/MM/yyyy"
        System.out.println("Current pattern: " + pattern);

        // 9. Format with custom Locale
        SimpleDateFormat sdfLocale = new SimpleDateFormat("EEEE, MMMM dd, yyyy", Locale.FRANCE);
        String frenchFormat = sdfLocale.format(date);  // 使用法语格式 -> "jeudi, mai 15, 2025"
        System.out.println("Format with French locale: " + frenchFormat);

        // 10. Format with milliseconds
        SimpleDateFormat sdfMillis = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
        String millisFormat = sdfMillis.format(date);  // 包含毫秒 -> "2025-05-15 09:02:00.000"
        System.out.println("Format with milliseconds: " + millisFormat);

        // 11. Format with AM/PM
        SimpleDateFormat sdfAmPm = new SimpleDateFormat("hh:mm a");
        String amPmFormat = sdfAmPm.format(date);  // 12小时制 -> "09:02 AM"
        System.out.println("Format with AM/PM: " + amPmFormat);

        // 12. Format with day of week
        SimpleDateFormat sdfDay = new SimpleDateFormat("E, yyyy-MM-dd");
        String dayFormat = sdfDay.format(date);  // 包含星期 -> "Thu, 2025-05-15"
        System.out.println("Format with day of week: " + dayFormat);

        // 13. Parse with different pattern
        SimpleDateFormat sdfParse = new SimpleDateFormat("dd-MM-yyyy");
        try {
            Date parsedCustom = sdfParse.parse("15-05-2025");  // 解析不同格式 -> 2025-05-15
            System.out.println("After parse (dd-MM-yyyy): " + parsedCustom);
        } catch (ParseException e) {
            System.out.println("Parse error: " + e.getMessage());
        }

        // 14. Format with short date
        SimpleDateFormat sdfShort = new SimpleDateFormat("MM/dd/yy");
        String shortFormat = sdfShort.format(date);  // 短日期格式 -> "05/15/25"
        System.out.println("Format with short date: " + shortFormat);

        // 15. clone()
        SimpleDateFormat sdfClone = (SimpleDateFormat) sdf.clone();  // 克隆 SimpleDateFormat 对象
        String clonedFormat = sdfClone.format(date);  // 使用克隆对象格式化 -> "15/05/2025"
        System.out.println("Format with cloned SDF: " + clonedFormat);
    }
}
```



## LocalDateTime

`LocalDateTime` 类用于表示日期和时间，不包含时区信息，精确到纳秒。

它是 Java 8 引入的 `java.time` 包的一部分，设计现代化、线程安全且 API 直观，广泛用于替代 `java.util.Date` 和 `java.util.Calendar`。

### 创建 `LocalDateTime` 对象

```java
import java.time.LocalDateTime;

// 1. 当前系统时间
LocalDateTime now = LocalDateTime.now();

// 2. 指定日期和时间
LocalDateTime specific = LocalDateTime.of(2025, 5, 15, 8, 48, 0); // 2025-05-15 08:48:00

// 3. 解析字符串
LocalDateTime parsed = LocalDateTime.parse("2025-05-15T08:48:00"); // ISO_LOCAL_DATE_TIME 格式
```

### 常用方法

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

public class LocalDateTimeMethodsExample {
    public static void main(String[] args) {
        // 初始化 LocalDateTime 对象（当前日期和时间）
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime yesterday = now.minusDays(1); // 昨天

        // 1. getYear()
        int year = now.getYear(); // 返回年份 -> 2025
        System.out.println("Year: " + year);

        // 2. getMonth() 或 getMonthValue()
        int month = now.getMonthValue(); // 返回月份（1-12） -> 5
        System.out.println("Month: " + month);

        // 3. getDayOfMonth()
        int day = now.getDayOfMonth(); // 返回日 -> 15
        System.out.println("Day of month: " + day);

        // 4. getDayOfWeek()
        int dayOfWeek = now.getDayOfWeek().getValue(); // 返回星期几（1=周一，7=周日） -> 4（周四）
        System.out.println("Day of week (1=Mon): " + dayOfWeek);

        // 5. getHour()
        int hours = now.getHour(); // 返回小时 -> 8
        System.out.println("Hours: " + hours);

        // 6. getMinute()
        int minutes = now.getMinute(); // 返回分钟 -> 48
        System.out.println("Minutes: " + minutes);

        // 7. getSecond()
        int seconds = now.getSecond(); // 返回秒 -> 0
        System.out.println("Seconds: " + seconds);

        // 8. getNano()
        int nanos = now.getNano(); // 返回纳秒
        System.out.println("Nanoseconds: " + nanos);

        // 9. plusXxx() / minusXxx() - 时间增减
        LocalDateTime oneHourAgo = now.minusHours(1); // 减1小时
        System.out.println("One hour ago: " + oneHourAgo);
        LocalDateTime oneDayLater = now.plus(1, ChronoUnit.DAYS); // 加1天
        System.out.println("One day later: " + oneDayLater);

        // 10. withXxx() - 修改特定字段
        LocalDateTime modified = now.withYear(2026).withHour(10); // 修改年为2026，小时为10
        System.out.println("Modified date: " + modified);

        // 11. isBefore()
        boolean isBefore = now.isBefore(yesterday); // 检查 now 是否早于 yesterday -> false
        System.out.println("Is now before yesterday? " + isBefore);

        // 12. isAfter()
        boolean isAfter = now.isAfter(yesterday); // 检查 now 是否晚于 yesterday -> true
        System.out.println("Is now after yesterday? " + isAfter);

        // 13. isEqual()
        LocalDateTime sameTime = LocalDateTime.of(now.getYear(), now.getMonth(), now.getDayOfMonth(),
                                                  now.getHour(), now.getMinute(), now.getSecond());
        boolean isEqual = now.isEqual(sameTime); // 检查是否相等 -> true
        System.out.println("Is now equal to sameTime? " + isEqual);

        // 14. toString()
        String dateStr = now.toString(); // 转换为字符串，格式如 "2025-05-15T08:48:00"
        System.out.println("To String: " + dateStr);

        // 15. truncatedTo()
        LocalDateTime truncated = now.truncatedTo(ChronoUnit.MINUTES); // 截断到分钟（秒和纳秒置零）
        System.out.println("Truncated to minutes: " + truncated);

        // 16. until() 或 between()
        long hoursBetween = ChronoUnit.HOURS.between(yesterday, now); // 计算时间差（小时）
        System.out.println("Hours between yesterday and now: " + hoursBetween);

        // 17. toLocalDate() / toLocalTime()
        System.out.println("LocalDate: " + now.toLocalDate()); // 提取日期部分
        System.out.println("LocalTime: " + now.toLocalTime()); // 提取时间部分
    }
}
```

### 三代日期对比

| 特性           | Date                                | Calendar                        | java.time (LocalDate/LocalDateTime/ZonedDateTime) |
| -------------- | ----------------------------------- | ------------------------------- | ------------------------------------------------- |
| **引入时间**   | JDK 1.0                             | JDK 1.1                         | JDK 8 (2014)                                      |
| **线程安全**   | 非线程安全                          | 非线程安全                      | 线程安全（不可变对象）                            |
| **不可变性**   | 可变（可修改时间）                  | 可变（可修改字段）              | 不可变（操作返回新对象）                          |
| **API 直观性** | 不直观，许多方法已废弃              | 较复杂（如 get(DAY_OF_MONTH)）  | 直观（如 getDayOfMonth()、plusDays()）            |
| **日期操作**   | 有限（仅支持毫秒操作）              | 支持字段操作（年、月、日等）    | 强大（支持加减、比较、区间等）                    |
| **时区支持**   | 有限（依赖 TimeZone）               | 支持，但操作繁琐                | 强大（ZonedDateTime 提供完整时区支持）            |
| **月份索引**   | 不适用（无月份操作）                | 0 起始（0=一月）                | 1 起始（1=一月）                                  |
| **中文支持**   | 依赖 SimpleDateFormat 和 Locale     | 依赖 SimpleDateFormat 和 Locale | 依赖 DateTimeFormatter 和 Locale                  |
| **格式化**     | 依赖 SimpleDateFormat（非线程安全） | 依赖 SimpleDateFormat           | 使用 DateTimeFormatter（线程安全）                |
| **性能**       | 较差（高并发下问题明显）            | 一般（复杂操作较慢）            | 较好（优化并发场景）                              |
| **推荐场景**   | 遗留代码                            | 遗留代码或需兼容旧 API          | 新项目或现代应用                                  |



## DateTimeFormatter

`DateTimeFormatter` 是 Java 中 `java.time.format` 包下的一个类，引入于 Java 8，用于格式化和解析日期时间对象（如 `LocalDate`、`LocalDateTime` 等）。

它提供了强大的功能来定义日期时间的格式，取代了老旧的 `SimpleDateFormat`，并且是**线程安全**的，适合在并发环境中使用。

### 创建 `DateTimeFormatter` 对象

```java
// 1. 通过 DateTimeFormatter.ofPattern 方法指定自定义格式.
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

// 2. DateTimeFormatter 提供了一些内置的格式化器
DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE; // 格式：2025-05-17
DateTimeFormatter formatter2 = DateTimeFormatter.ISO_LOCAL_DATE_TIME; // 格式：2025-05-17T15:56:00
DateTimeFormatter formatter3 = DateTimeFormatter.ISO_OFFSET_DATE_TIME; // 格式：2025-05-17T15:56:00+08:00
```

### 常用格式模式

以下是 `SimpleDateFormat` 中常用的格式符号：

- `yyyy`：四位年份（2025）
- `MM`：两位月份（05）
- `dd`：两位日期（15）
- `HH`：24小时制小时（09）
- `mm`：分钟（02）
- `ss`：秒（00）
- `SSS`：毫秒（000）
- `E`：星期几（Thu）
- `a`：AM/PM 标记
- `z`：时区（HKT）

### 常用方法

```java
import java.time.LocalDateTime;
import java.time.ZonedDateTime;
import java.time.ZoneId;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.time.format.FormatStyle;
import java.util.Locale;

public class DateTimeFormatterMethodsExample {
    public static void main(String[] args) {
        // 初始化 LocalDateTime 对象（当前日期和时间：2025-05-17 16:03:00 HKT）
        LocalDateTime dateTime = LocalDateTime.now();
        // 初始化 DateTimeFormatter 对象
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

        // 1. format(TemporalAccessor temporal)
        String formatted = dateTime.format(formatter); // 将 LocalDateTime 格式化为字符串 -> "2025-05-17 16:03:00"
        System.out.println("After format: " + formatted);

        // 2. parse(CharSequence text)
        try {
            LocalDateTime parsedDateTime = LocalDateTime.parse("2025-05-17 16:03:00", formatter); // 解析字符串为 LocalDateTime
            System.out.println("After parse: " + parsedDateTime);
        } catch (DateTimeParseException e) {
            System.out.println("Parse error: " + e.getMessage());
        }

        // 3. ofLocalizedDateTime(FormatStyle dateTimeStyle)
        DateTimeFormatter localizedFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL)
                                                              .withLocale(Locale.US); // 设置美国英语格式
        String localizedFormat = dateTime.format(localizedFormatter); // -> "Saturday, May 17, 2025 at 4:03:00 PM"
        System.out.println("After ofLocalizedDateTime (US): " + localizedFormat);

        // 4. withResolverStyle(ResolverStyle resolverStyle)
        DateTimeFormatter strictFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd")
                                                            .withResolverStyle(java.time.format.ResolverStyle.STRICT);
        try {
            strictFormatter.parse("2025-13-17"); // 无效月份，应抛出异常
        } catch (DateTimeParseException e) {
            System.out.println("Strict parse error (STRICT): " + e.getMessage());
        }

        // 5. withZone(ZoneId zone)
        DateTimeFormatter zonedFormatter = formatter.withZone(ZoneId.of("UTC")); // 设置时区为 UTC
        ZonedDateTime zonedDateTime = ZonedDateTime.of(dateTime, ZoneId.of("Asia/Hong_Kong"));
        String utcFormatted = zonedFormatter.format(zonedDateTime); // 转换为 UTC 时间 -> "2025-05-17 08:03:00"
        System.out.println("After withZone (UTC): " + utcFormatted);

        // 6. getZone()
        ZoneId zone = zonedFormatter.getZone(); // 获取当前时区 -> UTC
        System.out.println("Current time zone: " + zone.getId());

        // 7. ofPattern(String pattern)
        DateTimeFormatter newPatternFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy"); // 应用新格式模式 -> "17/05/2025"
        String newPattern = dateTime.format(newPatternFormatter);
        System.out.println("After ofPattern (dd/MM/yyyy): " + newPattern);

        // 8. toString()
        String pattern = formatter.toString(); // 获取当前格式模式 -> "yyyy-MM-dd HH:mm:ss"
        System.out.println("Current pattern: " + pattern);

        // 9. Format with custom Locale
        DateTimeFormatter frenchFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL, FormatStyle.MEDIUM)
                                                            .withLocale(Locale.FRANCE);
        String frenchFormat = dateTime.format(frenchFormatter); // 使用法语格式 -> "samedi 17 mai 2025 à 16:03:00"
        System.out.println("Format with French locale: " + frenchFormat);

        // 10. Format with milliseconds
        DateTimeFormatter millisFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss.SSS");
        String millisFormat = dateTime.format(millisFormatter); // 包含毫秒 -> "2025-05-17 16:03:00.000"
        System.out.println("Format with milliseconds: " + millisFormat);

        // 11. Format with AM/PM
        DateTimeFormatter amPmFormatter = DateTimeFormatter.ofPattern("hh:mm a");
        String amPmFormat = dateTime.format(amPmFormatter); // 12小时制 -> "04:03 PM"
        System.out.println("Format with AM/PM: " + amPmFormat);

        // 12. Format with day of week
        DateTimeFormatter dayFormatter = DateTimeFormatter.ofPattern("E, yyyy-MM-dd");
        String dayFormat = dateTime.format(dayFormatter); // 包含星期 -> "Sat, 2025-05-17"
        System.out.println("Format with day of week: " + dayFormat);

        // 13. Parse with different pattern
        DateTimeFormatter customParseFormatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
        try {
            LocalDateTime parsedCustom = LocalDateTime.parse("17-05-2025 00:00:00", 
                DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")); // 解析不同格式 -> 2025-05-17T00:00
            System.out.println("After parse (dd-MM-yyyy): " + parsedCustom);
        } catch (DateTimeParseException e) {
            System.out.println("Parse error: " + e.getMessage());
        }

        // 14. Format with short date
        DateTimeFormatter shortFormatter = DateTimeFormatter.ofPattern("MM/dd/yy");
        String shortFormat = dateTime.format(shortFormatter); // 短日期格式 -> "05/17/25"
        System.out.println("Format with short date: " + shortFormat);

        // 15. ISO_LOCAL_DATE_TIME
        DateTimeFormatter isoFormatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        String isoFormat = dateTime.format(isoFormatter); // ISO 格式 -> "2025-05-17T16:03:00"
        System.out.println("Format with ISO_LOCAL_DATE_TIME: " + isoFormat
```



# 集合框架

集合（Collections）和映射（Maps）是 Java 集合框架（Java Collections Framework）的两大核心组成部分，用于存储和操作一组数据。

## Collection 接口

![image-20250517170506364](images/image-20250517170506364.png)

`Collection` 接口是 Java 集合框架的根接口，位于 `java.util` 包中，定义了所有集合类（如 `List`、`Set`、`Queue`）的通用操作。

### Collection 接口方法

`Collection` 接口定义了以下**核心方法**（以下以泛型 `Collection<E>` 为例）：

| 方法签名                                              | 描述                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| boolean add(E e)                                      | 添加元素到集合，成功返回 true，失败（如重复元素被拒绝）返回 false。 |
| boolean addAll(Collection<? extends E> c)             | 添加指定集合中的所有元素。                                   |
| boolean remove(Object o)                              | 删除指定元素，成功返回 true。                                |
| boolean removeAll(Collection<?> c)                    | 删除与指定集合中的元素匹配的所有元素。                       |
| boolean retainAll(Collection<?> c)                    | 仅保留与指定集合中的元素匹配的元素（交集）。                 |
| void clear()                                          | 清空集合中的所有元素。                                       |
| boolean contains(Object o)                            | 检查集合是否包含指定元素。                                   |
| boolean containsAll(Collection<?> c)                  | 检查集合是否包含指定集合中的所有元素。                       |
| boolean isEmpty()                                     | 检查集合是否为空。                                           |
| int size()                                            | 返回集合中的元素数量。                                       |
| Iterator<E> iterator()                                | 返回用于遍历集合的迭代器。                                   |
| Object[] toArray()                                    | 将集合转换为对象数组。                                       |
| <T> T[] toArray(T[] a)                                | 将集合转换为指定类型的数组。                                 |
| default boolean removeIf(Predicate<? super E> filter) | 删除满足指定条件的元素（Java 8+）。                          |
| default Stream<E> stream()                            | 返回集合的顺序流（Java 8+）。                                |
| default Stream<E> parallelStream()                    | 返回集合的并行流（Java 8+）。                                |

### Iterable & Iterator

`Iterable` 接口里的 `iterator()` 方法返回一个迭代器。

```java
public interface Iterable<T> {
    // Returns an iterator over elements of type {@code T}.
    Iterator<T> iterator();
}
```

`Iterator` 是一个泛型接口，`E` 表示集合中元素的类型。

```java
public interface Iterator<E> {
    // Returns {@code true} if the iteration has more elements.
    boolean hasNext();
    // Returns the next element in the iteration.
    E next();
}
```

以下通过一个例子解释迭代器原理。通过 `Collection` 接口的 `iterator()` 方法获取迭代器，

```java
Collection col = new ArrayList<>();
col.add("a");
col.add("b");
col.add("c");
Iterator iter = col.iterator();

while (iter.hasNext()) {
    Object obj = iter.next();
    System.out.println(obj);
}

// 此时，iter.next()已经指向最后一个元素
// 如果希望再次遍历，需要重置迭代器
iter = col.iterator();

// 增强for循环
for (String obj : col) {
    System.out.println(obj);
}
```



## List 接口

`List` 接口是 Java 集合框架中的核心接口之一，位于 `java.util` 包中，继承自 `Collection` 接口。

它表示一个**有序集合**，允许**存储重复元素**，并支持通过索引访问元素。

### List 接口特点

1. 有序性
2. 索引访问
3. 允许重复元素
4. 允许null

### List 接口方法

```java
import java.util.*;
import java.time.LocalDateTime;

public class ListMethodsExample {
    public static void main(String[] args) {
        // 初始化 List 对象（当前时间：2025-05-17 21:12:00 HKT）
        List<String> list = new ArrayList<>();
        // 添加初始元素
        list.add("Apple");
        list.add("Banana");

        // 1. add(E e)
        list.add("Orange"); // 在列表末尾添加元素 -> [Apple, Banana, Orange]
        System.out.println("After add: " + list);

        // 2. add(int index, E element)
        list.add(1, "Mango"); // 在索引 1 插入元素 -> [Apple, Mango, Banana, Orange]
        System.out.println("After add at index 1: " + list);

        // 3. get(int index)
        String element = list.get(2); // 获取索引 2 的元素 -> "Banana"
        System.out.println("Element at index 2: " + element);

        // 4. set(int index, E element)
        list.set(2, "Grape"); // 替换索引 2 的元素 -> [Apple, Mango, Grape, Orange]
        System.out.println("After set at index 2: " + list);

        // 5. remove(int index)
        list.remove(1); // 删除索引 1 的元素 -> [Apple, Grape, Orange]
        System.out.println("After remove at index 1: " + list);

        // 6. remove(Object o)
        list.remove("Orange"); // 删除首次出现的指定元素 -> [Apple, Grape]
        System.out.println("After remove Orange: " + list);

        // 7. contains(Object o)
        boolean contains = list.contains("Apple"); // 检查是否包含 "Apple" -> true
        System.out.println("Contains Apple: " + contains);

        // 8. indexOf(Object o)
        int index = list.indexOf("Grape"); // 获取 "Grape" 的首次索引 -> 1
        System.out.println("Index of Grape: " + index);

        // 9. listIterator()
        ListIterator<String> iterator = list.listIterator(); // 获取双向迭代器
        System.out.print("Forward traverse with listIterator: ");
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
        System.out.println(); // Apple Grape

        // 10. subList(int fromIndex, int toIndex)
        List<String> subList = list.subList(0, 1); // 获取子列表 -> [Apple]
        System.out.println("SubList (0-1): " + subList);

        // 11. sort(Comparator<? super E> c)
        list.add("Cherry");
        list.sort(Comparator.naturalOrder()); // 按自然顺序排序 -> [Apple, Cherry, Grape]
        System.out.println("After sort: " + list);

        // 12. replaceAll(UnaryOperator<E> operator)
        list.replaceAll(String::toUpperCase); // 将所有元素转为大写 -> [APPLE, CHERRY, GRAPE]
        System.out.println("After replaceAll to uppercase: " + list);

        // 13. addAll(Collection<? extends E> c)
        List<String> moreFruits = Arrays.asList("Mango", "Orange");
        list.addAll(moreFruits); // 添加集合中的所有元素 -> [APPLE, CHERRY, GRAPE, Mango, Orange]
        System.out.println("After addAll: " + list);

        // 14. clear()
        list.clear(); // 清空列表 -> []
        System.out.println("After clear: " + list);

        // 15. isEmpty()
        boolean isEmpty = list.isEmpty(); // 检查列表是否为空 -> true
        System.out.println("Is empty: " + isEmpty);
        
        // 16. size()
        System.out.println("Size of empty list: " + list.size()); // 0
    }
}
```



## ArrayList

![image-20250326203239721](images/image-20250326203239721.png)



### `ArrayList` 私有方法

```java
import java.util.*;
import java.time.LocalDateTime;

public class ArrayListPrivateMethodsExample {
    public static void main(String[] args) {
        // 初始化 List 对象（当前时间：2025-05-18 12:52:00 HKT）
        List<String> list = new ArrayList<>(2); // 初始容量 2
        // 添加初始元素
        list.add("Apple");
        list.add("Banana");

        // 1. ensureCapacityInternal(int minCapacity) 确保底层数组的容量足以容纳指定数量的元素。如果当前容量不足，会触发扩容。
        list.add("Orange"); // 触发扩容，调用 ensureCapacityInternal -> [Apple, Banana, Orange]
        System.out.println("After ensureCapacityInternal (add Orange): " + list);

        // 2. grow(int minCapacity) 通常将容量增加到当前容量的 1.5 倍
        list.add("Mango"); // 容量不足，触发 grow（新容量 3） -> [Apple, Banana, Orange, Mango]
        System.out.println("After grow (add Mango): " + list);

        // 3. rangeCheck(int index)
        try {
            list.get(10); // 触发 rangeCheck，抛出 IndexOutOfBoundsException
        } catch (IndexOutOfBoundsException e) {
            System.out.println("After rangeCheck: " + e.getMessage()); // Index 10 out of bounds
        }

        // 4. rangeCheckForAdd(int index)
        try {
            list.add(10, "Grape"); // 触发 rangeCheckForAdd，抛出 IndexOutOfBoundsException
        } catch (IndexOutOfBoundsException e) {
            System.out.println("After rangeCheckForAdd: " + e.getMessage()); // Index 10 out of bounds
        }

        // 5. fastRemove(int index)
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            if (iterator.next().equals("Banana")) {
                iterator.remove(); // 触发 fastRemove -> [Apple, Orange, Mango]
            }
        }
        System.out.println("After fastRemove (remove Banana): " + list);

        // 6. shiftTailOverGap(Object[] es, int lo, int hi)
        list.subList(1, 2).clear(); // 触发 shiftTailOverGap -> [Apple, Mango]
        System.out.println("After shiftTailOverGap (clear sublist): " + list);

        // 7. ensureExplicitCapacity(int minCapacity)
        list.ensureCapacity(10); // 触发 ensureExplicitCapacity，扩容到 10
        System.out.println("After ensureExplicitCapacity: " + list); // [Apple, Mango]

        // 8. calculateCapacity(Object[] elementData, int minCapacity)
        List<String> newList = new ArrayList<>(); // 空列表
        newList.add("Cherry"); // 触发 calculateCapacity，分配默认容量 10
        System.out.println("After calculateCapacity (add to empty list): " + newList); // [Cherry]

        // 9. outOfBoundsMsg(int index)
        try {
            list.get(-1); // 触发 outOfBoundsMsg，生成异常消息
        } catch (IndexOutOfBoundsException e) {
            System.out.println("After outOfBoundsMsg: " + e.getMessage()); // Index -1 out of bounds
        }

        // 10. elementData(int index)
        String element = list.get(0); // 触发 elementData，获取元素 -> "Apple"
        System.out.println("After elementData (get index 0): " + element);

        // 11. hugeCapacity(int minCapacity)
        // 难以直接触发（需要超大容量），通过 ensureCapacity 模拟
        list.ensureCapacity(Integer.MAX_VALUE - 8); // 触发 hugeCapacity
        System.out.println("After hugeCapacity: " + list); // [Apple, Mango]

        // 12. batchRemove(Collection<?> c, boolean complement)
        List<String> toRemove = Arrays.asList("Apple");
        list.retainAll(toRemove); // 触发 batchRemove -> [Apple]
        System.out.println("After batchRemove (retain Apple): " + list);

        // 13. checkInvariants()
        // 内部调试方法，难以直接触发，通常在开发版本中检查一致性
        System.out.println("checkInvariants: Not directly triggered in production");

        // 14. writeObject(java.io.ObjectOutputStream s)
        try {
            java.io.ByteArrayOutputStream bos = new java.io.ByteArrayOutputStream();
            java.io.ObjectOutputStream oos = new java.io.ObjectOutputStream(bos);
            oos.writeObject(list); // 触发 writeObject（序列化）
            oos.close();
            System.out.println("After writeObject: List serialized");
        } catch (java.io.IOException e) {
            System.out.println("Serialization error: " + e.getMessage());
        }

        // 15. readObject(java.io.ObjectInputStream s)
        // 需序列化后再反序列化，简化示例仅说明
        System.out.println("readObject: Triggered during deserialization, not shown here");
    }
}
```

### 扩容机制

`ArrayList`中维护了一个`Object`类型的数组`ElementData`。

```java
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}

private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
```

当创建`ArrayLists`对象时，如果使用的是无参构造器，则初始`elementData`容量为0，第一次添加，则扩容为10，如需再次扩容，则扩容为`elementData`为1.5倍。

如果使用的是指定大小的构造器，则初始elementData容量为指定大小，如需再次扩容，则直接扩容为`elementData`为1.5倍。



## Vecotr

`Vector` 是 Java 集合框架中的一个类，位于 `java.util` 包中。

它实现了一个**动态数组**，类似于 `ArrayList`，可以根据需要增长或缩小。但是是**线程安全**的，其大多数方法是同步的（使用 `synchronized` 关键字），适合多线程环境。但这也导致性能较 ArrayList 低。

```java
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

### 扩容机制

`Vector`中也维护了一个`Object`类型的数组`ElementData`。

```java
public Vector(int initialCapacity) {
    this(initialCapacity, 0);
}

public Vector() {
    this(10);
}
```

当创建`ArrayLists`对象时，如果使用的是无参构造器，则初始`elementData`容量为**10**，如需再次扩容，则扩容为`elementData`为2倍。

如果指定大小，则直接扩容为`elementData`为2倍。



## LinkedList

`LinkedList` 是一个**双向链表**（doubly-linked list）实现的集合类。

它既可以作为**列表**（List），也可以作为**双端队列**（Deque）或栈使用。但是**线程不安全**。

继承自 `AbstractSequentialList`，并实现了 `List`、`Deque`、`Cloneable` 和 `Serializable` 接口。

```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```

### 内部实现

`LinkedList` 不是通过数组实现的，增删的效率较高。每个节点由 `Node` 内部类实现，

```java
private static class Node<E> {
    E item;          // 元素数据
    Node<E> next;    // 后继节点
    Node<E> prev;    // 前驱节点
    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

### 三种 `List` 对比

#### 容量管理

| 特性         | ArrayList                                      | Vector                                                       | LinkedList                        |
| ------------ | ---------------------------------------------- | ------------------------------------------------------------ | --------------------------------- |
| **默认容量** | 10（DEFAULT_CAPACITY = 10）                    | 10                                                           | 无固定容量（按需分配节点）        |
| **扩展机制** | 容量不足时，新容量 ≈ 旧容量 * 1.5（grow 方法） | 容量不足时，新容量 = 旧容量 + capacityIncrement（若为 0，则翻倍） | 无扩展机制，动态添加节点          |
| **扩展开     | 扩展时复制数组（Arrays.copyOf）                | 扩展时复制数组                                               | 无数组，直接调整节点引用          |
| **内存开销** | 数组预分配，浪费少量空间                       | 数组预分配，浪费少量空间                                     | 每个节点含 prev 和 next，额外开销 |

#### 适用场景

| 特性         | ArrayList                          | Vector                            | LinkedList                                   |
| ------------ | ---------------------------------- | --------------------------------- | -------------------------------------------- |
| **推荐场景** | **频繁修改查询**                   | - **线程安全需求** - 遗留代码维护 | - **频繁插入/删除** - 队列/栈 - 动态调整列表 |
| **避免场景** | - 多线程无同步 - 频繁中间插入/删除 | - 高性能单线程 - 现代并发需求     | - 随机访问 - 大量索引操作                    |

在程序中，百分之八九十都是查询，因此大部分情况选`ArrayList`。



## Set 接口

`Set` 接口是 `java.util` 包中的一个核心集合接口，继承自 `Collection` 接口。它表示一个**不允许重复元素**的集合，元素的**顺序通常不固定**（具体取决于实现类）。

### Set 接口的特点

- **无重复元素**：`Set` 不允许存储相同的元素（通过 `equals()` 方法判断是否相同）。

    ```java
    Set set = new HashSet();
    
    // 一个
    set.add("a");
    set.add("a");
    // 一个
    set.add(new String("a"));
    set.add(new String("a"));
    // 两个
    set.add(new Dog("pete"));
    set.add(new Dog("pete"));
    for (Object obj : set) {
        System.out.println(obj);
    }

- **无序性**：大多数实现（如 `HashSet`）不保证元素的顺序，`LinkedHashSet` 除外（维护插入顺序），`TreeSet` 按排序顺序存储。取出的顺序是固定的。

- **允许 null**：某些实现（如 `HashSet`、`LinkedHashSet`）**允许包含一个** `null` 元素，但 `TreeSet` 不允许 `null`。

- **线程不安全**：Set 的常见实现类（如 `HashSet`、`TreeSet`）都不是线程安全的。如果需要线程安全，可以使用 `Collections.synchronizedSet`() 或 `ConcurrentHashMap.newKeySet`()。

### Set 接口方法

```java
import java.util.*;
import java.time.LocalDateTime;

public class SetMethodsExample {
    public static void main(String[] args) {
        // 初始化 Set 对象（当前时间：2025-05-19 17:53:00 HKT）
        Set<String> set = new HashSet<>();
        // 添加初始元素
        set.add("Apple");
        set.add("Banana");

        // 1. add(E e)
        set.add("Orange"); // 添加元素，若不存在则添加 -> [Apple, Banana, Orange]
        System.out.println("After add: " + set);

        // 2. addAll(Collection<? extends E> c)
        Set<String> moreFruits = new HashSet<>(Arrays.asList("Mango", "Orange"));
        set.addAll(moreFruits); // 添加另一个集合的所有元素，重复元素不会添加 -> [Apple, Banana, Orange, Mango]
        System.out.println("After addAll: " + set);

        // 3. remove(Object o)
        set.remove("Banana"); // 删除指定元素 -> [Apple, Orange, Mango]
        System.out.println("After remove Banana: " + set);

        // 4. removeAll(Collection<?> c)
        Set<String> toRemove = new HashSet<>(Arrays.asList("Orange", "Grape"));
        set.removeAll(toRemove); // 删除另一个集合中的所有元素 -> [Apple, Mango]
        System.out.println("After removeAll: " + set);

        // 5. contains(Object o)
        boolean contains = set.contains("Apple"); // 检查是否包含指定元素 -> true
        System.out.println("Contains Apple: " + contains);

        // 6. containsAll(Collection<?> c)
        Set<String> checkSet = new HashSet<>(Arrays.asList("Apple", "Mango"));
        boolean containsAll = set.containsAll(checkSet); // 检查是否包含另一个集合的所有元素 -> true
        System.out.println("Contains all [Apple, Mango]: " + containsAll);

        // 7. isEmpty()
        boolean isEmpty = set.isEmpty(); // 检查集合是否为空 -> false
        System.out.println("Is empty: " + isEmpty);

        // 8. size()
        int size = set.size(); // 获取集合元素数量 -> 2
        System.out.println("Size of set: " + size);

        // 9. iterator()
        Iterator<String> iterator = set.iterator(); // 获取迭代器
        System.out.print("Traverse with iterator: ");
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
        System.out.println(); // Apple Mango

        // 10. toArray()
        Object[] array = set.toArray(); // 转换为 Object 数组
        System.out.println("To array: " + Arrays.toString(array)); // [Apple, Mango]

        // 11. toArray(T[] a)
        String[] strArray = set.toArray(new String[0]); // 转换为指定类型的数组
        System.out.println("To String array: " + Arrays.toString(strArray)); // [Apple, Mango]

        // 12. clear()
        set.clear(); // 清空集合 -> []
        System.out.println("After clear: " + set);

        // 13. isEmpty() (after clear)
        isEmpty = set.isEmpty(); // 检查集合是否为空 -> true
        System.out.println("Is empty after clear: " + isEmpty);

        // 14. size() (after clear)
        size = set.size(); // 获取集合元素数量 -> 0
        System.out.println("Size after clear: " + size);
    }
}
```



## HashSet

`HashSet` 类是 `java.util` 包中的一个集合类，实现了 Set 接口，基于哈希表（`HashMap` 内部实现）存储元素。

### 底层机制

`HashSet` 内部使用 `HashMap`，元素存储在 `HashMap` 的键中，值为一个固定对象（`PRESENT`）。

```java
public HashSet() {
    map = new HashMap<>();
}
```

执行`add`方法。添加一个元素时先计算出一个hash索引，

```java
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}

// HashMap 的 put 方法
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}

// HashMap 的 hash 方法（不同对象哈希值不一样）
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

如果这个索引位置没有元素，直接加入。如果有对此索引上链表的每个元素比较后再加入。

```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
    // 定义辅助变量。
    Node<K,V>[] tab; Node<K,V> p; int n, i;
    // table 是 HashMap 的一个Node数组
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length; // resize() 扩容函数
    
    // 根据(n - 1) 与 hash计算索引，并检查table当前索引是否为空
    if ((p = tab[i = (n - 1) & hash]) == null)
        // 创建新节点
        tab[i] = newNode(hash, key, value, null);
    else {
        Node<K,V> e; K k; // skill: 在一个代码块顶部创建局部辅助变量
        // 判断：新加元素的 hash相同 && 内容相同
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        // 判断：该索引是否为红黑树
        else if (p instanceof TreeNode)
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        // 逐个检查是否相同，若没有，则添加；若有，则break。
        else {
            for (int binCount = 0; ; ++binCount) {
                // 检查是否到达末尾
                if ((e = p.next) == null) {
                    p.next = newNode(hash, key, value, null);
                    // 检查是否树化
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    break;
                }
                // 检查相等
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    break;
                // 指向下一个
                p = e;
            }
        }
        // 替换已有键的值
        if (e != null) { // existing mapping for key
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null)
                e.value = value;
            afterNodeAccess(e);
            return oldValue;
        }
    }
    ++modCount;
    // 大于阈值扩容
    if (++size > threshold)
        resize();
    afterNodeInsertion(evict);
    return null;
}
```

### 扩容机制

`HashSet` 的扩容机制与其底层实现 `HashMap` 密切相关，因为 `HashSet` 使用 `HashMap` 存储元素。

#### 基本概念

**容量（Capacity）**：哈希表的桶（bucket）数量，即 `HashMap` 的数组长度。

**加载因子（Load Factor）**：决定哈希表在何时扩容的阈值比例，默认为 0.75。

**阈值（Threshold）**：当元素数量达到 容量 × 加载因子 时触发扩容。公式：`threshold = capacity * loadFactor`。

#### 扩容触发条件

如果添加新元素后元素数量（size）将超过或等于阈值，则触发扩容。即`size + 1 > threshold`。

初始情况下，默认容量为 16，加载因子为 0.75，因此初始阈值为 16 * 0.75 = 12。当第 12 个元素添加后，扩容被触发。

#### 扩容过程

1. **容量翻倍**：`New Capacity = Old Capacity<< 1`。哈希表容量通常扩大为原来的 **2 倍**（例如，从 16 变为 32）。

2. **重新分配桶（Rehashing）**：

- 创建一个新的、更大的数组。

- 遍历旧哈希表中的所有元素（键值对），根据元素的 hashCode 重新计算在新数组中的桶位置。

- 将元素迁移到新数组的对应桶中。

- 如果桶内有冲突（多个元素映射到同一桶），使用链表存储。

- 在Java8中，如果一条链表的元素个数  >= `TREEIFY_THRESHOLD`(默认8)，调用`treeifyBin`方法。若 table大小 >= `MIN_TREEIFY_CAPACITY`(默认64) ，就会进化为红黑树；如果小于64，则调用`resize()`扩容。

    ```java
    static final int TREEIFY_THRESHOLD = 8;
    static final int MIN_TREEIFY_CAPACITY = 64;

3. **更新阈值**：`New Threshold = New Capacity × Load Factor`。例如，容量从 16 扩到 32，阈值变为 32 * 0.75 = 24。

    ```java
    final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        // 情况 1: 哈希表已初始化 (oldCap > 0)
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            // 容量大于等于16，则容量翻倍，阈值也翻倍
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        // 情况 2: 哈希表未初始化，但阈值已设置（通过构造函数指定初始容量）
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        // 情况 3: 哈希表未初始化，使用默认值
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        /* 树化机制...*/
    }



## LinkedHashSet

`LinkedHashSet` 类是 `java.util` 包中的一个集合类，继承自 `HashSet`，并通过维护一个**双向链表**来保持元素的**插入顺序**。

![](images/7294e8d256ad47199604c88288dbbfe5.png)

**唯一性**：与 `HashSet` 一样，`LinkedHashSet` 不允许存储重复元素（根据 `equals()` 和 `hashCode()` 判断）。

**插入顺序**：按照元素插入的顺序进行迭代，区别于 `HashSet` 的无序性。

**性能**：提供接近 O(1) 的查找、插入和删除操作效率，但由于维护链表，性能略低于 `HashSet`。

**线程不安全**：`LinkedHashSet` 不是线程安全的，多线程环境下需外部同步（如使用 `Collections.synchronizedSet`）。

### 底层原理

添加原理其实和HashSet一样，底层都维护了一个**哈希表的桶** `LinkedHashMap`。

一开始直接创建一个大小为16的集合。

```java
public LinkedHashSet() {
    super(16, .75f, true);
}

// 父类构造器
HashSet(int initialCapacity, float loadFactor, boolean dummy) {
    map = new LinkedHashMap<>(initialCapacity, loadFactor);
}
```

接入的每个元素都是一个双向链表的节点 `Entry` 继承自 `HashMap.Node`，其中有 `before` 和 `after` 属性。

```java
// LinkedHashMap.java 内部类Entry
static class Entry<K,V> extends HashMap.Node<K,V> {
    Entry<K,V> before, after;
    Entry(int hash, K key, V value, Node<K,V> next) {
        super(hash, key, value, next);
    }
}
```

```java
// LinkedHashMap.java 中的方法
Node<K,V> newNode(int hash, K key, V value, Node<K,V> e) {
    LinkedHashMap.Entry<K,V> p =
        new LinkedHashMap.Entry<>(hash, key, value, e);
    linkNodeAtEnd(p);
    return p;
}

private void linkNodeAtEnd(LinkedHashMap.Entry<K,V> p) {
    if (putMode == PUT_FIRST) {
        LinkedHashMap.Entry<K,V> first = head;
        head = p;
        if (first == null)
            tail = p;
        else {
            p.after = first;
            first.before = p;
        }
    } else {
        LinkedHashMap.Entry<K,V> last = tail;
        tail = p;
        if (last == null)
            head = p;
        else {
            p.before = last;
            last.after = p;
        }
    }
}
```



## TreeSet

`TreeSet` 是 Java 集合框架中的一个类，位于 `java.util` 包下，实现了 `NavigableSet` 接口，基于 **红黑树**（自平衡二叉搜索树）实现，提供了一个**有序**且**无重复元素**的集合。

**特点**：

- **有序性**：`TreeSet` 中的元素按照**自然顺序**（natural ordering）或提供的**比较器（Comparator）**排序。

    ```java
    TreeSet<T> treeSet = new TreeSet<>(Comparator<T> comparator);
    // example
    TreeSet set = new TreeSet(new Comparator<Object>() {
        public int compare(Object o1, Object o2) {
            return o1.toString().length() - o2.toString().length();
        }
    });

- **线程不安全**：`TreeSet` 不是线程安全的，多线程环境下需要外部同步（如使用 `Collections.synchronizedSortedSet`）。

他的继承关系是，

```java
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
```

### 底层原理

`TreeSet` 的底层是 `TreeMap`，`comparator` 是 `TreeMap`的属性。

```java
// TreeSet.java
public TreeSet(Comparator<? super E> comparator) {
    this(new TreeMap<>(comparator));
}

// TreeMap.java
public TreeMap(Comparator<? super K> comparator) {
    this.comparator = comparator;
}
```

调用`add`方法，`set`中的`value`都是常量`PRESENT`。

```java
// TreeMap.java
private V put(K key, V value, boolean replaceOld) {
    Entry<K,V> t = root;
    // 初次添加，设置根节点
    if (t == null) {
        addEntryToEmptyMap(key, value);
        return null;
    }
    int cmp;
    Entry<K,V> parent;
    // split comparator and comparable paths
    Comparator<? super K> cpr = comparator;
    if (cpr != null) { // 设置了比较器
        do { // 遍历所有key
            parent = t;
            cmp = cpr.compare(key, t.key); // 动态绑定匿名内部类的compare方法
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else { // key相等，只替换值，不替换键
                V oldValue = t.value;
                if (replaceOld || oldValue == null) {
                    t.value = value;
                }
                return oldValue;
            }
        } while (t != null);
    } else { // 没有比较器
        Objects.requireNonNull(key);
        @SuppressWarnings("unchecked")
        Comparable<? super K> k = (Comparable<? super K>) key;
        do {
            parent = t;
            cmp = k.compareTo(t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else {
                V oldValue = t.value;
                if (replaceOld || oldValue == null) {
                    t.value = value;
                }
                return oldValue;
            }
        } while (t != null);
    }
    addEntry(key, value, parent, cmp < 0);
    return null;
}
```



## Map 接口

`Map` 接口是 Java 集合框架中的一部分，位于 `java.util` 包中，用于存储键值对（key-value pairs）。

key 不允许重复，value 可以重复。

在前面的 `Set` 里面，其底层其实就是  `Map` ，只不过数据存在 `key` 中，`value` 用常量 `PRESENT` 代替了。

```java
// HashSet.java
static final Object PRESENT = new Object();
```

![image-20250520195139966](images/image-20250520195139966.png)

### Map 接口特点

- **键唯一性**：Map 中的**键是唯一的**，不能重复。如果插入重复的键，新值会覆盖旧值。

- **键值对**：每个键可以映射到一个值，**值可以重复**。

- **无序性**：Map 接口本身不保证键值对的顺序（某些实现类如 LinkedHashMap 除外）。

- **非集合**：Map 不是 Collection 的子接口，因此不能直接使用 Collection 的方法。

- **允许空值**：key和value都可以为`null`，但是key中的`null`只能有一个。
- **只允许引用类型**：Map中的key和value可以是任何类型的数据，会封装到 `HashMap$Node[]` 。

### 底层原理

`HashMap` 中，`table` 是一个内部数组（`Node[] table`），用于存储键值对的哈希表结构。

```java
// HashMap.java
transient Node<K,V>[] table;

Node<K,V> newNode(int hash, K key, V value, Node<K,V> next) {
    return new Node<>(hash, key, value, next);
}

// 静态内部类 Node，实现了Entry接口
static class Node<K,V> implements Map.Entry<K,V> { 
    final int hash;
    final K key;
    V value;
    HashMap.Node<K,V> next;

    Node(int hash, K key, V value, HashMap.Node<K,V> next) {
        this.hash = hash;
        this.key = key;
        this.value = value;
        this.next = next;
    }

    public final K getKey()        { return key; }
    public final V getValue()      { return value; }
    public final String toString() { return key + "=" + value; }

    public final int hashCode() {
        return Objects.hashCode(key) ^ Objects.hashCode(value);
    }

    public final V setValue(V newValue) {
        V oldValue = value;
        value = newValue;
        return oldValue;
    }

    public final boolean equals(Object o) {
        if (o == this)
            return true;

        return o instanceof Map.Entry<?, ?> e
                && Objects.equals(key, e.getKey())
                && Objects.equals(value, e.getValue());
    }
}
```

### Map 接口方法

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import java.util.Collection;

public class MapMethodsExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        Map<String, Integer> anotherMap = new HashMap<>();
        anotherMap.put("Dave", 40);
        anotherMap.put("Eve", 45);

        // 1. put(K key, V value)
        map.put("Alice", 25);  // 插入键值对到 Map 中，若键已存在则更新值 -> 返回 null（新插入）或旧值
        map.put("Bob", 30);
        System.out.println("Put 'Alice': " + map.put("Alice", 26));  // 更新 Alice 的值 -> 返回旧值 25

        // 2. putAll(Map<? extends K, ? extends V> m)
        map.putAll(anotherMap);  // 将另一个 Map 的所有键值对添加到当前 Map -> Dave:40, Eve:45
        System.out.println("After putAll: " + map);  // 输出: {Alice=26, Bob=30, Dave=40, Eve=45}

        // 3. get(Object key)
        Integer value = map.get("Bob");  // 根据键获取值，若键不存在返回 null -> 30
        System.out.println("Get 'Bob': " + value);

        // 4. remove(Object key)
        Integer removedValue = map.remove("Dave");  // 移除指定键及其值，返回被移除的值 -> 40
        System.out.println("Remove 'Dave': " + removedValue);

        // 5. clear()
        Map<String, Integer> tempMap = new HashMap<>(map);
        tempMap.clear();  // 清空 Map 中的所有键值对 -> 空 Map
        System.out.println("After clear: " + tempMap);  // 输出: {}

        // 6. containsKey(Object key)
        boolean hasKey = map.containsKey("Alice");  // 检查是否包含指定键 -> true
        System.out.println("Contains key 'Alice': " + hasKey);

        // 7. containsValue(Object value)
        boolean hasValue = map.containsValue(30);  // 检查是否包含指定值 -> true
        System.out.println("Contains value 30: " + hasValue);

        // 8. size()
        int size = map.size();  // 返回 Map 中的键值对数量 -> 3
        System.out.println("Size: " + size);

        // 9. isEmpty()
        boolean isEmpty = tempMap.isEmpty();  // 检查 Map 是否为空 -> true
        System.out.println("Is tempMap empty: " + isEmpty);

        // 10. keySet()
        Set<String> keys = map.keySet();  // 返回所有键的 Set 视图 -> [Alice, Bob, Eve]
        System.out.print("Keys: ");
        for (String key : keys) {
            System.out.print(key + " ");
        }
        System.out.println();

        // 11. values()
        Collection<Integer> values = map.values();  // 返回所有值的 Collection 视图 -> [26, 30, 45]
        System.out.print("Values: ");
        for (Integer val : values) {
            System.out.print(val + " ");
        }
        System.out.println();

        // 12. entrySet()
        Set<Map.Entry<String, Integer>> entries = map.entrySet();  // 返回所有键值对的 Set 视图
        System.out.print("Entries: ");
        for (Map.Entry<String, Integer> entry : entries) {
            System.out.print(entry.getKey() + "=" + entry.getValue() + " ");
        }
        System.out.println();

        // 13. getOrDefault(Object key, V defaultValue)
        Integer defaultValue = map.getOrDefault("Charlie", 0);  // 获取键的值，若键不存在返回默认值 -> 0
        System.out.println("GetOrDefault 'Charlie': " + defaultValue);

        // 14. putIfAbsent(K key, V value)
        Integer oldValue = map.putIfAbsent("Bob", 31);  // 若键不存在则插入，否则返回现有值 -> 30
        System.out.println("PutIfAbsent 'Bob': " + oldValue);
        map.putIfAbsent("Charlie", 35);  // 新插入 -> Charlie=35
        System.out.println("After putIfAbsent 'Charlie': " + map);

        // 15. computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)
        Integer computedValue = map.computeIfAbsent("Frank", k -> k.length() * 10);  // 若键不存在，计算值并插入 -> 50
        System.out.println("ComputeIfAbsent 'Frank': " + computedValue);
        System.out.println("After computeIfAbsent: " + map);

        // 16. replace(K key, V value)
        Integer replacedValue = map.replace("Alice", 27);  // 替换指定键的值，返回旧值 -> 26
        System.out.println("Replace 'Alice': " + replacedValue);

        // 17. replace(K key, V oldValue, V newValue)
        boolean replaced = map.replace("Bob", 30, 31);  // 若键存在且旧值匹配，替换为新值 -> true
        System.out.println("Replace 'Bob' 30 with 31: " + replaced);
        System.out.println("After replace: " + map);
    }
    	
    	// 18. merge(K key, V value, BiFunction remappingFunction)
    	map.put("Alice", 25);
    	map.put("Bob", 30);
    	map.merge("Alice", 5, Integer::sum); // key存在 - 合并值；若key不存在 - 直接插入
    	System.out.println(map.get("Alice")); // 30
    	map.merge("Bob", 50, Math::max);  // 取最大值: max(30, 50) = 50
    	System.out.println(map.get("Bob")); // 50
}
```

### 遍历 Map

#### 底层原理

为了**方便遍历**，java在Map接口设计时提供了**一系列集合**单独引用 所有的 key `keySet()`，所有的 value `values()`，所有的 key-value `entrySet()`。

```java
// Map.java
interface Entry<K, V> {
    K getKey();
    V getValue();
    /* 还许多其他方法 */
}

Set<K> keySet();
Collection<V> values();
Set<Map.Entry<K, V>> entrySet();
```

#### 六种遍历方法

使用 `keySet()`

```java
for (K key : map.keySet()) {
    V value = map.get(key);
    System.out.println("Key: " + key + ", Value: " + value);
}
```

使用 `values()`

```java
for (V value : map.values()) {
    System.out.println("Value: " + value);
}
```

使用 `entrySet()`

```java
for (Map.Entry<K, V> entry : map.entrySet()) {
    K key = entry.getKey();
    V value = entry.getValue();
    System.out.println("Key: " + key + ", Value: " + value);
}
```

使用 `Iterator`

```java
Iterator<Map.Entry<K, V>> iterator = map.entrySet().iterator();

while (iterator.hasNext()) {
    Map.Entry<K, V> entry = iterator.next();
    K key = entry.getKey();
    V value = entry.getValue();
    System.out.println("Key: " + key + ", Value: " + value);
    // 如果需要移除：iterator.remove();
}
```

使用 `forEach` 方法 (Java 8+)

```java
map.forEach((key, value) -> {
    System.out.println("Key: " + key + ", Value: " + value);
});
```

### 常用实现类

| 实现类                | 线程安全 | 有序性               | 允许null          | 底层结构         | 时间复杂度 |
| :-------------------- | :------- | :------------------- | :---------------- | :--------------- | :--------- |
| **HashMap**           | 否       | 无顺序               | key/value都允许   | 数组+链表/红黑树 | O(1)       |
| **LinkedHashMap**     | 否       | 插入顺序/访问顺序    | key/value都允许   | 哈希表+双向链表  | O(1)       |
| **TreeMap**           | 否       | key自然顺序/定制顺序 | key不允许         | 红黑树           | O(log n)   |
| **Hashtable**         | 是       | 无顺序               | key/value都不允许 | 数组+链表        | O(1)       |
| **ConcurrentHashMap** | 是       | 无顺序               | key/value都不允许 | 分段锁/CAS       | O(1)       |



## HashMap

`HashMap` 是 Java 集合框架中的一个类，位于 java.util 包中，实现了 Map 接口，用于存储键值对（key-value pairs）。

`HashMap` **非线程安全**，适合单线程环境，多线程需使用 `ConcurrentHashMap` 或外部同步。

**其底层机制见之前的 `HashSet` 。**

以下是`HashMap`的继承关系，

```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {}
```



## HashTable

`Hashtable` 是 Java 集合框架中的一个类，位于 `java.util` 包中，实现了 `Map` 接口，用于存储键值对（key-value pairs）。

**特点**：

- **线程安全**：所有方法都用 `synchronized` 修饰，适合多线程环境，但性能较低。
- **键值限制**：键和值都不能为 `null`。否则抛出 **`NullPointerException`**

以下是`Hashtable`的继承关系，

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable {}
```

### 底层机制

```java
Hashtable map = new Hashtable();
```

调用构造器，初始容量为11，

```java
public Hashtable() {
    this(11, 0.75f);
}
```

 执行`put`方法，

```java
public synchronized V put(K key, V value) {
    // Make sure the value is not null
    if (value == null) {
        throw new NullPointerException();
    }

    // Makes sure the key is not already in the hashtable.
    Hashtable.Entry<?,?> tab[] = table;
    int hash = key.hashCode();
    int index = (hash & 0x7FFFFFFF) % tab.length;
    @SuppressWarnings("unchecked")
    Hashtable.Entry<K,V> entry = (Hashtable.Entry<K,V>)tab[index];
    for(; entry != null ; entry = entry.next) {
        if ((entry.hash == hash) && entry.key.equals(key)) {
            V old = entry.value;
            entry.value = value;
            return old;
        }
    }

    addEntry(hash, key, value, index); // 添加键值对，必要时扩容
    return null;
}
```

### 扩容机制

当 `Hashtable` 中的键值对数量（size）超过或等于阈值时，会触发扩容。

`New Capacity = Old Capacity × 2 + 1`。这种扩容方式（2n + 1）与 `HashMap`（直接翻倍）不同，旨在**保持容量为奇数**以减少哈希冲突。

例如，初始容量 = 11，负载因子 = 0.75，阈值 = 11 × 0.75 = 8（取整）。当存储第 8 个键值对后，尝试添加第 9 个键值对时，size + 1 = 9 > 8，触发扩容。

```java
// Hashtable.java
private void addEntry(int hash, K key, V value, int index) {
    Hashtable。.Entry<?,?> tab[] = table
    // 超过阈值，扩容
    if (count >= threshold) {
        // Rehash the table if the threshold is exceeded
        rehash(); // 两倍加一的大小扩容

        tab = table;
        hash = key.hashCode();
        index = (hash & 0x7FFFFFFF) % tab.length;
    }

    // Creates the new entry.
    @SuppressWarnings("unchecked")
    Hashtable.Entry<K,V> e = (Hashtable.Entry<K,V>) tab[index];
    tab[index] = new Hashtable.Entry<>(hash, key, value, e);
    count++;
    modCount++;
}

protected void rehash() {
    int oldCapacity = table.length;
    Hashtable.Entry<?,?>[] oldMap = table;

    // overflow-conscious code
    int newCapacity = (oldCapacity << 1) + 1; // 两倍加一的大小扩容
    if (newCapacity - MAX_ARRAY_SIZE > 0) {
        if (oldCapacity == MAX_ARRAY_SIZE)
            // Keep running with MAX_ARRAY_SIZE buckets
            return;
        newCapacity = MAX_ARRAY_SIZE;
    }
    // 创建新数组
    Hashtable.Entry<?,?>[] newMap = new Hashtable.Entry<?,?>[newCapacity];

    modCount++;
    // 更新阈值
    threshold = (int)Math.min(newCapacity * loadFactor, MAX_ARRAY_SIZE + 1);
    table = newMap;

    // 重新哈希（因为数组长度变化，哈希函数的结果会变）
    for (int i = oldCapacity ; i-- > 0 ;) {
        for (Hashtable.Entry<K,V> old = (Hashtable.Entry<K,V>)oldMap[i]; old != null ; ) {
            Hashtable.Entry<K,V> e = old;
            old = old.next;

            // 根据键的 hashCode() 和新数组的容量，重新计算每个键的索引位置
            int index = (e.hash & 0x7FFFFFFF) % newCapacity;
            e.next = (Hashtable.Entry<K,V>)newMap[index];
            newMap[index] = e;
        }
    }
}
```



## Properties

`Properties` 类是 `java.util` 包中的一个类，用于处理键值对形式的配置数据。

**特点**：

- **键值对存储**：`Properties` 是一个**线程安全**的类，键和值都是**字符串**（String），适合存储配置信息。
- **文件操作**：支持从文件（`.properties` 文件或 `XML` 文件）加载数据或将数据保存到文件中。
- **默认值**：支持设置默认属性，当查找某个键不存在时返回默认值。

他的继承关系是，

```java
public class Properties extends Hashtable<Object,Object> {}
```

### 私有方法

```java
import java.util.Properties;
import java.util.Set;
import java.io.FileOutputStream;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class PropertiesUniqueMethodsExample {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.setProperty("app.name", "MyApp");
        props.setProperty("app.port", "8080");

        // 1. setProperty(String key, String value)
        String oldValue = props.setProperty("app.name", "NewApp");  // 设置字符串键值对，若键存在则更新值 -> 返回旧值或 null
        System.out.println("Set 'app.name': " + oldValue);  // 输出: MyApp

        // 2. getProperty(String key)
        String value = props.getProperty("app.port");  // 获取指定键的字符串值，若键不存在返回 null -> 8080
        System.out.println("Get 'app.port': " + value);

        // 3. getProperty(String key, String defaultValue)
        String defaultValue = props.getProperty("app.user", "admin");  // 获取键的值，若键不存在返回默认值 -> admin
        System.out.println("GetOrDefault 'app.user': " + defaultValue);

        // 4. stringPropertyNames()
        Set<String> keys = props.stringPropertyNames();  // 返回所有字符串键的 Set 视图 -> [app.name, app.port]
        System.out.print("Keys: ");
        for (String key : keys) {
            System.out.print(key + " ");
        }
        System.out.println();

        // 5. load(InputStream inStream)
        Properties loadedProps = new Properties();
        try (FileInputStream fis = new FileInputStream("config.properties")) {
            loadedProps.load(fis);  // 从输入流加载 .properties 文件
            System.out.println("Loaded Properties: " + loadedProps);  // 输出: 取决于文件内容
        } catch (IOException e) {
            System.out.println("Load failed: " + e.getMessage());
        }

        // 6. load(Reader reader)
        loadedProps.clear();
        try (InputStreamReader reader = new InputStreamReader(
                new FileInputStream("config.properties"), "UTF-8")) {
            loadedProps.load(reader);  // 从字符流加载，支持指定编码（如 UTF-8）
            System.out.println("Loaded with Reader: " + loadedProps);  // 输出: 取决于文件内容
        } catch (IOException e) {
            System.out.println("Load with Reader failed: " + e.getMessage());
        }

        // 7. store(OutputStream out, String comments)
        try (FileOutputStream fos = new FileOutputStream("config.properties")) {
            props.store(fos, "Application Configuration");  // 将 Properties 保存到输出流，带注释
            System.out.println("Properties saved to config.properties");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 8. store(Writer writer, String comments)
        try (OutputStreamWriter writer = new OutputStreamWriter(
                new FileOutputStream("config_utf8.properties"), "UTF-8")) {
            props.store(writer, "UTF-8 Configuration");  // 保存到字符流，支持指定编码
            System.out.println("Properties saved to config_utf8.properties");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 9. storeToXML(OutputStream out, String comment)
        try (FileOutputStream fos = new FileOutputStream("config.xml")) {
            props.storeToXML(fos, "XML Configuration");  // 将 Properties 保存为 XML 文件
            System.out.println("Properties saved to config.xml");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 10. storeToXML(OutputStream out, String comment, String encoding)
        try (FileOutputStream fos = new FileOutputStream("config_utf8.xml")) {
            props.storeToXML(fos, "XML UTF-8 Configuration", "UTF-8");  // 保存为 XML 文件，指定编码
            System.out.println("Properties saved to config_utf8.xml");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 11. loadFromXML(InputStream in)
        Properties xmlProps = new Properties();
        try (FileInputStream fis = new FileInputStream("config.xml")) {
            xmlProps.loadFromXML(fis);  // 从 XML 文件加载 Properties
            System.out.println("Loaded from XML: " + xmlProps);  // 输出: {app.name=NewApp, app.port=8080}
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 12. list(PrintStream out)
        System.out.println("List all properties:");
        props.list(System.out);  // 输出所有键值对到指定 PrintStream
    }
}
```



## TreeMap

`TreeMap` 是 Java 集合框架中的一个类，位于 `java.util` 包下，实现了 `NavigableMap` 接口，基于**红黑树**（自平衡二叉搜索树）实现，提供了一个**键值对存储**的集合，键（key）按照**自然顺序**或**自定义 `Comparator`** 排序。

`TreeMap` 是**线程不安全**的，多线程环境下需外部同步（如使用 `Collections.synchronizedSortedMap`）。

```java
public class TreeMap<K,V>
    extends AbstractMap<K,V>
    implements NavigableMap<K,V>, Cloneable, java.io.Serializable
```

`TreeMap`可以指定 `Comparator` 自定义键的排序

```java
TreeMap map = new TreeMap(new Comparator<Object>() {
    public int compare(Object o1, Object o2) {
        return o1.toString().length() - o2.toString().length();
    }
});

map.put(1, 1);
map.put(222, 223);
map.put(333, 33);

// 222与333长度相等，所以key相等
// key相等, 只替换值，不替换键
System.out.println(map); // {1=1, 222=33}
```

其底层机制，见 `TreeSet`。









## Collections 工具类

`Collections` 是 `java.util` 包中的一个工具类，提供了许多静态方法，用于操作和处理集合（如 `List`、`Set`、`Map` 等）。

### Collections 类的作用

Collections 类提供了以下几类静态方法：

1. **排序操作**：对集合进行排序、反转等。
2. **搜索操作**：如二分查找。
3. **同步化**：将非线程安全的集合转换为线程安全的集合。
4. **不可修改集合**：创建只读集合。
5. **其他工具方法**：如最大/最小值、替换、填充等。

### 常用方法

```java
import java.util.*;
import java.time.LocalDateTime;

public class CollectionsMethodsExample {
    public static void main(String[] args) {
        // 初始化 TreeSet 和 TreeMap 对象（当前时间：2025-05-21 10:09:00 HKT）
        TreeSet<String> treeSet = new TreeSet<>(); // 使用自然顺序
        TreeMap<String, Integer> treeMap = new TreeMap<>(); // 使用自然顺序
        // 添加初始元素
        treeSet.add("Apple");
        treeSet.add("Banana");
        treeMap.put("Apple", 1);
        treeMap.put("Banana", 2);

        // 1. sort(List<T> list)
        // 对 List 排序（TreeSet/TreeMap 已有序，此处转换为 List 演示）
        List<String> list = new ArrayList<>(treeSet); // 从 TreeSet 转换为 List
        Collections.sort(list); // 触发 sort，保持自然顺序
        System.out.println("After Collections.sort (List from TreeSet): " + list); // 输出: [Apple, Banana]

        // 2. sort(List<T> list, Comparator<? super T> c)
        // 使用自定义 Comparator 排序 List
        Comparator<String> lengthComparator = Comparator.comparing(String::length);
        Collections.sort(list, lengthComparator); // 按长度排序
        System.out.println("After Collections.sort with lengthComparator: " + list); // 输出: [Apple, Banana]

        // 3. reverseOrder()
        // 创建逆序 Comparator，用于 TreeSet/TreeMap
        TreeSet<String> reverseSet = new TreeSet<>(Collections.reverseOrder());
        reverseSet.addAll(treeSet);
        System.out.println("After Collections.reverseOrder (TreeSet): " + reverseSet); // 输出: [Banana, Apple]

        // 4. reverseOrder(Comparator<T> cmp)
        // 反转自定义 Comparator
        TreeMap<String, Integer> reverseLengthMap = new TreeMap<>(Collections.reverseOrder(lengthComparator));
        reverseLengthMap.putAll(treeMap);
        System.out.println("After Collections.reverseOrder(lengthComparator) (TreeMap): " + reverseLengthMap); // 输出: {Banana=2, Apple=1}

        // 5. binarySearch(List<? extends Comparable<? super T>> list, T key)
        // 在有序 List 中进行二分查找
        int index = Collections.binarySearch(list, "Banana"); // 需确保 List 已排序
        System.out.println("After Collections.binarySearch (Banana): " + index); // 输出: 1

        // 6. binarySearch(List<? extends T> list, T key, Comparator<? super T> c)
        // 使用自定义 Comparator 进行二分查找
        index = Collections.binarySearch(list, "Apple", lengthComparator);
        System.out.println("After Collections.binarySearch with lengthComparator (Apple): " + index); // 输出: 0

        // 7. synchronizedSortedSet(SortedSet<T> s)
        // 将 TreeSet 转换为线程安全的 SortedSet
        SortedSet<String> syncSet = Collections.synchronizedSortedSet(new TreeSet<>(treeSet));
        syncSet.add("Orange"); // 线程安全添加
        System.out.println("After Collections.synchronizedSortedSet: " + syncSet); // 输出: [Apple, Banana, Orange]

        // 8. synchronizedSortedMap(SortedMap<K, V> m)
        // 将 TreeMap 转换为线程安全的 SortedMap
        SortedMap<String, Integer> syncMap = Collections.synchronizedSortedMap(new TreeMap<>(treeMap));
        syncMap.put("Orange", 3); // 线程安全添加
        System.out.println("After Collections.synchronizedSortedMap: " + syncMap); // 输出: {Apple=1, Banana=2, Orange=3}

        // 9. unmodifiableSortedSet(SortedSet<T> s)
        // 创建只读 TreeSet
        SortedSet<String> unmodifiableSet = Collections.unmodifiableSortedSet(treeSet);
        System.out.println("After Collections.unmodifiableSortedSet: " + unmodifiableSet); // 输出: [Apple, Banana]
        try {
            unmodifiableSet.add("Orange"); // 抛出 UnsupportedOperationException
        } catch (UnsupportedOperationException e) {
            System.out.println("After unmodifiableSortedSet (add attempt): " + e.getMessage());
        }

        // 10. unmodifiableSortedMap(SortedMap<K, V> m)
        // 创建只读 TreeMap
        SortedMap<String, Integer> unmodifiableMap = Collections.unmodifiableSortedMap(treeMap);
        System.out.println("After Collections.unmodifiableSortedMap: " + unmodifiableMap); // 输出: {Apple=1, Banana=2}
        try {
            unmodifiableMap.put("Orange", 3); // 抛出 UnsupportedOperationException
        } catch (UnsupportedOperationException e) {
            System.out.println("After unmodifiableSortedMap (put attempt): " + e.getMessage());
        }

        // 12. max(Collection<? extends T> coll[, Comparator<? super T> comp])
        // 使用自定义 Comparator 查找最大元素
        String maxLength = Collections.max(treeSet, lengthComparator);
        System.out.println("After Collections.max with lengthComparator: " + maxLength); // 输出: Banana

        // 14. min(Collection<? extends T> coll[, Comparator<? super T> comp])
        // 使用自定义 Comparator 查找最小元素
        String minLength = Collections.min(treeSet, lengthComparator);
        System.out.println("After Collections.min with lengthComparator: " + minLength); // 输出: Apple

        // 15. reverse(List<?> list)
        // 反转 List（需从 TreeSet/TreeMap 转换为 List）
        List<String> reverseList = new ArrayList<>(treeSet);
        Collections.reverse(reverseList);
        System.out.println("After Collections.reverse (List from TreeSet): " + reverseList); // 输出: [Banana, Apple]
    
    	// 16. shuffle(List<?> list[, Random random]) 使用指定随机源打乱 List
    	List<String> listFromMapKeys = new ArrayList<>(treeMap.keySet());
    	Random random = new Random(123); // 设置固定种子以便结果可重现
    	Collections.shuffle(listFromMapKeys, random); // 使用指定随机源打乱
    	System.out.println("After Collections.shuffle with Random (List from TreeMap keys): " + listFromMapKeys);
        // 输出示例: [Apple, Banana]（种子固定时结果一致）
    
    	// 17.swap(List<?> list, int i, int j)
    	List<String> listFromSet = new ArrayList<>(treeSet);
    	System.out.println("Before swap (List from TreeSet): " + listFromSet); // 输出: [Apple, Banana]
        Collections.swap(listFromSet, 0, 1); // 交换索引 0 和 2 的元素
        System.out.println("After Collections.swap (indexes 0 and 2): " + listFromSet); // 输出: [Banana, Apple]
    }
    
        // 18.frequency(Collection<?> c, Object o)
    	int appleFreqInSet = Collections.frequency(treeSet, "Apple");
        System.out.println("After Collections.frequency (Apple in TreeSet): " + appleFreqInSet); // 输出: 1
    
    	// 19.replaceAll(List<T> list, T oldVal, T newVal) 返回 true 如果至少替换了一个元素
    	List<String> listFromSet = new ArrayList<>(treeSet); // 从 TreeSet 转换为 List
        listFromSet.add("Apple"); // 添加重复元素
        System.out.println("Before replaceAll (List from TreeSet): " + listFromSet); // 输出: [Apple, Banana, Apple]
        boolean replacedInSet = Collections.replaceAll(listFromSet, "Apple", "Grape");
        System.out.println("After Collections.replaceAll (Apple -> Grape): " + listFromSet); // 输出: [Grape, Banana, Grape]
        System.out.println("Replaced: " + replacedInSet); // 输出: true
}
```



## Queue 接口

`Queue` 接口是 Java 集合框架中的一部分，位于 `java.util` 包中，用于处理遵循先进先出（FIFO）原则的元素集合。

在前面的 `Stack` 类中，虽然也是线性结构，但遵循后进先出（LIFO）原则，而 Queue 则是先进先出。

```java
// LinkedList 实现了 Queue 接口
Queue<String> queue = new LinkedList<>();
```

### Queue 接口特点

- **先进先出**：Queue 遵循**先进先出（FIFO）**原则，最先添加的元素最先被移除。

- **队尾插入**：新元素总是添加到队列的末尾。

- **队头移除**：元素总是从队列的头部被移除。

- **不允许空元素**：大多数 Queue 实现**不允许 null 元素**，但 LinkedList 等实现允许。

- **线程安全选项**：某些实现如 `ArrayBlockingQueue` 提供线程安全特性。

- **容量限制**：某些队列实现可能有容量限制。

### 底层原理

`LinkedList` 中，Queue 操作基于双向链表实现：

```java
// LinkedList.java
transient Node<E> first;
transient Node<E> last;

private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;

    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

### Queue 接口方法

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.PriorityQueue;
import java.util.ArrayDeque;

public class QueueMethodsExample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();
        
        // 1. add(E e) - 添加元素到队列尾部
        queue.add("Alice");  // 添加元素，如果队列已满则抛出异常
        queue.add("Bob");
        queue.add("Charlie");
        System.out.println("After add: " + queue);  // [Alice, Bob, Charlie]

        // 2. offer(E e) - 添加元素到队列尾部
        boolean offered = queue.offer("Dave");  // 添加元素，返回是否成功
        System.out.println("Offer 'Dave': " + offered);  // true
        System.out.println("After offer: " + queue);  // [Alice, Bob, Charlie, Dave]

        // 3. remove() - 移除并返回队列头部元素
        String removed = queue.remove();  // 移除头部元素，如果队列为空则抛出异常
        System.out.println("Removed: " + removed);  // Alice
        System.out.println("After remove: " + queue);  // [Bob, Charlie, Dave]

        // 4. poll() - 移除并返回队列头部元素
        String polled = queue.poll();  // 移除头部元素，队列为空时返回null
        System.out.println("Polled: " + polled);  // Bob
        System.out.println("After poll: " + queue);  // [Charlie, Dave]

        // 5. element() - 查看队列头部元素但不移除
        String head = queue.element();  // 返回头部元素，如果队列为空则抛出异常
        System.out.println("Head element: " + head);  // Charlie

        // 6. peek() - 查看队列头部元素但不移除
        String peeked = queue.peek();  // 返回头部元素，队列为空时返回null
        System.out.println("Peeked: " + peeked);  // Charlie

        // 7. size() - 返回队列中元素数量
        int size = queue.size();  // 返回队列大小
        System.out.println("Queue size: " + size);  // 2

        // 8. isEmpty() - 检查队列是否为空
        boolean empty = queue.isEmpty();  // 检查队列是否为空
        System.out.println("Is empty: " + empty);  // false

        // 9. clear() - 清空队列
        Queue<String> tempQueue = new LinkedList<>(queue);
        tempQueue.clear();  // 清空队列中的所有元素
        System.out.println("After clear: " + tempQueue);  // []

        // 10. contains(Object o) - 检查是否包含指定元素
        boolean containsCharlie = queue.contains("Charlie");  // 检查是否包含元素
        System.out.println("Contains 'Charlie': " + containsCharlie);  // true
}
```

### 队列操作对比

| 操作     | 抛出异常的方法 | 返回特殊值的方法 |
| -------- | -------------- | ---------------- |
| **插入** | `add(e)`       | `offer(e)`       |
| **移除** | `remove()`     | `poll()`         |
| **检查** | `element()`    | `peek()`         |

### 常用实现类

| 实现类                  | 特点                 | 适用场景         |
| ----------------------- | -------------------- | ---------------- |
| **LinkedList**          | 基于链表，无容量限制 | 通用队列需求     |
| **ArrayDeque**          | 基于数组，性能较好   | 高频插入删除     |
| **PriorityQueue**       | 优先级队列，元素排序 | 任务调度         |
| **ArrayBlockingQueue**  | 线程安全，容量固定   | 生产者消费者模式 |
| **LinkedBlockingQueue** | 线程安全，可选容量   | 高并发场景       |



## ArrayDeque

![集合框架之ArrayDeque类详解-CSDN博客](images/19570e6609b880d77f0353cda85ee0b8.png)

### 概述

`ArrayDeque` 是 Java 集合框架中的一个双端队列实现，基于可调整大小的数组。它既可以用作队列（FIFO），也可以用作栈（LIFO），性能优于 `LinkedList`。

```java
// ArrayDeque 的基本使用
ArrayDeque<String> deque = new ArrayDeque<>();
```

### 核心特性

- **双端操作**：支持在队列两端进行高效的插入和删除操作
- **数组实现**：基于可动态扩容的循环数组
- **无容量限制**：自动扩容（2的幂次方）
- **非线程安全**：需要外部同步
- **性能优异**：比 LinkedList 更快的随机访问
- **不允许 null 元素**：会抛出 NullPointerException

### `ArrayDeque` 私有方法

```java
import java.util.ArrayDeque;
import java.util.Iterator;

public class ArrayDequePrivateMethodsExample {
    public static void main(String[] args) {
        // 创建初始容量为 4 的 ArrayDeque
        ArrayDeque<String> deque = new ArrayDeque<>(4);
        
        System.out.println("初始 ArrayDeque，容量: 4");
        
        // 1. addFirst(E e) - 头部添加元素
        deque.addFirst("First");
        deque.addFirst("Head");
        System.out.println("After addFirst: " + deque); // [Head, First]
        
        // 2. addLast(E e) - 尾部添加元素
        deque.addLast("Last");
        deque.addLast("Tail");
        System.out.println("After addLast: " + deque); // [Head, First, Last, Tail]
        
        // 3. 触发扩容 - doubleCapacity()
        deque.addLast("New Element"); // 触发扩容，容量翻倍为 8
        System.out.println("After doubleCapacity: " + deque); 
        // [Head, First, Last, Tail, New Element]
        
        // 4. pollFirst() - 头部移除元素
        String first = deque.pollFirst();
        System.out.println("pollFirst: " + first); // Head
        System.out.println("After pollFirst: " + deque); // [First, Last, Tail, New Element]
        
        // 5. pollLast() - 尾部移除元素
        String last = deque.pollLast();
        System.out.println("pollLast: " + last); // New Element
        System.out.println("After pollLast: " + deque); // [First, Last, Tail]
        
        // 6. getFirst() 和 getLast() - 查看元素
        System.out.println("getFirst: " + deque.getFirst()); // First
        System.out.println("getLast: " + deque.getLast());   // Tail
        
        // 7. offerFirst(E e) 和 offerLast(E e) - 推荐使用的添加方法
        boolean offeredFirst = deque.offerFirst("New Head");
        boolean offeredLast = deque.offerLast("New Tail");
        System.out.println("After offer: " + deque); 
        // [New Head, First, Last, Tail, New Tail]
        
        // 8. peekFirst() 和 peekLast() - 安全查看元素
        System.out.println("peekFirst: " + deque.peekFirst()); // New Head
        System.out.println("peekLast: " + deque.peekLast());   // New Tail
        
        // 9. removeFirstOccurrence(Object o) - 删除第一次出现的元素
        deque.addLast("First"); // 添加重复元素
        boolean removed = deque.removeFirstOccurrence("First");
        System.out.println("removeFirstOccurrence 'First': " + removed); // true
        System.out.println("After removeFirstOccurrence: " + deque);
        // [New Head, Last, Tail, New Tail, First]
        
        // 10. removeLastOccurrence(Object o) - 删除最后一次出现的元素
        boolean removedLast = deque.removeLastOccurrence("First");
        System.out.println("removeLastOccurrence 'First': " + removedLast); // true
        System.out.println("After removeLastOccurrence: " + deque);
        // [New Head, Last, Tail, New Tail]
        
        // 11. size() 和 isEmpty()
        System.out.println("Size: " + deque.size()); // 4
        System.out.println("isEmpty: " + deque.isEmpty()); // false
        
        // 12. contains(Object o)
        System.out.println("Contains 'Last': " + deque.contains("Last")); // true
        
        // 13. toArray() - 转换为数组
        Object[] array = deque.toArray();
        System.out.print("toArray: ");
        for (Object obj : array) {
            System.out.print(obj + " ");
        }
        System.out.println();
        
        // 14. clear() - 清空队列
        deque.clear();
        System.out.println("After clear - Size: " + deque.size()); // 0
        System.out.println("After clear - isEmpty: " + deque.isEmpty()); // true
        
        // 15. 迭代器使用
        deque.addLast("A");
        deque.addLast("B");
        deque.addLast("C");
        
        System.out.print("Iterator: ");
        Iterator<String> iterator = deque.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " "); // A B C
        }
        System.out.println();
        
        System.out.print("Descending Iterator: ");
        Iterator<String> descIterator = deque.descendingIterator();
        while (descIterator.hasNext()) {
            System.out.print(descIterator.next() + " "); // C B A
        }
        System.out.println();
    }
}
```

### 扩容机制

**底层数据结构**

```java
// ArrayDeque 内部结构
transient Object[] elements;  // 存储元素的数组
transient int head;           // 头部指针
transient int tail;           // 尾部指针
private static final int MIN_INITIAL_CAPACITY = 8;
```

`ArrayDeque` 维护了一个 `Object` 类型的数组 `elements`，采用循环数组的方式实现。

```java
// 扩容核心方法
private void doubleCapacity() {
    assert head == tail;
    int p = head;
    int n = elements.length;
    int r = n - p; // number of elements to the right of p
    
    // 新容量是原容量的2倍
    int newCapacity = n << 1;
    if (newCapacity < 0)
        throw new IllegalStateException("Sorry, deque too big");
    
    Object[] a = new Object[newCapacity];
    
    // 复制元素到新数组
    System.arraycopy(elements, p, a, 0, r);
    System.arraycopy(elements, 0, a, r, p);
    
    elements = a;
    head = 0;
    tail = n;
}
```

**扩容规则：**
- **初始容量**：如果未指定，默认最小容量为 8
- **指定容量**：如果指定初始容量，会调整为大于等于该值的最小的 2 的幂次方
- **扩容时机**：当数组满时，容量翻倍（变为原来的 2 倍）
- **循环数组**：使用 `head` 和 `tail` 指针实现循环数组，提高空间利用率





# IO流



## 基本概念

**文件流**：文件在程序中是以流的形式来操作的，主要分为**字节流**和**字符流**两大类。

![image-20250730221251844](images/image-20250730221251844.png)

Java I/O 系统的核心是四个抽象基类，它们构成了整个Java I/O体系的基石。

### 字节流 & 字符流

| 抽象基类       | 方向 | 数据单位 | 直接子类示例                                |
| :------------- | :--- | :------- | :------------------------------------------ |
| `InputStream`  | 输入 | 字节     | `FileInputStream`, `ByteArrayInputStream`   |
| `OutputStream` | 输出 | 字节     | `FileOutputStream`, `ByteArrayOutputStream` |
| `Reader`       | 输入 | 字符     | `FileReader`, `StringReader`                |
| `Writer`       | 输出 | 字符     | `FileWriter`, `StringWriter`                |

![io](images/java-io-stream-preview-compression.png)



### 节点流 & 处理流

**节点流**：是直接与数据源/目的地连接的流，也称为低级流(low-level stream)。

| 数据源类型 | 输入流                               | 输出流                                |
| :--------- | :----------------------------------- | :------------------------------------ |
| 文件       | FileInputStream FileReader           | FileOutputStream FileWriter           |
| 内存       | ByteArrayInputStream CharArrayReader | ByteArrayOutputStream CharArrayWriter |
| 管道       | PipedInputStream PipedReader         | PipedOutputStream PipedWriter         |

**处理流（包装流）**：是对节点流或其他处理流的包装[装饰器模式]，也称为高级流(high-level stream)。

| 功能         | 输入流                             | 输出流                              |
| :----------- | :--------------------------------- | :---------------------------------- |
| 缓冲         | BufferedInputStream BufferedReader | BufferedOutputStream BufferedWriter |
| 数据转换     | DataInputStream                    | DataOutputStream                    |
| 对象序列化   | ObjectInputStream                  | ObjectOutputStream                  |
| 字符编码转换 | InputStreamReader                  | OutputStreamWriter                  |
| 行处理       | LineNumberReader                   | -                                   |



### 序列化 & 反序列化

**序列化** (Serialization)： 是将对象转换为字节流的过程。

**反序列化** (Deserialization)： 是将字节流转换回对象的过程。

序列化对象时，要求里面的属性的类型也需要实现序列化接口。

#### Serializable 接口

`Serializable` 是 Java 提供的**标记接口**（没有方法的接口），用于标识类的对象可以被序列化。它是 Java 对象序列化机制的核心。

```java
import java.io.*;

// 实现Serializable接口的类
class Person implements Serializable {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        // 序列化
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("person.ser"))) {
            Person person = new Person("张三", 25);
            oos.writeObject(person);
            System.out.println("对象已序列化");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // 反序列化
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("person.ser"))) {
            Person restoredPerson = (Person) ois.readObject();
            System.out.println("反序列化得到的对象: " + restoredPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

#### Externalizable 接口

`Externalizable` 是 Java 提供的另一个序列化接口，它继承自 `Serializable` 接口，但提供了更细粒度的控制，允许开发者完全**自定义序列化和反序列化**的过程，也就是必须实现`writeExternal/readExternal` 方法。

```java
import java.io.*;

class Book implements Externalizable {
    private String title;
    private String author;
    
    // 必须有无参构造函数
    public Book() {}
    
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
    
    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(title);
        out.writeUTF(author);
    }
    
    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        title = in.readUTF();
        author = in.readUTF();
    }
    
    @Override
    public String toString() {
        return "Book{title='" + title + "', author='" + author + "'}";
    }
}
```



#### `serialVersionUID`

`serialVersionUID` 是用来验证序列化对象和反序列化对象版本一致性的标识符，为了提高版本兼容性。

##### 基本概念

**1. 什么是 serialVersionUID**

- 每个可序列化类都有一个版本号
- 静态 final long 类型变量
- 用于验证序列化的发送者和接收者是否加载了与序列化兼容的类

**2. 默认行为**

如果类没有显式声明 `serialVersionUID`，序列化运行时将基于类的各个方面自动计算一个默认值：

```java
// 没有显式声明时，JVM会自动生成
private static final long serialVersionUID = 456789123L; // 示例值
```

##### 为什么重要

**1. 版本兼容性控制**

当类的结构发生变化时：

- **serialVersionUID 相同**：认为版本兼容
- **serialVersionUID 不同**：抛出 `InvalidClassException`

**2. 避免意外不兼容**

自动生成的 serialVersionUID 对类细节非常敏感，任何改变都会导致值变化：

- 添加/删除方法 - 不影响
- 添加/删除字段 - 影响
- 改变字段类型 - 影响
- 改变类继承结构 - 影响

#### transient 关键字

`transient` 是 Java 中的一个关键字，用于标记类的成员变量在对象序列化过程中应该被忽略。

- 标记为`transient`或`static`字段不应被序列化
- 反序列化时，transient 字段会被赋予默认值（null、0 或 false）





## File

在 Java 中，`File` 类用于表示文件和目录。

![image-20250730224409059](images/image-20250730224409059.png)

### 创建 File 对象

```java
// 引入File类
import java.io.File;

public class FileExample {
    public static void main(String[] args) {
        try {
        	// 使用文件路径创建 File 对象
        	File file = new File("example.txt");
        	// 使用目录路径创建 File 对象
        	File directory = new File("myDirectory");
        	// 使用绝对路径创建 File 对象
        	File file = new File("/home/user/docs/example.txt");
        } catch () {
            
        }
    }
}
```

### 常用方法

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.util.Date;

public class FileExample {
    public static void main(String[] args) {
        try {
            // 1. 创建File对象的方式
            File file1 = new File("example.txt");              // 当前目录下的文件
            File file2 = new File("C:/test/example.txt");      // 绝对路径
            File dir = new File("testDir");                    // 目录
            
            // 2. 创建文件和目录
            System.out.println("创建新文件: " + file1.createNewFile());
            System.out.println("创建目录: " + dir.mkdir());
            
            // 3. 文件基本信息获取
            System.out.println("文件名: " + file1.getName());
            System.out.println("绝对路径: " + file1.getAbsolutePath());
            System.out.println("父目录: " + file1.getParent());
            System.out.println("路径: " + file1.getPath());
            System.out.println("文件大小: " + file1.length() + " bytes");
            System.out.println("最后修改时间: " + new Date(file1.lastModified()));
            
            // 4. 文件状态检查
            System.out.println("是否存在: " + file1.exists());
            System.out.println("是文件吗: " + file1.isFile());
            System.out.println("是目录吗: " + file1.isDirectory());
            System.out.println("可读吗: " + file1.canRead());
            System.out.println("可写吗: " + file1.canWrite());
            System.out.println("可执行吗: " + file1.canExecute());
            System.out.println("是隐藏文件吗: " + file1.isHidden());
            
            // 5. 文件权限设置
            System.out.println("设置为只读: " + file1.setReadOnly());
            System.out.println("设置可写: " + file1.setWritable(true));
            System.out.println("设置可执行: " + file1.setExecutable(true));
            
            // 6. 创建临时文件
            File tempFile = File.createTempFile("prefix", ".tmp");
            System.out.println("临时文件路径: " + tempFile.getAbsolutePath());
            
            // 7. 文件空间信息
            System.out.println("总空间: " + file1.getTotalSpace() / 1024 / 1024 + " MB");
            System.out.println("剩余空间: " + file1.getFreeSpace() / 1024 / 1024 + " MB");
            System.out.println("可用空间: " + file1.getUsableSpace() / 1024 / 1024 + " MB");
            
            // 8. 列出目录内容
            File rootDir = new File(".");
            File[] files = rootDir.listFiles();
            if (files != null) {
                System.out.println("当前目录文件列表:");
                for (File f : files) {
                    System.out.println(f.getName() + (f.isDirectory() ? " [DIR]" : ""));
                }
            }
            
            // 9. 文件重命名
            File newFile = new File("example_new.txt");
            System.out.println("重命名: " + file1.renameTo(newFile));
            
            // 10. 删除文件
            System.out.println("删除临时文件: " + tempFile.delete());
            
            // 11. 设置最后修改时间
            System.out.println("设置修改时间: " + newFile.setLastModified(System.currentTimeMillis()));
            
            // 清理示例文件
            newFile.delete();
            dir.delete();

        } catch (IOException e) {
            System.out.println("发生错误: " + e.getMessage());
        }
    }
}
```



## 字节流

字节流以字节(8位)为单位进行读写，适合处理二进制文件(如图片、音频等)。



### FileOutputStream

`FileOutputStream` 是 Java I/O 系统中用于向文件写入原始字节流的一个类。它是 `OutputStream` 抽象类的子类，专门用于文件操作。

**常用方法**

| 方法                                     | 描述                         |
| :--------------------------------------- | :--------------------------- |
| `void write(int b)`                      | 写入单个字节                 |
| `void write(byte[] b)`                   | 写入字节数组                 |
| `void write(byte[] b, int off, int len)` | 写入字节数组的一部分         |
| `void close()`                           | 关闭流并释放资源             |
| `FileChannel getChannel()`               | 返回关联的FileChannel        |
| `void flush()`                           | 刷新输出流，强制写出缓冲数据 |

```java
// 1.基本写入示例
try (FileOutputStream fos = new FileOutputStream("output.txt")) {
    String content = "Hello, World!";
    fos.write(content.getBytes());
} catch (IOException e) {
    e.printStackTrace();
}

// 2.追加模式写入
try (FileOutputStream fos = new FileOutputStream("output.txt", true)) {
    String content = "\nAppended line";
    fos.write(content.getBytes());
} catch (IOException e) {
    e.printStackTrace();
}

// 3.写入二进制数据
byte[] data = {0x48, 0x65, 0x6C, 0x6C, 0x6F}; // "Hello"的ASCII码

try (FileOutputStream fos = new FileOutputStream("binary.dat")) {
    fos.write(data);
} catch (IOException e) {
    e.printStackTrace();
}
```





### FileInputStream

`FileInputStream` 是 Java I/O 系统中用于从文件中读取原始字节流的一个类。它是 `InputStream` 抽象类的子类，专门用于文件操作。

**常用方法**

| 方法                                   | 描述                                       |
| :------------------------------------- | :----------------------------------------- |
| `int read()`                           | 读取单个字节，返回读取的字节或-1(文件结束) |
| `int read(byte[] b)`                   | 读取字节到数组，返回读取的字节数           |
| `int read(byte[] b, int off, int len)` | 读取len个字节到数组的off位置               |
| `long skip(long n)`                    | 跳过并丢弃n个字节                          |
| `int available()`                      | 返回可读取的估计字节数                     |
| `void close()`                         | 关闭流并释放资源                           |
| `FileChannel getChannel()`             | 返回关联的FileChannel                      |

```java
// 1.基本读取示例
FileInputStream fis = null;

try {
    fis = new FileInputStream("example.txt");
    int content;
    while ((content = fis.read()) != -1) {
        System.out.print((char) content);
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fis != null) {
        try {
            fis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// 你也可以用 try-with-resources 语句
try (FileInputStream fis = new FileInputStream("example.txt")) {
    int content;
    while ((content = fis.read()) != -1) {
        System.out.print((char) content);
    }
} catch (IOException e) {
    e.printStackTrace();
}

// 2.使用缓冲区读取
try (FileInputStream fis = new FileInputStream("largefile.bin")) {
    byte[] buffer = new byte[1024];
    int bytesRead;
    while ((bytesRead = fis.read(buffer)) != -1) {
        // 处理读取的数据
        System.out.write(buffer, 0, bytesRead);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

**综合应用：文件拷贝**

```java
package com.test.java;

import java.io.IOException;
import java.io.FileInputStream;
import java.io.FileOutputStream;

@SuppressWarnings("all")

public class Test {
    public static void main(String[] args) {

        FileInputStream fis = null;
        FileOutputStream fos = null;
        String srcPath = "d:\\bomb_1.png";
        String destPath = "d:\\bomb_2.png";

        try {
            fis = new FileInputStream(srcPath);
            fos = new FileOutputStream(destPath);

            byte[] buffer = new byte[1024];
            int length = 0;
            while ((length = fis.read(buffer)) != -1) {
                // 从0到length
                fos.write(buffer, 0, length);
            }
            System.out.println("<UNK>");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fis != null) {
                    fis.close();
                }
                if (fos != null) {
                    fos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```



### BufferedOutputStream

`BufferedOutputStream` 是 Java I/O 库中用于高效写入二进制数据的类，它为输出流提供了缓冲功能，可以显著提高写入性能。

```java
try (BufferedOutputStream bos = new BufferedOutputStream(
        new FileOutputStream("output.bin"), 16384)) {
    
    byte[] data = {0x48, 0x65, 0x6C, 0x6C, 0x6F}; // "Hello"的ASCII码
    
    // 写入单个字节
    bos.write(0x23); // 写入'#'
    
    // 写入字节数组
    bos.write(data);
    
    // 写入数组的一部分
    bos.write(data, 1, 3); // 写入"ell"
    
    // 重要数据可以立即刷新
    bos.flush();
    
} catch (IOException e) {
    e.printStackTrace();
}
```





### BufferedInputStream

`BufferedInputStream` 是 Java I/O 库中的一个类，用于为输入流添加缓冲功能，提高读取效率。它是处理二进制输入数据的高效工具。内部维护一个缓冲区（默认8KB），减少实际的I/O操作次数。

提供了 mark/reset 方法：可以标记流中的位置并稍后重置。

- `mark(int readlimit)`: 标记当前位置
- `reset()`: 重置到上次标记的位置

**创建BufferedInputStream**

```java
// 从文件创建
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("data.bin"));

// 从网络流创建
// Socket socket = ...;
BufferedInputStream netBis = new BufferedInputStream(socket.getInputStream());

// 从字节数组创建
byte[] data = {1, 2, 3, 4, 5};
BufferedInputStream arrayBis = new BufferedInputStream(new ByteArrayInputStream(data));

// 使用16KB的缓冲区
BufferedInputStream bis16 = new BufferedInputStream(
    new FileInputStream("largefile.dat"), 16384);
```

**示例**

```java
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("data.bin"))) {
    byte[] buffer = new byte[1024];
    int bytesRead;
    while ((bytesRead = bis.read(buffer)) != -1) {
        // 处理读取的数据
        processData(buffer, bytesRead);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```



### ObjectOutputStream

`ObjectOutputStream` 是 Java 中用于对象序列化的核心类，它可以将 Java 对象转换为字节流，以便存储到文件或通过网络传输。

**核心方法**

| 方法                        | 描述                      |
| :-------------------------- | :------------------------ |
| `writeObject(Object obj)`   | 序列化并写入一个对象      |
| `writeInt(int val)`         | 写入一个int值             |
| `writeUTF(String str)`      | 写入一个UTF-8编码的字符串 |
| `writeBoolean(boolean val)` | 写入一个boolean值         |
| `writeByte(int val)`        | 写入一个byte值            |
| `writeChar(int val)`        | 写入一个char值            |
| `writeDouble(double val)`   | 写入一个double值          |
| `writeFloat(float val)`     | 写入一个float值           |
| `writeLong(long val)`       | 写入一个long值            |
| `writeShort(int val)`       | 写入一个short值           |
| `flush()`                   | 刷新输出流                |
| `close()`                   | 关闭输出流                |

**示例**

```java
public class Test {
    public static void main(String[] args) throws IOException {
        String path = "d:\\data.dat";

        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(path));
        oos.writeInt(100);
        oos.writeBoolean(true);
        oos.writeChar('a');
        oos.writeDouble(3.14);
        oos.writeUTF("hello");

        oos.writeObject(new Dog("Ken", 4));
        
        oos.close();
    }
}

class Dog implements Serializable{
    String name;
    int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```





### ObjectInputStream

`ObjectInputStream` 是 Java 中用于反序列化对象的核心类，它可以从输入流中读取被序列化的对象，并将其还原为内存中的 Java 对象。

**核心方法**

| 方法                    | 描述                      |
| :---------------------- | :------------------------ |
| `readObject()`          | 读取并反序列化一个对象    |
| `readInt()`             | 读取一个int值             |
| `readUTF()`             | 读取一个UTF-8编码的字符串 |
| `readBoolean()`         | 读取一个boolean值         |
| `readByte()`            | 读取一个byte值            |
| `readChar()`            | 读取一个char值            |
| `readDouble()`          | 读取一个double值          |
| `readFloat()`           | 读取一个float值           |
| `readLong()`            | 读取一个long值            |
| `readShort()`           | 读取一个short值           |
| `readFully(byte[] buf)` | 读取字节填充整个数组      |
| `skipBytes(int len)`    | 跳过指定数量的字节        |

**示例**：反序列化刚才的`data.dat`

```java
public class Test {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        String path = "d:\\data.dat";

        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(path));
        System.out.println(ois.readInt());
        System.out.println(ois.readBoolean());
        System.out.println(ois.readChar());
        System.out.println(ois.readDouble());
        System.out.println(ois.readUTF());

        Object dog = ois.readObject();
        System.out.println("运行类型" + dog.getClass());
        System.out.println(dog);

        ois.close();
    }
}
```



## 字符流



### FileWriter

`FileWriter` 是 Java 中用于写入字符文件的便捷类，继承自 `OutputStreamWriter`，专门用于处理字符流。

创建`FileWriter` 对象时，一般配合`try-with-resources`使用。

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        // 创建一个 FileWriter 对象并指定文件路径。
        // 如果文件存在，FileWriter 会覆盖原有内容。
        // 如果文件不存在，FileWriter 会自动创建它。
        try (FileWriter writer = new FileWriter("example.txt")) {
        
        } catch (IOException e) {
            
        }
        
        // 创建一个 FileWriter 对象，并指定追加模式 (第二个参数为 true)
        try (FileWriter writer = new FileWriter("example.txt", true)) {

        } catch (IOException e) {

        }
    }
}
```

**常用方法**

| 方法                                       | 描述               |
| :----------------------------------------- | :----------------- |
| `void write(int c)`                        | 写入单个字符       |
| `void write(char[] cbuf)`                  | 写入字符数组       |
| `void write(String str)`                   | 写入字符串         |
| `void write(String str, int off, int len)` | 写入字符串的一部分 |
| `void flush()`                             | 刷新缓冲区         |
| `void close()`                             | 关闭流并释放资源   |

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        // 创建一个 FileWriter 对象并指定文件路径
        try (FileWriter writer = new FileWriter("example.txt")) {
            // 使用 write(int c) 写入单个字符
            writer.write(65); // 'A' 的 ASCII 值
            System.out.println("Single character 'A' written.");

            // 使用 write(char[] cbuf) 写入字符数组
            char[] data = "This is a character array.".toCharArray();
            writer.write(data);
            System.out.println("Character array written.");

            // 使用 write(String str) 写入字符串
            String message = "This is a simple string message.";
            writer.write(message);
            System.out.println("String message written.");

            // 使用 flush() 强制刷新缓冲区(内存)内容到文件
            writer.flush();
            System.out.println("Flushed content to the file.");

            // 再次写入一些内容，验证 flush 的效果
            writer.write("\nThis is after flush.");
            System.out.println("New line written after flush.");

            // 最后关闭 FileWriter，释放资源
            writer.close();
            System.out.println("FileWriter closed.");
            
        } catch (IOException e) {
            // 处理文件操作时可能抛出的异常
            System.out.println("An error occurred: " + e.getMessage());
        }
    }
}

```





### FileReader

`FileReader` 是 Java 中用于读取字符文件的便捷类，继承自 `InputStreamReader`，专门用于从文件中读取字符流。

**常用方法**

| 方法                                      | 描述                                      |
| :---------------------------------------- | :---------------------------------------- |
| `int read()`                              | 读取单个字符（返回Unicode值，-1表示结束） |
| `int read(char[] cbuf)`                   | 读取字符到数组，返回读取的字符数          |
| `int read(char[] cbuf, int off, int len)` | 读取字符到数组的指定位置                  |
| `void close()`                            | 关闭流并释放资源                          |

```java
// 1.读取逐个字符
try (FileReader reader = new FileReader("input.txt")) {
    int character;
    while ((character = reader.read()) != -1) {
        System.out.print((char) character);
    }
} catch (IOException e) {
    e.printStackTrace();
}

// 2.批量读取
char[] buffer = new char[1024];
try (FileReader reader = new FileReader("input.txt")) {
    int charsRead;
    while ((charsRead = reader.read(buffer)) != -1) {
        System.out.print(new String(buffer, 0, charsRead));
    }
} catch (IOException e) {
    e.printStackTrace();
}
```



### BufferedWriter

提供了特有的`newLine()`方法，可以写入一个系统相关的换行符。

```java
// 在节点流启用追加模式
try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt", true))) {
    bw.write("Hello, World!");
    bw.newLine();  // 换行
    bw.write("This is a test.");
    bw.flush();    // 确保数据被写入（try-with-resources会自动调用）
} catch (IOException e) {
    e.printStackTrace();
}
```



### BufferedReader

`BufferedReader` 是 Java I/O 库中的一个类，用于高效地读取字符输入流。它通过缓冲输入来提高读取效率，特别适合读取大块的文本数据。

提供了特有的`readLine()`等便捷方法，方便逐行读取文本。

**创建BufferedReader**

```java
// 从文件创建
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));

// 从标准输入创建
BufferedReader stdin = new BufferedReader(new InputStreamReader(System.in));

// 从字符串创建
BufferedReader strReader = new BufferedReader(new StringReader("Some text"));
```

**示例**

```java
try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
    String line;
    // 读取完毕返回null
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```





## 转换流

转换流是Java I/O中用于在字节流和字符流之间进行转换的桥梁类，主要包括`InputStreamReader`和`OutputStreamWriter`。

### OutputStreamWriter

`OutputStreamWriter` 是 Java I/O 系统中将字符流转换为字节流的桥梁类，它继承自 `Writer` 类，能够将写入的字符按照指定编码转换为字节后写入底层字节流。

**构造方法**

```java
// 使用平台默认字符集
OutputStreamWriter(OutputStream out)

// 指定字符集
OutputStreamWriter(OutputStream out, String charsetName)
OutputStreamWriter(OutputStream out, Charset cs)
OutputStreamWriter(OutputStream out, CharsetEncoder enc)
```

**示例**

```java
// 写入文件并指定UTF-8编码
try (OutputStreamWriter osw = new OutputStreamWriter(
        new FileOutputStream("output.txt"), "UTF-8")) {
    
    osw.write("这是UTF-8编码的文本\n");
    osw.write("第二行内容");
} catch (IOException e) {
    e.printStackTrace();
}
```



### InputStreamReader

`InputStreamReader` 是 Java I/O 系统中将字节流转换为字符流的桥梁类，它继承自 `Reader` 类，能够按照指定编码将字节解码为字符。

**构造方法**

```java
// 使用平台默认字符集
InputStreamReader(InputStream in)

// 指定字符集
InputStreamReader(InputStream in, String charsetName)
InputStreamReader(InputStream in, Charset cs)
InputStreamReader(InputStream in, CharsetDecoder dec)
```

**示例**

```java
// 读取文件并指定UTF-8编码
try (InputStreamReader isr = new InputStreamReader(
        new FileInputStream("file.txt"), "UTF-8")) {
    
    char[] buffer = new char[1024];
    int length;
    while ((length = isr.read(buffer)) != -1) {
        System.out.print(new String(buffer, 0, length));
    }
} catch (IOException e) {
    e.printStackTrace();
}
```



## 打印流

打印流是 Java I/O 系统中专门用于输出数据的工具类，主要包括 `PrintStream` 和 `PrintWriter`，它们提供了方便的打印各种数据类型的方法。

| 类名        | 继承关系                         | 主要用途                 |
| :---------- | :------------------------------- | :----------------------- |
| PrintStream | FilterOutputStream ← PrintStream | 字节打印流，处理字节输出 |
| PrintWriter | Writer ← PrintWriter             | 字符打印流，处理字符输出 |

### 输出方法

#### 基本输出方法

| 方法                | 描述                     |
| :------------------ | :----------------------- |
| `print(boolean b)`  | 打印boolean值            |
| `print(char c)`     | 打印字符                 |
| `print(int i)`      | 打印整数                 |
| `print(long l)`     | 打印长整数               |
| `print(float f)`    | 打印浮点数               |
| `print(double d)`   | 打印双精度数             |
| `print(char[] s)`   | 打印字符数组             |
| `print(String s)`   | 打印字符串               |
| `print(Object obj)` | 打印对象(调用toString()) |

#### 换行输出方法

所有 `print` 方法都有对应的 `println` 版本，在输出后追加换行符。

```java
PrintStream ps = System.out;
ps.println("Hello World");  // 输出后换行
ps.println(100);            // 输出整数后换行
ps.println();               // 只输出换行
```

#### 格式化输出

```java
// printf方法（格式化输出）
PrintStream ps = System.out;
ps.printf("当前日期: %tF, 时间: %tT%n", new Date(), new Date());

// format方法与printf相同
ps.format("PI的值: %.4f, E的值: %.4f%n", Math.PI, Math.E);
```

#### 其他重要方法

| 方法                       | 描述         |
| :------------------------- | :----------- |
| `flush()`                  | 刷新输出流   |
| `close()`                  | 关闭流       |
| `checkError()`             | 检查错误状态 |
| `append(CharSequence csq)` | 追加字符序列 |

### PrintStream

`PrintStream` 是 Java 中用于输出数据的字节打印流，它继承自 `FilterOutputStream`，提供了丰富的打印方法，是 Java I/O 系统中最重要的输出类之一。

**构造方法**

```java
// 1.常用构造方法
// 基于现有输出流
PrintStream(OutputStream out)
PrintStream(OutputStream out, boolean autoFlush)
PrintStream(OutputStream out, boolean autoFlush, String encoding)

// 直接创建文件输出
PrintStream(String fileName)
PrintStream(String fileName, String csn) // 规定字符集
PrintStream(File file)
PrintStream(File file, String csn)
    
// 2.示例
// 创建自动刷新的UTF-8打印流
PrintStream ps1 = new PrintStream(
    new FileOutputStream("log.txt"), true, "UTF-8");

// 直接创建文件打印流
PrintStream ps2 = new PrintStream("data.txt");

// 标准错误输出重定向
PrintStream ps3 = new PrintStream(new File("error.log"));
System.setErr(ps3);
```



### PrintWriter

`PrintWriter` 是 Java 中面向字符的输出流，提供了格式化的对象打印功能，是处理文本输出的首选类。

**构造方法**

```java
// 1.常用构造方法
// 基于Writer
PrintWriter(Writer out)
PrintWriter(Writer out, boolean autoFlush)

// 基于OutputStream
PrintWriter(OutputStream out)
PrintWriter(OutputStream out, boolean autoFlush)

// 直接创建文件输出
PrintWriter(String fileName)
PrintWriter(String fileName, String csn)
PrintWriter(File file)
PrintWriter(File file, String csn)
    
// 2.示例
// 创建UTF-8编码的文件打印流(自动刷新)
PrintWriter pw1 = new PrintWriter(
    new OutputStreamWriter(
        new FileOutputStream("log.txt"), "UTF-8"), 
    true);

// 直接创建文件打印流
PrintWriter pw2 = new PrintWriter("data.txt");

// 创建网络输出打印流
Socket socket = new Socket("example.com", 80);
PrintWriter pw3 = new PrintWriter(
    new OutputStreamWriter(
        socket.getOutputStream(), "UTF-8"));
```



## 标准流

Java的标准输入输出流是Java程序与外界进行基本I/O操作的重要接口，主要包括System.in、System.out和System.err三个标准流。

**三种标准流**

| 流类型       | 对应对象   | 描述             | 默认设备 |
| :----------- | :--------- | :--------------- | :------- |
| 标准输入     | System.in  | 用于程序输入     | 键盘     |
| 标准输出     | System.out | 用于正常程序输出 | 控制台   |
| 标准错误输出 | System.err | 用于错误信息输出 | 控制台   |

### System.in

```java
// System.java
public static final InputStream in = null;
```

### System.out

```java
// System.java
public static final PrintStream out = null;
```

### System.err

```java
// System.java
public static final PrintStream err = null;
```



## Properties 读取配置文件

`Properties` 是 Java 中用于处理配置文件的工具类，它继承自 `Hashtable<Object,Object>`，专门用于管理键值对格式的配置信息。

### 核心特性

1. **键值对存储**：基于 String 类型的 key-value 存储
2. **配置文件支持**：可直接读写 .properties 文件
3. **层次化加载**：支持从多个输入流加载并合并
4. **编码感知**：正确处理 Unicode 转义字符
5. **线程安全**：继承自 Hashtable 的线程安全特性

### 常用方法

#### 加载方法

| 方法                          | 描述                       | 示例                                                   |
| :---------------------------- | :------------------------- | :----------------------------------------------------- |
| `load(InputStream in)`        | 从字节输入流加载           | `props.load(new FileInputStream("config.properties"))` |
| `load(Reader reader)`         | 从字符输入流加载(指定编码) | `props.load(new InputStreamReader(in, "UTF-8"))`       |
| `loadFromXML(InputStream in)` | 从XML格式加载              | `props.loadFromXML(new FileInputStream("config.xml"))` |

#### 存储方法

| 方法                                                         | 描述                       | 示例                                                         |
| :----------------------------------------------------------- | :------------------------- | :----------------------------------------------------------- |
| `store(OutputStream out, String comments)`                   | 保存到输出流               | `props.store(new FileOutputStream("config.properties"), "App Config")` |
| `store(Writer writer, String comments)`                      | 保存到字符输出流(指定编码) | `props.store(new OutputStreamWriter(out, "UTF-8"), null)`    |
| `storeToXML(OutputStream os, String comment)`                | 保存为XML格式(UTF-8编码)   | `props.storeToXML(new FileOutputStream("config.xml"), "Settings")` |
| `storeToXML(OutputStream os, String comment, String encoding)` | 保存为XML格式(指定编码)    | `props.storeToXML(out, "Config", "GBK")`                     |

#### 设置和获取属性

| 方法                                           | 描述                 | 示例                                                |
| :--------------------------------------------- | :------------------- | :-------------------------------------------------- |
| `setProperty(String key, String value)`        | 设置属性键值对       | `props.setProperty("username", "admin")`            |
| `getProperty(String key)`                      | 获取属性值           | `String user = props.getProperty("username")`       |
| `getProperty(String key, String defaultValue)` | 获取属性值(带默认值) | `String lang = props.getProperty("language", "en")` |

#### 查询和检查方法

| 方法                      | 描述                 | 示例                                              |
| :------------------------ | :------------------- | :------------------------------------------------ |
| `contains(Object value)`  | 检查是否包含指定值   | `boolean hasAdmin = props.contains("admin")`      |
| `containsKey(Object key)` | 检查是否包含指定键   | `boolean hasUser = props.containsKey("username")` |
| `propertyNames()`         | 返回属性名的枚举     | `Enumeration<?> e = props.propertyNames()`        |
| `list(PrintStream out)`   | 列出属性到打印流     | `props.list(System.out)`                          |
| `list(PrintWriter out)`   | 列出属性到打印写入器 | `props.list(new PrintWriter("props.txt"))`        |

### 加载并读取配置

```java
Properties config = new Properties();
try (InputStream in = getClass().getResourceAsStream("/app.properties")) {
    config.load(in);
    
    String dbUrl = config.getProperty("db.url");
    int timeout = Integer.parseInt(config.getProperty("timeout", "30"));
    
    System.out.println("数据库URL: " + dbUrl);
    System.out.println("超时设置: " + timeout + "秒");
} catch (IOException e) {
    System.err.println("加载配置文件失败: " + e.getMessage());
}
```

### 修改并保存配置

```java
Properties props = new Properties();
props.setProperty("theme", "dark");
props.setProperty("font.size", "14");
props.setProperty("auto.save", "true");

try (OutputStream out = new FileOutputStream("user_prefs.properties")) {
    props.store(out, "用户偏好设置");
    System.out.println("配置保存成功");
} catch (IOException e) {
    System.err.println("保存配置失败: " + e.getMessage());
}
```



# 绘图

`java.awt` (Abstract Window Toolkit) 是 Java 的基础图形用户界面(GUI)工具包，提供了一套丰富的类和接口用于创建图形界面和处理用户输入。



## 核心组件



### 基础类结构

```
java.lang.Object
  └─ java.awt.Component (所有GUI组件的基类)
      ├─ java.awt.Container (容器组件基类)
      │   ├─ java.awt.Window (窗口类)
      │   │   └─ java.awt.Frame (主窗口)
      │   └─ java.awt.Panel (面板)
      └─ 其他基本组件(Button, Label等)
```

### 主要组件

| 类名        | 描述                     |
| ----------- | ------------------------ |
| `Component` | 所有AWT组件的抽象基类    |
| `Container` | 可包含其他组件的容器     |
| `Window`    | 无边框和菜单的顶层窗口   |
| `Frame`     | 标准窗口，带标题栏、边框 |
| `Dialog`    | 对话框窗口               |
| `Panel`     | 通用容器组件             |
| `Button`    | 按钮                     |
| `Label`     | 文本标签                 |
| `TextField` | 单行文本输入框           |
| `TextArea`  | 多行文本区域             |
| `Checkbox`  | 复选框                   |
| `Choice`    | 下拉选择框               |
| `List`      | 列表组件                 |
| `Canvas`    | 自定义绘图区域           |

## 图形绘制

### 核心图形类

| 类/接口         | 描述             |
| --------------- | ---------------- |
| `Graphics`      | 基本绘图上下文   |
| `Graphics2D`    | 扩展的2D绘图功能 |
| `Color`         | 颜色表示         |
| `Font`          | 字体表示         |
| `Image`         | 图像抽象类       |
| `BufferedImage` | 内存中的图像数据 |

### 绘图示例

```java
import java.awt.*;
import java.awt.event.*;

public class AWTDrawing extends Frame {
    public AWTDrawing() {
        setSize(400, 300);
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    public void paint(Graphics g) {
        g.setColor(Color.RED);
        g.fillRect(50, 50, 100, 80);
        
        g.setColor(Color.BLUE);
        g.drawOval(200, 100, 120, 80);
    }

    public static void main(String[] args) {
        new AWTDrawing().setVisible(true);
    }
}
```

## 布局管理

AWT 提供多种布局管理器：

| 布局管理器      | 描述                         |
| --------------- | ---------------------------- |
| `FlowLayout`    | 按添加顺序排列(默认)         |
| `BorderLayout`  | 分为五个区域(NORTH, SOUTH等) |
| `GridLayout`    | 网格布局                     |
| `CardLayout`    | 卡片式布局                   |
| `GridBagLayout` | 灵活的网格布局               |

```java
Frame frame = new Frame("布局示例");
frame.setLayout(new BorderLayout());
frame.add(new Button("North"), BorderLayout.NORTH);
frame.add(new Button("Center"), BorderLayout.CENTER);
```

## 事件处理

AWT 使用**委托事件模型**，它采用了**事件源**与**事件监听器**分离的设计思想，通过委托方式处理事件。

1. **事件源（Event Source）**
    产生事件的GUI组件，如按钮、文本框等
2. **事件对象（Event Object）**
    封装事件相关数据的对象，继承自`java.util.EventObject`
3. **事件监听器（Event Listener）**
    定义事件处理方法（回调方法）的接口

工作流程：

```
[事件发生] → [事件源创建事件对象] → [调用已注册监听器的处理方法] → [监听器执行响应代码]
```

### 主要事件类

| 事件类        | 描述               |
| ------------- | ------------------ |
| `ActionEvent` | 按钮点击等动作事件 |
| `MouseEvent`  | 鼠标事件           |
| `KeyEvent`    | 键盘事件           |
| `WindowEvent` | 窗口事件           |
| `ItemEvent`   | 选项改变事件       |

### 事件监听器示例

事件监听器是通过实现特定**接口**来创建的，这些接口定义了处理相应事件的方法。当相关事件发生时，事件源会自动调用监听器中对应的方法。

```java
Button btn = new Button("Click Me");
btn.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked!");
    }
});
```



## 与 Swing 的关系

1. **基础与扩展**：
   - AWT 是基础，Swing 构建在 AWT 之上
   - Swing 组件通常以"J"开头(JFrame, JButton等)

2. **主要区别**：
   - AWT 使用原生组件(重量级)
   - Swing 使用纯Java实现(轻量级)
   - Swing 提供更丰富的组件和功能

## 现代应用中的角色

虽然 Swing 和 JavaFX 更常用，但 AWT 仍然重要：

1. **基础图形操作**：`Graphics2D` 仍是最强2D图形API
2. **系统集成**：剪贴板、打印、鼠标/键盘处理等
3. **轻量级应用**：简单GUI或需要最小依赖的场景
4. **小程序(Applet)**：历史上用于浏览器嵌入

## 高级功能

### 打印支持

```java
PrinterJob job = PrinterJob.getPrinterJob();
job.setPrintable(new Printable() {
    public int print(Graphics g, PageFormat pf, int page) {
        if (page > 0) return NO_SUCH_PAGE;
        g.drawString("Hello Printing!", 100, 100);
        return PAGE_EXISTS;
    }
});
if (job.printDialog()) {
    job.print();
}
```

### 系统托盘支持

```java
if (SystemTray.isSupported()) {
    SystemTray tray = SystemTray.getSystemTray();
    Image image = Toolkit.getDefaultToolkit().getImage("icon.png");
    TrayIcon trayIcon = new TrayIcon(image, "My App");
    tray.add(trayIcon);
}
```

`java.awt` 作为 Java GUI 开发的基石，虽然部分功能已被更现代的库取代，但它提供的核心图形功能和系统集成能力仍然是 Java 平台不可或缺的部分。



# 线程

## 基本概念

**程序**是为完成特定任务、用某种语言编写的一组指令的集合。

**进程**是计算机中**正在运行的程序**的实例，是操作系统进行资源分配和调度的基本单位。

> **进程**是程序执行一次的过程，或是正在运行的一个程序。这是一个动态的过程，有他自身的产生、存在和消亡的过程。

**线程**是程序执行的最小单元，是进程中的一个独立执行路径。Java 从语言层面支持多线程编程。CPU 调度的基本单位，共享进程的内存空间。

> **线程**是由进程创建的，是进程的一个实体。一个进程可以拥有多个线程。

**单线程**是指同一个时刻，只允许执行一个线程。

**多线程**是指同一个时刻，可以执行多个线程。

**并发**是指同一个时刻，多个任务交替执行，造成一种“貌似同时”的错觉。简单来说，**单核cpu**实现的多个任务就是并发。

**并行**是指同一个时刻，多个任务同时执行。**多核cpu**可以实现并行。

你可以通过Runtime查看你电脑的cpu个数，

```java
Runtime runtime = Runtime.getRuntime();
// 获取当前电脑cpu数量
int cpuNum = runtime.availableProcessors();
System.out.println(cpuNum);
```

## 创建线程

![image-20250723123956492](images/image-20250723123956492.png)

![image-20250722175414597](images/image-20250722175414597.png)

### 继承 Thread 类

当一个类继承了Thread类，该类就可以当作线程使用

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // 启动线程（调用 run()）
    }
}
```

### 实现 Runnable 接口

如果一个类已经继承了其他父类，无法再通过继承 `Thread` 类创建线程（因为 Java 不支持多继承）。所以 Java 提供了 **实现 `Runnable` 接口** 的方式创建线程，更灵活且符合面向接口编程原则。

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable myrun = new MyRunnable();
        // 底层使用了代理模式(静态代理)
        Thread thread = new Thread(myrun);
        thread.start();
    }
}
```

> ##### **静态代理**
>
> 手动编写代理类，在编译时确定代理关系。

```java
// Thread.java 
@Override
    public void run() {
        Runnable task = holder.task; // 向上转型
        if (task != null) {
            // 进行动态绑定
            Object bindings = scopedValueBindings();
            runWith(bindings, task);
        }
    }
```

### 对比

| **对比维度**     | **实现 `Runnable` 接口**               | **继承 `Thread` 类**                |
| :--------------- | :------------------------------------- | :---------------------------------- |
| **继承灵活性**   | ✅ **可继承其他类**                     | ❌ 占用唯一继承位                    |
| **代码复用性**   | ✅ 任务逻辑可复用（多线程**共享实例**） | ❌ 任务与线程绑定                    |
| **资源开销**     | ✅ 轻量（仅任务对象）                   | ❌ 每个线程需独立实例化 `Thread`     |
| **复杂度**       | ⚠️ 需结合 `Thread` 使用                 | ✅ 直接调用 `start()` 即可           |
| **线程池兼容性** | ✅ 可直接提交给 `ExecutorService`       | ❌ 需封装为 `Runnable` 或 `Callable` |
| **Lambda支持**   | ✅ 可用Lambda简化（`() -> {}`）         | ❌ 不适用                            |



## 多线程机制

Java 采用 **1:1 线程模型**（内核级线程模型），每个 Java 线程直接映射到一个操作系统原生线程。

![image-20250723121111782](images/image-20250723121111782.png)

```java
public class Test extends Thread {
    public static void main(String[] args) throws InterruptedException {
        // 使用线程
        Test test = new Test();
        test.start(); // 启动线程 Thread-0

        // 主线程名称就叫 main
        System.out.println("主线程继续执行");
        for (int i = 1; i < 11; i++) {
            System.out.println(i + ".线程名:" + Thread.currentThread().getName());

            Thread.sleep(1000);
        }
    }

    int times = 0;
    // 重写run方法
    @Override
    public void run() {
        while (true) {
            System.out.println((++times) + ".线程名:" + Thread.currentThread().getName());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            // 当times=20时，退出while，这是线程也就退出。
            if (times == 20) {
                break;
            }
        }
    }
}
```

可见，主线程结束后进程并不会结束，而是会等所有子线程全部结束后才会结束。



### 为什么用 start()，而不直接调用 run()

![image-20250722205020623](images/image-20250722205020623.png)

**start() 的内部工作原理**

1. **检查线程状态**：
    - 确保线程处于 NEW 状态
    - 如果已经启动过（≠NEW），抛出 `IllegalThreadStateException`
2. **加入线程组**：
    - 将线程添加到创建它的线程组中
3. **调用 native 方法**：
    - 最终调用 `start0()` 这个 native 方法
    - 通过 JNI 调用操作系统 API 创建系统级线程
4. **线程准备**：
    - 分配线程栈
    - 设置线程优先级等属性
    - 将线程状态改为 RUNNABLE
5. **执行 run()**：
    - 在新创建的线程上下文中调用 run() 方法

```java
// Thread.java 
public void start() {
        synchronized (this) {
            // zero status corresponds to state "NEW".
            if (holder.threadStatus != 0)
                throw new IllegalThreadStateException();
            start0();
        }
    }

private native void start0();
```

**start() 与 run() 的区别**

| 对比项       | start()                          | run()                           |
| :----------- | :------------------------------- | :------------------------------ |
| 调用结果     | 启动新线程，异步执行             | 在当前线程同步执行              |
| 调用次数限制 | 每个线程对象只能调用一次         | 可以多次调用                    |
| JVM 行为     | 创建新调用栈，在新线程执行 run() | 直接在当前调用栈执行 run() 内容 |
| 线程状态变化 | NEW → RUNNABLE                   | 不改变线程状态                  |



### 售票问题

假设一共有一百张票，三个窗口同时出售（用三个线程模拟），如下的代码就可能出现超售问题，即，

```txt
...
窗口Thread-1售出一张票剩余票数1
窗口Thread-1售出一张票剩余票数0
售票结束
窗口Thread-0售出一张票剩余票数-1
售票结束
窗口Thread-2售出一张票剩余票数-2
售票结束
```

`窗口Thread-1` 还没来得及减票，`窗口Thread-0` 与 `窗口Thread-2` 就进行判断了。

```java
public class Test extends Thread {
    public static void main(String[] args) {
        
        SellTicket s = new SellTicket();

        new Thread(s).start();
        new Thread(s).start();
        new Thread(s).start();
    }
}

class SellTicket implements Runnable {
    private static int num = 100;

    @Override
    public void run() {
        while (true) {
            
            if (num <= 0) {
                System.out.println("售票结束");
                break;
            }

            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }

            System.out.println(
                    "窗口"+Thread.currentThread().getName() + "售出一张票" + "剩余票数" + (--num)
            );
        }
    }
}

```





## 通知线程终止

在 Java 中，线程终止需要遵循安全规范，避免强制杀死线程导致资源泄漏或数据不一致。以下是线程终止方法，

### 自然终止

线程 `run()` 方法执行完毕后自动终止。

```java
Thread thread = new Thread(() -> {
    for (int i = 0; i < 5; i++) {
        System.out.println("执行中: " + i);
    }
    // run() 结束，线程自然终止
});
thread.start();
```

### 标志位控制（通知退出）

通过共享变量控制线程退出。这样在主线程里就可以控制子线程的终止。

```java
class MyTask implements Runnable {
    private volatile boolean running = true; // volatile 保证可见性

    public void stop() {
        running = false;
    }

    @Override
    public void run() {
        while (running) {
            System.out.println("线程运行中...");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt(); // 恢复中断状态
                break;
            }
        }
        System.out.println("线程安全退出");
    }
}

// 使用
MyTask task = new MyTask();
Thread thread = new Thread(task);
thread.start();

Thread.sleep(3000);
task.stop(); // 优雅终止
```



##  常用方法

```java
import java.util.*;
import java.time.LocalDateTime;

public class ThreadMethodsExample {
    public static void main(String[] args) throws InterruptedException {
        // 初始化线程对象
        Thread thread = new Thread(() -> {
            try {
                while (!Thread.currentThread().isInterrupted()) {
                    System.out.println("Thread is running...");
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Thread was interrupted during sleep");
                Thread.currentThread().interrupt(); // 恢复中断状态
            }
        });

        // 1. start()
        thread.start(); // 启动线程
        System.out.println("Thread started at: " + LocalDateTime.now());

        // 2. sleep(long millis)
        Thread.sleep(2000); // 主线程休眠2秒
        System.out.println("Main thread woke up at: " + LocalDateTime.now());

        // 3. currentThread()
        Thread current = Thread.currentThread(); // 获取当前线程引用
        System.out.println("Current thread name: " + current.getName());

        // 4. getName() 和 setName(String name)
        System.out.println("Worker thread name: " + thread.getName()); // Thread-0
        thread.setName("Worker-Thread");
        System.out.println("Renamed worker thread: " + thread.getName());

        // 5. getPriority() 和 setPriority(int priority)
        System.out.println("Default priority: " + thread.getPriority()); // 5
        thread.setPriority(Thread.MAX_PRIORITY); // 设置为最高优先级(10)
        System.out.println("New priority: " + thread.getPriority());

        // 6. isAlive()
        System.out.println("Is thread alive? " + thread.isAlive()); // true

        // 7. interrupt() 中断休眠中的线程。该线程会立即中断休眠状态，抛出 InterruptedException 异常。
        thread.interrupt(); // 中断线程
        System.out.println("Thread interrupted at: " + LocalDateTime.now());

        // 8. isInterrupted()
        System.out.println("Is thread interrupted? " + thread.isInterrupted()); // true

        // 9. join() 线程插队。例如，在t1的线程里执行t2.join(), t1就会等待t2执行完毕再继续执行。
        thread.join(); // 等待线程终止
        System.out.println("Thread joined at: " + LocalDateTime.now());

        // 10. getState()
        System.out.println("Thread state after join: " + thread.getState()); // TERMINATED

        // 11. yield()。线程礼让。提示线程调度器当前线程愿意让出 CPU 资源。
        Thread.yield(); // 提示调度器当前线程愿意放弃CPU使用
        System.out.println("Main thread yielded");

        // 12. activeCount()
        System.out.println("Active threads count: " + Thread.activeCount());

        // 13. daemon 线程相关 （守护线程）
        Thread daemonThread = new Thread(() -> {
            while (true) {
                System.out.println("Daemon thread running...");
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    break;
                }
            }
        });
        daemonThread.setDaemon(true); // 设置为守护线程
        System.out.println("Is daemon thread? " + daemonThread.isDaemon()); // true
        daemonThread.start();

        // 14. getId()
        System.out.println("Main thread ID: " + current.getId());

        // 15. holdsLock(Object obj)
        Object lock = new Object();
        synchronized (lock) {
            System.out.println("Current thread holds lock? " + Thread.holdsLock(lock)); // true
        }

        // 主线程休眠1秒让守护线程有机会执行
        Thread.sleep(1000);
        System.out.println("Main thread ending at: " + LocalDateTime.now());
    }
}
```



## 守护线程

**用户线程**也叫工作线程，当线程任务执行完或以通知方式终止。

**守护线程**是一种特殊的线程，它在后台运行并为其他线程提供服务。当所有非守护线程（用户线程）结束时，无论守护线程是否执行完毕，JVM 都会自动退出。

守护线程的典型应用场景：

1. **垃圾回收**：GC线程是最著名的守护线程
2. **日志记录**：后台异步记录日志
3. **监控系统**：定期检查系统状态
4. **自动保存**：文档编辑器的自动保存功能



## 生命周期

### 线程的6种状态（Java 5+）

Java 线程的生命周期由 `Thread.State` 枚举定义，共包含6种状态：

1. **NEW（新建）**
    - 线程被创建但尚未启动
    - 示例：`Thread t = new Thread();`
2. **RUNNABLE（可运行）**
    - 线程正在JVM中执行或准备执行，等待CPU资源
    - 包含操作系统线程状态中的就绪(Ready)和运行中(Running)
3. **BLOCKED（阻塞）**
    - 线程等待获取监视器锁以进入同步块/方法
    - 发生在尝试获取已被其他线程持有的锁时
4. **WAITING（无限期等待）**
    - 线程等待其他线程执行特定操作（唤醒/通知）
    - 通过以下方法进入：
        - `Object.wait()`
        - `Thread.join()`
        - `LockSupport.park()`
5. **TIMED_WAITING（限期等待）**
    - 线程在指定时间内等待
    - 通过以下方法进入：
        - `Thread.sleep(long)`
        - `Object.wait(long)`
        - `Thread.join(long)`
        - `LockSupport.parkNanos()`
        - `LockSupport.parkUntil()`
6. **TERMINATED（终止）**
    - 线程已完成执行或异常终止

### 线程状态转换图

下图中**READY**与**RUNNING**状态都属于上面六种中的**RUNNABLE**状态。

![image-20250727161750504](images/71d1321b345838427313031bd28f1f1f.jpg)

 ![image-20250727161750504](images/17eb3565b5f7c048a9507c2498517812.png)



## 同步机制

在多线程编程中，一些敏感数据不允许被多个线程同时访问。**同步访问机制**就是**保证数据在任何同一时刻，最多有一个线程访问**，以保证数据完整性。

### 锁

Java 提供了多种锁机制来保证多线程环境下的线程安全和数据一致性。

#### 互斥锁

**互斥锁**（Mutex）是多线程编程中最基本的同步机制，用于确保同一时间只有一个线程可以访问共享资源。

#### 死锁

多个线程都占用了对方的锁资源，但不肯相让。

典型死锁示例，

```java
class DeadlockDemo {
    private static final Object lock1 = new Object();
    private static final Object lock2 = new Object();
    
    boolean flag;
    
    public DeadlockDemo(boolean flag) {
        this.flag = flag;
    }
    
    @Override
    public void run() {
        if (flag) {
            synchronized (lock1) {
                System.out.println("Thread1 holds lock1");
                synchronized (lock2) {
                    System.out.println("Thread1 holds lock1 and lock2");
                }
            }
        } else {
            synchronized (lock2) {
                System.out.println("Thread2 holds lock2");
                synchronized (lock1) {
                    System.out.println("Thread2 holds lock1 and lock2");
                }
            }
        }
    }
}

public class Test extends Thread {
    public static void main(String[] args) {
        DeadlockDemo a = new DeadlockDemo(true);
        DeadlockDemo b = new DeadlockDemo(false);
        Thread t1 = new Thread(a);
        Thread t2 = new Thread(b);

        t1.start();
        t2.start();
    }
}
```

#### 锁对象

锁对象（Lock Object）是指被用作同步监视器的任意 Java 对象。

1. **隐式锁（内置锁）**

使用 `synchronized` 关键字实现的锁：

```java
// 实例锁 - 使用当前对象(this)作为锁对象
public synchronized void method() { 
    // 同步代码
}

// 或显式指定锁对象
Object lock = new Object();
public void method() {
    synchronized(lock) {  // 使用特定对象作为锁
        // 同步代码
    }
}
```

2. **显式锁**

`java.util.concurrent.locks` 包提供的锁对象：

```java
Lock lock = new ReentrantLock();  // 可重入锁对象

public void method() {
    lock.lock();  // 显式获取锁
    try {
        // 同步代码
    } finally {
        lock.unlock();  // 必须显式释放
    }
}
```

#### 释放锁





### `synchronized` 关键字

最基本的同步机制，可用于方法或代码块。Java 中最基本的互斥锁实现方式。

#### 同步实例方法

```java
public synchronized void syncMethod() {
    // 同步代码，锁对象是当前实例(this)
}
```

#### 同步静态方法

```java
public static synchronized void staticSyncMethod() {
    // 同步代码，锁对象是当前类的Class对象
}

// 或者
public void method() {
    synchronized(MyClass.class) { // 该方法的类
        // 临界区代码
    }
}
```

#### 同步代码块

```java
public void method() {
    // 非同步代码
    
    synchronized(this) { // 可以使用任意对象作为锁
        // 同步代码块
    }
    
    // 非同步代码
}

// 或者, 使用实例变量作为锁
private final Object lock = new Object();

public void method() {
    synchronized(lock) {  // 所有线程竞争同一个锁
        // 真正的同步代码块
    }
}
```

### 解决售票问题

```java
public class Test extends Thread {
    public static void main(String[] args) {

        SellTicket s = new SellTicket();

        new Thread(s).start();
        new Thread(s).start();
        new Thread(s).start();
    }
}

class SellTicket implements Runnable {
    private static int num = 100;
    private boolean loop = true;

    public void sell() {
        synchronized(this) {  // 只同步必要的部分
            if (num <= 0) {
                System.out.println("售票结束");
                loop = false;
                return;
            }
            num--;  // 减少票数
        }  // 释放锁

        // 非临界区操作放在锁外
        try {
            Thread.sleep(50);  // 模拟出票延迟
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }

        System.out.println("窗口"+Thread.currentThread().getName()
                + "售出一张票" + "剩余票数" + num);
    }

    @Override
    public void run() {
        while (loop) {
            sell();
        }
    }
}
```



# 网络



## InetAddress

`InetAddress` 是 Java 提供的用于表示 **IP 地址**（IPv4 或 IPv6）的类，位于 `java.net` 包中。它不仅可以封装 IP 地址，还能进行 **DNS 解析**（将域名转换为 IP 地址）。

### 主要功能

- 表示 **IP 地址**（如 `192.168.1.1` 或 `2001:db8::1`）。
- 支持 **DNS 查询**（如 `www.google.com` → `142.250.190.36`）。
- 提供 **网络可达性检测**（如 `ping` 测试）。
- 支持 **本地主机 IP 获取**（`localhost`）。
- **不可变（Immutable）**，线程安全。

### 常用方法

| 方法                                             | 说明                                       |
| :----------------------------------------------- | :----------------------------------------- |
| `static InetAddress getByName(String host)`      | 根据主机名或 域名获取 `InetAddress`        |
| `static InetAddress[] getAllByName(String host)` | 获取主机的所有 IP 地址（适用于多 IP 主机） |
| `static InetAddress getLocalHost()`              | 获取本机 IP 地址                           |
| `String getHostAddress()`                        | 返回 IP 地址字符串（如 `"192.168.1.1"`）   |
| `String getHostName()`                           | 返回主机名（可能触发 DNS 查询）            |
| `boolean isReachable(int timeout)`               | 检测 IP 是否可达（类似 `ping`）            |

```java
import java.net.*;

public class Test {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress ip = InetAddress.getLocalHost();
        System.out.println(ip); // HUAWEI-Matebook-14s/192.168.0.101

        InetAddress ip2 = InetAddress.getByName("127.0.0.1");
        System.out.println(ip2); // /127.0.0.1

        InetAddress ip3 = InetAddress.getByName("www.baidu.com");
        System.out.println(ip3); // www.baidu.com/183.2.172.17

        System.out.println(ip3.getHostName()); // www.baidu.com
        System.out.println(ip3.getHostAddress()); // 183.2.172.17
    }
}
```



## Socket

`Socket`（套接字）是 Java 网络编程的核心类，位于 `java.net` 包中，用于实现 **TCP/IP 网络通信**。它允许不同主机上的程序进行数据交换，支持 **客户端-服务器（Client-Server）** 模型。

### TCP 通信

TCP 是一种面向连接的、可靠的、基于字节流的传输层通信协议。在 Java 中，可以使用 `Socket` 和 `ServerSocket` 类来实现 TCP 字节流通信。

#### 服务器端

```java
public class Server {
    public static void main(String[] args) throws IOException {
        // 在本机9999端口监听，等待连接
        ServerSocket ss = new ServerSocket(9999);
        // 如果有客户端连接，则会返回Socket对象，程序继续
        Socket s = ss.accept();
        System.out.println("server: " + s.getClass());
        
        // 获取输入流
        InputStream is = s.getInputStream();
        // IO读取
        byte[] buffer = new byte[1024];
        int readLen = 0;
        while ((readLen = is.read(buffer)) != -1) {
            System.out.println("accepted: " + new String(buffer, 0, readLen));
        }

        OutputStream os = s.getOutputStream();
        os.write("hello, client".getBytes());
        s.shutdownOutput(); // 发送 EOF（End Of File）标记给对端

        // 关闭流, socket, serverSocket
        os.close();
        is.close();
        s.close();
        ss.close();
    }
}
```

#### 客户端

```java
public class Client {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("client: " + s.getClass());
        
        // 获取输出流
        OutputStream os = s.getOutputStream();
        os.write("hello, server".getBytes());
        s.shutdownOutput(); // 禁用此套接字的输出流
         
    	InputStream is = s.getInputStream();
        // IO读取
        byte[] buffer = new byte[1024];
        int readLen = 0;
        while ((readLen = is.read(buffer)) != -1) {
            System.out.println("accepted: " + new String(buffer, 0, readLen));
        }
        
        // 关闭流和socket
        is.close();
        os.close();
        s.close();
    }
}
```



### UDP 通信

与基于连接的、可靠的 TCP 不同，UDP（User Datagram Protocol，用户数据报协议）是一种无连接、不可靠的传输层协议。Java 通过 `DatagramSocket` (数据报套接字) 和 `DatagramPacket` (数据报包)两个类为其提供了强大的支持。

#### 核心类

##### `DatagramSocket`

此类表示用于发送和接收数据报包的套接字。可以把它想象成**邮局的邮箱或邮递员**。

- **作用**：绑定到一个本地端口，用来“寄出”和“接收”包裹（数据报）。
- **常用构造方法**：
    - `DatagramSocket()`: 创建一个套接字并绑定到本地可用端口（通常用于客户端）。
    - `DatagramSocket(int port)`: 创建一个套接字并绑定到指定的本地端口（通常用于服务器）。
- **常用方法**：
    - `void send(DatagramPacket p)`: 发送数据报包。
    - `void receive(DatagramPacket p)`: 接收数据报包（该方法会**阻塞**，直到收到数据）。
    - `void close()`: 关闭套接字。
    - `void setSoTimeout(int timeout)`: 设置接收超时时间（毫秒），超时后会抛 `SocketTimeoutException`，避免无限期阻塞。

##### `DatagramPacket`

此类表示一个数据报包。可以把它想象成**一封信或一个包裹**。

- **作用**：封装数据、目标地址（IP和端口）用于发送；或者提供一个“空包裹”（缓冲区）来接收数据。
- **常用构造方法**：
    - **用于接收**：`DatagramPacket(byte[] buf, int length)`
        - `buf`: 用来存储接收数据的缓冲区。
        - `length`: 要读取的字节数（通常为 `buf.length`）。
    - **用于发送**：`DatagramPacket(byte[] buf, int length, InetAddress address, int port)`
        - `buf`: 包含要发送数据的字节数组。
        - `length`: 要发送的字节数。
        - `address`: 目标主机的IP地址（`InetAddress`）。
        - `port`: 目标主机的端口号。

#### 发送端

```java
public class UDPSender {
    public static void main(String[] args) throws IOException {
        // 在本机9998接收数据
        DatagramSocket socket = new DatagramSocket(9998);
        // 封装发送的数据
        byte[] data = "Hello World".getBytes();
        DatagramPacket packet =
                new DatagramPacket(data, data.length, InetAddress.getLocalHost(), 9999);

        socket.send(packet);
        socket.close();
    }
}
```

#### 接收端

```java
public class UDPReceiver {
    public static void main(String[] args) throws IOException {
        DatagramSocket socket = new DatagramSocket(9999);
        // 准备数据报包
        byte[] buf = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buf, buf.length);
        // 接收数据，如果没有数据包发送到本机9999，程序就会阻塞
        socket.receive(packet);
        // 拆包
        int length = packet.getLength(); // 实际数据包长度
        byte[] data = packet.getData();
        // 打印传来的信息
        String s = new String(data, 0, length);
        System.out.println(s);

        socket.close();
    }
}
```



# 反射

**反射**可以让你获取任意一个类的所有属性和方法，你还可以调用这些方法和属性。

这样的需求在学习框架时特别多，即通过外部文件配置，在不修改源码情况下，来控制程序，也符合设计模式的 `ocp` 原则 (开闭原则：不修改源码，开扩容功能) 。像 `Spring/Spring Boot`、`MyBatis` 等等框架中都大量使用了反射机制。**这些框架中也大量使用了动态代理，而动态代理的实现也依赖反射。**另外，像 Java 中的一大利器 **注解** 的实现也用到了反射。



![](images/2175311-20211117183211977-95412853.jpg)



## Class 类

### 获取 Class 对象

如果我们动态获取到这些信息，我们需要依靠 Class 对象。Class 类对象将一个类的方法、变量等信息告诉运行的程序。

#### 知道具体类的情况下可以使用`obj.class`

```java
Class cls1 = Person.class;
```

这多用于参数的传递，比如通过反射得到对应的构造器对象

但是我们一般是不知道具体类的，基本都是通过遍历包下面的类来获取 Class 对象，通过此方式获取 Class 对象不会进行初始化

#### `Class.forName()`传入类的全路径获取

```java
Class cls2 = Class.forName("com.reflection.Person");
```

多用于配置文件，读取全路径加载类

#### 对象实例`instance.getClass()`获取

```java
Person person = new Person();
Class cls3 = person.getClass();
```

#### 类加载器`xxxClassLoader.loadClass()`传入类路径获取

```java
Class cls4 = ClassLoader.getSystemClassLoader().loadClass("com.reflection.Person");
```

通过类加载器获取 Class 对象不会进行初始化，意味着不进行包括初始化等一系列步骤，静态代码块和静态对象不会得到执行

#### `.TYPE`得到基本数据类型的包装类的Class对象

```java
Class<Integer> cls = Integer.TYPE;
Class<Integer> cls_ = int.class;
// cls 与 cls_ 对象的hashCode一样
```

### 有Class对象的类型

1. 外部类，成员内部类，静态内部类，局部内部类，匿名内部类
2. interface：接口
3. 数组
4. enum：枚举
5. annotation：注解
6. 基本数据类型
7. void

### 常用方法

```java
public class Class_ {
    public static void main(String[] args) throws Exception {
        String classPath = "com.reflection.Person";

        Class<?> cls = Class.forName(classPath);

        // 类名
        System.out.println(cls); // class com.reflection.Example
        System.out.println(cls.getName()); // com.reflection.Example
        System.out.println(cls.getClass()); // class java.lang.Class

        // 包名
        System.out.println(cls.getPackage()); // package com.reflection
        System.out.println(cls.getPackage().getName()); // com.reflection

        // 通过cls创建对象实例
        Person person = (Person) cls.getDeclaredConstructor().newInstance();
        System.out.println(person);

        // 获取单个字段(public), 修改值
        Field name = cls.getField("name");
        System.out.println(name.get(person));
        name.set(person, "Webb");
        System.out.println(name.get(person));

        // 获取方法, 并调用
        Method hi = cls.getMethod("hi");
        hi.invoke(person);

        // 获取构造器(public)
        Constructor<?>[] constructors = cls.getDeclaredConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("构造器: " + constructor);
        }
    }
}
```



## 类的加载

### 静态加载 v.s. 动态加载

静态加载是指在**编译期间**就确定需要加载的类，如果类不存在，编译就会失败。

动态加载是指在**运行期间**根据需要加载类，使用反射机制实现。

```java
public class ClassLoad {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter key: ");
        String key = scanner.nextLine();

        switch (key) {
            // 没有 class Dog 静态加载不通过
            case "1":
                Dog d = new Dog();
                d.bark();
                break;
            // 没有 class Cat 动态加载不通过
            case "2":
                Class cls = Class.forName("Cat");
                Object o = cls.getDeclaredConstructor().newInstance();
                cls.getMethod("meow").invoke(o);
                break;
            default:
                break;
        }
    }
}

class Dog {
    public void bark() {
        System.out.println("Bark");
    }
}
class Cat {
    public void meow() {
        System.out.println("Meow");
    }
}
```

### 类的生命周期

类从被加载到虚拟机内存中开始到卸载出内存为止，它的整个生命周期可以简单概括为 7 个阶段：加载（Loading）、验证（Verification）、准备（Preparation）、解析（Resolution）、初始化（Initialization）、使用（Using）和卸载（Unloading）。其中，验证、准备和解析这三个阶段可以统称为连接（Linking）。

这 7 个阶段的顺序如下图所示：

![一个类的完整生命周期](https://oss.javaguide.cn/github/javaguide/java/jvm/lifecycle-of-a-class.png)

### 加载过程

**Class 文件需要加载到虚拟机中之后才能运行和使用，那么虚拟机是如何加载这些 Class 文件呢？**

系统加载 Class 类型的文件主要三步：**加载->连接->初始化**。连接过程又可分为三步：**验证->准备->解析**。

![一个类的完整生命周期](images/class-loading-procedure.png)

#### 加载

类加载过程的第一步，主要完成下面 3 件事情：

1. 通过全类名获取定义此类的二进制字节流。
2. 将字节流所代表的静态存储结构转换为方法区的运行时数据结构。
3. 在内存中生成一个代表该类的 `Class` 对象，作为方法区这些数据的访问入口。

虚拟机规范上面这 3 点并不具体，因此是非常灵活的。比如："通过全类名获取定义此类的二进制字节流" 并没有指明具体从哪里获取（ `ZIP`、 `JAR`、`EAR`、`WAR`、网络、动态代理技术运行时动态生成、其他文件生成比如 `JSP`...）、怎样获取。

加载这一步主要是通过我们后面要讲到的 **类加载器** 完成的。类加载器有很多种，当我们想要加载一个类的时候，具体是哪个类加载器加载由 **双亲委派模型** 决定（不过，我们也能打破双亲委派模型）。

> 类加载器、双亲委派模型也是非常重要的知识点，这部分内容在[类加载器详解](https://javaguide.cn/java/jvm/classloader.html)这篇文章中有详细介绍到。阅读本篇文章的时候，大家知道有这么个东西就可以了。

每个 Java 类都有一个引用指向加载它的 `ClassLoader`。不过，数组类不是通过 `ClassLoader` 创建的，而是 JVM 在需要的时候自动创建的，数组类通过`getClassLoader()`方法获取 `ClassLoader` 的时候和该数组的元素类型的 `ClassLoader` 是一致的。

一个非数组类的加载阶段（加载阶段获取类的二进制字节流的动作）是可控性最强的阶段，这一步我们可以去完成还可以自定义类加载器去控制字节流的获取方式（重写一个类加载器的 `loadClass()` 方法）。

加载阶段与连接阶段的部分动作(如一部分字节码文件格式验证动作)是交叉进行的，加载阶段尚未结束，连接阶段可能就已经开始了。

#### 验证

**验证是连接阶段的第一步，这一阶段的目的是确保 Class 文件的字节流中包含的信息符合《Java 虚拟机规范》的全部约束要求，保证这些信息被当作代码运行后不会危害虚拟机自身的安全。**

验证阶段这一步在整个类加载过程中耗费的资源还是相对较多的，但很有必要，可以有效防止恶意代码的执行。任何时候，程序安全都是第一位。

不过，验证阶段也不是必须要执行的阶段。如果程序运行的全部代码(包括自己编写的、第三方包中的、从外部加载的、动态生成的等所有代码)都已经被反复使用和验证过，在生产环境的实施阶段就可以考虑使用 `-Xverify:none` 参数来关闭大部分的类验证措施，以缩短虚拟机类加载的时间。但是需要注意的是 `-Xverify:none` 和 `-noverify` 在 JDK 13 中被标记为 deprecated ，在未来版本的 JDK 中可能会被移除。

验证阶段主要由四个检验阶段组成：

1. 文件格式验证（Class 文件格式检查）
2. 元数据验证（字节码语义检查）
3. 字节码验证（程序语义检查）
4. 符号引用验证（类的正确性检查）

![一个类的完整生命周期](images/class-loading-process-verification.png)

文件格式验证这一阶段是基于该类的二进制字节流进行的，主要目的是保证输入的字节流能正确地解析并存储于方法区之内，格式上符合描述一个 Java 类型信息的要求。除了这一阶段之外，其余三个验证阶段都是基于方法区的存储结构上进行的，不会再直接读取、操作字节流了。

> 方法区属于是 JVM 运行时数据区域的一块逻辑区域，是各个线程共享的内存区域。当虚拟机要使用一个类时，它需要读取并解析 Class 文件获取相关信息，再将信息存入到方法区。方法区会存储已被虚拟机加载的 **类信息、字段信息、方法信息、常量、静态变量、即时编译器编译后的代码缓存等数据**。
>
> 关于方法区的详细介绍，推荐阅读 [Java 内存区域详解](https://javaguide.cn/java/jvm/memory-area.html) 这篇文章。

符号引用验证发生在类加载过程中的解析阶段，具体点说是 JVM 将符号引用转化为直接引用的时候（解析阶段会介绍符号引用和直接引用）。

符号引用验证的主要目的是确保解析阶段能正常执行，如果无法通过符号引用验证，JVM 会抛出异常，比如：

- `java.lang.IllegalAccessError`：当类试图访问或修改它没有权限访问的字段，或调用它没有权限访问的方法时，抛出该异常。
- `java.lang.NoSuchFieldError`：当类试图访问或修改一个指定的对象字段，而该对象不再包含该字段时，抛出该异常。
- `java.lang.NoSuchMethodError`：当类试图访问一个指定的方法，而该方法不存在时，抛出该异常。
- ……

#### 准备

**准备阶段是正式为类变量分配内存并设置类变量初始值的阶段**，这些内存都将在方法区中分配。对于该阶段有以下几点需要注意：

1. 这时候进行内存分配的仅包括类变量（ Class Variables ，即静态变量，被 `static` 关键字修饰的变量，只与类相关，因此被称为类变量），而不包括实例变量。实例变量会在对象实例化时随着对象一块分配在 Java 堆中。
2. 从概念上讲，类变量所使用的内存都应当在 **方法区** 中进行分配。不过有一点需要注意的是：JDK 7 之前，HotSpot 使用永久代来实现方法区的时候，实现是完全符合这种逻辑概念的。 而在 JDK 7 及之后，HotSpot 已经把原本放在永久代的字符串常量池、静态变量等移动到堆中，这个时候类变量则会随着 Class 对象一起存放在 Java 堆中。相关阅读：[《深入理解 Java 虚拟机（第 3 版）》勘误#75](https://github.com/fenixsoft/jvm_book/issues/75)
3. 这里所设置的初始值"通常情况"下是数据类型默认的零值（如 0、0L、null、false 等），比如我们定义了`public static int value=111` ，那么 value 变量在准备阶段的初始值就是 0 而不是 111（初始化阶段才会赋值）。特殊情况：比如给 value 变量加上了 final 关键字`public static final int value=111` ，那么准备阶段 value 的值就被赋值为 111。

**基本数据类型的零值**：(图片来自《深入理解 Java 虚拟机》第 3 版 7.3.3 )

![基本数据类型的零值](https://oss.javaguide.cn/github/javaguide/java/基本数据类型的零值.png)

#### 解析

**解析阶段是虚拟机将常量池内的符号引用替换为直接引用的过程。** 解析动作主要针对类或接口、字段、类方法、接口方法、方法类型、方法句柄和调用限定符 7 类符号引用进行。

《深入理解 Java 虚拟机》7.3.4 节第三版对符号引用和直接引用的解释如下：

![符号引用和直接引用](https://oss.javaguide.cn/github/javaguide/java/jvm/symbol-reference-and-direct-reference.png)

举个例子：在程序执行方法时，系统需要明确知道这个方法所在的位置。Java 虚拟机为每个类都准备了一张方法表来存放类中所有的方法。当需要调用一个类的方法的时候，只要知道这个方法在方法表中的偏移量就可以直接调用该方法了。通过解析操作符号引用就可以直接转变为目标方法在类中方法表的位置，从而使得方法可以被调用。

综上，解析阶段是虚拟机将常量池内的符号引用替换为直接引用的过程，也就是得到类或者字段、方法在内存中的指针或者偏移量。

#### 初始化

**初始化阶段是执行初始化方法 `<clinit> ()`方法的过程，是类加载的最后一步，这一步 JVM 才开始真正执行类中定义的 Java 程序代码(字节码)。**

> 说明：`<clinit> ()`方法是编译之后自动生成的。

对于`<clinit> ()` 方法的调用，虚拟机会自己确保其在多线程环境中的安全性。因为 `<clinit> ()` 方法是带锁线程安全，所以在多线程环境下进行类初始化的话可能会引起多个线程阻塞，并且这种阻塞很难被发现。**这个机制保证了一个类在内存中只有一个Class类对象。**

对于初始化阶段，虚拟机严格规范了有且只有 6 种情况下，必须对类进行初始化(只有主动去使用类才会初始化类)：

1. 遇到 `new`、`getstatic`、`putstatic` 或 `invokestatic` 这 4 条字节码指令时： 
    - `new`: 创建一个类的实例对象。
    - `getstatic`、`putstatic`: 读取或设置一个类型的静态字段（被 `final` 修饰、已在编译期把结果放入常量池的静态字段除外）。
    - `invokestatic`: 调用类的静态方法。

2. 使用 `java.lang.reflect` 包的方法对类进行反射调用时如 `Class.forName("...")`, `newInstance()` 等等。如果类没初始化，需要触发其初始化。

3. 初始化一个类，如果其父类还未初始化，则先触发该父类的初始化。

4. 当虚拟机启动时，用户需要定义一个要执行的主类 (包含 `main` 方法的那个类)，虚拟机会先初始化这个类。

5. `MethodHandle` 和 `VarHandle` 可以看作是轻量级的反射调用机制，而要想使用这 2 个调用，就必须先使用 `findStaticVarHandle` 来初始化要调用的类。

6. **「补充，来自[issue745](https://github.com/Snailclimb/JavaGuide/issues/745)」** 当一个接口中定义了 JDK8 新加入的默认方法（被 default 关键字修饰的接口方法）时，如果有这个接口的实现类发生了初始化，那该接口要在其之前被初始化。



## 类的结构信息

### `Class`

```java
public class ClassStructInfo {
    public static void main(String[] args) throws Exception {
        Class<?> aClass = Class.forName("com.reflection.Person");
        // getName:获取全类名
        System.out.println(aClass.getName());
        // getSimpleName:获取简单类名
        System.out.println(aClass.getSimpleName());
        // getFields:获取所有public修饰的属性，包含本类以及父类的
        Field[] fields = aClass.getFields();
        for (Field field : fields) {
            System.out.println(field.getName());
        }
        // getDeclaredFields:获取本类中所有属性
        Field[] declaredFields = aClass.getDeclaredFields();
        for (Field field : declaredFields) {
            System.out.println(field.getName());
        }
        // getMethods:获取所有public修饰的方法，包含本类以及父类的
        Method[] methods = aClass.getMethods();
        for (Method method : methods) {
            System.out.println(method.getName());
        }
        // getDeclaredMethods:获取本类中所有方法
        Method[] declaredMethods = aClass.getDeclaredMethods();
        for (Method method : declaredMethods) {
            System.out.println(method.getName());
        }
        // getConstructors:获取所有public修饰的构造器，不包含父类的
        Constructor<?>[] constructors = aClass.getConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println(constructor.getName()); // 只输出了名字吗，形参也可以打出来
        }
        // getDeclaredConstructors:获取本类中所有构造器
        Constructor<?>[] declaredConstructors = aClass.getDeclaredConstructors();
        for (Constructor<?> constructor : declaredConstructors) {
            System.out.println(constructor.getName());
        }
        // getPackage:以Package形式返回 包信息
        Package aPackage = aClass.getPackage();
        System.out.println(aPackage.getName());
        // getSuperClass:以Class形式返回父类信息
        // getInterfaces:以Class[]形式返回接口信息
        // getAnnotations:以Annotation[] 形式返回注释信息
    }
}
```

### `Field`

```java
// getName:返回属性名
// getModifiers:以lnt形式返回修饰符
// [说明: 默认修饰符是0，public 是1，private 是2，protected 是4，static 是8，final 是16]
// getType:以Class形式返回类型
System.out.println("// Field");
for (Field declaredField : declaredFields) {
    System.out.print(declaredField.getName() + " : ");
    System.out.print(declaredField.getModifiers() + " : ");
    System.out.println(declaredField.getType());
}
```

### `Method`

```java
// getName:返回方法名
// getModifiers:以Int形式返回修饰符
// [说明: 默认修饰符是0，public 是1，private 是2，protected 是4, static 是8，final 是16]
// getReturnType:以Class形式获取 返回类型
// getParameterTypes:以Class[]返回参数类型数组
for (Method declaredMethod : declaredMethods) {
	System.out.print(declaredMethod.getName() + " : ");
	System.out.print(declaredMethod.getModifiers() + " : ");
	System.out.print(declaredMethod.getReturnType() + " : ");
	Class<?>[] parameterTypes = declaredMethod.getParameterTypes();
	for (Class<?> parameterType : parameterTypes) {
		System.out.print(parameterType + ", ");
	}
}
```

### `Constructor`

```java
// getName: 返回构造器名（全类名）
// getModifiers: 以int形式返回修饰符
// getParameterTypes: 以Class[]返回参数类型数组
System.out.println("// Constructor");
for (Constructor<?> declaredConstructor : declaredConstructors) {
    System.out.print(declaredConstructor.getName() + " : ");
    System.out.print(declaredConstructor.getModifiers() + " : ");
    Class<?>[] parameterTypes = declaredConstructor.getParameterTypes();
    for (Class<?> parameterType : parameterTypes) {
        System.out.print(parameterType + ", ");
    }
    System.out.println();
}
```



## 反射爆破

**反射爆破**（reflection bomb/breaking encapsulation）就是**用反射 API 把本来不允许访问的私有成员“炸开”**，强行读写或调用。

核心只有两步：

1. 拿到目标成员（`Field` / `Method` / `Constructor`）。
2. 用 `setAccessible(true)` 关闭 Java 访问检查。

拿 `Animal` 为例，想从外部调用它的私有方法 `internal()` 就可以这样“爆”掉封装：

```java
Animal a = new Dog();          // 运行类型 Dog
Class<?> clazz = a.getClass(); // 得到真正运行时类 Dog.class

// 1. 拿到私有方法
Method m = clazz.getSuperclass()   // Animal.class
                .getDeclaredMethod("internal");

// 2. 爆破
m.setAccessible(true);

// 3. 调用
m.invoke(a);   // 输出：动物内部方法
```

如果想把父类 `Animal` 的私有字段也“爆”出来，只需把 `getDeclaredMethod` 换成 `getDeclaredField`，再 `setAccessible(true)` 即可。

一句话：**反射爆破 = 反射 + setAccessible(true)**，它能让你在运行时绕过 `private/protected/package` 的访问限制，但也会带来安全与维护风险，生产环境慎用。

























