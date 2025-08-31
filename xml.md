# XML（Extensible Markup Language）

[TOC]

## 介绍

XML（可扩展标记语言，Extensible Markup Language）是一种用于表示数据的标记语言，它设计的目的是简洁、可扩展和平台无关。XML用于存储和传输数据，广泛应用于文档格式、配置文件、数据交换以及Web服务中。

## 元素

### XML 命名规则

XML 元素必须遵循以下命名规则：

- 名称可以包含字母、数字以及其他的字符
- 名称不能以数字或者标点符号开始
- 名称不能以字母 xml（或者 XML、Xml 等等）开始
- 名称不能包含空格

可使用任何名称，没有保留的字词。

------

### 最佳命名习惯

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





# KML



## 什么是KML

KML，即Keyhole markup language，最初为[Google定义的文件格式](https://developers.google.com/kml/documentation/kml_tut)，用以描述地图中的关键数据，如路径、标记位置、叠加图层等信息。因此，使用KML文件可以记录一个简单的只包含街道、路径、多边形、标记位置等信息的简单地图，不包含高程、地形地貌等复杂信息。KML文件最终被[OGC组织](https://zhida.zhihu.com/search?content_id=227579647&content_type=Article&match_order=1&q=OGC组织&zhida_source=entity)采纳为国际通行标准。

但KML文件本质上是一个XML文件，完全遵循XML文件格式。

## 文件结构

1. **XML 头部**：这是每个 KML 文件的第一行。在这一行之前不能有空格或其他字符。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    ```

2. **KML 命名空间声明**：这是每个 KML 2.2 文件的第二行。它定义了该文件使用的 KML 标准的命名空间。

    ```xml
    <kml xmlns="http://www.opengis.net/kml/2.2"></kml>
    ```

3. **Placemark 对象**：这是 KML 文件中的一个元素，包含以下部分：

    - **name**：用于作为 Placemark（标记点）的标签，通常是该位置的名称。
    - **description**：在标记点的“气泡”中显示的描述内容，通常包含有关该位置的更多信息。
    - **若干地理位置元素标签**

    ```xml
    <Placemark>
        <name>Simple placemark</name>
        <description>Attached to the ground. Intelligently places itself 
           at the height of the underlying terrain.</description>
    	.....................
      </Placemark>
    ```

    

## 地理位置元素标签



### 地点标记

地点位置是用`<Point>`标签，其中`<coordinates>`标签定义了地理元素的具体位置，是许多几何标签的核心部分。其格式为**经度**在前，**纬度**在后，**高度**可选，默认为 0。

```xml
<Placemark>
  <name>简单地点标记</name>
  <description>这是一个简单的地点标记示例。</description>
  <Point>
    <coordinates>-122.0822035425683,37.42228990140251,0</coordinates>
  </Point>
</Placemark>
```

### 绘制路径

`<LineString>`可以绘制一条线（比如道路或边界）。

```xml
<Placemark>
  <name>一条路径</name>
  <LineString>
    <coordinates>
      -112.081423,36.106965,0
      -112.087846,36.090176,0
    </coordinates>
  </LineString>
</Placemark>
```

### 描述区域

想要描述一片闭合区域可以使用`<Polygon>`。`<coordinates>`坐标点序列，首尾必须相同以闭合。

```xml
<Placemark>
  <name>一个多边形</name>
  <Polygon>
    <outerBoundaryIs>
      <LinearRing>
        <coordinates>
          -122.366278,37.818844,0
          -122.365248,37.819267,0
          -122.365640,37.819861,0
          -122.366278,37.818844,0
        </coordinates>
      </LinearRing>
    </outerBoundaryIs>
  </Polygon>
</Placemark>
```













