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

# 1.基本语法



## 1.1.基本数据类型

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

### float

- float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
- float 在储存大型浮点数组的时候可节省内存空间；
- 默认值是 **0.0f**；
- 浮点数不能用来表示精确的值，如货币；
- 例子：float f1 = 234.5f。

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



## 1.2.对象和类

### 类（Class）

- 定义对象的蓝图，包括属性和方法。

- 示例：

    ```java
    public class Car { ... }
    ```

### 对象（Object）

- 类的实例，具有状态和行为。

- 示例：

    ```java
    Car myCar = new Car();
    ```

### 构造器（Constructor）

#### (1) 默认构造器（Default Constructor）

- 如果类中没有显式定义任何构造器，Java 编译器会自动提供一个无参的默认构造器。
- 默认构造器的作用是简单地创建对象，不进行额外初始化。

#### (2) 无参构造器（No-Argument Constructor）

- 由程序员显式定义的无参数构造器。
- 可以用来设置字段的默认值。

#### (3) 带参构造器（Parameterized Constructor）

- 接受参数，用于根据传入的值初始化对象。
- 支持灵活的初始化方式。

#### (4) 重写构造器（Overloaded Constructor）

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

### 继承（Inheritance）

- 一个类可以继承另一个类的属性和方法。

- 示例：

    ```java
    public class Dog extends Animal { ... }
    ```

### 封装（Encapsulation）

- 将对象的状态（字段）私有化，通过公共方法访问。

- 示例：

    ```java
    private String name; 
    public String getName() { return name; }
    ```

### 多态（Polymorphism）

- 对象可以表现为多种形态，主要通过**方法重载**和**方法重写**实现。

- 示例：

    - 方法重载：

        ```java
        public int add(int a, int b) { ... } 
        // AND
        public double add(double a, double b) { ... }
        ```

    - 方法重写：

        ```java
        @Override public void makeSound() { System.out.println("Meow"); }

### 抽象（Abstraction）

- 使用抽象类和接口来定义必须实现的方法，不提供具体实现。

- 示例：

    - 抽象类：

        ```java
        public abstract class Shape { 
            abstract void draw(); 
        }
        ```

    - 接口：

        ```java
        public interface Animal { 
            void eat(); 
        }
        ```

### 接口（Interface）

- 定义类必须实现的方法，支持多重继承。

- 示例：

    ```java
    public interface Drivable { void drive(); }
    ```

### 方法（Method）

- 定义类的行为，包含在类中的函数。

- 示例：

    ````java
    public void displayInfo() {
        System.out.println("Info"); 
    }
    ````

### 方法重载（Method Overload）

- 重载是指**在同一个类中**，**定义多个方法名相同但参数列表不同的方法。**Java 会根据方法调用时传递的参数类型和数量来决定调用哪个具体的方法。

- 示例：

    ```java
    public class MathUtils {
        public int add(int a, int b) {
            return a + b;
        }
    
        public double add(double a, double b) {
            return a + b;
        }
    }
    ```



### 方法重写（Method Override）

- 重写是指**子类重新定义父类中已有的方法**，以覆盖父类的实现。重写是实现运行时多态的基础，通常与继承和多态相关。

- 示例：

    ````java
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
    ````

    



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
        return age;
    }
 
    // 获取 name 的值
    public String getName() {
        return name;
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



## 1.3.源文件声明规则

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

------



## 1.4.变量

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



## 1.5.修饰符

### 访问修饰符（Access Modifiers）

访问修饰符控制成员的可见性，也就是定义了类、方法、字段等可以被哪些其他类访问。Java提供了四种访问修饰符：

- **`public`**：表示该成员可以被任何类访问，不受包限制。
- **`protected`**：表示该成员可以被同一个包中的其他类或不同包中的子类访问。
- **`private`**：表示该成员只能在当前类内部访问，不能被其他类访问。
- **默认（无修饰符）**：如果没有使用访问修饰符，表示该成员只能被同一个包中的其他类访问（包内访问）。

### 非访问修饰符（Non-access Modifiers）

非访问修饰符用于定义类、方法、字段等的其他特性，比如是否为静态、是否为常量等。常见的非访问修饰符有：

- **`static`**：表示该成员属于类，而不是某个具体的对象。可以通过类名直接访问，而不需要实例化对象。
- **`final`**：表示该成员不可改变。对于类来说，表示该类不能被继承；对于方法来说，表示该方法不能被重写；对于变量来说，表示该变量的值不能被改变。
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



## 1.6.运算符

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
| ==     | 检查如果两个操作数的值是否相等，如果相等则条件为真。         | （A == B）为假。 |
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
| &&     | 称为逻辑与运算符。当且仅当两个操作数都为真，条件才为真。     | （A && B）为假。    |
| \| \|  | 称为逻辑或操作符。如果任何两个操作数任何一个为真，条件为真。 | （A \| \| B）为真。 |
| ！     | 称为逻辑非运算符。用来反转操作数的逻辑状态。如果条件为true，则逻辑非运算符将得到false。 | ！（A && B）为真。  |

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

### 条件运算符（?:）

条件运算符也被称为三元运算符。该运算符有3个操作数，并且需要判断布尔表达式的值。该运算符的主要是决定哪个值应该赋值给变量。

```
variable x = (expression) ? value if true : value if false
```

### instanceof 运算符

该运算符用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）。

instanceof运算符使用格式如下：

```
( Object reference variable ) instanceof  (class/interface type)
```

如果运算符左侧变量所指的对象，是操作符右侧类或接口(class/interface)的一个对象，那么结果为真。

下面是一个例子：

```
String name = "James";
boolean result = name instanceof String; // 由于 name 是 String 类型，所以返回真
```

如果被比较的对象兼容于右侧类型，该运算符仍然返回 true。



## 1.7.控制语句

同js

### for遍历数组

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



### swicth语法

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
```



