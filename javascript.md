# JavaScript

JS全称JavaScript，是一种轻量级的面向对象的编程语言，既能用在浏览器中控制页面交互，也能用在服务器端作为网站后台（借助 Node.js），因此 JavaScript 是一种全栈式的编程语言。

[TOC]

# 1.基本语法

## 1.1.数据类型

JavaScript 拥有**动态类型**。这意味着相同的变量可用作不同的类型：

```js
typeof "John"                // 返回 string
typeof 3.14                  // 返回 number
typeof false                 // 返回 boolean
typeof [1,2,3,4]             // 返回 object
typeof {name:'John', age:34} // 返回 object
```





### 值类型

#### 字符串（String）

```js
// 可以使用单引号或双引号
var carname = "Volvo XC60";
var carname = 'Volvo XC60';

// 使用索引位置来访问字符串中的每个字符
var character = carname[7];

// 使用内置属性 length 来计算字符串的长度
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
var str_len = txt.length;
```

1. **创建字符串**

- **字面量**

  ```javascript
  const str = "Hello, world!";
  ```

- **构造函数**

  ```javascript
  const strObj = new String("Hello, world!");
  ```

2. **字符串属性**

- `length`

  ：获取字符串的长度。

  ```javascript
  const length = str.length; // 13
  ```

3. **常用字符串方法**

- **`charAt(index)`**：返回指定位置的字符。

  ```javascript
  const char = str.charAt(0); // 'H'
  ```

- **`charCodeAt(index)`**：返回指定位置字符的 Unicode 编码。

  ```javascript
  const code = str.charCodeAt(0); // 72
  ```

- **`concat(...strings)`**：连接一个或多个字符串。

  ```javascript
  const newStr = str.concat(" How are you?"); // "Hello, world! How are you?"
  ```

- **`includes(searchString)`**：判断字符串是否包含某个子字符串。

  ```javascript
  const hasHello = str.includes("Hello"); // true
  ```

- **`indexOf(searchString)`**：返回子字符串首次出现的位置，未找到时返回 -1。

  ```javascript
  const index = str.indexOf("world"); // 7
  ```

- **`lastIndexOf(searchString)`**：返回子字符串最后一次出现的位置，未找到时返回 -1。

  ```javascript
  const lastIndex = str.lastIndexOf("o"); // 8
  ```

- **`slice(start, end)`**：提取字符串的一个片段。

  ```javascript
  const sliced = str.slice(0, 5); // "Hello"
  ```

- **`substring(start, end)`**：提取字符串的一个子字符串。

  ```javascript
  const subStr = str.substring(7, 12); // "world"
  ```

- **`substr(start, length)`**：从指定位置开始提取指定长度的子字符串（不推荐使用）。

  ```javascript
  const sub = str.substr(7, 5); // "world"
  ```

- **`toLowerCase()`**：将字符串转换为小写。

  ```javascript
  const lower = str.toLowerCase(); // "hello, world!"
  ```

- **`toUpperCase()`**：将字符串转换为大写。

  ```javascript
  const upper = str.toUpperCase(); // "HELLO, WORLD!"
  ```

- **`trim()`**：去除字符串两端的空白字符。

  ```javascript
  const trimmed = "   Hello!   ".trim(); // "Hello!"
  ```

4. **分割和连接字符串**

- **`split(separator)`**：将字符串分割成数组。

  ```javascript
  const words = str.split(", "); // ["Hello", "world!"]
  ```

- **`join(separator)`**：将数组元素连接成字符串（与数组方法一起使用）。

  ```javascript
  const joined = words.join(" - "); // "Hello - world!"
  ```

5. **替换和重复**

- **`replace(searchValue, newValue)`**：替换第一个匹配的子字符串。

  ```javascript
  const replaced = str.replace("world", "everyone"); // "Hello, everyone!"
  ```

- **`replaceAll(searchValue, newValue)`**：替换所有匹配的子字符串。

  ```javascript
  const allReplaced = "I like cats and cats are cute.".replaceAll("cats", "dogs"); // "I like dogs and dogs are cute."
  ```

- **`repeat(count)`**：返回一个新字符串，表示将原字符串重复指定次数。

  ```javascript
  const repeated = "ha".repeat(3); // "hahaha"
  ```

6. **模板字符串**

- 模板字符串

  （使用**反引号`**）可以包含变量和表达式：

  ```javascript
  const name = "Alice";
  const greeting = `Hello, ${name}!`; // "Hello, Alice!"
  ```

7. **查找和匹配**

- **`match(regexp)`**：用正则表达式匹配字符串。

  ```javascript
  const matches = str.match(/o/g); // ['o', 'o']
  ```

- **`search(regexp)`**：返回正则表达式匹配的第一个位置。

  ```javascript
  const position = str.search("world"); // 7
  ```

- **`startsWith(searchString)`**：判断字符串是否以指定字符串开头。

  ```javascript
  const starts = str.startsWith("Hello"); // true
  ```

- **`endsWith(searchString)`**：判断字符串是否以指定字符串结尾。

  ```javascript
  const ends = str.endsWith("!"); // true
  ```

#### 数字（Number）

```js
// 数字可以带小数点，也可以不带
var x1=34.00;      //使用小数点来写
var x2=34;         //不使用小数点来写

// 通过科学（指数）计数法来书写
var y=123e5;      // 12300000
var z=123e-5;     // 0.00123
```

1. **`Number.isFinite(value)`**

   - 用于判断一个值是否是有限的数字（不是 `Infinity`、`-Infinity` 或 `NaN`）。
   - **返回值**: 布尔值 `true` 或 `false`。

   ```javascript
   console.log(Number.isFinite(123));       // true
   console.log(Number.isFinite(Infinity));  // false
   console.log(Number.isFinite(NaN));       // false
   console.log(Number.isFinite('123'));     // false
   ```

2. **`Number.isInteger(value)`**

   - 判断一个值是否为整数。
   - **返回值**: 布尔值 `true` 或 `false`。

   ```javascript
   console.log(Number.isInteger(123));       // true
   console.log(Number.isInteger(123.45));    // false
   console.log(Number.isInteger('123'));     // false
   ```

3. **`Number.isNaN(value)`**

   - 判断一个值是否是 `NaN`（Not-a-Number）。
   - **返回值**: 布尔值 `true` 或 `false`。

   ```javascript
   console.log(Number.isNaN(NaN));           // true
   console.log(Number.isNaN(123));           // false
   console.log(Number.isNaN('123'));         // false
   ```

4. **`Number.isSafeInteger(value)`**

   - 判断一个值是否是一个“安全整数”（在 `-(2^53 - 1)` 到 `2^53 - 1` 之间的整数）。
   - **返回值**: 布尔值 `true` 或 `false`。

   ```javascript
   console.log(Number.isSafeInteger(123));       // true
   console.log(Number.isSafeInteger(9007199254740991)); // true
   console.log(Number.isSafeInteger(9007199254740992)); // false
   ```

5. **`Number.parseFloat(string)`**

   - 将一个字符串解析为浮动点数（`float`）。与 `parseFloat` 相同。
   - **返回值**: 解析后的浮动点数。
   - **解析规则**：
       - `parseFloat()` 会从字符串的开头开始解析，直到遇到一个不是数字字符或者小数点的字符为止。在遇到非数字字符时，解析会停止。
       - 如果字符串的开头不是数字或者没有有效的小数部分，返回 `NaN`。
       - `parseFloat()` 会处理字符串中的数字，包括整数、小数和科学计数法。

   ```javascript
   console.log(Number.parseFloat('3.14abc'));   // 3.14
   console.log(Number.parseFloat('123abc'));    // 123
   console.log(Number.parseFloat('abc123'));    // NaN
   ```

6. **`Number.parseInt(string, radix)`**

   - 将一个字符串解析为整数，`radix` 是一个可选的参数，用来指定解析的进制。
   - **返回值**: 解析后的整数。
   - **解析规则**：
       - `parseInt()` 会从字符串的开头开始解析，直到遇到一个不是数字的字符为止。在遇到非数字字符时，解析会停止。
       - 如果字符串的开头不是数字，则返回 `NaN`。

   ```javascript
   console.log(Number.parseInt('10'));         // 10
   console.log(Number.parseInt('10', 2));      // 2  (二进制 10)
   console.log(Number.parseInt('10.5'));       // 10
   console.log(Number.parseInt('abc'));        // NaN
   ```

7. **`Number.toFixed(digits)`**

   - 将数字格式化为指定小数位数的字符串。
   - **返回值**: 格式化后的字符串。

   ```javascript
   let num = 123.456;
   console.log(num.toFixed(2)); // "123.46"
   console.log(num.toFixed(0)); // "123"
   console.log(num.toFixed(4)); // "123.4560"
   ```

8. **`Number.toExponential(digits)`**

   - 返回数字的指数表示法，并且可以指定小数点后保留的位数。
   - **返回值**: 格式化后的字符串（指数表示法）。

   ```javascript
   let num = 12345;
   console.log(num.toExponential(2));  // "1.23e+4"
   console.log(num.toExponential(4));  // "1.2345e+4"
   ```

9. **`Number.toPrecision(precision)`**

   - 将数字格式化为指定精度的字符串。
   - **返回值**: 格式化后的字符串。

   ```javascript
   let num = 12345.6789;
   console.log(num.toPrecision(4));  // "12350"
   console.log(num.toPrecision(6));  // "12345.7"
   ```

10. **`Number.prototype.valueOf()`**

    - 返回数字的原始值（通常与 `Number` 本身相同）。
    - **返回值**: 数字的原始值。

    ```javascript
    let num = new Number(123);
    console.log(num.valueOf());  // 123
    ```



#### 布尔（Boolean）

```js
// 布尔（逻辑）只能有两个值：true 或 false。
var x=true;
var y=false;

```



#### 空（Null）

```js
cars=null;
person=null;
```



#### 未定义（Undefined）

```js
var x;               // x 为 undefinedvar 
x = 5;               // 现在 x 为数字
var x = "John";      // 现在 x 为字符串

```



#### 符号（Symbol）

```js
// 使用 Symbol 函数创建一个新的符号。可以选择性地传入一个描述字符串，用于调试：
const sym1 = Symbol('description');
const sym2 = Symbol('description');

console.log(sym1 === sym2); // false，因为每个 Symbol 都是唯一的

// 可以使用 Symbol 作为对象的属性键：
const myObject = {
  [sym1]: 'value1'
};

console.log(myObject[sym1]); // 'value1'
console.log(myObject[sym2]); // undefined，因为 sym2 是不同的 Symbol

```







### 对象类型

#### 对象（Object）

```js
var person={firstname:"John", lastname:"Doe", id:5566};

// 对象属性有两种寻址方式：
name=person.lastname;
name=person["lastname"];
```



1. **创建对象**

- **字面量方式**

  ```javascript
  const person = {
      name: 'Alice',
      age: 30
  };
  ```

- **Object**

  ```js
  // 1.
  const person = new Objcet()
  person.name = 'Alice'
  person.age = 30
  
  // 2.
  const person = new Objcet({
      name: 'Alice',
      age: 30
  };)
  ```

- **构造函数**

  ```javascript
  function Person(name, age) {
      this.name = name;
      this.age = age;
  }
  const Alice = new Person('Alice', 30);
  ```

2. **访问和修改属性**

- **点符号**

  ```javascript
  console.log(person.name); // 'Alice'
  person.age = 31;
  ```

- **方括号符号**

  ```javascript
  console.log(person['age']); // 30
  person['name'] = 'Bob';
  ```

3. **对象方法**

- **`Object.keys(obj)`**：返回对象自身可枚举属性的数组。

  ```javascript
  const keys = Object.keys(person); // ['name', 'age']
  ```

- **`Object.values(obj)`**：返回对象自身可枚举属性值的数组。

  ```javascript
  const values = Object.values(person); // ['Bob', 31]
  ```

- **`Object.entries(obj)`**：返回对象自身可枚举属性的 [key, value] 数组。

  ```javascript
  const entries = Object.entries(person); // [['name', 'Bob'], ['age', 31]]
  ```

4. **属性描述符**

- **`Object.defineProperty(obj, prop, descriptor)`**：在对象上定义一个新属性或修改现有属性。

  ```javascript
  Object.defineProperty(person, 'gender', {
      value: 'female',
      writable: false // 该属性不可修改
  });
  ```

- **`Object.getOwnPropertyDescriptor(obj, prop)`**：返回对象中某个属性的描述符。

  ```javascript
  const descriptor = Object.getOwnPropertyDescriptor(person, 'age');
  ```

5. **合并和克隆对象**

- **`Object.assign(target, ...sources)`**：将源对象的所有可枚举属性复制到目标对象。

  ```javascript
  const obj1 = { a: 1 };
  const obj2 = { b: 2 };
  const merged = Object.assign(obj1, obj2); // { a: 1, b: 2 }
  ```

- **浅拷贝和深拷贝**

  ```javascript
  const shallowCopy = { ...person }; // 浅拷贝
  ```

  对于深拷贝，通常使用 `JSON.parse` 和 `JSON.stringify`：

  ```javascript
  const deepCopy = JSON.parse(JSON.stringify(person));
  ```

6. **遍历对象**

- **`for...in` 循环**：用于遍历对象的可枚举属性。

  ```javascript
  for (const key in person) {
      console.log(`${key}: ${person[key]}`);
  }
  ```

- **使用 `Object.keys` 与 `forEach`**

  ```javascript
  Object.keys(person).forEach(key => {
      console.log(`${key}: ${person[key]}`);
  });
  ```

7. **检查属性**

- **`hasOwnProperty(prop)`**：检查对象是否具有指定的自身属性。

  ```javascript
  const hasName = person.hasOwnProperty('name'); // true
  ```

- **`in` 操作符**：检查属性是否在对象或其原型链中。

  ```javascript
  const hasGender = 'gender' in person; // true
  ```

8. **其他方法**

- **`Object.freeze(obj)`**：冻结对象，防止修改其属性。

  ```javascript
  Object.freeze(person);
  ```

- **`Object.seal(obj)`**：封闭对象，防止添加新属性，但可以修改现有属性。

  ```javascript
  Object.seal(person);
  ```



#### 数组（Array）

```js
const fruits = ['apple', 'banana', 'cherry'];
const numbers = new Array(1, 2, 3, 4, 5);
const emptyArray = new Array(5); // 创建一个长度为5的空数组

