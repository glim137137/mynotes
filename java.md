# Java

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

所有的异常类是从 java.lang.Exception 类继承的子类。

`Exception` 类是 `Throwable` 类的子类。除了`Exception`类外，`Throwable`还有一个子类`Error` 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

`Error` 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：`IOException` 类和 `RuntimeException` 类。

### 异常的分类

#### 已检查异常（Checked Exception）

- 这些异常在**编译阶段**就会被检查，必须在代码中**显式处理**（使用 `try-catch` 或 `throws`）。
- 例如：
    - `IOException`
    - `SQLException`
    - `FileNotFoundException`

#### 未检查异常 / 运行时异常（Unchecked Exception）

- 这些异常发生在**运行时**，编译器不会强制要求开发者处理，但可以选择捕获。
- 例如：
    - `NullPointerException`
    - `ArrayIndexOutOfBoundsException`
    - `ArithmeticException`

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
try {
    int[] arr = new int[3];
    System.out.println(arr[5]); // 访问越界
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("捕获异常：" + e.getMessage());
} finally {
    System.out.println("执行 finally 代码块");
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

------

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

------

### 异常处理最佳实践

1. **尽量捕获具体异常**，而不是直接 `catch (Exception e)`，这样可以更精确地定位问题。
2. **避免过度捕获**，如果异常无法恢复，应该让它继续传播，而不是强行捕获。
3. **正确使用 `finally` 释放资源**，如关闭数据库连接、文件流等。
4. **日志记录（Logging）**，使用 `Logger` 记录异常信息，而不是简单地 `System.out.println(e)`。

------

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

#### 内部类

Java支持类内嵌类（inner classes）和静态内嵌类（static inner classes）。这些类通常用于实现某些特定的功能，它们的**生命周期**依赖于外部类。

- **成员内部类**：作为外部类的成员，通常用于增强外部类的功能。

```java
public class OuterClass {
    private String outerField = "Outer";

    class InnerClass {
        void display() {
            System.out.println("Accessing outer class field: " + outerField);
        }
    }
}
```

- **局部内部类**：通常在外部类的方法内部定义，用来实现方法内部的逻辑。

```java
public class OuterClass {
    private String outerField = "Outer";
    
	public void printName() {
        class LocalInnerClass {
        	void display() {
            	System.out.println("Accessing outer class field: " + outerField);
        	}
    	}
        LocalInnerClass lic = new LocalInnerClass();
        lic.display();
    }
    
}
```



### 成员（Member）

成员是类中定义的变量和方法，它们代表类的属性和行为。成员可以分为两种类型：

- **字段（Fields）**：类中的变量，用来存储对象的状态或数据。
- **方法（Methods）**：类中的函数，用来定义对象的行为或操作。
- **构造器（Constructor）**：特殊的方法，用于创建和初始化对象。
- **内部类（Inner Class）：**类的嵌套成员， 用于增强外部类的功能。

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





#### 静态方法

静态方法是属于类本身的，而不是类的实例。因此，静态方法不能直接访问实例变量和实例方法，只能访问静态变量和静态方法。

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

#### `@override` 注解

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

#### 默认构造器（Default Constructor）

- 如果类中**没有显式定义任何构造器**，Java 编译器会自动提供一个无参的默认构造器。
- 默认构造器的作用是简单地创建对象，不进行额外初始化。
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

#### 重写构造器（Overloaded Constructor）

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
    > - **执行**时由子类子类实现。
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

通过**方法重写（Overriding）**实现，即子类重写父类的方法，具体调用哪个方法由实际对象的类型决定（通常通过父类引用指向子类对象实现）。

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

- 在Java中，**抽象**（`abstract`）是面向对象编程的一个重要概念，它指的是将类的共同特性提取出来，放到一个抽象层面，而不关注其具体实现细节。

#### 抽象类

**抽象类**（`abstract class`）是一种不能被实例化的类，它是为了被继承而设计的。类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。

抽象类可以包含抽象方法和非抽象方法。抽象方法没有方法体，只声明方法的签名，具体的实现由子类提供。

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



### 接口（Interface）

**接口**（`interface`）是一种**特殊的抽象类**，它是定义一组方法声明，但**不提供实现细节**。接口主要用于定义类之间的**契约**，规定类必须实现的行为，而不关心具体的实现方式。接口强调的是"做什么"，而不是"怎么做"。

#### 声明一个接口

- 接口是隐式抽象的，当声明一个接口的时候，不必使用**`abstract`**关键字。
- 接口中每一个方法也是隐式抽象的，声明时同样不需要**`abstract`**关键字。
- 接口中的方法都是公有的 `public` 。

```java
interface Animal {
    void sound();  // 接口方法，子类需要实现
    void eat();    // 接口方法，子类需要实现
}
```

#### 实现接口

类使用 `implements` 关键字实现接口。当类实现接口的时候，类要实现接口中所有的方法。

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

#### 接口的继承

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



---



### 构造方法+实例化对象+访问实例变量和方法

```java
public class Puppy {
    private int age;
    private String name;
 
    // 构造器
    public Puppy(String name) {
        this.name = name;
        System.out.println("小狗的名字是 : " + name);
    }
 
    // 设置 age 的值
    public void setAge(int age) {
        this.age = age;
    }
 
    // 获取 age 的值
    public int getAge() {
        return this.age;
    }
 
    // 获取 name 的值
    public String getName() {
        return this.name;
    }
 
    // 主方法
    public static void main(String[] args) {
        // 创建对象
        Puppy myPuppy = new Puppy("Tommy");
 
        // 通过方法来设定 age
        myPuppy.setAge(2);
 
        // 调用另一个方法获取 age
        int age = myPuppy.getAge();
        System.out.println("小狗的年龄为 : " + age);
 
        // 也可以直接访问成员变量（通过 getter 方法）
        System.out.println("变量值 : " + myPuppy.getAge());
    }
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

### 修饰符的组合使用

修饰符可以组合使用，例如：

```java
public static final int MAX_VALUE = 100; // 公共的、静态的、常量
```

### 修饰符的适用范围

- **类修饰符**：`public`, `abstract`, `final`
- **方法修饰符**：`public`, `private`, `protected`, `abstract`, `static`, `final`, `synchronized`, `native`, `strictfp`
- **字段修饰符**：`public`, `private`, `protected`, `static`, `final`, `transient`, `volatile`
- **构造方法修饰符**：`public`, `private`, `protected`, `final`, `static`, `synchronized`



## Java包机制

在 Java 中，**包（package）** 是一种组织和管理代码的机制，用于将相关的类和接口分组，避免命名冲突，并提供访问控制。包是 Java 面向对象编程中的重要概念，尤其在大型项目中起到模块化的作用。以下是对 Java 包的详细说明：

---

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
- **`protected`**：对同一包内的类或子类可见。
- **默认（包级访问）**：如果不指定修饰符（如 `class MyClass`），类或成员只对同一包内的类可见。
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

---

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

---

### 包的作用

1. **命名冲突解决**：
    - 不同包中的同名类不会冲突。
2. **代码组织**：
    - 将功能相关的类放在同一包中，如 `com.example.model`（数据模型）、`com.example.util`（工具类）。
3. **访问控制**：
    - 通过包级访问限制某些类的可见性。
4. **模块化开发**：
    - 大型项目中，包可以按功能模块划分（如 MVC 架构中的 `controller`, `service`, `dao`）。

---

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

---

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

---





## 枚举

Java 枚举是一个**特殊的类**，一般表示一组常量，比如一年的 4 个季节，一年的 12 个月份，一个星期的 7 天，方向有东南西北等。

Java 枚举类使用 `enum` 关键字来定义，各个常量使用逗号 **`,`** 来分割。

### 声明一个枚举类

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
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
| `values()`             | 返回枚举的所有值（数组）        |
| `valueOf(String name)` | 根据名称返回枚举常量            |
| `ordinal()`            | 返回枚举常量的序号（从 0 开始） |
| `name()`               | 返回枚举常量的名称（字符串）    |

```java
Day day = Day.MONDAY;
Day.valueOf("TUESDAY") // Day.TUESDAY
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



## 泛型

泛型是 Java 5 引入的重要特性，它提供了编译时类型安全检查机制，并消除了强制类型转换的需要。

泛型的本质是**参数化类型**，也就是说所操作的数据类型被指定为一个参数。

### 泛型标记符

| 标记符   | 常见用途               | 示例            |
| :------- | :--------------------- | :-------------- |
| `T`      | Type（任意类型）       | `Box<T>`        |
| `E`      | Element（集合元素）    | `List<E>`       |
| `K`      | Key（键）              | `Map<K,V>`      |
| `V`      | Value（值）            | `Map<K,V>`      |
| `N`      | Number（数字类型）     | `Calculator<N>` |
| `S`, `U` | 第二、第三类型参数     | `Pair<T,U>`     |
| `?`      | 表示不确定的 java 类型 | `List<?>`       |

### 泛型类

泛型类允许我们创建可以操作多种数据类型的类，同时保持类型安全。

```java
public class Box<T> {
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
public class Pair<K, V> {
    private K key;
    private V value;
    
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    public K getKey() { return key; }
    public V getValue() { return value; }
    
    public void setKey(K key) { this.key = key; }
    public void setValue(V value) { this.value = value; }
}
```

### 泛型方法

所有泛型方法声明都有一个类型参数声明部分（由尖括号`<>`分隔），该类型参数声明部分**在方法返回类型之前**。

泛型方法体的声明和其他方法一样。注意类型参数只能代表**引用型类型**，不能是原始类型（像 int、double、char 等）。

```java
public class Util {
    // 泛型方法
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
}

// 使用泛型方法
Integer[] intArray = {1, 2, 3};
String[] stringArray = {"A", "B", "C"};
Util.printArray(intArray);
Util.printArray(stringArray);
```

### 泛型接口

```java
public interface List<T> {
    void add(T element);
    T get(int index);
}

public class ArrayList<T> implements List<T> {
    // 实现接口方法
}
```



# 内置包装类

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
| **典型用途** | 检查对象是否为同一实例或基本类型值相等 | 检查对象的内容是否逻辑上相等                                 |

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
> - 重写 `equals()` 后，必须同时重写 `hashCode()`，确保相等对象有相同哈希码。

##### hashCode() 的作用

- 性能优化：

    - 在哈希表中，`hashCode()` 确定对象存储的桶位置。哈希码相等的对象会被放入同一个桶，减少查找范围。减少哈希冲突（不同对象映射到同一桶），提高哈希表性能。

    - 示例：`HashMap` 使用 `key.hashCode()` 计算键的存储位置。

- 对象比较：

    - 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的。

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



## Arrays

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
        
        // 2. 打印原始数组
        System.out.println("原始int数组: " + Arrays.toString(intArray));
        System.out.println("原始str数组: " + Arrays.toString(strArray));
        
        // 3. Arrays.sort(array) 排序方法
        Arrays.sort(intArray); // 基本类型快速排序
        System.out.println("排序后int数组: " + Arrays.toString(intArray));
        
        Arrays.sort(strArray); // 对象类型归并排序
        System.out.println("排序后str数组: " + Arrays.toString(strArray));
        
        // Arrays.sort(array[, order])自定义排序
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



## Math

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



## String

### 创建 String 对象

```java
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建

public class StringDemo {
    public static void main(String args[]) {     
        String string1 = "菜鸟教程网址：";     
        System.out.println("1、" + string1 + "www.runoob.com");  
    }
}
```

![image-20250312210526289](images/image-20250312210526289.png)

> **注意:**String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了（详看笔记部分解析）。

### 常用方法

```java
public class StringMethodsExample {
    public static void main(String[] args) {
        String str = "Hello World";

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



## ArrayList

![image-20250326203239721](images/image-20250326203239721.png)

### 创建 ArrayList 对象

```java
import java.util.ArrayList; // 引入 ArrayList 类

// 1. 创建一个空的ArrayList
ArrayList<String> list1 = new ArrayList<>();

// 2. 创建具有初始容量的ArrayList
ArrayList<Integer> list2 = new ArrayList<>(20);

// 3. 从其他集合创建
List<String> existingList = Arrays.asList("A", "B", "C");
ArrayList<String> list3 = new ArrayList<>(existingList);
```

### 常用方法

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListMethodsExample {

    public static void main(String[] args) {
        // 创建一个 ArrayList 实例，存储 String 类型的元素
        ArrayList<String> list = new ArrayList<>();

        // 1. add(E e): 将元素添加到列表的末尾
        list.add("Java");          // 添加 "Java" 到列表
        list.add("Python");        // 添加 "Python" 到列表
        list.add("C++");           // 添加 "C++" 到列表
        System.out.println("After add() operations: " + list); // 打印添加后的列表

        // 2. add(int index, E element): 在指定位置插入元素
        list.add(1, "JavaScript");  // 在索引1的位置插入 "JavaScript"
        System.out.println("After add(index, element): " + list); // 打印插入后的列表

        // 3. get(int index): 获取指定位置的元素
        String element = list.get(2); // 获取索引为2的元素
        System.out.println("Element at index 2: " + element); // 打印该元素

        // 4. set(int index, E element): 设置指定位置的元素
        list.set(1, "Ruby"); // 将索引为1的位置的元素修改为 "Ruby"
        System.out.println("After set() operation: " + list); // 打印修改后的列表

        // 5. remove(int index): 移除指定位置的元素
        list.remove(3); // 移除索引为3的元素 "C++"
        System.out.println("After remove(index): " + list); // 打印移除后的列表

        // 6. remove(Object o): 移除指定元素
        list.remove("Python"); // 移除 "Python"
        System.out.println("After remove(element): " + list); // 打印移除后的列表

        // 7. contains(Object o): 判断列表是否包含某个元素
        boolean contains = list.contains("Ruby"); // 判断列表中是否包含 "Ruby"
        System.out.println("Contains 'Ruby': " + contains); // 打印结果

        // 8. indexOf(Object o): 获取指定元素第一次出现的位置
        int index = list.indexOf("Java"); // 获取 "Java" 在列表中的位置
        System.out.println("Index of 'Java': " + index); // 打印该位置

        // 9. size(): 获取列表中元素的个数
        int size = list.size(); // 获取列表的大小
        System.out.println("Size of list: " + size); // 打印列表大小

        // 10. clear(): 清空列表中的所有元素
        list.clear(); // 清空列表
        System.out.println("After clear(): " + list); // 打印清空后的列表（空）

        // 11. isEmpty(): 判断列表是否为空
        boolean isEmpty = list.isEmpty(); // 检查列表是否为空
        System.out.println("Is list empty? " + isEmpty); // 打印检查结果

        // 12. ensureCapacity(int minCapacity): 确保 ArrayList 至少有指定的容量
        ArrayList<Integer> numbers = new ArrayList<>();
        numbers.ensureCapacity(10); // 确保列表有至少10个容量
        System.out.println("ArrayList with ensured capacity: " + numbers); // 打印确保容量后的列表

        // 13. toArray(): 将 ArrayList 转换为数组
        list.add("Hello");
        list.add("World");
        Object[] array = list.toArray(); // 将 ArrayList 转换为数组
        System.out.println("ArrayList to Array: ");
        for (Object obj : array) { // 遍历并打印数组
            System.out.println(obj);
        }

        // 14. trimToSize(): 调整 ArrayList 的大小以匹配实际元素的个数
        list.trimToSize(); // 调整 ArrayList 容量
        System.out.println("Trimmed ArrayList: " + list); // 打印调整后的列表

        // 15. listIterator(): 获取 ListIterator，用于遍历列表
        list.add("Java");
        list.add("Python");
        list.add("Ruby");
        var iterator = list.listIterator(); // 获取 ListIterator
        System.out.println("ListIterator forward traversal:");
        while (iterator.hasNext()) { // 向前遍历
            System.out.println(iterator.next());
        }

        // 16. subList(int fromIndex, int toIndex): 获取从指定位置到另一个位置的子列表
        List<String> subList = list.subList(0, 2); // 获取索引从 0 到 2（不包括 2）的子列表
        System.out.println("SubList from index 0 to 2: " + subList);

        // 17. removeAll(Collection<?> c): 从列表中移除指定集合中的所有元素
        ArrayList<String> toRemove = new ArrayList<>();
        toRemove.add("Java");
        list.removeAll(toRemove); // 移除集合中的元素
        System.out.println("After removeAll() operation: " + list); // 打印移除后的列表
    }
}

```

**代码解释**：

1. **add(E e)**: 向列表末尾添加一个元素。
2. **add(int index, E element)**: 在指定位置插入一个元素。
3. **get(int index)**: 获取指定位置的元素。
4. **set(int index, E element)**: 设置指定位置的元素为新的值。
5. **remove(int index)**: 移除指定位置的元素。
6. **remove(Object o)**: 移除列表中指定的元素。
7. **contains(Object o)**: 判断列表中是否包含某个指定的元素。
8. **indexOf(Object o)**: 返回指定元素第一次出现的位置。如果不存在，返回 -1。
9. **size()**: 返回列表的元素个数。
10. **clear()**: 移除列表中的所有元素。
11. **isEmpty()**: 检查列表是否为空。
12. **ensureCapacity(int minCapacity)**: 确保列表至少有指定的容量，防止频繁扩容。
13. **toArray()**: 将列表转换为数组。
14. **trimToSize()**: 调整列表的大小，去除多余的容量。
15. **listIterator()**: 返回一个 `ListIterator`，用于遍历列表。
16. **subList(int fromIndex, int toIndex)**: 获取指定范围的子列表。
17. **removeAll(Collection<?> c)**: 移除列表中所有与指定集合相同的元素。

**运行结果**：

```txt
After add() operations: [Java, Python, C++]
After add(index, element): [Java, JavaScript, Python, C++]
Element at index 2: Python
After set() operation: [Java, Ruby, Python, C++]
After remove(index): [Java, Ruby, Python]
After remove(element): [Java, Ruby]
Contains 'Ruby': true
Index of 'Java': 0
Size of list: 2
After clear(): []
Is list empty? true
ArrayList with ensured capacity: []
ArrayList to Array: 
Hello
World
Trimmed ArrayList: [Hello, World]
ListIterator forward traversal:
Hello
World
SubList from index 0 to 2: [Hello, World]
After removeAll() operation: [World]

```



## File

在 Java 中，`File` 类用于表示文件和目录。

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



## FileWriter

`FileWriter` 是 Java 中的一个类，用于向文件中写入字符数据。

![image-20250421150409243](images/image-20250421150409243.png)

### 创建 FileWriter 对象

创建`FileWriter` 对象时，一般配合`try-catch`使用。

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



### 常用方法

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

            // 使用 flush() 强制刷新缓冲区内容到文件
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