## 1.8.数组

### 声明与创建

```java
// 声明
double[] myList;         // 首选的方法
double myList[];         //  效果相同，但不是首选方法，在Java中采用是为了让 C/C++ 程序员能够快速理解java语言。

// 创建
int size = 10;  					// 数组大小
double[] myList = new double[size]; // 定义数组
```

### 多维数组

多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素都是一个一维数组，例如：

```java
String[][] str = new String[3][4];
```



## 1.9.Java包机制

在 Java 中，**包（package）** 是一种组织和管理代码的机制，用于将相关的类和接口分组，避免命名冲突，并提供访问控制。包是 Java 面向对象编程中的重要概念，尤其在大型项目中起到模块化的作用。以下是对 Java 包的详细说明：

---

### 1. 什么是 Java 包？
#### 定义
包是类的命名空间（namespace），类似于文件系统中的目录。它通过将类、接口和其他资源组织到不同的包中，帮助开发者管理代码结构。

#### 本质
- **命名空间**：防止类名冲突。例如，两个不同的开发者可以定义名为 `Util` 的类，只要它们在不同的包中（如 `com.myapp.Util` 和 `org.lib.Util`），就不会冲突。
- **访问控制**：包与访问修饰符（如 `public`, `protected`, 默认（包级））结合，控制类和成员的可见性。
- **模块化**：将功能相似的类分组，提高代码的可维护性和可读性。

---

### 2. 包的语法
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

---

### 3. 导入包
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

---

### 4. Java 中的常见包
Java 标准库（Java API）包含许多内置包，例如：
- **`java.lang`**：核心类（如 `String`, `Math`, `System`），无需显式导入。
- **`java.util`**：实用工具类（如 `ArrayList`, `HashMap`, `Date`, `Scanner`）。
- **`java.io`**：输入输出相关类（如 `File`, `BufferedReader`）。
- **`java.net`**：网络相关类（如 `Socket`, `URL`）。
- **`javax.swing`**：GUI 组件（如 `JFrame`, `JButton`）。

---

### 5. 包的访问控制
包与 Java 的访问修饰符密切相关：
- **`public`**：类或成员对所有包可见。
- **`protected`**：对同一包内的类或子类可见。
- **默认（包级访问）**：如果不指定修饰符（如 `class MyClass`），类或成员只对同一包内的类可见。
- **`private`**：仅类内部可见，与包无关。

#### 示例
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

### 6. 包的物理结构
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

### 7. 包的作用
1. **命名冲突解决**：
   - 不同包中的同名类不会冲突。
2. **代码组织**：
   - 将功能相关的类放在同一包中，如 `com.example.model`（数据模型）、`com.example.util`（工具类）。
3. **访问控制**：
   - 通过包级访问限制某些类的可见性。