```

1. **添加和删除元素**：

   - **`push()`**：在数组末尾添加元素。

   ```javascript
   fruits.push('mango'); // ['apple', 'orange', 'cherry', 'mango']
   ```

   - **`pop()`**：删除并返回数组末尾的元素。

   ```javascript
   const lastFruit = fruits.pop(); // 'mango'
   ```

   - **`shift()`**：删除并返回数组开头的元素。

   ```javascript
   const firstFruit = fruits.shift(); // 'apple'
   ```

   - **`unshift()`**：在数组开头添加元素。

   ```javascript
   fruits.unshift('kiwi'); // ['kiwi', 'orange', 'cherry']
   ```

2. **查找和排序**：

   - **`indexOf()`**：查找元素的索引。

   ```javascript
   const index = fruits.indexOf('cherry'); // 2
   ```

   - **`includes()`**：判断数组是否包含某个元素。

   ```javascript
   const hasBanana = fruits.includes('banana'); // false
   ```

   - **`find()`**：用于查找数组中第一个满足指定条件的元素。

   ```js
   const users = [
     { id: 1, name: 'Alice' },
     { id: 2, name: 'Bob' },
     { id: 3, name: 'Charlie' }
   ];
   
   const user = users.find(function(user) {
     return user.name === 'Bob';
   });
   
   const user = users.find(user => user.name === 'Bob');
   ```

   - **`sort(compareFunction)`**：对数组进行排序。
     - 返回负值表示第一个元素应该排在第二个元素之前。
     - 返回正值表示第一个元素应该排在第二个元素之后。
     - 返回 0 表示两个元素相等。

   ```javascript
   let fruits = ["banana", "apple", "cherry", "date"];
   fruits.sort();  // 按字母顺序排序
   console.log(fruits);  // 输出: ['apple', 'banana', 'cherry', 'date']
   
   
   let numbers = [10, 3, 5, 1, 4];
   numbers.sort((a, b) => a - b);
   console.log(numbers);  // 输出: [1, 3, 4, 5, 10]
   
   let people = [
     { name: "John", age: 25 },
     { name: "Jane", age: 30 },
     { name: "Jack", age: 20 }
   ];
   people.sort((a, b) => a.age - b.age);
   ```

3. **遍历数组**：

   - **`forEach()`**：对数组的每个元素执行一个函数。

   ```javascript
   fruits.forEach((fruit) => {
     console.log(fruit);
   });
   ```

   - **`map()`**：返回一个新数组，数组中的元素为原数组元素调用函数处理后的值。

   ```javascript
   const upperFruits = fruits.map(fruit => fruit.toUpperCase()); // ['KIWI', 'ORANGE', 'CHERRY']
   ```

   - **`filter()`**：创建一个新数组，包含所有通过测试的元素。

   ```javascript
   const longFruits = fruits.filter(fruit => fruit.length > 5); // ['orange']
   ```

4. **合并和切割**：

   - **`concat()`**：合并两个或多个数组。

   ```javascript
   const moreFruits = ['grape', 'pear'];
   const allFruits = fruits.concat(moreFruits); // ['kiwi', 'orange', 'cherry', 'grape', 'pear']
   ```

   - **`slice()`**：返回数组的一个片段。

   ```javascript
   const citrus = fruits.slice(1, 3); // ['orange', 'cherry']
   ```

   - **`splice()`**：添加或删除数组中的元素。

   ```javascript
   fruits.splice(1, 1, 'lemon'); // 在索引1处删除1个元素并添加'lemon'
   ```

5. **其他常用方法：**

   - **`every(callback)`**：测试所有元素是否都通过指定的函数。

     ```javascript
     const allLong = fruits.every(fruit => fruit.length > 3); // false
     ```

   - **`some(callback)`**：测试是否至少有一个元素通过指定的函数。

     ```javascript
     const hasLong = fruits.some(fruit => fruit.length > 5); // false
     ```

   - **`reduce(callback, initialValue)`**：从左到右应用函数，减少数组为单个值。

     ```javascript
     const sum = [1, 2, 3].reduce((acc, val) => acc + val, 0); // 6
     ```

   - **`reduceRight(callback, initialValue)`**：从右到左应用函数，减少数组为单个值。

     ```javascript
     const reversedSum = [1, 2, 3].reduceRight((acc, val) => acc + val, 0); // 6
     ```

**多维数组**

JavaScript 也支持多维数组（数组中的数组）：

```javascript
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

**伪数组与数组的区别**

| 特性              | 数组（Array）                              | 伪数组（Array-like）                            |
| ----------------- | ------------------------------------------ | ----------------------------------------------- |
| **类型**          | 是 `Array` 类型                            | 不是 `Array` 类型（通常是普通对象）             |
| **索引访问**      | 支持使用索引访问元素                       | 支持使用索引访问元素                            |
| **`length` 属性** | 有 `length` 属性                           | 也有 `length` 属性                              |
| **数组方法**      | 可以直接使用数组方法，如 `push()`、`map()` | 无法直接使用数组方法（需要转换为数组）          |
| **转换为数组**    | 可以直接操作                               | 需要通过 `Array.from()` 或扩展运算符 `...` 转换 |
| **实例**          | `let arr = [1, 2, 3]`                      | `arguments`、`NodeList`、`HTMLCollection`       |



#### 函数（Function）

```js
function myFunction(var1, var2)
{
    var x = var1 + var2;
    return x;
}
```



#### 正则（RegExp）

- **JavaScript**：内置的 `RegExp` 对象

1. **字符匹配**

   - `a`：匹配字母 "a"。
   - `.`：匹配任意单个字符（除了换行符）。

2. **字符集**

   - `[abc]`：匹配 "a"、"b" 或 "c" 中的任意一个字符。
   - `[^abc]`：匹配不包含 "a"、"b" 或 "c" 的任意字符。

3. **数量词**

   - `*`：匹配前面的字符零次或多次。
   - `+`：匹配前面的字符一次或多次。
   - `?`：匹配前面的字符零次或一次。
   - `{n}`：匹配前面的字符恰好 n 次。
   - `{n,}`：匹配前面的字符至少 n 次。
   - `{n,m}`：匹配前面的字符至少 n 次，但不超过 m 次。

4. **边界匹配**

   - `^`：匹配输入的开始位置。
   - `$`：匹配输入的结束位置。

5. **分组与捕获**
   - `()`：用于分组，可以提取匹配的子串。
   - `|`：表示 "或" 的选择，`(a|b)` 匹配 "a" 或 "b"。
   
6. **转义字符**

   - `\`：用于转义特殊字符，例如 `\.` 匹配字面上的点号。

7. **常用预定义字符类**
   - `\b`：匹配一个单词边界，通常用于确保单词的完整性。
   - `\B`：匹配一个非单词边界。
   
   - `\d`：匹配任何数字，等价于 `[0-9]`。
   - `\D`：匹配任何非数字字符。
   - `\w`：匹配任何单词字符，等价于 `[a-zA-Z0-9_]`。
   - `\W`：匹配任何非单词字符。
   - `\s`：匹配任何空白字符（空格、制表符、换行等）。
   - `\S`：匹配任何非空白字符。

**常用正则表达式方法**

1. `test()` - 测试字符串是否匹配正则表达式

该方法返回一个布尔值，表示字符串是否匹配正则表达式。

```javascript
let regex = /abc/;
console.log(regex.test("abcdef"));  // true
console.log(regex.test("xyz"));     // false
```

2. `exec()` - 提取匹配的结果（字符串在正则里的）

该方法返回一个包含匹配信息的数组，若没有匹配，返回 `null`。

```javascript
let regex = /a(bc)/;
let result = regex.exec("abcdef");
console.log(result);  // ["abc", "bc"]
```

如果没有匹配，`exec()` 返回 `null`。

3. `match()` - 在字符串中执行匹配（正则在字符串里的）

`String.prototype.match()` 方法用于匹配正则表达式，返回匹配的结果。

```javascript
let str = "hello world";
let result = str.match(/world/);
console.log(result);  // ["world"]
```

- 如果使用全局标志 `g`，它会返回一个所有匹配项的数组。

```javascript
let str = "abc abc abc";
let result = str.match(/abc/g);
console.log(result);  // ["abc", "abc", "abc"]
```

4. `replace()` - 替换匹配的内容

`String.prototype.replace()` 用于查找匹配的部分并替换成指定的内容。

```javascript
let str = "hello world";
let result = str.replace(/world/, "JavaScript");
console.log(result);  // "hello JavaScript"
```

- 如果使用全局标志 `g`，它会替换所有匹配项。

```javascript
let str = "abc abc abc";
let result = str.replace(/abc/g, "xyz");
console.log(result);  // "xyz xyz xyz"
```

5. `split()` - 按匹配分割字符串

`String.prototype.split()` 将字符串按匹配的正则表达式分割成数组。

```javascript
let str = "apple,banana,orange";
let result = str.split(/,/);
console.log(result);  // ["apple", "banana", "orange"]
```



#### 日期（Date）

1. **当前日期和时间**

   ```javascript
   const now = new Date();
   ```

2. **特定日期和时间**

   ```javascript
   const specificDate = new Date('2024-11-01T10:00:00');
   ```

3. **使用时间戳**

   ```javascript
   const timestampDate = new Date(1633046400000); // 代表特定的时间戳
   ```

**常用方法**

1. **获取日期和时间组件**

   - `getFullYear()`：获取四位年份。
   - `getMonth()`：获取月份（0-11）。
   - `getDate()`：获取一个月中的日期（1-31）。
   - `getHours()`：获取小时（0-23）。
   - `getMinutes()`：获取分钟（0-59）。
   - `getSeconds()`：获取秒（0-59）。
   - `getMilliseconds()`：获取毫秒（0-999）。
   - `getTime()`：返回自1970年1月1日00:00:00 UTC以来的毫秒数。

   ```javascript
   const date = new Date();
   console.log(date.getFullYear()); // 2024
   console.log(date.getMonth()); // 10 (11月)
   ```

2. **设置日期和时间组件**

   - `setFullYear(year)`：设置年份。
   - `setMonth(month)`：设置月份（0-11）。
   - `setDate(date)`：设置日期（1-31）。
   - `setHours(hours)`：设置小时（0-23）。
   - `setMinutes(minutes)`：设置分钟（0-59）。
   - `setSeconds(seconds)`：设置秒（0-59）。
   - `setMilliseconds(milliseconds)`：设置毫秒（0-999）。

   ```javascript
   const date = new Date();
   date.setFullYear(2025);
   date.setMonth(11); // 12月
   ```

3. **格式化日期**

   - `toString()`：返回日期对象的字符串表示。
   - `toISOString()`：返回 ISO 格式的字符串（YYYY-MM-DDTHH:mm:ss.sssZ）。
   - `toLocaleDateString()`：返回本地日期字符串。
   - `toLocaleTimeString()`：返回本地时间字符串。
   - `toUTCString()`：返回 UTC 字符串表示。

   ```javascript
   const date = new Date();
   console.log(date.toISOString()); // 2024-11-01T10:00:00.000Z
   console.log(date.toLocaleDateString()); // 根据本地设置格式化日期
   ```

4. **比较和计算日期**

   - 可以直接使用比较运算符（如 `<`、`>`）来比较日期对象。
   - 可以通过时间戳进行计算。

   ```javascript
   const date1 = new Date('2024-11-01');
   const date2 = new Date('2025-01-01');
   console.log(date1 < date2); // true
   ```

## 1.2.运算符

### 算数运算符

| 运算符 | 描述                           | 实例             |
| :----- | :----------------------------- | :--------------- |
| +      | 加                             | A + B 将得到 30  |
| -      | 减                             | A - B 将得到 -10 |
| *      | 乘                             | A * B 将得到 200 |
| /      | 除                             | B / A 将得到 2   |
| %      | 取模(取余)运算符，整除后的余数 | B % A 将得到 0   |
| ++     | 自增运算符，整数值增加 1       | A++ 将得到 11    |
| --     | 自减运算符，整数值减少 1       | A-- 将得到 9     |

### 比较运算符

**x = 5**

| 运算符  | 描述             | 实例                   |
| :------ | :--------------- | :--------------------- |
| **==**  | 值相等           | x == ‘5’   ->  true    |
| **===** | 类型和值都相等   | x === ‘5’   ->   false |
| **!=**  | 值不相等         | x != 5   ->  false     |
| **!==** | 类型和值都不相等 | x !== ‘5’   ->  false  |
| >       | 大于             |                        |
| <       | 小于             |                        |
| >=      | 大于等于         |                        |
| <=      | 小于等于         |                        |

### 逻辑运算符

**x=6, y=3**

| 运算符 | 描述 | 例子                          |
| :----- | :--- | :---------------------------- |
| &&     | and  | (x < 10 && y > 1) 为 true     |
| \|\|   | or   | (x == 5 \|\| y == 5) 为 false |
| !      | not  | !(x==y) 为 true               |



### 条件运算符

```js
variablename = (condition)?value1:value2 
```



## 1.3.判断，循环

**同C**

```js
// 新增特性
for (key in object) {
  // code block to be executed
}

for (variable of iterable) {
  // code block to be executed
}
```



### 异常处理

在 JavaScript 中，异常处理是通过 `try...catch` 语句实现的，允许捕获和处理运行时错误。异常处理机制主要包括 `try`、`catch`、`finally` 这三个部分。下面是详细的介绍：

#### 1. `try` 块

`try` 块包含可能抛出错误的代码。当代码抛出异常时，程序会跳到 `catch` 块执行。

```javascript
try {
  // 可能会抛出错误的代码
  let result = someFunction();
} 
```

#### 2. `catch` 块

`catch` 块用于捕获并处理 `try` 块中抛出的异常。`catch` 会接收一个参数，通常是一个错误对象，用于获取详细的错误信息。

```javascript
try {
  let result = someFunction();
} catch (error) {
  // 捕获并处理错误
  console.error("Error occurred:", error);
}
```

#### 3. `finally` 块

`finally` 块中的代码无论 `try` 块是否抛出异常都会执行。通常用于清理操作，如关闭文件、释放资源等。

```javascript
try {
  let result = someFunction();
} catch (error) {
  console.error("Error occurred:", error);
} finally {
  console.log("This will run no matter what.");
}
```

#### 4. `throw` 语句

`throw` 用来手动抛出一个异常，可以是任何类型的值，通常是一个错误对象或字符串。

```javascript
try {
  let age = -1;
  if (age < 0) {
    throw new Error("Age cannot be negative.");
  }
} catch (error) {
  console.error(error.message);  // 输出: Age cannot be negative.
}
```

#### 完整示例

```javascript
function divide(a, b) {
  try {
    if (b === 0) {
      throw new Error("Cannot divide by zero.");
    }
    return a / b;
  } catch (error) {
    console.error(error.message);  // 输出: Cannot divide by zero.
  } finally {
    console.log("Division attempt finished.");
  }
}

