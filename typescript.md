# TypeScript (JavaScript with syntax for types)



[TOC]

## 简介

TypeScript 与 JavaScript 有着不同寻常的关系。TypeScript 提供了 JavaScript 的所有功能，以及在这些功能之上的附加层：TypeScript 的类型系统。

例如，JavaScript 提供像 `string` 和 `number` 这样的语言原语，但它不会检查你是否一致地分配了这些。TypeScript 可以。

这意味着您现有的工作 JavaScript 代码也是 TypeScript 代码。TypeScript 的主要好处是它可以突出显示代码中的意外行为，从而降低出现错误的可能性。



## 基本语法



### 变量声明

```typescript
var [variable] : [typre] = value;
var name : string = "Runoob";
```

TypeScript 包含的数据类型如下表:

| 类型        | 描述                             | 示例                                                    |
| :---------- | :------------------------------- | :------------------------------------------------------ |
| `string`    | 表示文本数据                     | `let name: string = "Alice";`                           |
| `number`    | 表示数字，包括整数和浮点数       | `let age: number = 30;`                                 |
| `boolean`   | 表示布尔值 `true` 或 `false`     | `let isDone: boolean = true;`                           |
| `array`     | 表示相同类型的元素数组           | `let list: number[] = [1, 2, 3];`                       |
| `tuple`     | 表示已知类型和长度的数组         | `let person: [string, number] = ["Alice", 30];`         |
| `enum`      | 定义一组命名常量                 | `enum Color { Red, Green, Blue };`                      |
| `any`       | 任意类型，不进行类型检查         | `let value: any = 42;`                                  |
| `void`      | 无返回值（常用于函数）           | `function log(): void {}`                               |
| `null`      | 表示空值                         | `let empty: null = null;`                               |
| `undefined` | 表示未定义                       | `let undef: undefined = undefined;`                     |
| `never`     | 表示不会有返回值                 | `function error(): never { throw new Error("error"); }` |
| `object`    | 表示非原始类型                   | `let obj: object = { name: "Alice" };`                  |
| `union`     | 联合类型，表示可以是多种类型之一 | `let id: string                                         |
| `unknown`   | 不确定类型，需类型检查后再使用   | `let value: unknown = "Hello";`                         |