4. **模块化开发**：
   - 大型项目中，包可以按功能模块划分（如 MVC 架构中的 `controller`, `service`, `dao`）。

---

### 8. Java 9+ 的模块化（Module System）
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

### 9. 实际示例
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

### 总结
- **Java 包的本质**：一种命名空间和代码组织机制，通过目录结构和访问控制实现模块化。
- **核心功能**：避免命名冲突、提高代码可维护性、支持访问控制。
- **使用方式**：通过 `package` 定义，`import` 引入，结合访问修饰符使用。
- **进化**：从简单的包管理到 Java 9 的模块系统，Java 不断增强其代码组织能力。

包是 Java 中实现封装和模块化的基础工具，熟练掌握包的使用对于编写结构清晰、可扩展的代码至关重要。



## 1.10.异常处理

![image-20250327082213358](images/image-20250327082213358.png)

所有的异常类是从 java.lang.Exception 类继承的子类。

Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

Error 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：IOException 类和 RuntimeException 类。

### Java 异常处理详解

Java 的异常处理机制用于处理程序运行过程中可能发生的错误，使程序能够更健壮地应对异常情况，而不会直接崩溃。

------

### 1. 异常的分类

#### （1）Checked Exception（已检查异常）

- 这些异常在**编译阶段**就会被检查，必须在代码中显式处理（使用 `try-catch` 或 `throws`）。
- 例如：
    - `IOException`
    - `SQLException`
    - `FileNotFoundException`

#### （2）Unchecked Exception（未检查异常 / 运行时异常）

- 这些异常发生在**运行时**，编译器不会强制要求开发者处理，但可以选择捕获。
- 例如：
    - `NullPointerException`
    - `ArrayIndexOutOfBoundsException`
    - `ArithmeticException`

#### （3）Error（错误）

- 这种类型的异常通常表示**JVM 或系统层面**的问题，无法通过代码处理。
- 例如：
    - `StackOverflowError`
    - `OutOfMemoryError`

------

### 2. 异常处理的方式

Java 提供了 **`try-catch-finally`** 机制来处理异常，以及 **`throws`** 关键字用于声明异常。

#### （1）try-catch 语句

```java
try {
    int result = 10 / 0; // 可能会发生 ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("捕获异常：" + e.getMessage());
}
```

#### （2）try-catch-finally

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

#### （3）多异常捕获

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

#### （4）throws 关键字

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

#### （5）throw 关键字

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

### 3. 自定义异常

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

### 4. 异常处理最佳实践

1. **尽量捕获具体异常**，而不是直接 `catch (Exception e)`，这样可以更精确地定位问题。
2. **避免过度捕获**，如果异常无法恢复，应该让它继续传播，而不是强行捕获。
3. **正确使用 `finally` 释放资源**，如关闭数据库连接、文件流等。
4. **日志记录（Logging）**，使用 `Logger` 记录异常信息，而不是简单地 `System.out.println(e)`。

------

### 5. 总结

| 关键字    | 用途                           |
| --------- | ------------------------------ |
| `try`     | 监控可能发生异常的代码块       |
| `catch`   | 捕获异常并处理                 |
| `finally` | 代码块无论是否发生异常都会执行 |
| `throw`   | 手动抛出异常                   |
| `throws`  | 方法声明抛出异常，由调用者处理 |

Java 的异常机制是保证程序稳定性的关键部分，合理地使用异常处理可以提高代码的健壮性和可维护性。



# 2.内置包装类

## 2.1.Math

