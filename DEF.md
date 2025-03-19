# 数据交换格式 (Data Exchange Formats)

[TOC]





**数据交换格式**（Data Exchange Formats）是用于在不同系统、应用程序、平台之间交换和传输数据的标准化结构。这些格式定义了数据的组织方式，使得不同的系统可以理解和处理这些数据。常见的数据交换格式包括 **XML**、**JSON**、**CSV**、**YAML**、**Protocol Buffers**、**MessagePack** 等。它们的选择取决于数据的复杂度、应用场景以及性能需求。



# XML（可扩展标记语言，Extensible Markup Language）

XML（可扩展标记语言，Extensible Markup Language）是一种用于表示数据的标记语言，它设计的目的是简洁、可扩展和平台无关。XML用于存储和传输数据，广泛应用于文档格式、配置文件、数据交换以及Web服务中。

## 元素

**XML 命名规则**

XML 元素必须遵循以下命名规则：

- 名称可以包含字母、数字以及其他的字符
- 名称不能以数字或者标点符号开始
- 名称不能以字母 xml（或者 XML、Xml 等等）开始
- 名称不能包含空格

可使用任何名称，没有保留的字词。

------

**最佳命名习惯**

使名称具有描述性。使用下划线的名称也很不错：<first_name>、<last_name>。

名称应简短和简单，比如：<book_title>，而不是：<the_title_of_the_book>。

避免 "-" 字符。如果您按照这样的方式进行命名："first-name"，一些软件会认为您想要从 first 里边减去 name。

避免 "." 字符。如果您按照这样的方式进行命名："first.name"，一些软件会认为 "name" 是对象 "first" 的属性。

避免 ":" 字符。冒号会被转换为命名空间来使用（稍后介绍）。

XML 文档经常有一个对应的数据库，其中的字段会对应 XML 文档中的元素。有一个实用的经验，即使用数据库的命名规则来命名 XML 文档中的元素。

在 XML 中，éòá 等非英语字母是完全合法的，不过需要留意，您的软件供应商不支持这些字符时可能出现的问题。



```xml
<!-- XML 声明 -->
<?xml version="1.0" encoding="utf-8"?>

<!-- XML 文档必须有根元素 -->
<note>
<date>
<day>10</day>
<month>01</month>
<year>2008</year>
</date>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>
    <message>Don't forget me this weekend!</message>
</body>
</note>
```



## 属性

XML由**元素, 实体与属性**构成。没有什么规矩可以告诉我们什么时候该使用属性，而什么时候该使用元素。我的经验是在 HTML 中，属性用起来很便利，但是在 XML 中，您应该**尽量避免使用属性**。如果信息感觉起来很像数据，那么请使用元素吧。

因使用属性而引起的一些问题：

- 属性不能包含多个值（元素可以）
- 属性不能包含树结构（元素可以）
- 属性不容易扩展（为未来的变化）

**属性难以阅读和维护**。请尽量使用元素来描述数据。而**仅仅使用属性来提供与数据无关的信息**。

下面的三个 XML 文档包含完全相同的信息：

第一个实例中使用了 date 属性：

```xml
<note date="10/01/2008">
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

第二个实例中使用了 date 元素：

```xml
<note>
<date>10/01/2008</date>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```





第三个实例中使用了扩展的 date 元素（这是我的最爱）：

```xml
<note>
<date>
<day>10</day>
<month>01</month>
<year>2008</year>
</date>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```



## 实体

在 XML 中，一些字符拥有特殊的意义。

如果您把字符 "<" 放在 XML 元素中，会发生错误，这是因为解析器会把它当作新元素的开始。

这样会产生 XML 错误：

```
<message>if salary < 1000 then</message>
```

为了避免这个错误，请用**实体引用**来代替 "<" 字符：

```
<message>if salary &lt; 1000 then</message>
```

在 XML 中，有 5 个预定义的实体引用：

| &lt;   | <    | less than      |
| ------ | ---- | -------------- |
| &gt;   | >    | greater than   |
| &amp;  | &    | ampersand      |
| &apos; | '    | apostrophe     |
| &quot; | "    | quotation mark |

**注释：**在 XML 中，只有字符 "<" 和 "&" 确实是非法的。大于号是合法的，但是用实体引用来代替它是一个好习惯。





# JSON（JS对象标记语言, JavaScript Object Notation）

JSON是一种轻量级的数据交换格式，基于文本且易于人类读取和编写。它通常用于客户端与服务器之间的数据交换，是一种完全语言无关的数据表示方式。JSON 被广泛应用于 Web 开发、API 设计、数据传输和存储等领域。

## 语法

**JSON 语法**：

- 数据在名称/值对中
- 数据由逗号分隔
- 花括号容纳对象
- 方括号容纳数组

**有效的数据类型**

在 JSON 中，值必须是以下数据类型之一：

- 字符串
- 数字
- 对象（JSON 对象）
- 数组
- 布尔
- Null

JSON 的值*不可以*是以下数据类型之一：

- 函数
- 日期
- undefined

```json
{"employees":[
    { "firstName":"Bill", "lastName":"Gates" },
    { "firstName":"Steve", "lastName":"Jobs" },
    { "firstName":"Elon", "lastName":"Musk" }
]}
```

```xml
<employees>
    <employee>
         <firstName>Bill</firstName>
         <lastName>Gates</lastName>
     </employee>
     <employee>
         <firstName>Steve</firstName>
         <lastName>Jobs</lastName>
     </employee>
     <employee>
         <firstName>Elon</firstName>
         <lastName>Musk</lastName>
     </employee>