divide(10, 0);
```

#### 错误对象（`Error` 对象）

当异常被抛出时，可以创建一个 `Error` 对象，它有几个常用的属性：

- `message`：包含错误信息的字符串。
- `name`：错误的名称，默认是 `Error`，可以自定义。
- `stack`：包含错误发生时的堆栈追踪信息（浏览器中通常可以访问）。

```javascript
try {
  throw new Error("Something went wrong");
} catch (error) {
  console.error(error.name);    // 输出: Error
  console.error(error.message); // 输出: Something went wrong
  console.error(error.stack);   // 输出: 错误堆栈信息
}
```

除了 `Error` 外，JavaScript 还提供了一些内置的错误类型，它们是 `Error` 的子类，通常用于特定的错误场景：

- **`TypeError`**：表示变量或参数的类型不正确。
- **`SyntaxError`**：表示代码语法错误。
- **`ReferenceError`**：表示访问一个不存在的变量。
- **`RangeError`**：表示一个值超出了有效范围。
- **`EvalError`**：与 `eval()` 函数相关的错误。





## 1.4.函数

```js
function myFunction(var1, var2)
{
    var x = var1 + var2;
    return x;
}
```





### filter()

`filter()` 是一个用于数组的高阶函数，它可以用来根据特定条件过滤数组中的元素，并返回一个新数组。这个新数组包含了所有符合条件的元素，原数组不会被修改。

```js
array.filter(callback(element, index, array))
```

- **`callback`**：这是一个回调函数，用来定义过滤的条件。这个回调函数会对数组中的每一个元素执行一次。
  - **`element`**：当前处理的元素。
  - **`index`**：当前元素在数组中的索引（可选）。
  - **`array`**：调用 `filter()` 的原数组（可选）。
- **返回值**：`filter()` 返回一个新数组，这个数组包含所有满足条件的元素。如果没有任何元素满足条件，则返回一个空数组。

**例子**：

假设我们有一个电影对象数组，想要过滤出所有评分大于 8 的电影：

```js
const films = [
  { title: 'Inception', rating: 8.8 },
  { title: 'Titanic', rating: 7.8 },
  { title: 'The Dark Knight', rating: 9.0 },
  { title: 'Avatar', rating: 7.9 }
];

const highRatedFilms = films.filter(film => film.rating > 8);

console.log(highRatedFilms);
// 输出：
// [
//   { title: 'Inception', rating: 8.8 },
//   { title: 'The Dark Knight', rating: 9.0 }
// ]
```



### eval()

`eval()` 是 JavaScript 中的一个内置函数，它将一个字符串作为 JavaScript 代码执行。简单来说，`eval()` 可以执行传入的字符串，并返回执行结果。

```js
eval(string)
```

**基本用法：**

```javascript
let x = 10;
let result = eval('x + 5');
console.log(result);  // 15
```

在这个例子中，`eval()` 执行了字符串 `'x + 5'`，并返回了 `x + 5` 的值，最终结果是 `15`。

**例子 2：执行表达式**

```javascript
javascriptlet expression = '2 + 3 * 4';
let result = eval(expression);
console.log(result);  // 14
```

此例中，`eval()` 计算了表达式 `2 + 3 * 4` 并返回了结果 `14`。

**例子 3：执行函数调用**

```javascript
function greet() {
  return 'Hello, World!';
}

let result = eval('greet()');
console.log(result);  // "Hello, World!"
```

在这个例子中，`eval()` 执行了 `greet()` 函数，并返回了 `"Hello, World!"`。

**例子 4：执行赋值语句**

```javascript
let x = 5;
eval('x = x + 10');
console.log(x);  // 15
```

`eval()` 允许执行赋值语句，因此 `x` 的值变成了 `15`。

### Math

**常用的 `Math` 方法**

1. **`Math.abs(x)`**
    返回数值 `x` 的绝对值：

   ```javascript
   console.log(Math.abs(-5));  // 5
   ```

2. **`Math.ceil(x)`**
    向上取整，返回大于或等于 `x` 的最小整数：

   ```javascript
   console.log(Math.ceil(4.2));  // 5
   ```

3. **`Math.floor(x)`**
    向下取整，返回小于或等于 `x` 的最大整数：

   ```javascript
   console.log(Math.floor(4.8));  // 4
   ```

4. **`Math.round(x)`**
    四舍五入，返回最接近 `x` 的整数：

   ```javascript
   console.log(Math.round(4.5));  // 5
   ```

5. **`Math.max(a, b, c, ...)`**
    返回给定的一组数值中的最大值：

   ```javascript
   console.log(Math.max(1, 5, 3));  // 5
   ```

6. **`Math.min(a, b, c, ...)`**
    返回给定的一组数值中的最小值：

   ```javascript
   console.log(Math.min(1, 5, 3));  // 1
   ```

7. **`Math.random()`**
    返回一个介于 `0`（包含）和 `1`（不包含）之间的随机数：

   ```javascript
   console.log(Math.random());  // 例如：0.3928
   ```

8. **`Math.pow(x, y)`**
    返回 `x` 的 `y` 次方：

   ```javascript
   console.log(Math.pow(2, 3));  // 8
   ```

9. **`Math.sqrt(x)`**
    返回 `x` 的平方根：

   ```javascript
   console.log(Math.sqrt(16));  // 4
   ```

10. **`Math.sin(x)`**, **`Math.cos(x)`**, **`Math.tan(x)`**
     返回角度 `x` 的正弦、余弦和正切值（角度需要转换为弧度）：

    ```javascript
    console.log(Math.sin(Math.PI / 2));  // 1
    ```

11. **`Math.log(x)`**
     返回 `x` 的自然对数（以 `e` 为底）：

    ```javascript
    console.log(Math.log(10));  // 2.302585
    ```

12. **`Math.exp(x)`**
     返回 `e` 的 `x` 次方：

    ```javascript
    console.log(Math.exp(2));  // 7.389056
    ```



### localStorage

`localStorage` 是 Web 存储 API 提供的一部分，它允许在用户的浏览器中以键值对的形式永久性地存储数据。`localStorage` 的数据在浏览器会话结束后仍然存在，并且不会过期，直到被显式删除。它适用于存储需要长期保存的数据，例如用户设置、登录信息等。

**主要特点**：

- **数据持久性**：`localStorage` 存储的数据没有过期时间，除非被显式删除。
- **同源策略**：存储的数据只能在同一域名下的页面中访问，不同的域名、协议或端口之间的数据是隔离的。
- **存储大小限制**：`localStorage` 通常允许存储每个域名约 5MB 的数据，具体大小可能因浏览器而异。
- **同步存储**：对 `localStorage` 的操作是同步的，即在操作完成后，数据会立即可用。

**常用方法**：

1. **`localStorage.setItem(key, value)`**

    - 用于将数据存储在 `localStorage` 中。
    - 参数：
        - `key`: 键名，表示数据的名称。
        - `value`: 值，存储的数据，通常是字符串类型。

    ```javascript
    localStorage.setItem('username', 'Alice');
    ```

2. **`localStorage.getItem(key)`**

    - 用于从 `localStorage` 获取指定 `key` 的数据。

    - 参数

        ：

        - `key`: 键名，表示要获取的数据。

    - **返回值**：如果找到了对应的值，返回该值；如果没有找到，返回 `null`。

    ```javascript
    const username = localStorage.getItem('username');
    console.log(username);  // 输出: Alice
    ```

3. **`localStorage.removeItem(key)`**

    - 用于从 `localStorage` 删除指定 `key` 的数据。
    - 参数：
        - `key`: 键名，表示要删除的数据。

    ```javascript
    localStorage.removeItem('username');
    ```

4. **`localStorage.clear()`**

    - 用于清空 `localStorage` 中的所有数据。

    ```javascript
    localStorage.clear();
    ```

5. **`localStorage.length`**

    - 返回 `localStorage` 中存储的键值对数量。

    ```javascript
    console.log(localStorage.length);  // 输出存储的键值对数量
    ```

6. **`localStorage.key(index)`**

    - 根据索引获取 `localStorage` 中的键名。

    ```js
    const key = localStorage.key(0);
    console.log(key);  // 输出第一个键名
    ```



## 1.5.输入输出

**输入**

```js
// 1.页面弹出输入对话框
prompt('plz enter your name:')
```

**输出**

```js
// 1.向body内输出内容
document.write('<h1>title</h1>')

// 2.页面弹出警告对话框
window.alert('warning:invalid action')

// 3.控制台输出，程序员调试使用
console.log('console-print')
```



## 1.6.ES6

ES6（也称为 ECMAScript 2015）是 ECMAScript 标准的第 6 版，它引入了许多重要的新特性和改进，使得 JavaScript 更加强大、灵活且易于使用。以下是 ES6 的一些关键特性：

**ECMAScript 的背景**

JavaScript 是大家所了解的语言名称，但是这个语言名称是商标（ Oracle 公司注册的商标）。因此，JavaScript 的正式名称是 ECMAScript 。1996年11月，JavaScript 的创造者网景公司将 JS 提交给国际化标准组织 ECMA（European computer manufactures association，欧洲计算机制造联合会），希望这种语言能够成为国际标准，随后 ECMA 发布了规定浏览器脚本语言的标准，即 ECMAScript。这也有利于这门语言的开放和中立。

### 变量与常量的声明

```js
// 1.常量
const BASE_URL = 'http://filmhub.com/api';

// 2.变量
let i = 0;
i++;
```



### 模板字符串

```js
const name = 'Peter';
const greeting = `I'm ${name}`
```



### 闭包

在 JavaScript 中，**闭包（Closure）** 是一个函数与其词法作用域（即函数声明时所在的作用域）的组合。换句话说，闭包允许一个函数访问并操作它外部函数的变量，即使外部函数已经返回。

简而言之，闭包可以理解为：**函数被定义时的作用域**，而不仅仅是它执行时的作用域  <==>  **内层函数 + 外层函数的变量**

#### 闭包的工作原理

闭包的实现依赖于 **词法作用域**。当一个函数被定义时，它会记住外部函数的作用域，这就是闭包的核心。

例子：闭包的作用域链

```javascript
function outer() {
  let outerVar = "I'm an outer variable";

  function inner() {
    console.log(outerVar);  // 访问外部函数的变量
  }

  return inner;
}