```java
// 常用的 Math 方法

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



## 2.2.Number

| 序号 | 方法与描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [xxxValue()](https://www.runoob.com/java/number-xxxvalue.html) 将 Number 对象转换为xxx数据类型的值并返回。 |
| 2    | [compareTo()](https://www.runoob.com/java/number-compareto.html) 将number对象与参数比较。 |
| 3    | [equals()](https://www.runoob.com/java/number-equals.html) 判断number对象是否与参数相等。 |
| 4    | [valueOf()](https://www.runoob.com/java/number-valueof.html) 返回一个 Number 对象指定的内置数据类型 |
| 5    | [toString()](https://www.runoob.com/java/number-tostring.html) 以字符串形式返回值。 |
| 6    | [parseInt()](https://www.runoob.com/java/number-parseInt.html) 将字符串解析为int类型。 |

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





## 2.3.Character

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



## 2.4.String

### 创建字符串

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



1. **`length()`**

- 返回字符串的长度（字符数）。

```java
String str = "Hello";
int length = str.length();  // 返回 5
```

2. **`charAt(int index)`**

- 返回指定索引位置的字符。

```java
String str = "Hello";
char ch = str.charAt(1);  // 返回 'e'
```

3. **`substring(int beginIndex, [int endIndex])`**

- 返回从指定索引开始到字符串末尾的子字符串。
- 返回从 `beginIndex` 到 `endIndex` （不包括 `endIndex`）的子字符串。

```java
String str = "Hello";
String sub = str.substring(1, 4);  // 返回 "ell"
```

4. **`indexOf(String str, [int fromIndex])`**

- 返回指定子字符串首次出现的索引位置，如果没有找到则返回 -1。
- 从指定的 `fromIndex` 开始查找指定子字符串，返回首次出现的位置。

```java
String str = "Hello";
int index = str.indexOf("l");  // 返回 2