</employees>
```



## 访问

**JS对象**

```js
myObj =  {
   "name":"Bill Gates",
   "age":62,
   "cars": {
	  "car1":"Porsche",
	  "car2":"BMW",
	  "car3":"Volvo"
   }
}

// 1.使用点号（.）来访问对象值
x = myObj.name;
x = myObj.cars.car2;
// 2.使用方括号（[]）来访问对象值
x = myObj["name"];
x = myObj["cars"]["car2"];
// 3.使用 for-in 遍历对象属性
for (x in myObj) {
   document.getElementById("demo").innerHTML  += x;
}
// 4.使用 delete 关键词来删除 JSON 对象的属性
delete myObj.cars.car1;

```

**JS数组**

```js
{
"name":"Bill Gates",
"age":62,
"cars":[ "Porsche", "BMW", "Volvo" ]
}

// 1.通过使用索引号来访问数组值：
x = myObj.cars[0];
// 2.通过使用 for-in 循环来访问数组值
for (i in myObj.cars) {
     x  += myObj.cars[i];
}

myObj =  {
   "name":"Bill Gates",
   "age":62,
   "cars": [
	  { "name":"Porsche",  "models":[ "911", "Taycan" ] },
	  { "name":"BMW", "models":[ "M5", "M3", "X5" ] },
	  { "name":"Volvo", "models":[ "XC60", "V60" ] }
   ]
}

// 4.访问嵌套数组，请对每个数组使用 for-in 循环：
for (i in myObj.cars) {
    x += "<h1>" + myObj.cars[i].name  + "</h1>";
    for (j in myObj.cars[i].models) {
         x += myObj.cars[i].models[j];
    }
}
```





## 解析

### 普通解析 `JSON.parse()`

`JSON.parse()` 方法用于将一个 JSON 字符串转换为 JavaScript 对象。

```js
var text = '{"employees":[' +
'{"firstName":"Bill","lastName":"Gates" },' +
'{"firstName":"Steve","lastName":"Jobs" },' +
'{"firstName":"Elon","lastName":"Musk" }]}';

obj = JSON.parse(text);
document.getElementById("demo").innerHTML =
obj.employees[1].firstName + " " + obj.employees[1].lastName;
```

解析日期

1. Date()

```js
var text =  '{ "name":"Bill Gates", "birth":"1955-10-28", "city":"Seattle"}';
var obj = JSON.parse(text);
obj.birth = new Date(obj.birth);
 
document.getElementById("demo").innerHTML = obj.name + ", " + obj.birth;
```

2. Date() + reviver参数

使用 `JSON.parse()` 函数的第二个参数，被称为 *reviver*。这个 *reviver* 参数是函数，在返回值之前，它会检查每个属性。

将字符串转换为日期，使用 reviver 函数：

```js
var text =  '{ "name":"Bill Gates", "birth":"1955-10-28", "city":"Seattle"}';
var obj = JSON.parse(text, function (key, value) {
    if  (key == "birth") {
        return new Date(value);
    } else {
         return value;
   }});
 
document.getElementById("demo").innerHTML = obj.name + ", " + obj.birth;
```



### 在Ajax中解析 `response.json()`

```js
// 使用 fetch() 发起 GET 请求
fetch('https://api.example.com/data')
  .then(response => {
    // 检查响应是否为成功状态 (200-299)
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    // 使用 response.json() 解析响应体中的 JSON 数据
    return response.json();
  })
  .then(data => {
    // 处理解析后的 JSON 数据
    console.log(data);
  })
  .catch(error => {
    // 处理错误
    console.error('There was a problem with the fetch operation:', error);
  });

```



### 将数据转换为 JSON 数据 `JSON.stringify()`

`JSON.stringify()` 方法用于将一个 JavaScript 对象转换为 JSON 字符串。

```js
// JavaScript 对象
const obj = { name: "John", age: 30, city: "New York" };

// 将对象转换为 JSON 字符串
const jsonString = JSON.stringify(obj);

console.log(jsonString);
// 输出: '{"name":"John","age":30,"city":"New York"}'

```













# CSV (逗号分隔值，Comma-Separated Values)

CSV (Comma-Separated Values) 是一种广泛使用的文件格式，用于存储表格数据。它的特点是数据以逗号（`,`）分隔，每行代表一条记录，每个字段（column）之间通过逗号隔开。CSV 文件通常用于数据交换、导入和导出数据、以及处理简单的表格结构数据。



## 文件格式

假设你有一个包含姓名、年龄和城市的简单数据集，CSV 文件的内容可能是：

```csv
name,age,city
Bill Gates,62,Seattle
Elon Musk,52,Los Angeles
Jeff Bezos,60,Washington D.C.
```

## 文件特点

1. **分隔符**：最常见的分隔符是逗号（`,`），但有时也可能是分号（`;`）、制表符（Tab）等，取决于地区或应用。
2. **每行代表一条记录**：每一行的内容对应数据库或表格中的一行。
3. **字段类型**：字段通常是文本（字符串），但是数字、日期等也可以在 CSV 文件中存储。
4. **头部行（可选）**：CSV 文件中通常包含一个头部行，它定义了每列数据的名称。

## 使用场景

- **数据导入导出**：许多数据分析工具和数据库系统支持从 CSV 文件导入数据或导出数据。
- **电子表格应用**：Excel、Google Sheets 等电子表格软件可以轻松打开和保存 CSV 文件。
- **数据交换**：CSV 格式由于其简单性，常用于跨平台和应用程序之间的数据交换。