const closureFunc = outer();
closureFunc();  // 输出 "I'm an outer variable"
```

#### 闭包的使用场景

##### 1. 模拟私有变量

在 JavaScript 中，我们可以通过闭包来模拟私有变量的行为。通过将变量封装在函数内部，只暴露需要的函数来操作这些私有变量。

```javascript
function createCounter() {
  let count = 0; // 私有变量
  return {
    increment: function() {
      count++;
      return count;
    },
    decrement: function() {
      count--;
      return count;
    },
    getCount: function() {
      return count;
    }
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount()); // 2
console.log(counter.decrement()); // 1
```

在上面的例子中，`count` 是 `createCounter` 函数的私有变量，它无法直接访问，但是通过闭包暴露了 `increment`、`decrement` 和 `getCount` 等方法，可以访问和修改它。

##### 2. 延迟执行或回调函数

闭包常用于异步编程，例如，回调函数、定时器等，可以在不同的时间点使用外部函数的变量。

```javascript
function createDelayedMessage(message) {
  return function() {
    console.log(message);
  };
}

const delayedHello = createDelayedMessage("Hello, World!");
setTimeout(delayedHello, 1000);  // 1秒后输出 "Hello, World!"
```

在这个例子中，`setTimeout` 延迟执行的回调函数可以访问 `createDelayedMessage` 函数中的 `message` 变量，即使 `createDelayedMessage` 函数已经执行完毕。







### 解构赋值

#### 1.数组的解构赋值

```js
// 1.解构赋值
let arr = [1, 2, 3];
let [a, b, c] = arr;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3

// 2.跳过某些元素
let arr = [1, 2, 3];
let [, b, c] = arr;

console.log(b); // 2
console.log(c); // 3

// 3.默认值
let arr = [1];

// 如果没有提供第二个值，使用默认值
let [a, b = 2] = arr;

console.log(a); // 1
console.log(b); // 2


// 4.剩余操作
let arr = [1, 2, 3, 4, 5];

// 获取前两个元素，剩下的部分放在其他变量中
let [a, b, ...rest] = arr;

console.log(a);     // 1
console.log(b);     // 2
console.log(rest);  // [3, 4, 5]
```



#### 2.对象的解构赋值

```js
// 1.解构赋值
let person = { name: 'Alice', age: 25 };
let { name, age } = person;

console.log(name); // Alice
console.log(age);  // 25

// 2.重命名变量
let person = { name: 'Alice', age: 25 };
let { name: fullName, age: years } = person;

console.log(fullName); // Alice
console.log(years);    // 25

// 3.默认值
let person = { name: 'Alice' };

// 如果没有提供 age 属性，使用默认值
let { name, age = 30 } = person;

console.log(name); // Alice
console.log(age);  // 30

// 4.嵌套解构
let person = { name: 'Alice', address: { city: 'New York', zip: 10001 } };

// 解构嵌套对象
let { name, address: { city, zip } } = person;

console.log(name); // Alice
console.log(city); // New York
console.log(zip);  // 10001

// 5.剩余操作
let person = { name: 'Alice', age: 25, gender: 'female' };

// 提取剩余属性
let { name, ...otherInfo } = person;

console.log(name);  // Alice
console.log(otherInfo);  // { age: 25, gender: 'female' }
```



#### 3.解构赋值可以直接用在函数参数中

```js
// 1.
function print([a, b]) {
  console.log(a, b);
}

print([1, 2]); // 1 2

// 2.
function greet({ name, age }) {
  console.log(`Hello, ${name}. You are ${age} years old.`);
}

greet({ name: 'Alice', age: 25 }); // Hello, Alice. You are 25 years old.

```



### 拓展

#### 1.数组的拓展



##### 1. 扩展运算符 `...`

扩展运算符 (`...`) 可以用于数组，来快速复制、合并或提取元素。

数组合并：

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];

let mergedArr = [...arr1, ...arr2];
console.log(mergedArr); // [1, 2, 3, 4]
```

数组复制：

```javascript
let arr = [1, 2, 3];
let copiedArr = [...arr];

console.log(copiedArr); // [1, 2, 3]
```

插入元素：

```javascript
let arr = [1, 2, 3];
let extendedArr = [0, ...arr, 4];

console.log(extendedArr); // [0, 1, 2, 3, 4]
```



##### 2. `Array.from()`

`Array.from()` 方法可以将类似数组的对象（如字符串、Set、Map等）转换为数组。

**语法**：

```javascript
Array.from(arrayLike, mapFn, thisArg)
```

- **arrayLike**：类数组对象或可迭代对象（如 `String`、`Set`、`Map`、`NodeList` 等）。
- **mapFn**（可选）：一个映射函数，用于对每个元素进行处理。在创建新数组时，它会应用于每个元素。
- **thisArg**（可选）：用于执行映射函数时的 `this` 值。

**返回值**：

返回一个新的数组，包含由 `arrayLike` 中的元素组成的值，经过 `mapFn` 处理后（如果提供了该函数）。

```javascript
let str = "hello";
let arr = Array.from(str);

console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```





#### 2.对象的拓展

##### 1. 扩展运算符 `...`

同样，扩展运算符也可以用于对象的合并、复制和提取属性。

对象合并：

```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { b: 3, c: 4 };

let mergedObj = { ...obj1, ...obj2 };
console.log(mergedObj); // { a: 1, b: 3, c: 4 }
```

对象复制：

```javascript
let obj = { a: 1, b: 2 };

let copiedObj = { ...obj };
console.log(copiedObj); // { a: 1, b: 2 }
```



##### 2. `Object.assign()`

`Object.assign()` 方法用于将一个或多个源对象的可枚举属性复制到目标对象中。

**语法**：

```javascript
Object.assign(target, ...sources)
```

- **target**：目标对象，`Object.assign()` 会将源对象的属性复制到这个目标对象中。
- **sources**：一个或多个源对象，其属性会被复制到目标对象中。如果有多个源对象，它们的属性会依次复制到目标对象。

**返回值**：

返回目标对象 `target`，其中包含所有源对象的属性。

```javascript
let obj1 = { a: 1 };
let obj2 = { b: 2 };

let mergedObj = Object.assign({}, obj1, obj2);
console.log(mergedObj); // { a: 1, b: 2 }
```



### 原型

在 JavaScript 中，**原型**（Prototype）是每个对象都有的一个内部属性，它指向另一个对象，称为“原型对象”。原型是 JavaScript 实现继承和共享方法、属性的基础。每个 Java式对象都有一个原型对象（通过`__proto__` 或者 `Object.getPrototypeOf()` 访问），原型对象也可以有自己的原型对象，从而形成一个链式结构，叫做**原型链**。

#### 1. 原型链

JavaScript 中的对象继承是通过原型链来实现的。每当你访问一个对象的属性时，如果对象本身没有该属性，它会在对象的原型上查找，依次查找直到原型链的尽头（通常是 `Object.prototype`，它的原型为 `null`）。

例如：

```javascript
let animal = {
  eat() {
    console.log('Eating...');
  }
};

let dog = Object.create(animal);  // dog 的原型是 animal
dog.bark = function() {
  console.log('Barking...');
};

dog.bark();  // "Barking..."
dog.eat();   // "Eating..."  (从原型 animal 中继承的)
```

在这个例子中，`dog` 对象没有 `eat` 方法，但是它的原型 `animal` 有，所以 `dog` 通过原型链可以访问到 `eat` 方法。

#### 2. 原型的属性和方法

- **`__proto__`**: **对象原型**，每个对象都有一个 `__proto__` 属性（浏览器中的非标准实现）。它指向该对象的构造函数的 `prototype` 属性。

- **`constructor`**: 每个对象的原型对象都有一个 `constructor` 属性，指向创建该对象的构造函数。

  ```javascript
  let obj = {};
  console.log(obj.__proto__ === Object.prototype);  // true
  
  console.log(obj.__proto__.constructor === Object); // true
  ```

- **`Object.getPrototypeOf(obj)`**: 用来获取对象的原型。

  ```javascript
  let obj = {};
  console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
  ```

- **`Object.setPrototypeOf(obj, prototype)`**: 用来设置对象的原型。

  ```javascript
  let obj = {};
  let prototypeObj = { sayHi() { console.log("Hi!"); } };
  Object.setPrototypeOf(obj, prototypeObj);
  obj.sayHi(); // "Hi!"
  ```

#### 3. 构造函数与原型

每个通过构造函数创建的对象都有一个**原型对象**，该原型对象是通过构造函数的 `prototype` 属性来设置的。

例如：

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function() {
  console.log('Hello ' + this.name);
};

let john = new Person('John', 25);
john.sayHello();  // "Hello John"
```

在这个例子中，`john` 是 `Person` 的实例，它继承了 `Person.prototype` 上的方法 `sayHello`。

#### 4. 原型链示例

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.sayName = function() {
  console.log(this.name);
};

function Dog(name) {
  Animal.call(this, name);  // 继承 Animal 的属性
}

Dog.prototype = Object.create(Animal.prototype);  // 继承 Animal 的方法
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  console.log('Woof!');
};

const dog = new Dog('Buddy');
dog.sayName();  // "Buddy" (继承自 Animal)
dog.bark();     // "Woof!" (Dog 特有方法)
```

在这个例子中，`Dog` 通过 `Object.create(Animal.prototype)` 继承了 `Animal` 的方法，并且 `dog` 实例能够访问 `sayName` 和 `bark` 方法。

#### 5. 原型的继承

通过构造函数和原型机制，JavaScript 实现了继承。原型链允许一个对象继承另一个对象的属性和方法，从而实现了对象的共享和复用。

- **原型继承的缺点**：所有的实例共享原型对象上的属性和方法。如果原型上有可变的属性（例如数组、对象等），则多个实例间的属性可能会相互影响。

```javascript
function Dog(name) {
  this.name = name;
}

Dog.prototype.friends = [];  // 共享的属性

const dog1 = new Dog('Buddy');
const dog2 = new Dog('Max');

dog1.friends.push('Charlie');
console.log(dog1.friends);  // ["Charlie"]
console.log(dog2.friends);  // ["Charlie"]  (共享了同一个数组)
```

为避免共享原型属性带来的问题，可以使用 `constructor` 函数中的 `this` 来确保每个实例都有独立的属性。

```javascript
function Dog(name) {
  this.name = name;
  this.friends = [];  // 独立的属性
}
```



### class类

在 JavaScript 中，`class` 是一种定义对象和构造函数的语法糖，它使得创建和管理对象更加简洁和直观。`class` 语法引入了面向对象编程（OOP）的概念，如构造函数、方法和继承等。

#### 基本语法

```javascript
class ClassName {
  constructor() {
    // 构造函数，用于创建实例
  }

  // 实例方法
  methodName() {
    // 方法逻辑
  }

  // 静态方法
  static staticMethod() {
    // 静态方法逻辑
  }
}
```

1. **`constructor`**：构造函数，用来初始化类的实例。每次创建类的实例时，`constructor` 会被调用。
2. **实例方法**：可以在类中定义方法，这些方法会成为类的实例的属性。
3. **静态方法**：静态方法使用 `static` 关键字定义，不能通过实例调用，而是通过类本身调用。

#### 示例

```javascript
class Person {
  // 构造函数
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  // 实例方法
  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }

  // 静态方法
  static species() {
    return 'Homo sapiens';
  }
}

// 创建类的实例
const person1 = new Person('Alice', 30);
person1.greet(); // 输出: Hello, my name is Alice and I am 30 years old.

// 调用静态方法
console.log(Person.species()); // 输出: Homo sapiens
```

1. **`constructor()`**：是一个特殊的方法，用来初始化对象的状态。当你通过 `new` 创建类的实例时，`constructor` 方法会自动被调用。它可以接受参数并将它们赋值给实例属性。
2. **实例方法**：是定义在类中的普通方法。实例化该类时，所有实例都会继承这些方法。
3. **静态方法**：通过 `static` 关键字定义的静态方法与类本身关联，而不是与实例关联。因此，静态方法只能通过类来访问，而不能通过实例访问。

#### 继承

JavaScript 中的类支持继承，可以通过 `extends` 关键字继承父类的功能。子类可以继承父类的属性和方法，也可以重写父类的方法。

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 调用父类的构造函数
    this.breed = breed;
  }

  // 重写父类的方法
  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog('Rex', 'Golden Retriever');
dog.speak(); // 输出: Rex barks.
```

- **`extends`**：用于继承父类。`Dog` 类继承自 `Animal` 类。
- **`super()`**：在子类的构造函数中调用父类的构造函数，通常用来初始化继承的属性。

#### 自定义行为

JavaScript 中的类还支持 getter 和 setter，允许你定义访问和设置对象属性时的自定义行为。

```javascript
class Circle {
  constructor(radius) {
    this._radius = radius;
  }

  // getter
  get radius() {
    return this._radius;
  }

  // setter
  set radius(value) {
    if (value <= 0) {
      console.log('Radius must be positive');
    } else {
      this._radius = value;
    }
  }

  area() {
    return Math.PI * this._radius ** 2;
  }
}

const circle = new Circle(10);
console.log(circle.area()); // 输出: 314.1592653589793

circle.radius = -5; // 输出: Radius must be positive
circle.radius = 15; // 修改半径为 15
console.log(circle.area()); // 输出: 706.8583470577034
```

- **getter**：定义了一个获取属性的自定义方法。
- **setter**：定义了一个设置属性时的自定义行为。







### this关键字

JavaScript `this` 关键词指的是它所属的对象。

它拥有不同的值，具体取决于它的使用位置：

- 在方法中，`this` 指的是**所有者对象**。eg: fullName

  ```js
  const person = {
    firstName: "John",
    lastName: "Doe",
    fullName: function() {
      return this.firstName + " " + this.lastName; // this 代表 person 对象
    }
  };
  
  console.log(person.fullName());  // 输出: "John Doe"
  ```

  

- 单独的情况下，`this` 指的是**全局对象window**。

  ```js
  var x = this;
  ```

  

- 在普通函数中，`this` 指的是**全局对象window**。

- 在箭头函数中，`this` 指的是**最近作用域中的this**（向外层作用域中，一层一层查找）

- 在函数中，严格模式下，`this` 是 **undefined**。

  ```js
  function myFunction() {
    return this;
  }
  
  "use strict";
  function myFunction() {
    return this;
  }
  ```

  

- 在事件中，`this` 指的是接收事件的元素。

  ```js
  const button = document.querySelector('.button');
  button.addEventListener('click', function() {
    console.log(this);  // this 指向 button 元素
  });
  
  ```

  

像 `call()` 和 `apply()` 这样的方法可以将 this 引用到任何对象。

- `call()`：立即调用函数，并明确指定 `this` 的值。

  ```javascript
  func.call(thisArg, arg1, arg2, ...);
  ```

  

- `apply()`：与 `call` 类似，区别在于 `apply` 接收的是一个数组作为参数。

  ```javascript
  func.apply(thisArg, [arg1, arg2, ...]);
  ```

  

- `bind()`：`bind` 返回一个新函数，绑定了指定的 `this` 值。

  ```javascript
  const newFunc = func.bind(thisArg, arg1, arg2, ...);
  ```
  
  
  
  ```js
  // call()
  function greet() {
    console.log(this.name);
  }
  
  const person = { name: 'David' };
  greet.call(person);  // 输出 'David'，this 指向 person 对象
  
  
  // apply()
  function greet(city, country) {
    console.log(this.name + ' from ' + city + ', ' + country);
  }
  
  const person = { name: 'David' };
  greet.apply(person, ['New York', 'USA']);  // 输出 'David from New York, USA'
  
  
  // bind()
  function greet() {
    console.log(this.name);
  }
  
  const person = { name: 'David' };
  const boundGreet = greet.bind(person);
  boundGreet();  // 输出 'David'
  
  ```
  
  



### 自执行函数

自执行函数（**Immediately Invoked Function Expression**，简称 IIFE）是一种 JavaScript 函数，它在定义时立即执行。这种模式常常用来创建一个独立的作用域，避免全局作用域污染，尤其在模块化编程中非常常见。

**IIFE 的基本形式**

IIFE 的语法是将一个函数表达式包裹在圆括号中，然后在末尾加上一对小括号来立即调用它。

```javascript
(function() {
    // 代码
    console.log('This is an IIFE!');
})();

// 2.带参数的 IIFE：
(function(name) {
    console.log("Hello, " + name + "!");
})('Alice');
```

**解释**

1. `function()` 是一个匿名函数表达式。
2. 外面的圆括号 `( ... )` 是将函数表达式包装起来，使其成为一个表达式，而不是声明。
3. 函数的末尾 `()` 表示立即调用该函数。



### 箭头函数

箭头函数（Arrow Function）是 JavaScript 中的一种简化函数表达式的语法。它在 ES6（ECMAScript 2015）中引入，提供了比传统函数表达式更简洁的写法，并且在函数内部的 `this` 行为上有所不同。

**语法**

箭头函数的基本语法如下：

```javascript
const functionName = (parameters) => {
    // function body
}
```

- **`parameters`**：函数的参数，可以是一个或多个参数。如果只有一个参数，可以省略括号。
- **`=>`**：箭头符号，表示函数的定义。
- **`function body`**：函数的主体，执行逻辑。如果函数体只有一行，可以省略大括号和 `return` 关键字。

**示例**

1. **没有参数的箭头函数：**

   ```javascript
   const sayHello = () => {
       console.log('Hello!');
   };
   
   sayHello();  // 输出: Hello!
   ```

2. **一个参数的箭头函数：**

   ```javascript
   const square = (x) => {
       return x * x;
   };
   
   console.log(square(5));  // 输出: 25
   ```

   如果参数只有一个，圆括号可以省略：

   ```javascript
   const square = x => x * x;
   
   console.log(square(5));  // 输出: 25
   ```

3. **多个参数的箭头函数：**

   ```javascript
   const add = (a, b) => {
       return a + b;
   };
   
   console.log(add(3, 4));  // 输出: 7
   ```

   如果参数有多个，圆括号是必须的。

4. **没有函数体的箭头函数（隐式返回）：**

   当箭头函数的主体只有一个表达式时，返回值会自动返回，无需使用 `return` 关键字。这个特性叫做 **隐式返回**。

   ```javascript
   const multiply = (a, b) => a * b;
   
   console.log(multiply(2, 3));  // 输出: 6
   ```

   这相当于：

   ```javascript
   const multiply = (a, b) => {
       return a * b;
   };
   ```

**箭头函数的特点**

1. **简洁的语法**： 箭头函数的语法更简洁，尤其是在处理简短的逻辑时。它可以显著减少函数表达式的代码量。

2. **`this` 绑定**： 箭头函数与传统函数的一个重要区别在于，它不会创建自己的 `this`，而是继承**外部上下文**的 `this`。这意味着箭头函数不会改变 `this` 的指向，它的 `this` 由它定义时的上下文决定，而传统的函数会根据调用方式来动态绑定 `this`。

   例如：

   ```javascript
   function Person(name) {
       this.name = name;
       this.sayHello = function() {
           setTimeout(function() {
               console.log('Hello, ' + this.name);  // 'this' 在这里指向 global 或 window
           }, 1000);
       };
   }
   
   const john = new Person('John');
   john.sayHello();  // 输出: Hello, undefined
   ```

   在传统函数中，`this` 由调用环境决定，因此在 `setTimeout` 中，`this` 会指向 `window` 或 `global`，导致 `this.name` 为 `undefined`。

   使用箭头函数可以避免这个问题：

   ```javascript
   function Person(name) {
       this.name = name;
       this.sayHello = function() {
           setTimeout(() => {
               console.log('Hello, ' + this.name);  // 'this' 继承自 Person 构造函数
           }, 1000);
       };
   }
   
   const john = new Person('John');
   john.sayHello();  // 输出: Hello, John
   ```

   在这种情况下，箭头函数不会改变 `this` 的指向，它继承了 `sayHello` 方法所在的 `Person` 构造函数的 `this`，因此能够正确地访问到 `this.name`。



### 异步

在 JavaScript 中，异步编程允许你执行时间较长的操作（如网络请求、文件读取等）而不会阻塞主线程，从而保持用户界面的响应性。**异步任务会在当前存在的同步任务都执行完毕后再触发。**

举个例子：

想象你正在做一顿晚餐。你在切菜时，把水壶放在炉子上加热水，但是你并不需要一直站在水壶旁边等待它烧开。你可以去做其他事情，比如继续切菜或者准备其他食材。等水烧开了，水壶会提醒你“好了，可以用了”。你就去接水，继续做晚餐。

这个过程中的“烧水”就是一个**异步**操作——你不需要等待它完成才去做其他的事情，烧水的过程和你做其他事是**同时进行**的，等水烧开后，系统会通知你。

关键点：

1. **同时进行**：可以做多个事情，而不需要一个完成了才能做下一个。
2. **不阻塞**：不需要等待某个任务完成，程序可以继续执行其他任务。
3. **通知完成**：任务完成后，系统或程序会通知你结果。

| 特性             | 同步                                         | 异步                                       |
| ---------------- | -------------------------------------------- | ------------------------------------------ |
| **执行顺序**     | 按顺序执行，前一个任务完成后再执行下一个任务 | 不按顺序执行，任务可以并行进行             |
| **是否阻塞**     | 阻塞，前一个任务未完成，后续任务无法开始     | 非阻塞，任务可以并行进行                   |
| **执行效率**     | 在I/O操作较多时效率较低                      | 可以在I/O操作时继续执行其他任务，提高效率  |
| **代码复杂性**   | 简单易懂                                     | 需要处理回调函数、`Promise` 等，代码较复杂 |
| **常见应用场景** | 计算密集型任务，顺序操作                     | I/O密集型任务，网络请求，文件操作等        |

#### 1. Callback

回调函数是最基本的异步编程方式。当异步操作完成时，传入的回调函数会被调用。

```javascript
// 异步操作示例：setTimeout
setTimeout(function() {
    console.log('异步操作完成');
}, 1000);

