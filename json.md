# JSON（JavaScript Object Notation）

[TOC]

## 介绍

JSON是一种轻量级的数据交换格式，基于文本且易于人类读取和编写。它通常用于客户端与服务器之间的数据交换，是一种完全语言无关的数据表示方式。JSON 被广泛应用于 Web 开发、API 设计、数据传输和存储等领域。

## 语法

### JSON 语法：

- 数据在名称/值对中
- 数据由逗号分隔
- 花括号容纳对象
- 方括号容纳数组

### 有效的数据类型

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

### JS对象

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

### JS数组

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



### 在 `fetch()` 中解析 `response.json()`

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



