# Progamming Project



## 1.Modular programming and Makefile



### Software Scale

 KLOC = 1000 lines of code; MLOC = 1,000,000 lines of code



![image-20250325085817080](images/image-20250325085817080.png)



### Modularity

**模块化编程**：将大程序拆分为小块（模块或函数），避免代码重复，提高可读性和维护性。

**函数设计原则**：一个函数的功能应能用一句话描述，否则应考虑拆分。

> If you can’t describe what your function does in one  sentence you should consider splitting it.

**模块术语**：

> 模块之间需明确接口和通信方式。

**模块接口（Module Interface, .h 文件）**

- **定义**：这是模块的正式描述，告诉其他模块或程序员这个模块包含什么。
- **内容**：通常包括数据结构定义（如结构体 struct）、函数原型（function prototypes）以及必要的宏定义（#define）。
- **作用**：作为模块的“门面”，它指定了模块对外暴露的功能和数据，其他模块通过包含（#include）这个头文件来使用这些功能，而无需关心内部实现细节。
- **特点**：内容应简洁、稳定，避免频繁修改，因为它会被多个文件依赖。
- **例子**：在 customer.h 中定义 struct customer 和函数 customer_new() 的原型。

**模块实现（Module Implementation, .c 文件）**

- **定义**：这是模块的具体实现，提供人类可读的细节描述。
- **内容**：包含头文件中声明的函数的具体代码实现，以及模块内部使用的私有变量和辅助函数。
- **作用**：实现模块的功能，是程序逻辑的核心部分。程序员通过阅读 .c 文件可以理解模块的工作原理。
- **特点**：与 .h 文件分离，修改 .c 文件通常不会影响依赖此模块的其他代码（只要接口不变）。
- **例子**：在 customer.c 中实现 customer_new() 函数，分配内存并初始化 customer 结构体的字段。

**对象文件（Object File, .o 文件）**

- **定义**：这是模块的机器可读描述，由编译器从 .c 文件生成。
- **内容**：包含编译后的二进制代码（机器指令），不再是人类可读的文本，而是处理器可以理解的格式。
- **作用**：作为编译过程中的中间产物，多个 .o 文件最终会被链接器（linker）组合成可执行文件。
- **特点**：依赖于特定的硬件架构，无法直接阅读，但可以用工具（如 objdump）检查其内容（如符号表或反汇编代码）。
- **例子**：通过 gcc -c customer.c -o customer.o 生成 customer.o，供后续链接使用。



### Pre-processing -> Compilation -> Linking



![image-20250325091141563](images/image-20250325091141563.png)



**Pre-processing**

The pre-processor expands all the directives that start with   “#”, such as: 

#include //importing libraries   

#define //creating macros

#ifdef  #if  #ifndef   #elif   #endif   #else  //conditional comilation