console.log('这条语句会先执行');
```

**输出：**

```
这条语句会先执行
异步操作完成
```



**setTimeout 和 setInterval**

这两个方法可以用于延时执行代码：

- `setTimeout`: 在指定的延时之后执行一次代码。
- `setInterval`: 每隔指定的时间间隔执行一次代码。

```js
// setTimeout 示例
setTimeout(() => {
    console.log('1秒后执行');
}, 1000);

// setInterval 示例
let counter = 0;
let intervalId = setInterval(() => {
    counter++;
    console.log('每秒执行一次', counter);
    if (counter === 5) {
        clearInterval(intervalId);  // 停止定时器
    }
}, 1000);
```



#### 2. Promise

在 JavaScript 中，**`Promise`** 是一种用于表示**异步操作最终完成（或失败）及其结果值的对象**。它可以帮助你管理异步操作，避免回调地狱（callback hell），使得异步代码更加简洁、可读。

**Promise 的三种状态**

1. **pending（等待中）**：Promise 被创建后，初始状态是“等待中”，即异步操作还没有完成。
2. **resolved/fulfilled（已解决/已完成）**：异步操作成功完成，Promise 的状态变为已解决，值是异步操作的结果。
3. **rejected（已拒绝）**：异步操作失败，Promise 的状态变为已拒绝，值是错误信息或原因。

**如何创建和使用 Promise**

```javascript
// 创建一个 Promise
const promise = new Promise((resolve, reject) => {
  // 模拟异步操作
  let success = true;  // 这个可以根据需求改变

  if (success) {
    resolve("操作成功！");  // 成功时调用 resolve()
  } else {
    reject("操作失败！");   // 失败时调用 reject()
  }
});

// 使用 Promise
promise.then((result) => {
  console.log(result);  // 输出：操作成功！
}).catch((error) => {
  console.log(error);   // 如果失败，输出：操作失败！
});
```

**Promise 的链式调用**

由于 `then()` 和 `catch()` 方法返回一个新的 Promise，你可以将它们链式调用，使得代码更加简洁和直观。

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("步骤 1 完成");
  }, 1000);
});

promise
  .then((result) => {
    console.log(result);  // 输出：步骤 1 完成
    return "步骤 2 完成"; // 返回一个新的 Promise 或值
  })
  .then((result) => {
    console.log(result);  // 输出：步骤 2 完成
  })
  .catch((error) => {
    console.log(error);  // 如果中间发生错误会被捕获
  });
```

**`Promise.all` 和 `Promise.race`**

- **`Promise.all()`**：接受一个包含多个 Promise 的数组，当所有 Promise 都成功完成时，它会返回一个新的 Promise，结果是一个包含所有 Promise 结果的数组。如果其中有任何一个 Promise 失败，它会直接被拒绝。

  ```javascript
  const promise1 = Promise.resolve(3);
  const promise2 = new Promise((resolve, reject) => setTimeout(resolve, 100, "foo"));
  const promise3 = 42;
  
  Promise.all([promise1, promise2, promise3]).then((values) => {
    console.log(values);  // 输出: [3, "foo", 42]
  });
  ```

- **`Promise.race()`**：接受一个包含多个 Promise 的数组，返回的 Promise 将根据第一个完成（无论是成功还是失败）而决定结果。

  ```javascript
  const promise1 = new Promise((resolve, reject) => setTimeout(resolve, 500, "First"));
  const promise2 = new Promise((resolve, reject) => setTimeout(resolve, 100, "Second"));
  
  Promise.race([promise1, promise2]).then((value) => {
    console.log(value);  // 输出: Second（因为 promise2 最先完成）
  });
  ```

**Promise 的优点**

1. **链式调用**：可以在 `.then()` 中逐步处理多个异步操作，而不需要嵌套。
2. **错误处理**：可以通过 `.catch()` 来捕获和处理异步操作中的错误。
3. **避免回调地狱**：相比于传统的回调函数，`Promise` 使异步代码更加清晰和可维护。

**`async`和`await`**

- **`async`**：用于声明一个函数为异步函数，异步函数总是返回一个 `Promise` 对象。如果函数中有返回值，`Promise` 会自动被解析为该值。如果函数抛出错误，`Promise` 会变为拒绝状态。
- **`await`**：只能在 `async` 函数内部使用。它会等待一个 `Promise` 完成，并返回该 `Promise` 的结果。如果 `Promise` 被拒绝（即失败），`await` 会抛出错误。

基本用法：

```javascript
// 声明一个异步函数
async function myAsyncFunction() {
  // 等待一个 Promise 完成并返回结果
  const result = await new Promise((resolve, reject) => {
    setTimeout(() => resolve("操作成功！"), 1000);
  });

  console.log(result); // 输出：操作成功！
}

// 调用异步函数
myAsyncFunction();
```

理解：

- **`async` 函数**：无论你在函数内写什么内容，它都会返回一个 `Promise`。如果函数返回的是一个普通值，它会被自动封装成一个 `Promise` 并解析。
- **`await`**：它使得代码在执行时“等待”一个 `Promise` 的完成，而不是阻塞整个程序。`await` 后面必须跟一个 `Promise`，它会暂停当前函数的执行，直到 `Promise` 完成，然后返回其结果。

**示例：等待异步操作**

```javascript
async function fetchData() {
  const data = await new Promise((resolve) => {
    setTimeout(() => resolve("从服务器获取的数据"), 2000);
  });
  console.log(data);  // 输出：从服务器获取的数据
}

fetchData();
```

**处理错误**

在 `async/await` 中，错误处理使用 `try/catch` 语法来捕获和处理异常，就像同步代码一样。

```javascript
async function fetchData() {
  try {
    const data = await new Promise((resolve, reject) => {
      setTimeout(() => reject("获取数据失败"), 2000);
    });
    console.log(data); 
  } catch (error) {
    console.log("错误：", error);  // 输出：错误： 获取数据失败
  }
}

fetchData();
```

**多个异步操作**

如果有多个异步操作，`await` 会按顺序一个个等待每个异步操作完成，但如果这些异步操作可以并发执行，我们可以使用 `Promise.all()` 来提高效率。

```javascript
async function fetchData() {
  const promise1 = new Promise((resolve) => setTimeout(() => resolve("数据 1"), 1000));
  const promise2 = new Promise((resolve) => setTimeout(() => resolve("数据 2"), 2000));

  // 按顺序执行
  const result1 = await promise1;
  const result2 = await promise2;
  console.log(result1, result2);  // 输出：数据 1 数据 2
}

fetchData();
```

如果不需要按顺序执行这些异步操作，可以同时执行它们，再使用 `await` 等待所有操作完成。

```javascript
async function fetchData() {
  const promise1 = new Promise((resolve) => setTimeout(() => resolve("数据 1"), 1000));
  const promise2 = new Promise((resolve) => setTimeout(() => resolve("数据 2"), 2000));

  const [result1, result2] = await Promise.all([promise1, promise2]);
  console.log(result1, result2);  // 输出：数据 1 数据 2
}

fetchData();
```

**总结**

- **`async`**：声明一个异步函数，它总是返回一个 `Promise`。
- **`await`**：暂停异步函数的执行，等待 `Promise` 解决后再继续执行。
- `async/await` 使得异步代码的编写像同步代码一样清晰和简洁，避免了回调函数的嵌套，并且让错误处理更加直观。





### Proxy

在 JavaScript 中，`Proxy` 是一个非常强大的工具，它允许你定义自定义的行为来拦截和修改对对象的基本操作，比如属性访问、赋值、函数调用等。

#### 1. Proxy 的基本概念

`Proxy` 是一种用于创建对象代理的机制，允许你拦截和定义对象的基本操作，如属性读取、写入、函数调用等。这对于调试、日志记录、性能监控、数据绑定等场景非常有用。

#### 2. Proxy 的构造函数

`Proxy` 是通过构造函数创建的，接受两个参数：

- **目标对象（target）**：要被代理的对象。
- **处理程序（handler）**：定义如何拦截对象操作的对象。

#### 语法：

```javascript
let proxy = new Proxy(target, handler);
```

- **target**：原始对象。
- **handler**：一个对象，它包含拦截方法，定义了如何处理对 `target` 的操作。

#### 3. 常用的拦截操作

`Proxy` 的 `handler` 对象可以包含多个方法，每个方法对应一种对象操作的拦截。这些方法被称为“陷阱”（traps）。以下是一些常见的陷阱方法：

- **get**：拦截对象的属性读取。
- **set**：拦截对象的属性赋值。
- **has**：拦截 `in` 操作符。
- **deleteProperty**：拦截 `delete` 操作符。
- **apply**：拦截函数调用。
- **construct**：拦截构造函数的调用。

#### 4. 示例代码

##### 1. 基本使用示例

```javascript
const target = {
  message: "Hello, Proxy!"
};

const handler = {
  get: function(target, prop, receiver) {
    if (prop in target) {
      return `Property ${prop} is: ${target[prop]}`;
    } else {
      return `Property ${prop} does not exist`;
    }
  }
};

const proxy = new Proxy(target, handler);

console.log(proxy.message); // "Property message is: Hello, Proxy!"
console.log(proxy.nonExistent); // "Property nonExistent does not exist"
```

在这个例子中，`handler.get` 方法定义了如何处理属性的读取。它检查目标对象是否有该属性，如果有则返回相应的值，如果没有则返回自定义的消息。

##### 2. 拦截 `set` 操作

```javascript
const target = { name: 'John' };

const handler = {
  set: function(target, prop, value) {
    console.log(`Setting ${prop} to ${value}`);
    target[prop] = value;  // 必须执行操作，确保属性被正确赋值
  }
};

const proxy = new Proxy(target, handler);
proxy.name = 'Alice'; // 输出: "Setting name to Alice"
console.log(target.name); // "Alice"
```

在这个例子中，`set` 方法在每次给属性赋值时被调用。

##### 3. 拦截 `delete` 操作

```javascript
const target = { name: 'John', age: 30 };

const handler = {
  deleteProperty: function(target, prop) {
    if (prop in target) {
      console.log(`Deleting property: ${prop}`);
      delete target[prop];
      return true; // 表示操作成功
    } else {
      console.log(`Property ${prop} does not exist`);
      return false; // 表示操作失败
    }
  }
};

const proxy = new Proxy(target, handler);
delete proxy.name; // 输出: "Deleting property: name"
console.log(target); // { age: 30 }
```

这里，`deleteProperty` 用于拦截 `delete` 操作，确保我们能够在删除属性时做一些额外的操作。

#### 5. 应用场景

- **数据验证**：通过 `set` 陷阱，可以在属性赋值时进行验证，确保数据的正确性。
- **属性访问监控**：通过 `get` 陷阱，可以监控对象的属性访问，记录日志或进行性能分析。
- **虚拟属性**：通过拦截访问不存在的属性，`Proxy` 可以实现虚拟属性或动态计算属性。

#### 6. 总结

`Proxy` 是一个非常灵活且强大的工具，允许你以非常细粒度的方式控制对对象的操作。它使得 JavaScript 对象的行为可以变得更加灵活、可定制，非常适用于各种高级的编程任务。



### Module

#### 1. CommonJS

CommonJS 是 Node.js 最早采用的模块系统，它在服务器端 JavaScript 中广泛使用。CommonJS 模块的主要特点是同步加载，它适用于服务器端环境。

CommonJS 的基本语法：

- **导出模块**：使用 `module.exports` 或 `exports` 来导出模块。
- **导入模块**：使用 `require()` 来导入模块。

示例：

```javascript
// 导出模块 (myModule.js)
module.exports = {
    id: 1
};
module.exports = function greeting(name) {
  return `Hello, ${name}!`;
};

exports.a = 1
exports.b = 2

// 导入模块 (index.js)
const moduleName = require('./myModule');
console.log(myModule.greet('World')); // 输出: Hello, World!
```

特点：

- **同步加载**：`require()` 是同步的，这意味着模块会在程序运行时阻塞直到被完全加载。
- **每个模块只有一个缓存实例**：模块一旦被加载，后续的 `require` 会直接返回之前加载的缓存，避免重复加载。
- **在 Node.js 中普遍使用**：CommonJS 是 Node.js 默认的模块系统，因此许多 Node.js 应用程序和库都采用 CommonJS。

------

#### 2. ESM (ECMAScript Modules)

ESM 是现代 JavaScript 模块化的标准，逐步被现代浏览器和 Node.js 所支持。ESM 是基于浏览器原生的模块化支持，并且使用了静态分析的方式进行模块加载，因此它的性能在某些场景下优于 CommonJS。

ESM 的基本语法：

- **导出模块**：使用 `export` 关键字导出模块。
- **导入模块**：使用 `import` 关键字导入模块。

示例：

```javascript
// 引入module的文件，type="module"
// 即：<script src="index.js" type="module"></script>

// 导出模块 (myModule.js)
export default {
    id: 1
}
export const name = "Peter";
export function greeting(name) {
  return `Hello, ${name}!`;
}

// 导入模块 (index.js)
import moduleName from './myModule.js';
import { name, greeting as greet } from './myModule.js';
console.log(moduleName); // 输出: {id: 1;}
console.log(name); // 输出: Peter
console.log(greet(name)); // 输出: Hello, Peter!
```

特点：

- **异步加载**：`import` 是异步加载的，它支持浏览器中的延迟加载，并且可以在运行时动态加载模块。
- **静态分析**：ESM 通过静态分析文件的导入和导出，允许浏览器和打包工具（如 Webpack）进行优化，如树摇（tree shaking）。
- **支持顶级 `await`**：在 ESM 中，可以直接在模块的顶层使用 `await`，而 CommonJS 不支持。
- **默认导入和命名导入**：ESM 支持命名导入和默认导入，这在模块化设计中非常灵活。

------

#### 3. **CommonJS vs ESM 比较**