String str = "Hello";
int index = str.indexOf("l", 3);  // 返回 3
```

7. **`lastIndexOf(String str)`**

- 返回指定子字符串最后一次出现的索引位置，如果没有找到则返回 -1。

```java
String str = "Hello";
int index = str.lastIndexOf("l");  // 返回 3
```

8. **`equals(Object obj)`**

- 比较两个字符串的内容是否相同，返回布尔值。

```java
String str1 = "Hello";
String str2 = "Hello";
boolean isEqual = str1.equals(str2);  // 返回 true
```

9. **`equalsIgnoreCase(String anotherString)`**

- 比较两个字符串的内容是否相同，忽略大小写。

```java
String str1 = "Hello";
String str2 = "hello";
boolean isEqual = str1.equalsIgnoreCase(str2);  // 返回 true
```

10. **`toLowerCase()`**

- 返回将字符串转换为小写字母后的新字符串。

```java
String str = "HELLO";
String lower = str.toLowerCase();  // 返回 "hello"
```

11. **`toUpperCase()`**

- 返回将字符串转换为大写字母后的新字符串。

```java
String str = "hello";
String upper = str.toUpperCase();  // 返回 "HELLO"
```

12. **`trim()`**

- 返回删除前后空白字符的新字符串。

```java
String str = "  Hello  ";
String trimmed = str.trim();  // 返回 "Hello"
```

13. **`replace(char oldChar, char newChar)`**

- 替换字符串中所有指定字符的出现。

```java
String str = "Hello";
String replaced = str.replace('l', 'p');  // 返回 "Heppo"
```

14. **`replace(String target, String replacement)`**

- 替换字符串中所有指定子字符串的出现。

```java
String str = "Hello World";
String replaced = str.replace("World", "Java");  // 返回 "Hello Java"
```

15. **`split(String regex)`**

- 根据指定的正则表达式分割字符串，返回一个字符串数组。

```java
String str = "apple,banana,orange";
String[] fruits = str.split(",");  // 返回 ["apple", "banana", "orange"]
```

16. **`startsWith(String prefix)`**

- 判断字符串是否以指定的前缀开始。

```java
String str = "Hello";
boolean starts = str.startsWith("He");  // 返回 true
```

17. **`endsWith(String suffix)`**

- 判断字符串是否以指定的后缀结尾。

```java
String str = "Hello";
boolean ends = str.endsWith("lo");  // 返回 true
```

18. **`contains(CharSequence sequence)`**

- 判断字符串是否包含指定的子字符串。

```java
String str = "Hello";
boolean contains = str.contains("ll");  // 返回 true
```

19. **`format(String format, Object... args)`**

- 使用指定的格式字符串和参数返回格式化后的字符串。

```java
String formatted = String.format("Hello %s", "World");  // 返回 "Hello World"
```

20. **`valueOf(int i)`**

- 将整数转换为字符串。

```java
int num = 123;
String str = String.valueOf(num);  // 返回 "123"
```

21. **`join(CharSequence delimiter, CharSequence... elements)`**

- 用指定的分隔符连接多个字符串元素。

```java
String result = String.join(", ", "Apple", "Banana", "Orange");  // 返回 "Apple, Banana, Orange"
```

22. **`matches(String regex)`**

- 判断字符串是否与指定的正则表达式匹配。

```java
String str = "12345";
boolean isMatch = str.matches("\\d+");  // 返回 true
```





## 2.5.Scanner

1. **创建 Scanner 对象**:

    - 从键盘读取数据：

        ```java
        Scanner scanner = new Scanner(System.in);
        ```

    - 从文件读取数据：

        ```java
        Scanner scanner = new Scanner(new File("filename.txt"));
        ```

2. **常用方法**:

    - `nextInt()`：读取一个整数。

        ```java
        int num = scanner.nextInt();
        ```

    - `nextDouble()`：读取一个浮点数。

        ```java
        javadouble num = scanner.nextDouble();
        ```

    - `nextLine()`：读取一整行字符串。

        ```java
        String line = scanner.nextLine();
        ```

    - `next()`：读取下一个单词（以空格为分隔符）。

        ```java
        String word = scanner.next();
        ```

3. **关闭 Scanner**: 使用完 Scanner 后，最好调用 `close()` 方法关闭它，防止资源泄漏：

    ```java
    scanner.close();
    ```



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







## 2.6.ArrayList

![image-20250326203239721](images/image-20250326203239721.png)

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



## 2.7.File

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



## 2.8.FileWriter

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        // 使用 try-with-resources 确保资源自动关闭
        try (FileWriter writer = new FileWriter("example.txt")) {
            // 1. 基本写入操作
            writer.write("这是一个简单的字符串\n");  // 写入字符串
            System.out.println("写入字符串完成");

            // 2. 写入字符数组
            char[] charArray = {'H', 'e', 'l', 'l', 'o', '\n'};
            writer.write(charArray);  // 写入整个字符数组
            System.out.println("写入字符数组完成");

            // 3. 写入字符数组的一部分
            writer.write(charArray, 1, 3);  // 从索引1开始，写入3个字符（"ell"）
            System.out.println("写入字符数组部分完成");

            // 4. 写入单个字符（使用int表示）
            writer.write(65);  // 写入字符 'A'（ASCII码65）
            System.out.println("写入单个字符完成");

            // 5. 追加字符串（append方法）
            writer.append("追加的内容\n");  // 返回Writer对象，支持链式调用
            System.out.println("追加字符串完成");

            // 6. 追加字符序列
            CharSequence charSeq = "追加的CharSequence";
            writer.append(charSeq);  // 追加CharSequence
            System.out.println("追加CharSequence完成");

            // 7. 追加单个字符
            writer.append('!');  // 追加单个字符
            System.out.println("追加单个字符完成");

            // 8. 刷新缓冲区
            writer.flush();  // 确保所有数据写入文件
            System.out.println("刷新缓冲区完成");

            // 注意：FileWriter没有close以外的其他特有方法
            // 以下是从Writer继承的方法
            // 9. 获取文件描述符（仅在构造时使用FileDescriptor时可用，此处不可用）
            // writer.getFD();  // 需要使用FileWriter(FileDescriptor)构造

        } catch (IOException e) {
            System.out.println("发生错误: " + e.getMessage());
        }

        // 10. 追加模式示例
        try (FileWriter appendWriter = new FileWriter("example.txt", true)) {
            appendWriter.write("追加模式写入的新内容\n");
            System.out.println("追加模式写入完成");
        } catch (IOException e) {
            System.out.println("追加模式错误: " + e.getMessage());
        }

        // 11. 使用不同构造方法示例
        try {
            // 使用文件路径字符串构造（覆盖模式）
            FileWriter fw1 = new FileWriter("example2.txt");
            fw1.write("使用路径构造\n");
            fw1.close();

            // 使用文件路径字符串构造（追加模式）
            FileWriter fw2 = new FileWriter("example2.txt", true);
            fw2.write("追加模式\n");
            fw2.close();

            // 使用File对象构造
            java.io.File file = new java.io.File("example3.txt");
            FileWriter fw3 = new FileWriter(file);
            fw3.write("使用File对象构造\n");
            fw3.close();

            // 使用File对象构造（追加模式）
            FileWriter fw4 = new FileWriter(file, true);
            fw4.write("File对象追加模式\n");
            fw4.close();

            System.out.println("不同构造方法测试完成");
        } catch (IOException e) {
            System.out.println("构造方法错误: " + e.getMessage());
        }
    }
}
```