| 特性                  | CommonJS                               | ESM (ECMAScript Modules)                |
| --------------------- | -------------------------------------- | --------------------------------------- |
| **导出语法**          | `module.exports` / `exports`           | `export` / `export default`             |
| **导入语法**          | `require()`                            | `import`                                |
| **加载方式**          | 同步加载（服务器端）                   | 异步加载（支持浏览器端）                |
| **模块缓存**          | 加载一次后会缓存，后续引用直接返回缓存 | 也是缓存，但每次都会进行静态分析        |
| **兼容性**            | 主要用于 Node.js，浏览器不支持         | 现代浏览器和 Node.js 都支持（ES6 标准） |
| **静态分析**          | 不支持，不能进行树摇优化               | 支持，可以进行树摇优化                  |
| **顶级 `await` 支持** | 不支持                                 | 支持                                    |
| **使用场景**          | 主要用于 Node.js                       | 适用于浏览器和 Node.js，支持前后端统一  |















# 2.文档对象模型（DOM）

## 2.1.DOM树

```js
Document
 └── html
      ├── head
      │    └── title
      │         └── "My Page"
      └── body
           ├── h1
           │    └── "Welcome to My Page"
           └── p
                └── "This is a paragraph."

```

## 2.2.DOM元素



### 查找 HTML 元素

| 方法                                       | 描述                                |
| :----------------------------------------- | :---------------------------------- |
| **element.getElementById(*id*)**           | 通过元素 id 来查找元素              |
| **element.getElementsByTagName(*name*)**   | 通过标签名来查找元素                |
| **element.getElementsByClassName(*name*)** | 通过类名来查找元素                  |
| element.querySelector(name)                | 通过 CSS 选择器查找元素**(第一个)** |
| **element.querySelectorAll(name)**         | 通过 CSS 选择器查找元素**(所有)**   |

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .intro {
            color: red;
            font-size: 20px;
        }
    </style>
</head>
    
<body>
	<h1>example</h1>
    <!-- 3.4. -->
	<p class="intro"></p>
    <!-- 1. -->
	<div id="main">
		<p>DOM 很有用</p>
		<p>本例演示<b>查找 HTML 元素</b>方法</p>
	</div>

	<p id="demo"></p>
    
    <!-- 5. -->
    <form id="frm1" action="/demo/demo_form.asp">
  	First name: <input type="text" name="fname" value="Bill"><br>
  	Last name: <input type="text" name="lname" value="Gates"><br><br>
  	<input type="submit" value="提交">
	</form> 

	<p>单击“试一试”按钮，显示表单中每个元素的值。</p>

	<button onclick="myFunction()">试一试</button>
</body>
</html>
```

```js
// 1.通过 id 查找 HTML 元素
const x = document.getElementById("main");

// 2.通过标签名查找 HTML 元素。
const y = x.getElementsByTagName("p");

// 3.通过类名查找 HTML 元素
const i = document.getElementsByClassName("intro");

// 4.通过 CSS 选择器查找 HTML 元素
var x = document.querySelectorAll(".intro");

// 5.通过 HTML 对象选择器查找 HTML 对象
function myFunction() {
  var x = document.forms["frm1"];
  var text = "";
  var i;
  for (i = 0; i < x.length ;i++) {
    text += x.elements[i].value + "<br>";
  }
  document.getElementById("demo").innerHTML = text;
}
/*
以下 HTML 对象（和对象集合）也是可访问的：
document.anchors
document.body
document.documentElement
document.embeds
document.forms
document.head
document.images
document.links
document.scripts
document.title
*/
```



### 改变 HTML 元素

| 方法                                       | 描述                                  |
| :----------------------------------------- | :------------------------------------ |
| **element.innerHTML = *new html content*** | 改变元素的 inner HTML                 |
| element.innerTEXT = *new html text conent* | 改变元素的 inner TEXT**(不解析标签)** |
| **element.attribute = *new value***        | 改变 HTML 元素的属性值                |
| element.setAttribute(*attribute*, *value*) | 改变 HTML 元素的属性值                |
| **element.style.property = *new style***   | 改变 HTML 元素的样式                  |

```html
<!DOCTYPE html>
<html>
<body>
<!-- 1. -->
<h1 id="title">旧标题</h1>
<!-- 2. -->
<img id="myImage" src="smiley.gif">
<!-- 3. -->
<p id='myText'>Hello World!</p>
</body>
</html>
```

```js
// 1.改变 HTML 内容
let element = document.getElementById("title"); // 获取
element.innerHTML = "<i>新标题</i>";  // 改变

// 2.改变属性的值
document.getElementById("myImage").src = "landscape.jpg";
document.getElementById("myImage").setAttribute('src', 'landscape.jpg');

// 3.改变 HTML 元素的样式
document.getElementById("myText").style.color = 'red';
```





### 添加和删除元素

| 方法                                 | 描述             |
| :----------------------------------- | :--------------- |
| **element.createElement(*element*)** | 创建 HTML 元素   |
| **element.appendChild(*element*)**   | 添加 HTML 元素   |
| **element.insertBefore(*element*)**  | 插入 HTML 元素   |
| **element.removeChild(*element*)**   | 删除 HTML 元素   |
| **element.replaceChild(*element*)**  | 替换 HTML 元素   |
| **element.write(*text*)**            | 写入 HTML 输出流 |



### Document 对象属性

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [document.activeElement](https://www.runoob.com/jsref/prop-document-activeelement.html) | 返回当前获取焦点元素                                         |
| [document.anchors](https://www.runoob.com/jsref/coll-doc-anchors.html) | 返回对文档中所有 Anchor 对象的引用。                         |
| document.applets                                             | 返回对文档中所有 Applet 对象的引用。**注意:** HTML5 已不支持 <applet> 元素。 |
| [document.baseURI](https://www.runoob.com/jsref/prop-doc-baseuri.html) | 返回文档的绝对基础 URI                                       |
| [document.body](https://www.runoob.com/jsref/prop-doc-body.html) | 返回文档的body元素                                           |
| [document.cookie](https://www.runoob.com/jsref/prop-doc-cookie.html) | 设置或返回与当前文档有关的所有 cookie。                      |
| [document.doctype](https://www.runoob.com/jsref/prop-document-doctype.html) | 返回与文档相关的文档类型声明 (DTD)。                         |
| [document.documentElement](https://www.runoob.com/jsref/prop-document-documentelement.html) | 返回文档的根节点                                             |
| [document.documentMode](https://www.runoob.com/jsref/prop-doc-documentmode.html) | 返回用于通过浏览器渲染文档的模式                             |
| [document.documentURI](https://www.runoob.com/jsref/prop-document-documenturi.html) | 设置或返回文档的位置                                         |
| [document.domain](https://www.runoob.com/jsref/prop-doc-domain.html) | 返回当前文档的域名。                                         |
| document.domConfig                                           | **已废弃**。返回 normalizeDocument() 被调用时所使用的配置。  |
| [document.embeds](https://www.runoob.com/jsref/coll-doc-embeds.html) | 返回文档中所有嵌入的内容（embed）集合                        |
| [document.forms](https://www.runoob.com/jsref/coll-doc-forms.html) | 返回对文档中所有 Form 对象引用。                             |
| [document.images](https://www.runoob.com/jsref/coll-doc-images.html) | 返回对文档中所有 Image 对象引用。                            |
| [document.implementation](https://www.runoob.com/jsref/prop-document-implementation.html) | 返回处理该文档的 DOMImplementation 对象。                    |
| [document.inputEncoding](https://www.runoob.com/jsref/prop-document-inputencoding.html) | 返回用于文档的编码方式（在解析时）。                         |
| [document.lastModified](https://www.runoob.com/jsref/prop-doc-lastmodified.html) | 返回文档被最后修改的日期和时间。                             |
| [document.links](https://www.runoob.com/jsref/coll-doc-links.html) | 返回对文档中所有 Area 和 Link 对象引用。                     |
| [document.readyState](https://www.runoob.com/jsref/prop-doc-readystate.html) | 返回文档状态 (载入中……)                                      |
| [document.referrer](https://www.runoob.com/jsref/prop-doc-referrer.html) | 返回载入当前文档的文档的 URL。                               |
| [document.scripts](https://www.runoob.com/jsref/coll-doc-scripts.html) | 返回页面中所有脚本的集合。                                   |
| [document.strictErrorChecking](https://www.runoob.com/jsref/prop-document-stricterrorchecking.html) | 设置或返回是否强制进行错误检查。                             |
| [document.title](https://www.runoob.com/jsref/prop-doc-title.html) | 返回当前文档的标题。                                         |
| [document.URL](https://www.runoob.com/jsref/prop-doc-url.html) | 返回文档完整的URL                                            |





### Element 对象属性

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [*element*.accessKey](https://www.runoob.com/jsref/prop-html-accesskey.html) | 设置或返回accesskey一个元素                                  |
| [*element*.attributes](https://www.runoob.com/jsref/prop-node-attributes.html) | 返回一个元素的属性数组                                       |
| [***element*.classList**](https://www.runoob.com/jsref/prop-element-classList.html) | 返回元素的类名，作为 DOMTokenList 对象。                     |
| [*element*.className](https://www.runoob.com/jsref/prop-html-classname.html) | 设置或返回元素的class属性                                    |
| [*element*.clientTop](https://www.runoob.com/jsref/prop-element-clienttop.html) | 表示一个元素的顶部边框的宽度，以像素表示。                   |
| [*element*.clientLeft](https://www.runoob.com/jsref/prop-element-clientleft.html) | 表示一个元素的左边框的宽度，以像素表示。                     |
| [*element*.clientHeight](https://www.runoob.com/jsref/prop-element-clientheight.html) | 在页面上返回内容的可视高度（高度包含内边距（padding），不包含边框（border），外边距（margin）和滚动条） |
| [*element*.clientWidth](https://www.runoob.com/jsref/prop-element-clientwidth.html) | 在页面上返回内容的可视宽度（宽度包含内边距（padding），不包含边框（border），外边距（margin）和滚动条） |
| [*element*.contentEditable](https://www.runoob.com/jsref/prop-html-contenteditable.html) | 设置或返回元素的内容是否可编辑                               |
| [*element*.dir](https://www.runoob.com/jsref/prop-html-dir.html) | 设置或返回一个元素中的文本方向                               |
| [*element*.id](https://www.runoob.com/jsref/prop-html-id.html) | 设置或者返回元素的 id。                                      |
| [*element*.isContentEditable](https://www.runoob.com/jsref/prop-html-iscontenteditable.html) | 如果元素内容可编辑返回 true，否则返回false                   |
| [*element*.lang](https://www.runoob.com/jsref/prop-html-lang.html) | 设置或者返回一个元素的语言。                                 |
| [*element*.namespaceURI](https://www.runoob.com/jsref/prop-node-namespaceuri.html) | 返回命名空间的 URI。                                         |
| [*element*.nextElementSibling](https://www.runoob.com/jsref/prop-element-nextelementsibling.html) | 返回指定元素之后的下一个兄弟元素（相同节点树层中的下一个元素节点）。 |
| [*element*.nodeName](https://www.runoob.com/jsref/prop-node-nodename.html) | 返回元素的标记名（大写）                                     |
| [*element*.nodeType](https://www.runoob.com/jsref/prop-node-nodetype.html) | 返回元素的节点类型                                           |
| [*element*.nodeValue](https://www.runoob.com/jsref/prop-node-nodevalue.html) | 返回元素的节点值                                             |
| [*element*.offsetHeight](https://www.runoob.com/jsref/prop-element-offsetheight.html) | 返回任何一个元素的高度包括边框（border）和内边距（padding），但不包含外边距（margin） |
| [*element*.offsetWidth](https://www.runoob.com/jsref/prop-element-offsetwidth.html) | 返回元素的宽度，包括边框（border）和内边距（padding），但不包含外边距（margin） |
| [*element*.offsetLeft](https://www.runoob.com/jsref/prop-element-offsetleft.html) | 返回当前元素的相对水平偏移位置的偏移容器                     |
| [*element*.offsetParent](https://www.runoob.com/jsref/prop-element-offsetparent.html) | 返回元素的偏移容器                                           |
| [*element*.offsetTop](https://www.runoob.com/jsref/prop-element-offsettop.html) | 返回当前元素的相对垂直偏移位置的偏移容器                     |
| [*element*.ownerDocument](https://www.runoob.com/jsref/prop-node-ownerdocument.html) | 返回元素的根元素（文档对象）                                 |
| [*element*.previousElementSibling](https://www.runoob.com/jsref/prop-element-previouselementsibling.html) | 返回指定元素的前一个兄弟元素（相同节点树层中的前一个元素节点）。 |
| [*element*.scrollHeight](https://www.runoob.com/jsref/prop-element-scrollheight.html) | 返回整个元素的高度（包括带滚动条的隐蔽的地方）               |
| [*element*.scrollLeft](https://www.runoob.com/jsref/prop-element-scrollleft.html) | 返回当前视图中的实际元素的左边缘和左边缘之间的距离           |
| [***element*.scrollTop**](https://www.runoob.com/jsref/prop-element-scrolltop.html) | 返回当前视图中的实际元素的顶部边缘和顶部边缘之间的距离       |
| [*element*.scrollWidth](https://www.runoob.com/jsref/prop-element-scrollwidth.html) | 返回元素的整个宽度（包括带滚动条的隐蔽的地方）               |
| [***element*.style**](https://www.runoob.com/jsref/prop-element-style.html) | 设置或返回元素的样式属性                                     |
| [*element*.tabIndex](https://www.runoob.com/jsref/prop-html-tabindex.html) | 设置或返回元素的标签顺序。                                   |
| [*element*.tagName](https://www.runoob.com/jsref/prop-element-tagname.html) | 作为一个字符串返回某个元素的标记名（大写）                   |
| [*element*.textContent](https://www.runoob.com/jsref/prop-node-textcontent.html) | 设置或返回一个节点和它的文本内容                             |
| [*element*.title](https://www.runoob.com/jsref/prop-html-title.html) | 设置或返回元素的title属性                                    |
| [*nodelist*.length](https://www.runoob.com/jsref/prop-nodelist-length.html) | 返回节点列表的节点数目。                                     |





## 2.3.DOM事件

### 事件

| 事件                  | 描述                                                       |
| --------------------- | ---------------------------------------------------------- |
| **鼠标事件**          |                                                            |
| onclick               | 点击鼠标时触发此事件                                       |
| ondblclick            | 双击鼠标时触发此事件                                       |
| onmousedown           | 按下鼠标时触发此事件                                       |
| onmouseup             | 鼠标按下后又松开时触发此事件                               |
| onmouseover           | 当鼠标移动到某个元素上方时触发此事件                       |
| onmousemove           | 移动鼠标时触发此事件                                       |
| on**mouseenter**      | 当鼠标进入某个元素范围时触发此事件                         |
| on**mouseleave**      | 当鼠标离开某个元素范围时触发此事件                         |
| **键盘事件**          |                                                            |
| onkeypress            | 当按下并松开键盘上的某个键时触发此事件                     |
| onkeydown             | 当按下键盘上的某个按键时触发此事件                         |
| on**keyup**           | 当放开键盘上的某个按键时触发此事件                         |
| **页面/文件加载事件** |                                                            |
| onabort               | 图片在下载过程中被用户中断时触发此事件                     |
| onbeforeunload        | 当前页面的内容将要被改变时触发此事件                       |
| onerror               | 出现错误时触发此事件                                       |
| onload                | 页面内容加载完成时触发此事件                               |
| onunload              | 改变当前页面时触发此事件                                   |
| **浏览器/窗口事件**   |                                                            |
| onmove                | 当移动浏览器的窗口时触发此事件                             |
| onresize              | 当改变浏览器的窗口大小时触发此事件                         |
| onscroll              | 当滚动浏览器的滚动条时触发此事件                           |
| onstop                | 当按下浏览器的停止按钮或者正在下载的文件被中断时触发此事件 |
| oncontextmenu         | 当弹出右键上下文菜单时触发此事件                           |
| **表单事件**          |                                                            |
| on**blur**            | 当前元素失去焦点时触发此事件                               |
| onchange              | 当前元素失去焦点并且元素的内容发生改变时触发此事件         |
| on**focus**           | 当某个元素获得焦点时触发此事件                             |
| onreset               | 当点击表单中的重置按钮时触发此事件                         |
| onsubmit              | 当提交表单时触发此事件                                     |

### 事件监听程序

**1.添加事件监听器**

`addEventListener` 方法允许你为指定的元素绑定事件监听程序，它的基本语法如下：

```js
element.addEventListener(event, handler, options);
```

- `event`：事件类型（字符串），如 `'click'`、`'keydown'`、`'submit'` 等。

  **注意：**请勿对事件使用 **"on" 前缀**；请使用 "click" 代替 "onclick"。

- `handler`：事件发生时调用的回调函数，事件对象会作为参数传入该函数。
- `options`：可选参数，允许你指定额外的选项，通常包括：
  - `capture`（布尔值）：指定事件是在哪个阶段触发（捕获阶段或冒泡阶段）。默认是 `false`，即冒泡阶段。如果为 `true`，则在捕获阶段触发。
  - `once`（布尔值）：如果为 `true`，事件监听程序会在触发一次之后自动移除。 **`{ once: true }`**
  - `passive`（布尔值）：如果为 `true`，表示事件处理程序不会调用 `preventDefault()`，提高性能。**` { passive: true }`**



**事件对象**

事件对象（`event`）包含了与事件相关的所有信息。你可以通过该对象访问关于事件的详细信息，比如：

- `event.type`：事件的类型（如 `'click'`、`'keydown'`）。
- `event.target`：触发事件的元素。
- `event.clientX` 和 `event.clientY`：鼠标事件中，鼠标指针相对于视口的位置。
- `event.key`：键盘事件中，按下的键的值。

```js
<input type="text" id="myInput" placeholder="输入一些文字">

<script>
  const input = document.getElementById('myInput');

  // 监听键盘按键事件
  // 在这个例子中，keydown 事件会在用户按下任何键时触发，事件对象 event 会包含有关按下的键的信息。
  input.addEventListener('keydown', function(event) {
    console.log('按下了键：', event.key);
  });
</script>

```



**事件捕获与冒泡**

在浏览器中，事件会按层级结构传播。事件传播有两种模式：**捕获阶段**和**冒泡阶段**。

- **捕获阶段**：事件从文档根节点开始，逐层向下传播到事件目标。
- **冒泡阶段**：事件从事件目标开始，逐层向上传播到文档根节点。

```js
element.addEventListener('click', function(event) {
  console.log('捕获阶段触发');
}, true); // 捕获阶段

element.addEventListener('click', function(event) {
  console.log('冒泡阶段触发');
}, false); // 冒泡阶段（默认）

```



**2.移除事件监听器**

```
element.removeEventListener(event, handler, options);
```

示例

```html
<!DOCTYPE html>
<html>
<head>
<style>
#myDIV {
  background-color: coral;
  border: 1px solid;
  padding: 50px;
  color: white;
  font-size: 20px;
}
</style>
</head>
<body>

<h1>JavaScript removeEventListener()</h1>

<div id="myDIV">
  <p>这个 div 元素有一个 onmousemove 事件处理程序，每次在这个橙色字段中移动鼠标时都会显示一个随机数。</p>
  <p>单击按钮以删除 div 的事件处理程序。</p>
  <button onclick="removeHandler()" id="myBtn">删除</button>
</div>

<p id="demo"></p>

<script>
document.getElementById("myDIV").addEventListener("mousemove", myFunction);

function myFunction() {
  document.getElementById("demo").innerHTML = Math.random();
}

function removeHandler() {
  document.getElementById("myDIV").removeEventListener("mousemove", myFunction);
}
</script>

</body>
</html>

```



## 2.4.DOM节点

![image-20241106113429440](images/image-20241106113429440.png)

**主要操作的是元素节点**

### 节点导航

使用以下节点属性在节点之间导航：

- **parentNode**
- **childNodes[*nodenumber*]**
- **children**
- **firstChild**
- **lastChild**
- **nextSibling**
- **previousSibling**



**nodeName**

`nodeName` 属性规定节点的名称。

- nodeName 是只读的
- 元素节点的 nodeName 等同于标签名
- 属性节点的 nodeName 是属性名称
- 文本节点的 nodeName 总是 #text
- 文档节点的 nodeName 总是 #document

```html
<h1 id="id01">我的第一张网页</h1>
<p id="id02">Hello!</p>

<script>
document.getElementById("id02").innerHTML = document.getElementById("id01").nodeName;
</script>
```



**nodeValue** 

`nodeValue` 属性规定节点的值。

- 元素节点的 nodeValue 是 undefined
- 文本节点的 nodeValue 是文本文本
- 属性节点的 nodeValue 是属性值

```html
<h1 id="id01">我的第一张页面</h1>
<p id="id02">Hello!</p>

<script>
document.getElementById("id02").innerHTML = document.getElementById("id01").firstChild.nodeValue;
</script>
```



**nodeType** 

`nodeType` 属性返回节点的类型。`nodeType` 是只读的。

```html
<h1 id="id01">我的第一张网页</h1>
<p id="id02">Hello!</p>

<script>
document.getElementById("id02").innerHTML  = document.getElementById("id01").nodeType;
</script>
```

| 节点               | 类型 | 例子                              |
| :----------------- | :--- | :-------------------------------- |
| ELEMENT_NODE       | 1    | <h1 class="heading">W3School</h1> |
| ATTRIBUTE_NODE     | 2    | class = "heading" （弃用）        |
| TEXT_NODE          | 3    | W3School                          |
| COMMENT_NODE       | 8    | <!-- 这是注释 -->                 |
| DOCUMENT_NODE      | 9    | HTML 文档本身（<html> 的父）      |
| DOCUMENT_TYPE_NODE | 10   | <!Doctype html>                   |



### 节点操作

**创建新 HTML 元素（节点）**

appendChild()

createElement()

creatTextNode()

parentNode.**insertBefore**(newNode, referenceNode);

**删除已有 HTML 元素**

remove()

removeChild()

**替换 HTML 元素**

replaceChild()

**克隆 HTML 元素**

cloneNode()

### 节点列表

1. **定义**

- **`NodeList`**：是一个类数组对象，表示一组 DOM 节点。它可以包含任何类型的节点，如元素节点、文本节点、注释节点等。
- **`HTMLCollection`**：是一个专门的类数组对象，表示一组 **HTML 元素节点**（即 `Element` 节点），它只包含 DOM 树中的元素节点。

2. **包含的内容**

- **`NodeList`**：可以包含任何类型的节点（包括元素节点、文本节点、注释节点等）。

  - 例如，通过 `document.querySelectorAll()` 获取的返回值就是一个 `NodeList`，它可以包含各种类型的节点。

  ```javascript
  const nodes = document.querySelectorAll('*');  // NodeList 包含所有节点，包括元素、文本等
  ```

- **`HTMLCollection`**：只包含 **元素节点**，即 DOM 中的 `<div>`, `<span>`, `<p>` 等 HTML 标签。

  - 例如，`document.getElementsByTagName()` 或 `document.getElementsByClassName()` 返回的就是 `HTMLCollection`。

  ```javascript
  const elements = document.getElementsByTagName('div');  // HTMLCollection 只包含 <div> 元素
  ```

3. **实时性（Live vs Non-Live）**

- **`HTMLCollection`**：通常是 **实时的（live）**，这意味着当 DOM 中的元素发生变化时，`HTMLCollection` 会自动更新。例如，如果你向 DOM 中添加或删除元素，`HTMLCollection` 会反映这些变化。

  ```javascript
  let divs = document.getElementsByTagName('div');
  console.log(divs.length);  // 初始 div 的数量
  // 假设动态添加或删除了 div 元素
  divs = document.getElementsByTagName('div');
  console.log(divs.length);  // div 的数量会自动更新
  ```

- **`NodeList`**：取决于方法的不同，可以是实时的，也可以是非实时的（静态的）。

  - 例如，`document.querySelectorAll()` 返回的是 **非实时的（static）** `NodeList`，它不会随着 DOM 的变化而自动更新。
  - 但某些方法返回的 `NodeList`（例如 `childNodes`）是 **实时的**。

  ```javascript
  const nodes = document.querySelectorAll('div');  // 返回非实时 NodeList
  console.log(nodes.length);  // 初始数量
  // 添加/删除 div 后，nodes 不会自动更新
  ```

4. **访问方式**

- **`NodeList` 和 `HTMLCollection`** 都是类数组对象，意味着它们都可以通过索引访问单个元素（如 `nodeList[0]`）。

  - **`NodeList`**：

    ```javascript
    let node = document.querySelectorAll('div');
    console.log(node[0]);  // 获取第一个 <div>
    ```

  - **`HTMLCollection`**：

    ```javascript
    let divs = document.getElementsByTagName('div');
    console.log(divs[0]);  // 获取第一个 <div>
    ```

- **`NodeList`**：通常支持 `forEach()` 方法来遍历所有节点，但并不是所有 `NodeList` 对象都支持。

  **语法**：
  
  ```javascript
  array.forEach(function(element, index, array) {
    // 执行操作
  });
  
  array.forEach((element, index, array) => {
    // 执行操作
  });
  ```
  
  **参数说明**：
  
  - `element`：当前遍历的元素。
  - `index`：当前元素的索引（可选）。
  - `array`：原始数组（可选）。
  
  **示例**：
  
  ```javascript
  const nodes = document.querySelectorAll('div');
  nodes.forEach(node => console.log(node));  // 可以直接使用 forEach() 遍历
  ```
  
  **注意**：`HTMLCollection` 不支持 `forEach()` 方法（在早期的浏览器中），但现代浏览器（如 Chrome 和 Firefox）现在支持 `forEach()`。
  
  ```javascript
  const divs = document.getElementsByTagName('div');
  Array.from(divs).forEach(div => console.log(div));  // 通过转换为数组使用 forEach()
  ```
  
  

5. **常见方法**

- **`NodeList`** 通常由 `document.querySelectorAll()` 或 `parentNode.childNodes` 等方法返回。
- **`HTMLCollection`** 通常由 `document.getElementsByTagName()`, `document.getElementsByClassName()` 或 `parentNode.getElementsByTagName()` 等方法返回。

| **特性**           | **NodeList**                                                 | **HTMLCollection**                                           |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **包含的内容**     | 可以是任何类型的节点（元素、文本、注释等）。                 | 只包含 HTML 元素节点。                                       |
| **实时性**         | 可以是实时的（如 `childNodes`），也可以是非实时的（如 `querySelectorAll()`）。 | 是实时的（即会随着 DOM 的变化而更新）。                      |
| **支持的遍历方法** | 支持 `forEach()` 遍历（大部分浏览器）。                      | 只支持通过索引访问元素，不支持 `forEach()`，但可以转为数组遍历。 |
| **返回的方式**     | 由 `document.querySelectorAll()`, `parentNode.childNodes` 等返回。 | 由 `document.getElementsByTagName()`, `document.getElementsByClassName()` ，`parentNode.getElementsByTagName()`等返回。 |





# 3.浏览器对象模型（BOM）

**BOM**（Browser Object Model，浏览器对象模型）是浏览器中用于表示和管理浏览器窗口及其相关功能的一组对象和接口。通过 BOM，开发者可以与浏览器的窗口、历史记录、位置、屏幕等进行交互，以实现动态网页和更复杂的用户体验。

BOM 并没有像 DOM（文档对象模型）那样的标准结构，而是由不同的浏览器提供一些方法和属性来实现特定功能。因此，BOM 实际上是一个集合，它的功能主要用于浏览器环境下操作窗口、导航、控制浏览器行为等。

## window

- window.innerHeight - 浏览器窗口的内高度（以像素计）
- window.innerWidth - 浏览器窗口的内宽度（以像素计）
- window.open() - 打开新窗口
- window.close() - 关闭当前窗口
- window.moveTo(x, y) -移动当前窗口
- window.resizeTo(w, h) -重新调整当前窗口
- window.scrollTo(x, y) - 滚动窗口到指定的位置。
- window.moveBy(x, y) -将浏览器窗口相对于当前的位置移动指定的距离。
- window.resizeBy(w, h) -根据给定的宽度和高度，调整浏览器窗口的大小。
- window.scrollBy(x, y) - 在当前页面位置基础上滚动指定的距离。

## screen

**window.screen 对象包含用户屏幕的信息。**

- screen.width - 属性返回以像素计的访问者屏幕宽度。
- screen.height - 属性返回以像素计的访问者屏幕的高度。
- screen.availWidth - 属性返回访问者屏幕的宽度，以像素计，减去诸如窗口工具条之类的界面特征。
- screen.availHeight - 属性返回访问者屏幕的高度，以像素计，减去诸如窗口工具条之类的界面特征。
- screen.colorDepth - 属性返回用于显示一种颜色的比特数。
- screen.pixelDepth - 属性返回屏幕的像素深度。

## location

**window.location 对象可用于获取当前页面地址（URL）并把浏览器重定向到新页面。**

- location.href - 返回当前页面的 href (URL)
- location.hostname - 返回 web 主机的域名
- location.pathname - 返回当前页面的路径或文件名
- location.protocol - 返回使用的 web 协议（http: 或 https:）
- location.assign - 加载新文档



## history

**window.history 对象包含浏览器历史。**为了保护用户的隐私，JavaScript 访问此对象存在限制。

- history.back() - 等同于在浏览器点击后退按钮
- history.forward() - 等同于在浏览器中点击前进按钮

## navigator

**window.navigator 对象包含有关访问者的信息。**

- navigator.appName
- navigator.appCodeName
- navigator.platform

## pop-up

**JavaScript 有三种类型的弹出框：警告框、确认框和提示框。**

- window.alert() - 用于显示一个简单的提示框，通常只包含一条消息和一个“确定”按钮。
- window.confirm() -  用于显示一个确认框，通常包含“确定”和“取消”两个按钮，返回 `true` 或 `false`。
- window.prompt() - 用于显示一个输入框，用户可以在框中输入内容，返回用户输入的值。如果用户点击取消，会返回 `null`。

## timing

`setTimeout(function, milliseconds)` 用于在指定的时间延迟后执行一次代码。

`setInterval(function, milliseconds)` 用于在指定的时间间隔内重复执行代码，直到手动清除。

`requestAnimationFrame()` 用于在浏览器重绘之前执行代码，通常用于动画效果，具有更好的性能。

`clearTimeout()` 和 `clearInterval()`用于清除已设置的 `setTimeout()` 或 `setInterval()`，避免重复执行。

示例

```js
myVar = setTimeout(function, milliseconds);
clearTimeout(myVar);
```



## cookies

**Cookie 让您在网页中存储用户信息。**

```js
function setCookie(cname, cvalue, exdays) {
    var d = new Date();
    d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
    var expires = "expires="+d.toUTCString();
    document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
}

function getCookie(cname) {
    var name = cname + "=";
    var ca = document.cookie.split(';');
    for(var i = 0; i < ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
         }
        if (c.indexOf(name)  == 0) {
            return c.substring(name.length, c.length);
         }
    }
    return "";
}

function checkCookie() {
    var user = getCookie("username");
    if (user != "") {
        alert("Welcome again " + user);
    } else {
        user = prompt("Please enter your name:", "");
        if (user != "" && user != null) {
            setCookie("username", user, 365);
        }
    }
}
```



# 4.jQuery库

**jQuery** 是一个快速、简洁的 JavaScript 库，旨在简化 HTML 文档遍历、事件处理、动画效果和 Ajax 操作等常见任务的处理。它使得网页开发变得更加简便，并且具有很好的跨浏览器兼容性。jQuery 是基于 JavaScript 语言的，提供了简化的语法，使得开发者无需编写复杂的 JavaScript 代码即可实现许多功能。

## 特点

1. **简化的 DOM 操作**：jQuery 提供了更简洁的语法来操作 HTML 元素，使得对 DOM（文档对象模型）的操作更方便。
2. **事件处理**：jQuery 可以简化事件的绑定和处理，如鼠标点击、悬停、表单提交等事件。
3. **动画效果**：jQuery 内置了许多动画效果（如淡入淡出、滑动、隐藏等），让开发者可以轻松实现网页交互效果。
4. **Ajax 操作**：通过 jQuery，可以快速实现异步数据请求（AJAX），而无需直接编写原生的 JavaScript。
5. **跨浏览器兼容性**：jQuery 自动处理浏览器之间的差异性，确保代码在不同浏览器中运行一致。

## 基本用法

1. **引入 jQuery**
    在网页中使用 jQuery，首先需要引入 jQuery 库。你可以从 jQuery 官网下载并引入本地文件，或者通过 CDN 引入。例如：

   ```html
   <!-- 引入 jQuery 库 -->
   <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
   ```

   如果你使用的是本地文件，文件路径可以是：

   ```html
   <script src="js/jquery.min.js"></script>
   ```

2. **基本选择器和操作**
    jQuery 的选择器语法与 CSS 类似，你可以使用它来选择页面元素并对其进行操作：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>jQuery 示例</title>
       <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
   </head>
   <body>
       <h1>Hello, jQuery!</h1>
       <button id="myButton">Click Me!</button>
   
       <script>
           // 当文档加载完成后，执行以下代码
           $(document).ready(function(){
               // 绑定点击事件
               $('#myButton').click(function(){
                   $('h1').text('Hello, World!'); // 修改 <h1> 标签的内容
               });
           });
       </script>
   </body>
   </html>
   ```

   这里使用了 `$(document).ready()` 来确保在文档加载完成后才执行代码。`$('#myButton')` 是通过 ID 选择器选择元素，`click()` 用于绑定点击事件。

3. **链式调用**
    jQuery 允许链式调用，即你可以将多个操作串联在一起，减少代码量：

   ```javascript
   $('#myButton').css('color', 'red').text('Click Me Again!').fadeOut(1000);
   ```

   上面的代码首先将按钮文本颜色改为红色，再更改按钮文本内容，最后使按钮淡出。

4. **常见的 jQuery 动画效果** jQuery 提供了几个内置的动画方法，例如：`fadeIn()`、`fadeOut()`、`slideUp()`、`slideDown()` 等。

   ```javascript
   // 淡入效果
   $('#myButton').fadeIn(1000);
   
   // 淡出效果
   $('#myButton').fadeOut(1000);
   
   // 滑动隐藏
   $('#myButton').slideUp(1000);
   ```

5. **Ajax 请求**
    jQuery 使得发送异步请求变得非常简单：

   ```javascript
   $.ajax({
       url: 'data.json',  // 请求的 URL
       method: 'GET',     // 请求方式
       success: function(data) {
           console.log(data);  // 请求成功后的回调函数
       },
       error: function(xhr, status, error) {
           console.error('请求失败:', error);
       }
   });
   ```

   你可以使用 `$.ajax()` 发送 GET 或 POST 请求，从服务器加载数据或提交数据。

## 常用方法

1. **选择器**：

   - `$('#id')`：通过 ID 选择元素

     ```js
     var myElement = $("#id01");
     var myElement = document.getElementById("id01");
     ```

   - `$('.class')`：通过类名选择元素

     ```js
     var myElements = $(".intro");
     var myElements = document.getElementsByClassName("intro");
     ```

   - `$('tag')`：通过标签名选择元素

     ```js
     var myElements = $("p");
     var myElements = document.getElementsByTagName("p");
     ```

   - `$('css selector')`：通过CSS选择器选择元素

     ```js
     var myElements = $("p.intro");
     var myElements = document.querySelectorAll("p.intro");
     ```

   - `$(this)`：当前选中的元素（通常在事件回调函数中使用）

     

     

2. **操作 DOM**：

   - `text()`：获取或设置元素的文本内容

     ```js
     var myText = myElement.text();
     var myText = myElement.textContent || myElement.innerText;
     
     var myElement.text("Hello China!");
     var myElement.textContent = "Hello China!";
     ```

   - `html()`：获取或设置元素的 HTML 内容

     ```js
     var content = myElement.html();
     var content = myElement.innerHTML;
     
     var myElement.html("<p>Hello World</p>");
     var myElement.innerHTML = "<p>Hello World</p>";
     ```

   - `val()`：获取或设置表单元素的值（如 `<input>`、`<textarea>` 等）

   - 

     ```js
     var myElement.css("font-size","35px");
     var myElement.style.fontSize = "35px";
     ```

   - `hide()`,`show()`：隐藏或展示元素

     ```js
     var myElement.hide();
     var myElement.style.display = "none";
     var myElement.show();
     var myElement.style.display = "";
     ```

   - `addClass()`, `removeClass()`, `toggleClass()`：修改元素的类

3. **事件处理**：

   - `click()`: 绑定点击事件
   - `hover()`: 绑定鼠标进入和离开事件
   - `keydown()`, `keyup()`: 绑定键盘事件
   - `submit()`: 绑定表单提交事件

4. **动画效果**：

   - `fadeIn()`, `fadeOut()`, `fadeToggle()`: 淡入、淡出、切换效果
   - `slideUp()`, `slideDown()`, `slideToggle()`: 滑动上升、下降、切换效果
   - `animate()`: 自定义动画

## 优缺点

**优点**

- **简洁易用**：提供了更简洁的语法来操作 DOM，减少了编写 JavaScript 的复杂度。
- **跨浏览器兼容性**：jQuery 自动处理了浏览器之间的差异性，保证代码在不同浏览器中的表现一致。
- **丰富的插件生态**：有大量的 jQuery 插件可以用来实现各种功能（如日期选择器、图表、弹窗等）。

**缺点**

- **性能问题**：由于 jQuery 是一个库，相较于原生 JavaScript，可能会有些性能损失，尤其是在复杂的页面或大量操作时。
- **过于依赖**：jQuery 使用简单，但过度依赖它可能会导致无法充分利用现代浏览器本身的原生 API，随着浏览器更新，很多 jQuery 的功能已被原生 JavaScript 取代。





# 5.技巧



## 电梯栏

```html
<div id="lift">
	<a class="default-color active-color" onclick="toFunction.call(this,0)">顶部</a>
	<span class="line"></span>
	<a class="default-color" onclick="toFunction.call(this,960)">中间</a>
	<span class="line"></span>
	<a class="default-color" onclick="toFunction.call(this,2000)">底部</a>
</div>
```





```js
// warning: 当写 window.addEventListener("scroll", s()) 时，s() 会立即执行
window.addEventListener("scroll", s)

function s () {
  // 用于获取当前文档的垂直滚动位置，即网页的滚动条位置
  let height = document.documentElement.scrollTop;
  const btns = document.querySelectorAll("#lift a");
  console.log(height)

  if (height < 960) {
    document.querySelector(".active-color").classList.remove("active-color")
    btns[0].classList.add("active-color");
  } else if (height >= 960 && height < 1920) {
    document.querySelector(".active-color").classList.remove("active-color")
    btns[1].classList.add("active-color");
  } else if (height >= 1920){
    document.querySelector(".active-color").classList.remove("active-color")
    btns[2].classList.add("active-color");
  }

}
/**
 * @param {Object} scrollTopVal：到达指定位置需要滚动的高度
 * 点击按钮，滚动到指定位置
 */
function toFunction(scrollTopVal) {
  window.scrollTo({
    top: scrollTopVal,
    behavior: 'smooth'
  })
  s();
}
```





```
// TODO：请补充代码
function startGame() {
    let score = 0

    let flag = 0
    let remain = 16
    let prev = {}
    const imgs = document.querySelectorAll(".img-box img")

    imgs.forEach(element => {
        element.style.transition = "0.3s ease-in-out"
        element.style.display = "block"
    });
    setTimeout(() => {
        imgs.forEach(element => {
            element.style.display = "none"
        });
    }, 1000)

    const items = document.querySelectorAll(".img-box")

    function flip(alt) {
        console.log(alt)
    }

    items.forEach(element => {
        element.addEventListener('click', () => {flip(element)})
    });

    function flip(f) {
        flag++
        if (flag == 1) {
            f.childNodes[1].style.display = 'block'
            prev = f.childNodes[1]
            console.log(prev.parentNode)
        }
        if (flag == 2) {
            f.childNodes[1].style.display = 'block'
            if (prev.alt != f.childNodes[1].alt) {
                setTimeout(() => {
                    prev.style.display = 'none'
                    f.childNodes[1].style.display = 'none'
                }, 1000)
                score = score-2
            } else {
                setTimeout(() => {
                    prev.parentNode.style.all = 'unset'
                    f.style.all = 'unset'
                    prev.style.display = 'none'
                    f.childNodes[1].style.display = 'none'
                }, 1000)
                score = score+2
                
            }
            flag = 0
            document.getElementById("score").innerHTML = `${score}`
        }
    }

}

```





## 判断类型

```js
typeof data[1][key] === 'string'
```



## 随机功能

### 随机整数

在 JavaScript 中，要生成一个介于 `n` 和 `m` 之间的随机整数，可以使用 `Math.random()` 结合 `Math.floor()` 来实现。

这里是一个简单的函数：

```javascript
function getRandomBetween(n, m) {
  return Math.floor(Math.random() * (m - n + 1)) + n;
}
```

解释：

- `Math.random()` 生成一个介于 `0`（包括）和 `1`（不包括）之间的随机小数。
- `Math.random() * (m - n + 1)` 生成一个介于 `0` 和 `(m - n + 1)` 之间的随机小数。
- `Math.floor()` 用来将这个小数向下取整，确保返回的是一个整数。
- 最后，`+ n` 是为了确保随机数的范围是从 `n` 到 `m`（包括 `n` 和 `m`）。

### 1/2概率

```js
  function bool() {
    return Math.random() < 0.5
  }
```



## 可选链操作符

**可选链操作符**（Optional Chaining Operator）`?.` 是 JavaScript 中的一种新语法，它允许你在访问对象的深层嵌套属性时安全地避免出现 `TypeError` 错误。如果在访问某个属性或方法时，目标对象是 `null` 或 `undefined`，则表达式会短路并返回 `undefined`，而不会抛出错误。

### 语法：

```javascript
obj?.property
obj?.[property]
obj?.method()
```

### 解释：

1. **`obj?.property`**：访问对象 `obj` 的属性 `property`，如果 `obj` 是 `null` 或 `undefined`，则返回 `undefined`，而不是抛出错误。
2. **`obj?.[property]`**：使用可选链访问对象的动态属性（通过变量 `property`），如果 `obj` 是 `null` 或 `undefined`，返回 `undefined`。
3. **`obj?.method()`**：调用对象的 `method` 方法，如果 `obj` 是 `null` 或 `undefined`，则不会执行方法，而是返回 `undefined`。

### 例子：

#### 1. 访问对象属性

```javascript
const user = { name: 'Alice', address: { city: 'New York' } };

console.log(user?.address?.city); // 输出: 'New York'
console.log(user?.address?.zipcode); // 输出: undefined (address 存在，但 zipcode 不存在)
console.log(user?.contact?.phone); // 输出: undefined (contact 是 null 或 undefined)
```

#### 2. 调用对象方法

```javascript
const obj = {
  greet: () => 'Hello, world!',
};

console.log(obj?.greet()); // 输出: 'Hello, world!'
console.log(obj?.nonExistentMethod()); // 输出: undefined (不会抛出错误)
```

#### 3. 访问数组元素

```javascript
const arr = [{ name: 'Alice' }, { name: 'Bob' }];

console.log(arr?.[1]?.name); // 输出: 'Bob'
console.log(arr?.[2]?.name); // 输出: undefined (数组长度不足)
```

### 优势：

1. **避免错误**：在传统的代码中，访问 `null` 或 `undefined` 的属性会抛出 `TypeError`，而可选链操作符允许你安全地访问深层嵌套的属性。
2. **简化代码**：在使用可选链时，你不再需要显式地检查每一层对象是否为 `null` 或 `undefined`，这使得代码更加简洁和易读。

### 使用场景：

- **访问深层嵌套的对象属性**：当你不确定某个对象的深层嵌套属性是否存在时，可选链可以避免访问不存在的属性时抛出错误。
- **函数调用**：当你调用一个可能不存在的方法时，使用可选链可以避免错误。
- **动态属性访问**：当你访问的属性名是动态的，例如通过变量来访问属性时，可选链同样有效。

### 总结：

可选链操作符 `?.` 是一种让代码更加安全和简洁的特性。它能让你在访问对象的属性、调用方法、或访问数组元素时，如果目标对象是 `null` 或 `undefined`，不会抛出错误，而是返回 `undefined`。这大大简化了代码并减少了错误发生的风险。





## DOM位置操作

### 1.同级DOM从后方插入

```html
<div id="parent">
    <div id="1"></div>
    <div id="2"></div>
</div>
```

```javascript
// 获取节点1和节点2
const node1 = document.getElementById('1');
const node2 = document.getElementById('2');

// 获取节点2的父节点
const parent = node2.parentNode;

// 获取节点2的下一个兄弟节点（即节点2之后的第一个兄弟节点）
const nextSibling = node2.nextSibling;***

// 将节点1插入到节点2之后
parent.insertBefore(node1, nextSibling);
```





## 类型转换



### 1.String -> Number

```js
const numInt = Number.parseInt(String)
const numFloat = Number.parseFloat(String)
```



### 2.Array-like -> Array

```js
const arr = Array.from(arrayLike, mapFn, thisArg)
```



