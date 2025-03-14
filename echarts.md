# Echarts

[TOC]



ECharts 是一个使用 JavaScript 实现的开源可视化库，涵盖各行业图表，满足各种需求。

ECharts 提供了丰富的图表类型和交互能力，使用户能够通过简单的配置生成各种各样的图表，包括但不限于折线图、柱状图、散点图、饼图、雷达图、地图等。

ECharts 遵循 Apache-2.0 开源协议，免费商用。

ECharts 兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等）及兼容多种设备，可随时随地任性展示。



# 1.配置示例

**index.html**

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>第一个 ECharts 实例</title>
</head>

<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <!-- 引入cdn,也可以下载到本地引入 -->
    <script src="https://cdn.jsdelivr.net/npm/echarts@4.3.0/dist/echarts.min.js"></script>
    <script src="index.js"></script>
</body>
</html>
```



**index.js**

```js
// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'), "dark");
 
// 指定图表的配置项和数据
var option = {
    width: 600,
    height: 400,
    title: {
        text: '第一个 ECharts 实例'
    },
    tooltip: {},
    legend: {
        data:['销量']
    },
    xAxis: {
        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
    },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
    }]
};

// 使用刚指定的配置项和数据显示图表。
myChart.setOption(option);
// 在图表容器被销毁之后，调用 echartsInstance.dispose 销毁实例，在图表容器重新被添加后再次调用 echarts.init 初始化。
myChart.dispose
```



# 2.初始化

`echarts.init` 是 ECharts 的一个方法，用于初始化图表实例。它的基本语法如下：

```javascript
var chart = echarts.init(dom, theme, opts);
```

**参数解释**：

1. **dom** (必需)：要将图表挂载到的 DOM 元素，通常是通过 `document.getElementById()` 获取的一个元素。
2. **theme** (可选)：图表的主题，可以是一个字符串（例如 `'dark'`, `'light'`）或一个对象（自定义主题）。如果不传递，使用默认主题。
3. **opts** (可选)：配置选项对象，用于定制图表实例的一些配置。常见的配置项包括 `renderer`（渲染模式，'canvas' 或 'svg'）、`devicePixelRatio`（设备像素比）等。



## 2.1.dom

### 父容器大小

通常来说，需要在 HTML 中先定义一个 `<div>` 节点，并且通过 CSS 使得该节点具有宽度和高度。初始化的时候，传入该节点，图表的大小默认即为该节点的大小，除非声明了 `opts.width` 或 `opts.height` 将其覆盖。

```html
<div id="main" style="width: 600px;height:400px;"></div>
<script type="text/javascript">
  var myChart = echarts.init(document.getElementById('main'));
</script>
```

### 图表大小

如果图表容器不存在宽度和高度，或者，你希望图表宽度和高度不等于容器大小，也可以在初始化的时候指定大小。

```html
<div id="main"></div>
<script type="text/javascript">
  var myChart = echarts.init(document.getElementById('main'), null, {
    width: 600,
    height: 400
  });
</script>
```

需要注意的是，使用这种方法在调用 `echarts.init` 时需保证容器已经有宽度和高度了。

### 响应容器大小的变化

在有些场景下，我们希望当容器大小改变时，图表的大小也相应地改变。

比如，图表容器是一个高度为 400px、宽度为页面 100% 的节点，你希望在浏览器宽度改变的时候，始终保持图表宽度是页面的 100%。

这种情况下，可以监听页面的 `resize` 事件获取浏览器大小改变的事件，然后调用 [`echartsInstance.resize`](https://echarts.apache.org/api.html#echartsInstance.resize) 改变图表的大小。

```html
<style>
  #main,
  html,
  body {
    width: 100%;
  }
  #main {
    height: 400px;
  }
</style>
<div id="main"></div>
<script type="text/javascript">
  var myChart = echarts.init(document.getElementById('main'));
  window.addEventListener('resize', function() {
    myChart.resize();
  });
</script>
```



> 小贴士：有时候我们可能会通过 JS 或 CSS 调整容器大小，由于页面大小并未发生改变，因此 `resize` 事件将不会被触发。如果有需要覆盖这种情况，可以借助浏览器的 [`ResizeObserver`](https://developer.mozilla.org/zh-CN/docs/Web/API/ResizeObserver) API 来实现更细粒度的监听。





## 2.2.theme

最简单的更改全局样式的方式，是直接采用颜色主题（theme）。例如，在 [示例集合](https://echarts.apache.org/examples) 中，可以通过切换深色模式，直接看到采用主题的效果。

ECharts5 除了一贯的默认主题外，还内置了`'dark'`主题。可以像这样切换成深色模式：

```js
var chart = echarts.init(dom, 'dark');
```



其他的主题，没有内置在 ECharts 中，需要自己加载。这些主题可以在 [主题编辑器](https://echarts.apache.org/theme-builder.html) 里访问到。也可以使用这个主题编辑器，自己编辑主题。下载下来的主题可以这样使用：

如果主题保存为 JSON 文件，则需要自行加载和注册，例如：

```js
// 假设主题名称是 "vintage"
fetch('theme/vintage.json')
  .then(r => r.json())
  .then(theme => {
    echarts.registerTheme('vintage', theme);
    var chart = echarts.init(dom, 'vintage');
  })
```



如果保存为 UMD 格式的 JS 文件，文件内部已经做了自注册，直接引入 JS 即可：

```js
// HTML 引入 vintage.js 文件后（假设主题名称是 "vintage"）
var chart = echarts.init(dom, 'vintage');
// ...
```





## 2.3.opts

https://echarts.apache.org/zh/option.html





### title 标题

#### [title.](https://echarts.apache.org/zh/option.html#title) [id](https://echarts.apache.org/zh/option.html#title.id)

string

组件 ID。默认不指定。指定则可用于在 option 或者 API 中引用组件。

#### [title.](https://echarts.apache.org/zh/option.html#title) [show](https://echarts.apache.org/zh/option.html#title.show) = true

boolean

是否显示标题组件。

#### [title.](https://echarts.apache.org/zh/option.html#title) [text](https://echarts.apache.org/zh/option.html#title.text) = ''

string

主标题文本，支持使用 `\n` 换行。

#### [title.](https://echarts.apache.org/zh/option.html#title) [link](https://echarts.apache.org/zh/option.html#title.link) = ''

string

主标题文本超链接。

#### [title.](https://echarts.apache.org/zh/option.html#title) [target](https://echarts.apache.org/zh/option.html#title.target) = 'blank'

string

指定窗口打开主标题超链接。

**可选：**

- `'self'` 当前窗口打开
- `'blank'` 新窗口打开

#### [title.](https://echarts.apache.org/zh/option.html#title) [textStyle](https://echarts.apache.org/zh/option.html#title.textStyle)

Object

##### 所有属性

{ [color](https://echarts.apache.org/zh/option.html#title.textStyle.color) , [fontStyle](https://echarts.apache.org/zh/option.html#title.textStyle.fontStyle) , [fontWeight](https://echarts.apache.org/zh/option.html#title.textStyle.fontWeight) , [fontFamily](https://echarts.apache.org/zh/option.html#title.textStyle.fontFamily) , [fontSize](https://echarts.apache.org/zh/option.html#title.textStyle.fontSize) , [lineHeight](https://echarts.apache.org/zh/option.html#title.textStyle.lineHeight) , [width](https://echarts.apache.org/zh/option.html#title.textStyle.width) , [height](https://echarts.apache.org/zh/option.html#title.textStyle.height) , [textBorderColor](https://echarts.apache.org/zh/option.html#title.textStyle.textBorderColor) , [textBorderWidth](https://echarts.apache.org/zh/option.html#title.textStyle.textBorderWidth) , [textBorderType](https://echarts.apache.org/zh/option.html#title.textStyle.textBorderType) , [textBorderDashOffset](https://echarts.apache.org/zh/option.html#title.textStyle.textBorderDashOffset) , [textShadowColor](https://echarts.apache.org/zh/option.html#title.textStyle.textShadowColor) , [textShadowBlur](https://echarts.apache.org/zh/option.html#title.textStyle.textShadowBlur) , [textShadowOffsetX](https://echarts.apache.org/zh/option.html#title.textStyle.textShadowOffsetX) , [textShadowOffsetY](https://echarts.apache.org/zh/option.html#title.textStyle.textShadowOffsetY) , [overflow](https://echarts.apache.org/zh/option.html#title.textStyle.overflow) , [ellipsis](https://echarts.apache.org/zh/option.html#title.textStyle.ellipsis) , [rich](https://echarts.apache.org/zh/option.html#title.textStyle.rich) }

#### [title.](https://echarts.apache.org/zh/option.html#title) [subtext](https://echarts.apache.org/zh/option.html#title.subtext) = ''

#### [title.](https://echarts.apache.org/zh/option.html#title) [sublink](https://echarts.apache.org/zh/option.html#title.sublink) = ''

#### [title.](https://echarts.apache.org/zh/option.html#title) [subtarget](https://echarts.apache.org/zh/option.html#title.subtarget) = 'blank'

#### [title.](https://echarts.apache.org/zh/option.html#title) [subtextStyle](https://echarts.apache.org/zh/option.html#title.subtextStyle)

#### [title.](https://echarts.apache.org/zh/option.html#title) [textAlign](https://echarts.apache.org/zh/option.html#title.textAlign) = 'auto'

string

整体（包括 text 和 subtext）的水平对齐。

可选值：`'auto'`、`'left'`、`'right'`、`'center'`。

#### [title.](https://echarts.apache.org/zh/option.html#title) [textVerticalAlign](https://echarts.apache.org/zh/option.html#title.textVerticalAlign) = 'auto'

string

整体（包括 text 和 subtext）的垂直对齐。

可选值：`'auto'`、`'top'`、`'bottom'`、`'middle'`。

#### [title.](https://echarts.apache.org/zh/option.html#title) [triggerEvent](https://echarts.apache.org/zh/option.html#title.triggerEvent)

boolean

是否触发事件。

#### [title.](https://echarts.apache.org/zh/option.html#title) [padding](https://echarts.apache.org/zh/option.html#title.padding) = 5

numberArray

标题内边距，单位px，默认各方向内边距为5，接受数组分别设定上右下左边距。

使用示例：

```ts
// 设置内边距为 5
padding: 5
// 设置上下的内边距为 5，左右的内边距为 10
padding: [5, 10]
// 分别设置四个方向的内边距
padding: [
    5,  // 上
    10, // 右
    5,  // 下
    10, // 左
]
```

#### [title.](https://echarts.apache.org/zh/option.html#title) [itemGap](https://echarts.apache.org/zh/option.html#title.itemGap) = 10

number

主副标题之间的间距。

#### [title.](https://echarts.apache.org/zh/option.html#title) [zlevel](https://echarts.apache.org/zh/option.html#title.zlevel)

number

所有图形的 zlevel 值。

`zlevel`用于 Canvas 分层，不同`zlevel`值的图形会放置在不同的 Canvas 中，Canvas 分层是一种常见的优化手段。我们可以把一些图形变化频繁（例如有动画）的组件设置成一个单独的`zlevel`。需要注意的是过多的 Canvas 会引起内存开销的增大，在手机端上需要谨慎使用以防崩溃。

`zlevel` 大的 Canvas 会放在 `zlevel` 小的 Canvas 的上面。

#### [title.](https://echarts.apache.org/zh/option.html#title) [z](https://echarts.apache.org/zh/option.html#title.z) = 2

number

组件的所有图形的`z`值。控制图形的前后顺序。`z`值小的图形会被`z`值大的图形覆盖。

`z`相比`zlevel`优先级更低，而且不会创建新的 Canvas。

#### [title.](https://echarts.apache.org/zh/option.html#title) [left](https://echarts.apache.org/zh/option.html#title.left) (top, right, bottom) = 'auto' 

string number

title 组件离容器左侧的距离。

`left` 的值可以是像 `20` 这样的具体像素值，可以是像 `'20%'` 这样相对于容器高宽的百分比，也可以是 `'left'`, `'center'`, `'right'`。

如果 `left` 的值为 `'left'`, `'center'`, `'right'`，组件会根据相应的位置自动对齐。

#### [title.](https://echarts.apache.org/zh/option.html#title) [backgroundColor](https://echarts.apache.org/zh/option.html#title.backgroundColor) = 'transparent'

Color

标题背景色，默认透明。

> 颜色可以使用 RGB 表示，比如 `'rgb(128, 128, 128)'` ，如果想要加上 alpha 通道，可以使用 RGBA，比如 `'rgba(128, 128, 128, 0.5)'`，也可以使用十六进制格式，比如 `'#ccc'`

#### [title.](https://echarts.apache.org/zh/option.html#title) [borderColor](https://echarts.apache.org/zh/option.html#title.borderColor) = '#ccc'

Color

标题的边框颜色。支持的颜色格式同 backgroundColor。

#### [title.](https://echarts.apache.org/zh/option.html#title) [borderWidth](https://echarts.apache.org/zh/option.html#title.borderWidth)

number

标题的边框线宽。

#### [title.](https://echarts.apache.org/zh/option.html#title) [borderRadius](https://echarts.apache.org/zh/option.html#title.borderRadius)

numberArray

圆角半径，单位px，支持传入数组分别指定 4 个圆角半径。 如:

```ts
borderRadius: 5, // 统一设置四个角的圆角大小
borderRadius: [5, 5, 0, 0] //（顺时针左上，右上，右下，左下）
```

#### [title.](https://echarts.apache.org/zh/option.html#title) [shadowBlur](https://echarts.apache.org/zh/option.html#title.shadowBlur)

number

图形阴影的模糊大小。该属性配合 `shadowColor`,`shadowOffsetX`, `shadowOffsetY` 一起设置图形的阴影效果。

示例：

```ts
{
    shadowColor: 'rgba(0, 0, 0, 0.5)',
    shadowBlur: 10
}
```

**注意**：此配置项生效的前提是，设置了 `show: true` 以及值不为 `transparent` 的背景色 `backgroundColor`。

#### [title.](https://echarts.apache.org/zh/option.html#title) [shadowColor](https://echarts.apache.org/zh/option.html#title.shadowColor)

Color

阴影颜色。支持的格式同`color`。

**注意**：此配置项生效的前提是，设置了 `show: true`。

#### [title.](https://echarts.apache.org/zh/option.html#title) [shadowOffsetX](https://echarts.apache.org/zh/option.html#title.shadowOffsetX)

number

阴影水平方向上的偏移距离。

**注意**：此配置项生效的前提是，设置了 `show: true`。

#### [title.](https://echarts.apache.org/zh/option.html#title) [shadowOffsetY](https://echarts.apache.org/zh/option.html#title.shadowOffsetY)

number

阴影垂直方向上的偏移距离。

**注意**：此配置项生效的前提是，设置了 `show: true`。





### legend 图例

#### id, show, zlevel, z, left, top, right, bottom, padding, itemGap, backgroundColor, border一系列, shadow一系列

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [type](https://echarts.apache.org/zh/option.html#legend.type)

string

图例的类型。可选值：

- `'plain'`：普通图例。缺省就是普通图例。
- `'scroll'`：可滚动翻页的图例。当图例数量较多时可以使用。

参见 [滚动图例（垂直）](https://echarts.apache.org/examples/zh/editor.html?c=pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](https://echarts.apache.org/examples/zh/editor.html?c=radar2&edit=1&reset=1)。

当使用 `'scroll'` 时，使用这些设置进行细节配置：

- [legend.scrollDataIndex](https://echarts.apache.org/zh/option.html#legend.scrollDataIndex)
- [legend.pageButtonItemGap](https://echarts.apache.org/zh/option.html#legend.pageButtonItemGap)
- [legend.pageButtonGap](https://echarts.apache.org/zh/option.html#legend.pageButtonGap)
- [legend.pageButtonPosition](https://echarts.apache.org/zh/option.html#legend.pageButtonPosition)
- [legend.pageFormatter](https://echarts.apache.org/zh/option.html#legend.pageFormatter)
- [legend.pageIcons](https://echarts.apache.org/zh/option.html#legend.pageIcons)
- [legend.pageIconColor](https://echarts.apache.org/zh/option.html#legend.pageIconColor)
- [legend.pageIconInactiveColor](https://echarts.apache.org/zh/option.html#legend.pageIconInactiveColor)
- [legend.pageIconSize](https://echarts.apache.org/zh/option.html#legend.pageIconSize)
- [legend.pageTextStyle](https://echarts.apache.org/zh/option.html#legend.pageTextStyle)
- [legend.animation](https://echarts.apache.org/zh/option.html#legend.animation)
- [legend.animationDurationUpdate](https://echarts.apache.org/zh/option.html#legend.animationDurationUpdate)

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [width](https://echarts.apache.org/zh/option.html#legend.width) = 'auto'

stringnumber

图例组件的宽度。默认自适应。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [height](https://echarts.apache.org/zh/option.html#legend.height) = 'auto'

stringnumber

图例组件的高度。默认自适应。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [orient](https://echarts.apache.org/zh/option.html#legend.orient) = 'horizontal'

string

图例列表的布局朝向。

可选：

- `'horizontal'`
- `'vertical'`

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [align](https://echarts.apache.org/zh/option.html#legend.align) = 'auto'

string

图例标记和文本的对齐。默认自动，根据组件的位置和 orient 决定，当组件的 [left](https://echarts.apache.org/zh/option.html#legend.left) 值为 `'right'` 以及纵向布局（[orient](https://echarts.apache.org/zh/option.html#legend.orient) 为 `'vertical'`）的时候为右对齐，即为 `'right'`。

可选：

- `'auto'`
- `'left'`
- `'right'`

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [itemWidth](https://echarts.apache.org/zh/option.html#legend.itemWidth) = 25

number

图例标记的图形宽度。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [itemHeight](https://echarts.apache.org/zh/option.html#legend.itemHeight) = 14

number

图例标记的图形高度。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [itemStyle](https://echarts.apache.org/zh/option.html#legend.itemStyle)

Object

图例的图形样式。其属性的取值为 `'inherit'` 时，表示继承系列中的属性值。

##### 所有属性

{ [color](https://echarts.apache.org/zh/option.html#legend.itemStyle.color) , [borderColor](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderColor) , [borderWidth](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderWidth) , [borderType](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderType) , [borderDashOffset](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderDashOffset) , [borderCap](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderCap) , [borderJoin](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderJoin) , [borderMiterLimit](https://echarts.apache.org/zh/option.html#legend.itemStyle.borderMiterLimit) , [shadowBlur](https://echarts.apache.org/zh/option.html#legend.itemStyle.shadowBlur) , [shadowColor](https://echarts.apache.org/zh/option.html#legend.itemStyle.shadowColor) , [shadowOffsetX](https://echarts.apache.org/zh/option.html#legend.itemStyle.shadowOffsetX) , [shadowOffsetY](https://echarts.apache.org/zh/option.html#legend.itemStyle.shadowOffsetY) , [opacity](https://echarts.apache.org/zh/option.html#legend.itemStyle.opacity) , [decal](https://echarts.apache.org/zh/option.html#legend.itemStyle.decal) }

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [lineStyle](https://echarts.apache.org/zh/option.html#legend.lineStyle)

Object

图例图形中线的样式，用于诸如折线图图例横线的样式设置。其属性的取值为 `'inherit'` 时，表示继承系列中的属性值。

##### 所有属性

{ [color](https://echarts.apache.org/zh/option.html#legend.lineStyle.color) , [width](https://echarts.apache.org/zh/option.html#legend.lineStyle.width) , [type](https://echarts.apache.org/zh/option.html#legend.lineStyle.type) , [dashOffset](https://echarts.apache.org/zh/option.html#legend.lineStyle.dashOffset) , [cap](https://echarts.apache.org/zh/option.html#legend.lineStyle.cap) , [join](https://echarts.apache.org/zh/option.html#legend.lineStyle.join) , [miterLimit](https://echarts.apache.org/zh/option.html#legend.lineStyle.miterLimit) , [shadowBlur](https://echarts.apache.org/zh/option.html#legend.lineStyle.shadowBlur) , [shadowColor](https://echarts.apache.org/zh/option.html#legend.lineStyle.shadowColor) , [shadowOffsetX](https://echarts.apache.org/zh/option.html#legend.lineStyle.shadowOffsetX) , [shadowOffsetY](https://echarts.apache.org/zh/option.html#legend.lineStyle.shadowOffsetY) , [opacity](https://echarts.apache.org/zh/option.html#legend.lineStyle.opacity) , [inactiveColor](https://echarts.apache.org/zh/option.html#legend.lineStyle.inactiveColor) , [inactiveWidth](https://echarts.apache.org/zh/option.html#legend.lineStyle.inactiveWidth) }

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [symbolRotate](https://echarts.apache.org/zh/option.html#legend.symbolRotate) = 'inherit'

numberstring

图形旋转角度，类型为 `number | 'inherit'`。如果为 `'inherit'`，表示取系列的 `symbolRotate`。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [formatter](https://echarts.apache.org/zh/option.html#legend.formatter)

stringFunction

用来格式化图例文本，支持字符串模板和回调函数两种形式。

示例：

```ts
// 使用字符串模板，模板变量为图例名称 {name}
formatter: 'Legend {name}'
// 使用回调函数
formatter: function (name) {
    return 'Legend ' + name;
}
```

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [selectedMode](https://echarts.apache.org/zh/option.html#legend.selectedMode) = true

stringboolean

图例选择的模式，控制是否可以通过点击图例改变系列的显示状态。默认开启图例选择，可以设成 `false` 关闭。

除此之外也可以设成 `'single'` 或者 `'multiple'` 使用单选或者多选模式。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [inactiveColor](https://echarts.apache.org/zh/option.html#legend.inactiveColor) = '#ccc'

Color

图例关闭时的颜色。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [inactiveBorderColor](https://echarts.apache.org/zh/option.html#legend.inactiveBorderColor) = '#ccc'

Color

图例关闭时的描边颜色。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [inactiveBorderWidth](https://echarts.apache.org/zh/option.html#legend.inactiveBorderWidth) = 'auto'

numberstring

图例关闭时的描边粗细。

如果为 `'auto'` 表示：如果系列存在描边，则取 2，如果系列不存在描边，则取 0。

如果为 `'inherit'` 表示：始终取系列的描边粗细。

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [selected](https://echarts.apache.org/zh/option.html#legend.selected)

Object

图例选中状态表。

示例：

```ts
selected: {
    // 选中'系列1'
    '系列1': true,
    // 不选中'系列2'
    '系列2': false
}
```

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [textStyle](https://echarts.apache.org/zh/option.html#legend.textStyle)

Object

图例的公用文本样式。

##### 所有属性

{ [color](https://echarts.apache.org/zh/option.html#legend.textStyle.color) , [fontStyle](https://echarts.apache.org/zh/option.html#legend.textStyle.fontStyle) , [fontWeight](https://echarts.apache.org/zh/option.html#legend.textStyle.fontWeight) , [fontFamily](https://echarts.apache.org/zh/option.html#legend.textStyle.fontFamily) , [fontSize](https://echarts.apache.org/zh/option.html#legend.textStyle.fontSize) , [lineHeight](https://echarts.apache.org/zh/option.html#legend.textStyle.lineHeight) , [backgroundColor](https://echarts.apache.org/zh/option.html#legend.textStyle.backgroundColor) , [borderColor](https://echarts.apache.org/zh/option.html#legend.textStyle.borderColor) , [borderWidth](https://echarts.apache.org/zh/option.html#legend.textStyle.borderWidth) , [borderType](https://echarts.apache.org/zh/option.html#legend.textStyle.borderType) , [borderDashOffset](https://echarts.apache.org/zh/option.html#legend.textStyle.borderDashOffset) , [borderRadius](https://echarts.apache.org/zh/option.html#legend.textStyle.borderRadius) , [padding](https://echarts.apache.org/zh/option.html#legend.textStyle.padding) , [shadowColor](https://echarts.apache.org/zh/option.html#legend.textStyle.shadowColor) , [shadowBlur](https://echarts.apache.org/zh/option.html#legend.textStyle.shadowBlur) , [shadowOffsetX](https://echarts.apache.org/zh/option.html#legend.textStyle.shadowOffsetX) , [shadowOffsetY](https://echarts.apache.org/zh/option.html#legend.textStyle.shadowOffsetY) , [width](https://echarts.apache.org/zh/option.html#legend.textStyle.width) , [height](https://echarts.apache.org/zh/option.html#legend.textStyle.height) , [textBorderColor](https://echarts.apache.org/zh/option.html#legend.textStyle.textBorderColor) , [textBorderWidth](https://echarts.apache.org/zh/option.html#legend.textStyle.textBorderWidth) , [textBorderType](https://echarts.apache.org/zh/option.html#legend.textStyle.textBorderType) , [textBorderDashOffset](https://echarts.apache.org/zh/option.html#legend.textStyle.textBorderDashOffset) , [textShadowColor](https://echarts.apache.org/zh/option.html#legend.textStyle.textShadowColor) , [textShadowBlur](https://echarts.apache.org/zh/option.html#legend.textStyle.textShadowBlur) , [textShadowOffsetX](https://echarts.apache.org/zh/option.html#legend.textStyle.textShadowOffsetX) , [textShadowOffsetY](https://echarts.apache.org/zh/option.html#legend.textStyle.textShadowOffsetY) , [overflow](https://echarts.apache.org/zh/option.html#legend.textStyle.overflow) , [ellipsis](https://echarts.apache.org/zh/option.html#legend.textStyle.ellipsis) , [rich](https://echarts.apache.org/zh/option.html#legend.textStyle.rich) }

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [tooltip](https://echarts.apache.org/zh/option.html#legend.tooltip)

Object

图例的 tooltip 配置，配置项同 [tooltip](https://echarts.apache.org/zh/option.html#tooltip)。默认不显示，可以在 legend 文字很多的时候对文字做裁剪并且开启 tooltip，如下示例：

```ts
legend: {
    formatter: function (name) {
        return echarts.format.truncateText(name, 40, '14px Microsoft Yahei', '…');
    },
    tooltip: {
        show: true
    }
}
```

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [icon](https://echarts.apache.org/zh/option.html#legend.icon)

string

图例项的 icon。

ECharts 提供的标记类型包括

```ts
'circle'`, `'rect'`, `'roundRect'`, `'triangle'`, `'diamond'`, `'pin'`, `'arrow'`, `'none'
```

可以通过 `'image://url'` 设置为图片，其中 URL 为图片的链接，或者 `dataURI`。

URL 为图片链接例如：

```ts
'image://http://example.website/a/b.png'
```

URL 为 `dataURI` 例如：

```ts
'image://data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7'
```

可以通过 `'path://'` 将图标设置为任意的矢量路径。这种方式相比于使用图片的方式，不用担心因为缩放而产生锯齿或模糊，而且可以设置为任意颜色。路径图形会自适应调整为合适的大小。路径的格式参见 [SVG PathData](http://www.w3.org/TR/SVG/paths.html#PathData)。可以从 Adobe Illustrator 等工具编辑导出。

例如：

```ts
'path://M30.9,53.2C16.8,53.2,5.3,41.7,5.3,27.6S16.8,2,30.9,2C45,2,56.4,13.5,56.4,27.6S45,53.2,30.9,53.2z M30.9,3.5C17.6,3.5,6.8,14.4,6.8,27.6c0,13.3,10.8,24.1,24.101,24.1C44.2,51.7,55,40.9,55,27.6C54.9,14.4,44.1,3.5,30.9,3.5z M36.9,35.8c0,0.601-0.4,1-0.9,1h-1.3c-0.5,0-0.9-0.399-0.9-1V19.5c0-0.6,0.4-1,0.9-1H36c0.5,0,0.9,0.4,0.9,1V35.8z M27.8,35.8 c0,0.601-0.4,1-0.9,1h-1.3c-0.5,0-0.9-0.399-0.9-1V19.5c0-0.6,0.4-1,0.9-1H27c0.5,0,0.9,0.4,0.9,1L27.8,35.8L27.8,35.8z'
```

#### [legend.](https://echarts.apache.org/zh/option.html#legend) [data](https://echarts.apache.org/zh/option.html#legend.data)

Array

图例的数据数组。数组项通常为一个字符串，每一项代表一个系列的 `name`（如果是[饼图](https://echarts.apache.org/zh/option.html#series-pie)，也可以是饼图单个数据的 `name`）。图例组件会自动根据对应系列的图形标记（symbol）来绘制自己的颜色和标记，特殊字符串 `''`（空字符串）或者 `'\n'`（换行字符串）用于图例的换行。

如果 `data` 没有被指定，会自动从当前系列中获取。多数系列会取自 [series.name](https://echarts.apache.org/zh/option.html#series.name) 或者 [series.encode](https://echarts.apache.org/zh/option.html#series.encode) 的 `seriesName` 所指定的维度。如 [饼图](https://echarts.apache.org/zh/option.html#series-pie) and [漏斗图](https://echarts.apache.org/zh/option.html#series-funnel) 等会取自 series.data 中的 name。

如果要设置单独一项的样式，也可以把该项写成配置项对象。此时必须使用 `name` 属性对应表示系列的 `name`。

示例

```
data: [{
    name: '系列1',
    // 强制设置图形为圆。
    icon: 'circle',
    // 设置文本为红色
    textStyle: {
        color: 'red'
    }
}]
```

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#legend.data.name) , [icon](https://echarts.apache.org/zh/option.html#legend.data.icon) , [itemStyle](https://echarts.apache.org/zh/option.html#legend.data.itemStyle) , [lineStyle](https://echarts.apache.org/zh/option.html#legend.data.lineStyle) , [symbolRotate](https://echarts.apache.org/zh/option.html#legend.data.symbolRotate) , [inactiveColor](https://echarts.apache.org/zh/option.html#legend.data.inactiveColor) , [inactiveBorderColor](https://echarts.apache.org/zh/option.html#legend.data.inactiveBorderColor) , [inactiveBorderWidth](https://echarts.apache.org/zh/option.html#legend.data.inactiveBorderWidth) , [textStyle](https://echarts.apache.org/zh/option.html#legend.data.textStyle) }





### grid 直角坐标系

直角坐标系内绘图网格，单个 grid 内最多可以放置上下两个 X 轴，左右两个 Y 轴。可以在网格上绘制[折线图](https://echarts.apache.org/zh/option.html#series-line)，[柱状图](https://echarts.apache.org/zh/option.html#series-bar)，[散点图（气泡图）](https://echarts.apache.org/zh/option.html#series-scatter)。

在 ECharts 2.x 里单个 echarts 实例中最多只能存在一个 grid 组件，在 ECharts 3 中可以存在任意个 grid 组件。

#### id, show, zlevel, z, left, top, right, bottom, padding, itemGap, width, height, backgroundColor, border一系列, shadow一系列

#### [grid.](https://echarts.apache.org/zh/option.html#grid) [containLabel](https://echarts.apache.org/zh/option.html#grid.containLabel)

boolean

grid 区域是否包含坐标轴的[刻度标签](https://echarts.apache.org/zh/option.html#yAxis.axisLabel)。

- containLabel 为 `false` 的时候：
  - `grid.left` `grid.right` `grid.top` `grid.bottom` `grid.width` `grid.height` 决定的是由坐标轴形成的矩形的尺寸和位置。
  - 这比较适用于多个 `grid` 进行对齐的场景，因为往往多个 `grid` 对齐的时候，是依据坐标轴来对齐的。
- containLabel 为 `true` 的时候：
  - `grid.left` `grid.right` `grid.top` `grid.bottom` `grid.width` `grid.height` 决定的是包括了坐标轴标签在内的所有内容所形成的矩形的位置。
  - 这常用于『防止标签溢出』的场景，标签溢出指的是，标签长度动态变化时，可能会溢出容器或者覆盖其他组件。

#### [grid.](https://echarts.apache.org/zh/option.html#grid) [tooltip](https://echarts.apache.org/zh/option.html#grid.tooltip)

Object

本坐标系特定的 tooltip 设定。

**提示框组件的通用介绍：**

提示框组件可以设置在多种地方：

- 可以设置在全局，即 [tooltip](https://echarts.apache.org/zh/option.html#tooltip)
- 可以设置在坐标系中，即 [grid.tooltip](https://echarts.apache.org/zh/option.html#grid.tooltip)、[polar.tooltip](https://echarts.apache.org/zh/option.html#polar.tooltip)、[single.tooltip](https://echarts.apache.org/zh/option.html#single.tooltip)
- 可以设置在系列中，即 [series.tooltip](https://echarts.apache.org/zh/option.html#series.tooltip)
- 可以设置在系列的每个数据项中，即 [series.data.tooltip](https://echarts.apache.org/zh/option.html#series.data.tooltip)

##### 所有属性

{ [show](https://echarts.apache.org/zh/option.html#grid.tooltip.show) , [trigger](https://echarts.apache.org/zh/option.html#grid.tooltip.trigger) , [axisPointer](https://echarts.apache.org/zh/option.html#grid.tooltip.axisPointer) , [position](https://echarts.apache.org/zh/option.html#grid.tooltip.position) , [formatter](https://echarts.apache.org/zh/option.html#grid.tooltip.formatter) , [valueFormatter](https://echarts.apache.org/zh/option.html#grid.tooltip.valueFormatter) , [backgroundColor](https://echarts.apache.org/zh/option.html#grid.tooltip.backgroundColor) , [borderColor](https://echarts.apache.org/zh/option.html#grid.tooltip.borderColor) , [borderWidth](https://echarts.apache.org/zh/option.html#grid.tooltip.borderWidth) , [padding](https://echarts.apache.org/zh/option.html#grid.tooltip.padding) , [textStyle](https://echarts.apache.org/zh/option.html#grid.tooltip.textStyle) , [extraCssText](https://echarts.apache.org/zh/option.html#grid.tooltip.extraCssText) }

### xAxis x轴 (yAxis y轴)

#### id, show, position, triggerEvent

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [gridIndex](https://echarts.apache.org/zh/option.html#xAxis.gridIndex)

number

x 轴所在的 grid 的索引，默认位于第一个 grid。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [alignTicks](https://echarts.apache.org/zh/option.html#xAxis.alignTicks)

boolean

> 从 `v5.3.0` 开始支持

在多个 x 轴为数值轴的时候，可以开启该配置项自动对齐刻度。只对`'value'`和`'log'`类型的轴有效。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [offset](https://echarts.apache.org/zh/option.html#xAxis.offset)

number

X 轴相对于默认位置的偏移，在相同的 `position` 上有多个 X 轴的时候有用。
注：若未将 `xAxis.axisLine.onZero` 设为 `false` , 则该项无法生效

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [type](https://echarts.apache.org/zh/option.html#xAxis.type) = 'category'

string

坐标轴类型。

可选：

- `'value'` 数值轴，适用于连续数据。
- `'category'` 类目轴，适用于离散的类目数据。为该类型时类目数据可自动从 [series.data](https://echarts.apache.org/zh/option.html#series.data) 或 [dataset.source](https://echarts.apache.org/zh/option.html#dataset.source) 中取，或者可通过 [xAxis.data](https://echarts.apache.org/zh/option.html#xAxis.data) 设置类目数据。
- `'time'` 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
- `'log'` 对数轴。适用于对数数据。对数轴下的堆积柱状图或堆积折线图可能带来很大的视觉误差，并且在一定情况下可能存在非预期效果，应避免使用。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [name](https://echarts.apache.org/zh/option.html#xAxis.name)

string

坐标轴名称。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameLocation](https://echarts.apache.org/zh/option.html#xAxis.nameLocation) = 'end'

string

坐标轴名称显示位置。

**可选：**

- `'start'`
- `'middle'` 或者 `'center'`
- `'end'`

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameTextStyle](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle)

Object

坐标轴名称的文字样式。

##### 所有属性

{ [color](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.color) , [fontStyle](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.fontStyle) , [fontWeight](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.fontWeight) , [fontFamily](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.fontFamily) , [fontSize](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.fontSize) , [align](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.align) , [verticalAlign](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.verticalAlign) , [lineHeight](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.lineHeight) , [backgroundColor](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.backgroundColor) , [borderColor](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.borderColor) , [borderWidth](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.borderWidth) , [borderType](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.borderType) , [borderDashOffset](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.borderDashOffset) , [borderRadius](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.borderRadius) , [padding](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.padding) , [shadowColor](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.shadowColor) , [shadowBlur](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.shadowBlur) , [shadowOffsetX](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.shadowOffsetX) , [shadowOffsetY](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.shadowOffsetY) , [width](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.width) , [height](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.height) , [textBorderColor](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textBorderColor) , [textBorderWidth](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textBorderWidth) , [textBorderType](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textBorderType) , [textBorderDashOffset](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textBorderDashOffset) , [textShadowColor](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textShadowColor) , [textShadowBlur](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textShadowBlur) , [textShadowOffsetX](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textShadowOffsetX) , [textShadowOffsetY](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.textShadowOffsetY) , [overflow](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.overflow) , [ellipsis](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.ellipsis) , [rich](https://echarts.apache.org/zh/option.html#xAxis.nameTextStyle.rich) }

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameGap](https://echarts.apache.org/zh/option.html#xAxis.nameGap) = 15

number

坐标轴名称与轴线之间的距离。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameRotate](https://echarts.apache.org/zh/option.html#xAxis.nameRotate)

number

坐标轴名字旋转，角度值。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameRotate](https://echarts.apache.org/zh/option.html#xAxis.nameRotate)

number

坐标轴名字旋转，角度值。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [nameTruncate](https://echarts.apache.org/zh/option.html#xAxis.nameTruncate)

Object

坐标轴名字的截断。

##### 所有属性

{ [maxWidth](https://echarts.apache.org/zh/option.html#xAxis.nameTruncate.maxWidth) , [ellipsis](https://echarts.apache.org/zh/option.html#xAxis.nameTruncate.ellipsis) }

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [inverse](https://echarts.apache.org/zh/option.html#xAxis.inverse)

boolean

是否是反向坐标轴。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [boundaryGap](https://echarts.apache.org/zh/option.html#xAxis.boundaryGap)

booleanArray

坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。

类目轴中 `boundaryGap` 可以配置为 `true` 和 `false`。默认为 `true`，这时候[刻度](https://echarts.apache.org/zh/option.html#xAxis.axisTick)只是作为分隔线，标签和数据点都会在两个[刻度](https://echarts.apache.org/zh/option.html#xAxis.axisTick)之间的带(band)中间。

非类目轴，包括时间，数值，对数轴，`boundaryGap`是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 [min](https://echarts.apache.org/zh/option.html#xAxis.min) 和 [max](https://echarts.apache.org/zh/option.html#xAxis.max) 后无效。 **示例：**

```ts
boundaryGap: ['20%', '20%']
```

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [min (max)](https://echarts.apache.org/zh/option.html#xAxis.min)

numberstringFunction

坐标轴刻度最小值。

可以设置成特殊值 `'dataMin'`，此时取数据在该轴上的最小值作为最小刻度。

不设置时会自动计算最小值保证坐标轴刻度的均匀分布。

在类目轴中，也可以设置为类目的序数（如类目轴 `data: ['类A', '类B', '类C']` 中，序数 `2` 表示 `'类C'`。也可以设置为负数，如 `-3`）。

当设置成 `function` 形式时，可以根据计算得出的数据最大最小值设定坐标轴的最小值。如：

```ts
min: function (value) {
    return value.min - 20;
}
```

其中 `value` 是一个包含 `min` 和 `max` 的对象，分别表示数据的最大最小值，这个函数可返回坐标轴的最小值，也可返回 `null`/`undefined` 来表示“自动计算最小值”（返回 `null`/`undefined` 从 `v4.8.0` 开始支持）。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [scale](https://echarts.apache.org/zh/option.html#xAxis.scale)

boolean

只在数值轴中（[type](https://echarts.apache.org/zh/option.html#xAxis.type): 'value'）有效。

是否是脱离 0 值比例。设置成 `true` 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。

在设置 [min](https://echarts.apache.org/zh/option.html#xAxis.min) 和 [max](https://echarts.apache.org/zh/option.html#xAxis.max) 之后该配置项无效。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [logBase](https://echarts.apache.org/zh/option.html#xAxis.logBase) = 10

number

对数轴的底数，只在对数轴中（[type](https://echarts.apache.org/zh/option.html#xAxis.type): 'log'）有效。

#### [xAxis.](https://echarts.apache.org/zh/option.html#xAxis) [data](https://echarts.apache.org/zh/option.html#xAxis.data)

Array

类目数据，在类目轴（[type](https://echarts.apache.org/zh/option.html#xAxis.type): `'category'`）中有效。

如果没有设置 [type](https://echarts.apache.org/zh/option.html#xAxis.type)，但是设置了 `axis.data`，则认为 `type` 是 `'category'`。

如果设置了 [type](https://echarts.apache.org/zh/option.html#xAxis.type) 是 `'category'`，但没有设置 `axis.data`，则 `axis.data` 的内容会自动从 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中获取，这会比较方便。不过注意，`axis.data` 指明的是 `'category'` 轴的取值范围。如果不指定而是从 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中获取，那么只能获取到 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中出现的值。比如说，假如 [series.data](https://echarts.apache.org/zh/option.html#series.data) 为空时，就什么也获取不到。

示例：

```ts
// 所有类目名称列表
data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
// 每一项也可以是具体的配置项，此时取配置项中的 `value` 为类目名
data: [{
    value: '周一',
    // 突出周一
    textStyle: {
        fontSize: 20,
        color: 'red'
    }
}, '周二', '周三', '周四', '周五', '周六', '周日']
```

##### 所有属性

{ [value](https://echarts.apache.org/zh/option.html#xAxis.data.value) , [textStyle](https://echarts.apache.org/zh/option.html#xAxis.data.textStyle) }



### polar 极坐标系

极坐标系，可以用于散点图和折线图。每个极坐标系拥有一个[角度轴](https://echarts.apache.org/zh/option.html#angleAxis)和一个[半径轴](https://echarts.apache.org/zh/option.html#radiusAxis)。

#### id, zlevel, z, tooltip

#### [polar.](https://echarts.apache.org/zh/option.html#polar) [center](https://echarts.apache.org/zh/option.html#polar.center) = ['50%', '50%']

Array

极坐标系的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。

支持设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度。

**使用示例：**

```
// 设置成绝对的像素值
center: [400, 300]
// 设置成相对的百分比
center: ['50%', '50%']
```

#### [polar.](https://echarts.apache.org/zh/option.html#polar) [radius](https://echarts.apache.org/zh/option.html#polar.radius)

number string Array

极坐标系的半径。可以为如下类型：

- `number`：直接指定外半径值。
- `string`：例如，`'20%'`，表示外半径为可视区尺寸（容器高宽中较小一项）的 20% 长度。

- `Array.<number|string>`：数组的第一项是内半径，第二项是外半径。每一项遵从上述 `number` `string` 的描述。





### radiusAxis 径向轴

#### [radiusAxis.](https://echarts.apache.org/zh/option.html#radiusAxis) [polarIndex](https://echarts.apache.org/zh/option.html#radiusAxis.polarIndex) 

number

径向轴所在的极坐标系的索引，默认使用第一个极坐标系。

#### [radiusAxis.](https://echarts.apache.org/zh/option.html#radiusAxis) [data](https://echarts.apache.org/zh/option.html#radiusAxis.data) 

Array

类目数据，在类目轴（[type](https://echarts.apache.org/zh/option.html#radiusAxis.type): `'category'`）中有效。

如果没有设置 [type](https://echarts.apache.org/zh/option.html#radiusAxis.type)，但是设置了 `axis.data`，则认为 `type` 是 `'category'`。

如果设置了 [type](https://echarts.apache.org/zh/option.html#radiusAxis.type) 是 `'category'`，但没有设置 `axis.data`，则 `axis.data` 的内容会自动从 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中获取，这会比较方便。不过注意，`axis.data` 指明的是 `'category'` 轴的取值范围。如果不指定而是从 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中获取，那么只能获取到 [series.data](https://echarts.apache.org/zh/option.html#series.data) 中出现的值。比如说，假如 [series.data](https://echarts.apache.org/zh/option.html#series.data) 为空时，就什么也获取不到。

示例：

```ts
// 所有类目名称列表
data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
// 每一项也可以是具体的配置项，此时取配置项中的 `value` 为类目名
data: [{
    value: '周一',
    // 突出周一
    textStyle: {
        fontSize: 20,
        color: 'red'
    }
}, '周二', '周三', '周四', '周五', '周六', '周日']
```

##### 所有属性

{ [value](https://echarts.apache.org/zh/option.html#radiusAxis.data.value) , [textStyle](https://echarts.apache.org/zh/option.html#radiusAxis.data.textStyle) }

### angleAxis 角度轴

#### [angleAxis.](https://echarts.apache.org/zh/option.html#angleAxis) [polarIndex](https://echarts.apache.org/zh/option.html#angleAxis.polarIndex) 

number

角度轴所在的极坐标系的索引，默认使用第一个极坐标系。

#### [angleAxis.](https://echarts.apache.org/zh/option.html#angleAxis) [startAngle](https://echarts.apache.org/zh/option.html#angleAxis.startAngle)

number

起始刻度的角度，默认为 90 度，即圆心的正上方。0 度为圆心的正右方。

#### [angleAxis.](https://echarts.apache.org/zh/option.html#angleAxis) [endAngle](https://echarts.apache.org/zh/option.html#angleAxis.endAngle)

number

结束刻度的角度，默认为 `null`，表示一整个圆。

#### [angleAxis.](https://echarts.apache.org/zh/option.html#angleAxis) [clockwise](https://echarts.apache.org/zh/option.html#angleAxis.clockwise) = true

boolean

刻度增长是否按顺时针，默认顺时针。



### radar 雷达图坐标系

雷达图坐标系组件，只适用于[雷达图](https://echarts.apache.org/zh/option.html#series-radar)。该组件等同 ECharts 2 中的 polar 组件。因为 3 中的 polar 被重构为标准的极坐标组件，为避免混淆，雷达图使用 radar 组件作为其坐标系。

雷达图坐标系与极坐标系不同的是它的每一个轴（indicator 指示器）都是一个单独的维度，可以通过 [name](https://echarts.apache.org/zh/option.html#radar.name)、[axisLine](https://echarts.apache.org/zh/option.html#radar.axisLine)、[axisTick](https://echarts.apache.org/zh/option.html#radar.axisTick)、[axisLabel](https://echarts.apache.org/zh/option.html#radar.axisLabel)、[splitLine](https://echarts.apache.org/zh/option.html#radar.splitLine)、 [splitArea](https://echarts.apache.org/zh/option.html#radar.splitArea) 几个配置项配置指示器坐标轴线的样式。

#### [radar.](https://echarts.apache.org/zh/option.html#radar) [indicator](https://echarts.apache.org/zh/option.html#radar.indicator)

Array

雷达图的指示器，用来指定雷达图中的多个变量（维度），如下示例。

```ts
indicator: [
   { name: '销售（sales）', max: 6500},
   { name: '管理（Administration）', max: 16000, color: 'red'}, // 标签设置为红色
   { name: '信息技术（Information Techology）', max: 30000},
   { name: '客服（Customer Support）', max: 38000},
   { name: '研发（Development）', max: 52000},
   { name: '市场（Marketing）', max: 25000}
]
```

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#radar.indicator.name) , [max](https://echarts.apache.org/zh/option.html#radar.indicator.max) , [min](https://echarts.apache.org/zh/option.html#radar.indicator.min) , [color](https://echarts.apache.org/zh/option.html#radar.indicator.color) }





### dataZoom 数据区域缩放组件

`dataZoom` 组件 用于区域缩放，从而能自由关注细节的数据信息，或者概览数据整体，或者去除离群点的影响。

#### [dataZoom.](https://echarts.apache.org/zh/option.html#dataZoom-inside) [type](https://echarts.apache.org/zh/option.html#dataZoom-inside.type)

现在支持这几种类型的 `dataZoom` 组件：

- [内置型数据区域缩放组件（dataZoomInside）](https://echarts.apache.org/zh/option.html#dataZoom-inside)：内置于坐标系中，使用户可以在坐标系上通过鼠标拖拽、鼠标滚轮、手指滑动（触屏上）来缩放或漫游坐标系。
- [滑动条型数据区域缩放组件（dataZoomSlider）](https://echarts.apache.org/zh/option.html#dataZoom-slider)：有单独的滑动条，用户在滑动条上进行缩放或漫游。
- [框选型数据区域缩放组件（dataZoomSelect）](https://echarts.apache.org/zh/option.html#toolbox.feature.dataZoom)：提供一个选框进行数据区域缩放。即 [toolbox.feature.dataZoom](https://echarts.apache.org/zh/option.html#toolbox.feature.dataZoom)，配置项在 `toolbox` 中。

#### [dataZoom.](https://echarts.apache.org/zh/option.html#dataZoom-inside) [xAxisIndex](https://echarts.apache.org/zh/option.html#dataZoom-inside.xAxisIndex)

**✦ dataZoom 和 数轴的关系 ✦**

`dataZoom` 主要是对 `数轴（axis）` 进行操作（控制数轴的显示范围，或称窗口（window））。

> 可以通过 [dataZoom.xAxisIndex](https://echarts.apache.org/zh/option.html#dataZoom.xAxisIndex) 或 [dataZoom.yAxisIndex](https://echarts.apache.org/zh/option.html#dataZoom.yAxisIndex) 或 [dataZoom.radiusAxisIndex](https://echarts.apache.org/zh/option.html#dataZoom.radiusAxisIndex) 或 [dataZoom.angleAxisIndex](https://echarts.apache.org/zh/option.html#dataZoom.angleAxisIndex) 来指定 `dataZoom` 控制哪个或哪些数轴。

`dataZoom` 组件可 **同时存在多个**，起到共同控制的作用。如果多个 `dataZoom` 组件共同控制同一个数轴，他们会自动联动。

#### [dataZoom.](https://echarts.apache.org/zh/option.html#dataZoom-inside) [filterMode](https://echarts.apache.org/zh/option.html#dataZoom-inside.filterMode) = 'filter'

**✦ dataZoom 组件如何影响轴和数据 ✦**

`dataZoom` 的运行原理是通过 `数据过滤` 以及在内部设置轴的显示窗口来达到 `数据窗口缩放` 的效果。

数据过滤模式（[dataZoom.filterMode](https://echarts.apache.org/zh/option.html#dataZoom.filterMode)）的设置不同，效果也不同。

可选值为：

- 'filter'：当前数据窗口外的数据，被 **过滤掉**。即 **会** 影响其他轴的数据范围。每个数据项，只要有一个维度在数据窗口外，整个数据项就会被过滤掉。
- 'weakFilter'：当前数据窗口外的数据，被 **过滤掉**。即 **会** 影响其他轴的数据范围。每个数据项，只有当全部维度都在数据窗口同侧外部，整个数据项才会被过滤掉。
- 'empty'：当前数据窗口外的数据，被 **设置为空**。即 **不会** 影响其他轴的数据范围。
- 'none': 不过滤数据，只改变数轴范围。

如何设置，由用户根据场景和需求自己决定。经验来说：

- 当『只有 X 轴 或 只有 Y 轴受 `dataZoom` 组件控制』时，常使用 `filterMode: 'filter'`，这样能使另一个轴自适应过滤后的数值范围。
- 当『X 轴 Y 轴分别受 `dataZoom` 组件控制』时：
  - 如果 X 轴和 Y 轴是『同等地位的、不应互相影响的』，比如在『双数值轴散点图』中，那么两个轴可都设为 `filterMode: 'empty'`。
  - 如果 X 轴为主，Y 轴为辅，比如在『柱状图』中，需要『拖动 `dataZoomX` 改变 X 轴过滤柱子时，Y 轴的范围也自适应剩余柱子的高度』，『拖动 `dataZoomY` 改变 Y 轴过滤柱子时，X 轴范围不受影响』，那么就 X轴设为 `filterMode: 'filter'`，Y 轴设为 `filterMode: 'empty'`，即主轴 `'filter'`，辅轴 `'empty'`。

下面是个具体例子：

```javascript
option = {
    dataZoom: [
        {
            id: 'dataZoomX',
            type: 'slider',
            xAxisIndex: [0],
            filterMode: 'filter'
        },
        {
            id: 'dataZoomY',
            type: 'slider',
            yAxisIndex: [0],
            filterMode: 'empty'
        }
    ],
    xAxis: {type: 'value'},
    yAxis: {type: 'value'},
    series: {
        type: 'bar',
        data: [
            // 第一列对应 X 轴，第二列对应 Y 轴。
            [12, 24, 36],
            [90, 80, 70],
            [3, 9, 27],
            [1, 11, 111]
        ]
    }
}
```

上例中，`dataZoomX` 的 `filterMode` 设置为 `'filter'`。于是，假设当用户拖拽 `dataZoomX`（不去动 `dataZoomY`）导致其 valueWindow 变为 `[2, 50]` 时，`dataZoomX` 对 series.data 的第一列进行遍历，窗口外的整项去掉，最终得到的 series.data 为：

```javascript
[
    // 第一列对应 X 轴，第二列对应 Y 轴。
    [12, 24, 36],
    // [90, 80, 70] 整项被过滤掉，因为 90 在 dataWindow 之外。
    [3, 9, 27]
    // [1, 11, 111] 整项被过滤掉，因为 1 在 dataWindow 之外。
]
```

过滤前，series.data 中对应 Y 轴的值有 `24`、`80`、`9`、`11`，过滤后，只剩下 `24` 和 `9`，那么 Y 轴的显示范围就会自动改变以适应剩下的这两个值的显示（如果 Y 轴没有被设置 `min`、`max` 固定其显示范围的话）。

所以，`filterMode: 'filter'` 的效果是：过滤数据后使另外的轴也能自动适应当前数据的范围。

再从头来，上例中 `dataZoomY` 的 `filterMode` 设置为 `'empty'`。于是，假设当用户拖拽 `dataZoomY`（不去动 `dataZoomX`）导致其 dataWindow 变为 `[10, 60]` 时，`dataZoomY` 对 series.data 的第二列进行遍历，窗口外的值被设置为 empty （即替换为 NaN，这样设置为空的项，其所对应柱形，在 X 轴还有占位，只是不显示出来）。最终得到的 series.data 为：

```javascript
[
    // 第一列对应 X 轴，第二列对应 Y 轴。
    [12, 24, 36],
    [90, NaN, 70], // 设置为 empty (NaN)
    [3, NaN, 27],  // 设置为 empty (NaN)
    [1, 11, 111]
]
```

这时，series.data 中对应于 X 轴的值仍然全部保留不受影响，为 `12`、`90`、`3`、`1`。那么用户对 `dataZoomY` 的拖拽操作不会影响到 X 轴的范围。这样的效果，对于离群点（outlier）过滤功能，比较清晰。

另外，如果在任一个数轴上设置了 `min`、`max`（如设置 `yAxis: {min: 0, max: 400}`），那么这个数轴无论如何也不会被其他数轴的 dataZoom 行为影响了。

#### [dataZoom.](https://echarts.apache.org/zh/option.html#dataZoom-inside) [start](https://echarts.apache.org/zh/option.html#dataZoom-inside.start)

**✦ 数据窗口的设置 ✦**

`dataZoom` 的数据窗口范围的设置，目前支持两种形式：

- 百分比形式：即设置 [dataZoom.start](https://echarts.apache.org/zh/option.html#dataZoom.start) 和 [dataZoom.end](https://echarts.apache.org/zh/option.html#dataZoom.end)。
- 绝对数值形式：即设置 [dataZoom.startValue](https://echarts.apache.org/zh/option.html#dataZoom.startValue) 和 [dataZoom.endValue](https://echarts.apache.org/zh/option.html#dataZoom.endValue)。

注意：当使用百分比形式指定 `dataZoom` 范围时，且处于如下场景（或类似场景）中，`dataZoom` 的结果是和 `dataZoom` 组件的定义顺序相关的。

```javascript
option = {
    dataZoom: [
        {
            id: 'dataZoomX',
            type: 'slider',
            xAxisIndex: [0],
            filterMode: 'filter', // 设定为 'filter' 从而 X 的窗口变化会影响 Y 的范围。
            start: 30,
            end: 70
        },
        {
            id: 'dataZoomY',
            type: 'slider',
            yAxisIndex: [0],
            filterMode: 'empty',
            start: 20,
            end: 80
        }
    ],
    xAxis: {
        type: 'value'
    },
    yAxis: {
        type: 'value'
        // yAxis 中并没有使用 min、max 来显示限定轴的显示范围。
    },
    series: {
        type: 'bar',
        data: [
            // 第一列对应 X 轴，第二列对应 Y 轴。
            [12, 24, 36],
            [90, 80, 70],
            [3, 9, 27],
            [1, 11, 111]
        ]
    }
}
```

在上例中，`dataZoomY` 的 `start: 20, end: 80` 到底表示什么意思？

- 如果 `yAxis.min`、`yAxis.max` 进行了直接设置：

  那么 `dataZoomY` 的 `start: 20, end: 80` 表示 `yAxis.min` ~ `yAxis.max` 的 `20%` 到 `80%`。

- 如果 `yAxis.min`、`yAxis.max` 没有设置：

  - 如果 `dataZoomX` 设置为 `filterMode: 'empty'`：

    那么 `dataZoomY` 的 `start: 20, end: 80` 表示 series.data 中 `dataMinY` ~ `dataMaxY`（即上例中的 `9` ~ `80`）的 `20%` 到 `80%`。

  - 如果 `dataZoomX` 设置为 `filterMode: 'filter'`：

    那么，因为 `dataZoomX` 定义 `dataZoomY` 组件之前，所以 `dataZoomX` 的 `start: 30, end: 70` 表示全部数据的 `30%` 到 `70%`，而 `dataZoomY` 组件的 `start: 20, end: 80` 表示经过 `dataZoomX` 过滤处理后，所得数据集的 `20%` 到 `80%`。

    如果需要改变这种处理顺序，那么改变 `dataZoomX` 和 `dataZoomY` 在 option 中的出现顺序即可。



### visualMap 视觉映射组件

`visualMap` 是视觉映射组件，用于进行『视觉编码』，也就是将数据映射到视觉元素（视觉通道）。

`visualMap` 的主要功能：

1. **视觉映射**：根据数据值的大小动态调整视觉效果。
2. **色彩映射**：将数值映射到颜色上，通过颜色的变化来表示数值的不同。
3. **大小映射**：将数据值映射到图形元素的大小上，通常用于散点图等。

视觉元素可以是：

- `symbol`: 图元的图形类别。
- `symbolSize`: 图元的大小。
- `color`: 图元的颜色。
- `colorAlpha`: 图元的颜色的透明度。
- `opacity`: 图元以及其附属物（如文字标签）的透明度。
- `colorLightness`: 颜色的明暗度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorSaturation`: 颜色的饱和度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorHue`: 颜色的色调，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。

`visualMap` 组件可以定义多个，从而可以同时对数据中的多个维度进行视觉映射。

#### [visualMap.](https://echarts.apache.org/zh/option.html#visualMap-continuous) [type](https://echarts.apache.org/zh/option.html#visualMap-continuous.type)

`visualMap` 组件可以定义为 [分段型（visualMapPiecewise）](https://echarts.apache.org/zh/option.html#visualMap-piecewise) 或 [连续型（visualMapContinuous）](https://echarts.apache.org/zh/option.html#visualMap-continuous)，通过 `type` 来区分。

- **`continuous`（连续型）**：适用于连续数据，通过渐变色来表现数值变化。
- **`piecewise`（分段型）**：适用于离散数据，将不同的区间映射到不同的颜色。

#### [visualMap-continuous.](https://echarts.apache.org/zh/option.html#visualMap-continuous) [range](https://echarts.apache.org/zh/option.html#visualMap-continuous.range)

Array

指定手柄对应数值的位置。`range` 应在 `min` `max` 范围内。例如：

```javascript
chart.setOption({
    visualMap: {
        min: 0,
        max: 100,
        // 两个手柄对应的数值是 4 和 15
        range: [4, 15],
        ...
    }
});
```

#### [visualMap-continuous.](https://echarts.apache.org/zh/option.html#visualMap-continuous) [inRange](https://echarts.apache.org/zh/option.html#visualMap-continuous.inRange)

Object

定义 **在选中范围中** 的视觉元素。（用户可以和 visualMap 组件交互，用鼠标或触摸选择范围）

可选的视觉元素有：

- `symbol`: 图元的图形类别。
- `symbolSize`: 图元的大小。
- `color`: 图元的颜色。
- `colorAlpha`: 图元的颜色的透明度。
- `opacity`: 图元以及其附属物（如文字标签）的透明度。
- `colorLightness`: 颜色的明暗度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorSaturation`: 颜色的饱和度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorHue`: 颜色的色调，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。

`inRange` 能定义目标系列（参见 [visualMap-continuous.seriesIndex](https://echarts.apache.org/zh/option.html#visualMap-continuous.seriesIndex)）视觉形式，也同时定义了 `visualMap-continuous` 本身的视觉样式。通俗来讲就是，假如 `visualMap-continuous`控制的是散点图，那么 `inRange` 同时定义了散点图的 `颜色`、`尺寸` 等，也定义了 `visualMap-continuous` 本身的 `颜色`、`尺寸` 等。这二者能对应上。

定义方式，例如：

```javascript
visualMap: [
    {
        ...,
        inRange: {
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        }
    }
]
```

#### [visualMap-piecewise.](https://echarts.apache.org/zh/option.html#visualMap-piecewise) [splitNumber](https://echarts.apache.org/zh/option.html#visualMap-piecewise.splitNumber) = 5

number

对于连续型数据，自动平均切分成几段。默认为5段。 连续数据的范围需要 [max](https://echarts.apache.org/zh/option.html#visualMap-piecewise.max) 和 [min](https://echarts.apache.org/zh/option.html#visualMap-piecewise.min) 来指定。

如果设置了 [visualMap-piecewise.pieces](https://echarts.apache.org/zh/option.html#visualMap-piecewise.pieces) 或者 [visualMap-piecewise.categories](https://echarts.apache.org/zh/option.html#visualMap-piecewise.categories)，则 `splitNumber` 无效。

#### [visualMap-piecewise.](https://echarts.apache.org/zh/option.html#visualMap-piecewise) [pieces](https://echarts.apache.org/zh/option.html#visualMap-piecewise.pieces)

Array

自定义『分段式视觉映射组件（visualMapPiecewise）』的每一段的范围，以及每一段的文字，以及每一段的特别的样式。例如：

```javascript
pieces: [
    {min: 1500}, // 不指定 max，表示 max 为无限大（Infinity）。
    {min: 900, max: 1500},
    {min: 310, max: 1000},
    {min: 200, max: 300},
    {min: 10, max: 200, label: '10 到 200（自定义label）'},
    {value: 123, label: '123（自定义特殊颜色）', color: 'grey'}, // 表示 value 等于 123 的情况。
    {max: 5}     // 不指定 min，表示 min 为无限大（-Infinity）。
]
```

或者，更精确得，可以使用 `lt`（小于，less than），`gt`（大于，greater than），`lte`（小于等于 less than or equals），`gte`（大于等于，greater than or equals）来表达边界：

```javascript
pieces: [
    {gt: 1500},            // (1500, Infinity]
    {gt: 900, lte: 1500},  // (900, 1500]
    {gt: 310, lte: 1000},  // (310, 1000]
    {gt: 200, lte: 300},   // (200, 300]
    {gt: 10, lte: 200, label: '10 到 200（自定义label）'},       // (10, 200]
    {value: 123, label: '123（自定义特殊颜色）', color: 'grey'},  // [123, 123]
    {lt: 5}                 // (-Infinity, 5)
]
```

注意，如果两个 piece 的区间重叠，则会自动进行去重。

在每个 piece 中支持的 visualMap 属性有：

- `symbol`: 图元的图形类别。
- `symbolSize`: 图元的大小。
- `color`: 图元的颜色。
- `colorAlpha`: 图元的颜色的透明度。
- `opacity`: 图元以及其附属物（如文字标签）的透明度。
- `colorLightness`: 颜色的明暗度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorSaturation`: 颜色的饱和度，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。
- `colorHue`: 颜色的色调，参见 [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)。

[参见示例](https://echarts.apache.org/examples/zh/editor.html?c=doc-example/map-visualMap-pieces&edit=1&reset=1)

（注：在 ECharts2 中，`pieces` 叫做 `splitList`。现在后者仍兼容，但推荐使用 `pieces`）

`pieces` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](https://echarts.apache.org/zh/option.html#visualMap.inverse)。

#### [visualMap-piecewise.](https://echarts.apache.org/zh/option.html#visualMap-piecewise) [categories](https://echarts.apache.org/zh/option.html#visualMap-piecewise.categories)

Array

用于表示离散型数据（或可以称为类别型数据、枚举型数据）的全集。

当所指定的维度（[visualMap-piecewise.dimension](https://echarts.apache.org/zh/option.html#visualMap-piecewise.dimension)）的数据为离散型数据时，例如数据值为『优』、『良』等，那么可如下配置：

```javascript
categories: ['严重污染', '重度污染', '中度污染', '轻度污染', '良', '优'],
```

[参见示例](https://echarts.apache.org/examples/zh/editor.html?c=doc-example/scatter-visualMap-categories&edit=1&reset=1)

`categories` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](https://echarts.apache.org/zh/option.html#visualMap.inverse)。



### tooltip 提示框组件

`tooltip` **的主要功能**：

1. **显示数据**：当用户将鼠标悬停在某个图表元素上时，显示该元素的相关数据。
2. **格式化内容**：可以自定义显示内容的格式，例如显示多个数据系列的值。
3. **交互性**：支持动态展示和隐藏，能够与其他图表交互配合，提升用户体验。

**提示框组件的通用介绍：**

提示框组件可以设置在多种地方：

- 可以设置在全局，即 [tooltip](https://echarts.apache.org/zh/option.html#tooltip)
- 可以设置在坐标系中，即 [grid.tooltip](https://echarts.apache.org/zh/option.html#grid.tooltip)、[polar.tooltip](https://echarts.apache.org/zh/option.html#polar.tooltip)、[single.tooltip](https://echarts.apache.org/zh/option.html#single.tooltip)
- 可以设置在系列中，即 [series.tooltip](https://echarts.apache.org/zh/option.html#series.tooltip)
- 可以设置在系列的每个数据项中，即 [series.data.tooltip](https://echarts.apache.org/zh/option.html#series.data.tooltip)

#### [tooltip.](https://echarts.apache.org/zh/option.html#tooltip) [trigger](https://echarts.apache.org/zh/option.html#tooltip.trigger) = 'item'

string

触发类型。

可选：

- `'item'`

  数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。

- `'axis'`

  坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。

  在 ECharts 2.x 中只支持类目轴上使用 axis trigger，在 ECharts 3 中支持在[直角坐标系](https://echarts.apache.org/zh/option.html#grid)和[极坐标系](https://echarts.apache.org/zh/option.html#polar)上的所有类型的轴。并且可以通过 [axisPointer.axis](https://echarts.apache.org/zh/option.html#tooltip.axisPointer.axis) 指定坐标轴。

- `'none'`

  什么都不触发。

#### [tooltip.](https://echarts.apache.org/zh/option.html#tooltip) [formatter](https://echarts.apache.org/zh/option.html#tooltip.formatter) 

stringFunction

提示框浮层内容格式器，支持字符串模板和回调函数两种形式。

**1. 字符串模板**

模板变量有 `{a}`, `{b}`，`{c}`，`{d}`，`{e}`，分别表示系列名，数据名，数据值等。 在 [trigger](https://echarts.apache.org/zh/option.html#tooltip.trigger) 为 `'axis'` 的时候，会有多个系列的数据，此时可以通过 `{a0}`, `{a1}`, `{a2}` 这种后面加索引的方式表示系列的索引。 不同图表类型下的 `{a}`，`{b}`，`{c}`，`{d}` 含义不一样。 其中变量`{a}`, `{b}`, `{c}`, `{d}`在不同图表类型下代表数据含义为：

- 折线（区域）图、柱状（条形）图、K线图 : `{a}`（系列名称），`{b}`（类目值），`{c}`（数值）, `{d}`（无）
- 散点图（气泡）图 : `{a}`（系列名称），`{b}`（数据名称），`{c}`（数值数组）, `{d}`（无）
- 地图 : `{a}`（系列名称），`{b}`（区域名称），`{c}`（合并数值）, `{d}`（无）
- 饼图、仪表盘、漏斗图: `{a}`（系列名称），`{b}`（数据项名称），`{c}`（数值）, `{d}`（百分比）

更多其它图表模板变量的含义可以见相应的图表的 label.formatter 配置项。

**示例：**

```ts
formatter: '{b0}: {c0}<br />{b1}: {c1}'
```

**2. 回调函数**

回调函数格式：

```ts
(params: Object|Array, ticket: string, callback: (ticket: string, html: string)) => string | HTMLElement | HTMLElement[]
```

支持返回 HTML 字符串或者创建的 DOM 实例。

第一个参数 `params` 是 formatter 需要的数据集。格式如下：

```ts
{
    componentType: 'series',
    // 系列类型
    seriesType: string,
    // 系列在传入的 option.series 中的 index
    seriesIndex: number,
    // 系列名称
    seriesName: string,
    // 数据名，类目名
    name: string,
    // 数据在传入的 data 数组中的 index
    dataIndex: number,
    // 传入的原始数据项
    data: Object,
    // 传入的数据值。在多数系列下它和 data 相同。在一些系列下是 data 中的分量（如 map、radar 中）
    value: number|Array|Object,
    // 坐标轴 encode 映射信息，
    // key 为坐标轴（如 'x' 'y' 'radius' 'angle' 等）
    // value 必然为数组，不会为 null/undefined，表示 dimension index 。
    // 其内容如：
    // {
    //     x: [2] // dimension index 为 2 的数据映射到 x 轴
    //     y: [0] // dimension index 为 0 的数据映射到 y 轴
    // }
    encode: Object,
    // 维度名列表
    dimensionNames: Array<String>,
    // 数据的维度 index，如 0 或 1 或 2 ...
    // 仅在雷达图中使用。
    dimensionIndex: number,
    // 数据图形的颜色
    color: string,
    // 饼图/漏斗图的百分比
    percent: number,
    // 旭日图中当前节点的祖先节点（包括自身）
    treePathInfo: Array,
    // 树图/矩形树图中当前节点的祖先节点（包括自身）
    treeAncestors: Array,
    // 坐标轴标签文本是否溢出隐藏，可以使用此函数判断是否需要弹出提示框
    isTruncated: Function,
    // 当前坐标轴标签刻度索引
    tickIndex: number
}
```





### dataset 数据集

ECharts 4 开始支持了 `数据集`（`dataset`）组件用于单独的数据集声明，从而数据可以单独管理，被多个组件复用，并且可以自由指定数据到视觉的映射。这在不少场景下能带来使用上的方便。

#### id

#### [dataset.](https://echarts.apache.org/zh/option.html#dataset) [source](https://echarts.apache.org/zh/option.html#dataset.source)

ArrayObject

原始数据。一般来说，原始数据表达的是二维表。可以用如下这些格式表达二维表：

二维数组，其中第一行/列可以给出 [维度名](https://echarts.apache.org/zh/option.html#dataset.dimensions)，也可以不给出，直接就是数据：

```ts
[
    ['product', '2015', '2016', '2017'],
    ['Matcha Latte', 43.3, 85.8, 93.7],
    ['Milk Tea', 83.1, 73.4, 55.1],
    ['Cheese Cocoa', 86.4, 65.2, 82.5],
    ['Walnut Brownie', 72.4, 53.9, 39.1]
]
```

按行的 key-value 形式（对象数组），其中键（key）表明了 [维度名](https://echarts.apache.org/zh/option.html#dataset.dimensions)：

```ts
[
    {product: 'Matcha Latte', count: 823, score: 95.8},
    {product: 'Milk Tea', count: 235, score: 81.4},
    {product: 'Cheese Cocoa', count: 1042, score: 91.2},
    {product: 'Walnut Brownie', count: 988, score: 76.9}
]
```

按列的 key-value 形式，每一项表示二维表的 “一列”：

```ts
{
    'product': ['Matcha Latte', 'Milk Tea', 'Cheese Cocoa', 'Walnut Brownie'],
    'count': [823, 235, 1042, 988],
    'score': [95.8, 81.4, 91.2, 76.9]
}
```

#### [dataset.](https://echarts.apache.org/zh/option.html#dataset) [dimensions](https://echarts.apache.org/zh/option.html#dataset.dimensions) 

Array

使用 dimensions 定义 `series.data` 或者 `dataset.source` 的每个维度的信息。

注意：如果使用了 [dataset](https://echarts.apache.org/zh/option.html#dataset)，那么可以在 [dataset.dimensions](https://echarts.apache.org/zh/option.html#dataset.dimensions) 中定义 dimension ，或者在 [dataset.source](https://echarts.apache.org/zh/option.html#dataset.source) 的第一行/列中给出 dimension 名称。于是就不用在这里指定 dimension。但如果在这里指定了 `dimensions`，那么优先使用这里的。

例如：

```ts
option = {
    dataset: {
        source: [
            // 有了上面 dimensions 定义后，下面这五个维度的名称分别为：
            // 'date', 'open', 'close', 'highest', 'lowest'
            [12, 44, 55, 66, 2],
            [23, 6, 16, 23, 1],
            ...
        ]
    },
    series: {
        type: 'xxx',
        // 定义了每个维度的名称。这个名称会被显示到默认的 tooltip 中。
        dimensions: ['date', 'open', 'close', 'highest', 'lowest']
    }
}

```

```ts
series: {
    type: 'xxx',
    dimensions: [
        null,                // 如果此维度不想给出定义，则使用 null 即可
        {type: 'ordinal'},   // 只定义此维度的类型。
                             // 'ordinal' 表示离散型，一般文本使用这种类型。
                             // 如果类型没有被定义，会自动猜测类型。
        {name: 'good', type: 'number'},
        'bad'                // 等同于 {name: 'bad'}
    ]
}
```

`dimensions` 数组中的每一项可以是：

- `string`，如 `'someName'`，等同于 `{name: 'someName'}`
- `Object`，属性可以有：
  - name: `string`。
  - type: `string`，支持
    - `number`，默认，表示普通数据。
    - `ordinal`，对于类目、文本这些 string 类型的数据，如果需要能在数轴上使用，须是 'ordinal' 类型。ECharts 默认会自动判断这个类型。但是自动判断也是不可能很完备的，所以使用者也可以手动强制指定。
    - `float`，即 [Float64Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array)。
    - `int`，即 [Int32Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array)。
    - `time`，表示时间类型。设置成 'time' 则能支持自动解析数据成时间戳（timestamp），比如该维度的数据是 '2017-05-10'，会自动被解析。时间类型的支持参见 [data](https://echarts.apache.org/zh/option.html#series.data)。
  - displayName: 一般用于 tooltip 中维度名的展示。`string` 如果没有指定，默认使用 name 来展示。

值得一提的是，当定义了 `dimensions` 后，默认 `tooltip` 中对个维度的显示，会变为『竖排』，从而方便显示每个维度的名称。如果没有定义 `dimensions`，则默认 `tooltip` 会横排显示，且只显示数值没有维度名称可显示。

#### [dataset.](https://echarts.apache.org/zh/option.html#dataset) [sourceHeader](https://echarts.apache.org/zh/option.html#dataset.sourceHeader) 

boolean number

`dataset.source` 第一行/列是否是 [维度名](https://echarts.apache.org/zh/option.html#dataset.dimensions) 信息。可选值：

- `null/undefined/'auto'`：默认，自动探测。
- `true`：第一行/列是维度名信息。
- `false`：第一行/列直接开始是数据。
- `number`: 维度名行/列数，也就是数据行/列的开始索引。例如：`sourceHeader: 2` 意味着前两行/列为维度名，从第三行/列开始为数据。

注意：“第一行/列” 的意思是，如果 [series.seriesLayoutBy](https://echarts.apache.org/zh/option.html#series.seriesLayoutBy) 设置为 `'column'`（默认值），则取第一行，如果 `series.seriesLayoutBy` 设置为 `'row'`，则取第一列。

#### [dataset.](https://echarts.apache.org/zh/option.html#dataset) [transform](https://echarts.apache.org/zh/option.html#dataset.transform)

Array

参见 [数据变换教程](https://echarts.apache.org/handbook/zh/concepts/data-transform)

##### 所有属性

{ [transform-filter](https://echarts.apache.org/zh/option.html#dataset.transform-filter) , [transform-sort](https://echarts.apache.org/zh/option.html#dataset.transform-sort) , [transform-xxx:xxx](https://echarts.apache.org/zh/option.html#dataset.transform-xxx:xxx) }



### series 系列

系列是用来定义图表中各个数据系列的配置项。每个 `series` 对应一个图表中的数据系列，可以是折线图、柱状图、饼图等不同类型的图形。每个 `series` 配置项包含了数据、样式、图表类型等信息，决定了图表中如何展示数据。

### series-line 折线图

```ts
option = {
  xAxis: {
    type: "category",
    data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
  },
  yAxis: {},
  series: [{
    data: [820, 932, 901, 934, 1290, 1330, 1320],
    type: "line"
  }]
}
```

#### [series-line.](https://echarts.apache.org/zh/option.html#series-line) [data](https://echarts.apache.org/zh/option.html#series-line.data)

Array

系列中的数据内容数组。数组项通常为具体的数据项。

注意，如果系列没有指定 `data`，并且 option 有 [dataset](https://echarts.apache.org/zh/option.html#dataset)，那么默认使用第一个 [dataset](https://echarts.apache.org/zh/option.html#dataset)。如果指定了 `data`，则不会再使用 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

可以使用 `series.datasetIndex` 指定其他的 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

通常来说，数据用一个二维数组表示。如下，每一列被称为一个『维度』。

```ts
series: [{
    data: [
        // 维度X   维度Y   其他维度 ...
        [  3.4,    4.5,   15,   43],
        [  4.2,    2.3,   20,   91],
        [  10.8,   9.5,   30,   18],
        [  7.2,    8.8,   18,   57]
    ]
}]
```

- 在 [直角坐标系 (grid)](https://echarts.apache.org/zh/option.html#grid) 中『维度X』和『维度Y』会默认对应于 [xAxis](https://echarts.apache.org/zh/option.html#xAxis) 和 [yAxis](https://echarts.apache.org/zh/option.html#yAxis)。
- 在 [极坐标系 (polar)](https://echarts.apache.org/zh/option.html#polar) 中『维度X』和『维度Y』会默认对应于 [radiusAxis](https://echarts.apache.org/zh/option.html#radiusAxis) 和 [angleAxis](https://echarts.apache.org/zh/option.html#angleAxis)。
- 后面的其他维度是可选的，可以在别处被使用，例如：
  - 在 [visualMap](https://echarts.apache.org/zh/option.html#visualMap) 中可以将一个或多个维度映射到颜色，大小等多个图形属性上。
  - 在 [series.symbolSize](https://echarts.apache.org/zh/option.html#series.symbolSize) 中可以使用回调函数，基于某个维度得到 symbolSize 值。
  - 使用 [tooltip.formatter](https://echarts.apache.org/zh/option.html#tooltip.formatter) 或 [series.label.formatter](https://echarts.apache.org/zh/option.html#series.label.formatter) 可以把其他维度的值展示出来。

特别地，当只有一个轴为类目轴（axis.type 为 `'category'`）的时候，数据可以简化用一个一维数组表示。例如：

```ts
xAxis: {
    data: ['a', 'b', 'm', 'n']
},
series: [{
    // 与 xAxis.data 一一对应。
    data: [23,  44,  55,  19]
    // 它其实是下面这种形式的简化：
    // data: [[0, 23], [1, 44], [2, 55], [3, 19]]
}]
```

**『值』与 [轴类型](https://echarts.apache.org/zh/option.html#xAxis.type) 的关系：**

- 当某维度对应于数值轴（axis.type 为 `'value'` 或者 `'log'`）的时候：

  其值可以为 `number`（例如 `12`）。（也可以兼容 `string` 形式的 number，例如 `'12'`）

- 当某维度对应于类目轴（axis.type 为 `'category'`）的时候：

  其值须为类目的『序数』（从 `0` 开始）或者类目的『字符串值』。例如：

  ```ts
    xAxis: {
        type: 'category',
        data: ['星期一', '星期二', '星期三', '星期四']
    },
    yAxis: {
        type: 'category',
        data: ['a', 'b', 'm', 'n', 'p', 'q']
    },
    series: [{
        data: [
            // xAxis    yAxis
            [  0,        0,    2  ], // 意思是此点位于 xAxis: '星期一', yAxis: 'a'。
            [  '星期四',  2,    1  ], // 意思是此点位于 xAxis: '星期四', yAxis: 'm'。
            [  2,       'p',   2  ], // 意思是此点位于 xAxis: '星期三', yAxis: 'p'。
            [  3,        3,    5  ]
        ]
    }]
  ```

  双类目轴的示例可以参考 [Github Punchcard](https://echarts.apache.org/examples/zh/editor.html?c=scatter-punchCard) 示例。

- 当某维度对应于时间轴（type 为 `'time'`）的时候，值可以为：

  - 一个时间戳，如 `1484141700832`，表示 UTC 时间。
  - 或者字符串形式的时间描述：
    - ISO 8601 的子集，只包含这些形式（这几种格式，除非指明时区，否则均表示本地时间，与moment一致）：
      - 部分年月日时间: `'2012-03'`, `'2012-03-01'`, `'2012-03-01 05'`, `'2012-03-01 05:06'`.
      - 使用 `'T'` 或空格分割: `'2012-03-01T12:22:33.123'`, `'2012-03-01 12:22:33.123'`.
      - 时区设定: `'2012-03-01T12:22:33Z'`, `'2012-03-01T12:22:33+8000'`, `'2012-03-01T12:22:33-05:00'`.
    - 其他的时间字符串，包括（均表示本地时间）: `'2012'`, `'2012-3-1'`, `'2012/3/1'`, `'2012/03/01'`, `'2009/6/12 2:00'`, `'2009/6/12 2:05:08'`, `'2009/6/12 2:05:08.123'`
  - 或者用户自行初始化的 Date 实例：
    - 注意，用户自行初始化 Date 实例的时候，[浏览器的行为有差异，不同字符串的表示也不同](https://dygraphs.com/date-formats.html)。
    - 例如：在 chrome 中，`new Date('2012-01-01')` 表示 UTC 时间的 2012 年 1 月 1 日，而 `new Date('2012-1-1')` 和 `new Date('2012/01/01')` 表示本地时间的 2012 年 1 月 1 日。在 safari 中，不支持 `new Date('2012-1-1')` 这种表示方法。
    - 所以，使用 `new Date(dataString)` 时，可使用第三方库解析（如 [moment](https://momentjs.com/)），或者使用 `echarts.time.parse`，或者参见 [这里](https://dygraphs.com/date-formats.html)。

**当需要对个别数据进行个性化定义时：**

数组项可用对象，其中的 `value` 像表示具体的数值，如：

```ts
[
    12,
    34,
    {
        value : 56,
        //自定义标签样式，仅对该数据项有效
        label: {},
        //自定义特殊 itemStyle，仅对该数据项有效
        itemStyle:{}
    },
    10
]
// 或
[
    [12, 33],
    [34, 313],
    {
        value: [56, 44],
        label: {},
        itemStyle:{}
    },
    [10, 33]
]
```

**空值：**

当某数据不存在时（ps：*不存在*不代表值为 0），可以用 `'-'` 或者 `null` 或者 `undefined` 或者 `NaN` 表示。

例如，无数据在折线图中可表现为该点是断开的，在其它图中可表示为图形不存在。

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-line.data.name) , [value](https://echarts.apache.org/zh/option.html#series-line.data.value) , [groupId](https://echarts.apache.org/zh/option.html#series-line.data.groupId) , [childGroupId](https://echarts.apache.org/zh/option.html#series-line.data.childGroupId) , [symbol](https://echarts.apache.org/zh/option.html#series-line.data.symbol) , [symbolSize](https://echarts.apache.org/zh/option.html#series-line.data.symbolSize) , [symbolRotate](https://echarts.apache.org/zh/option.html#series-line.data.symbolRotate) , [symbolKeepAspect](https://echarts.apache.org/zh/option.html#series-line.data.symbolKeepAspect) , [symbolOffset](https://echarts.apache.org/zh/option.html#series-line.data.symbolOffset) , [label](https://echarts.apache.org/zh/option.html#series-line.data.label) , [labelLine](https://echarts.apache.org/zh/option.html#series-line.data.labelLine) , [itemStyle](https://echarts.apache.org/zh/option.html#series-line.data.itemStyle) , [emphasis](https://echarts.apache.org/zh/option.html#series-line.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-line.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-line.data.select) , [tooltip](https://echarts.apache.org/zh/option.html#series-line.data.tooltip) }

### series-bar 柱状图

```ts
option = {
  tooltip: {},
  legend: {},
  xAxis: {
    data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
  },
  yAxis: {},
  series: [{
    name: "Sale",
    type: "bar",
    data: [5, 20, 36, 10, 10, 20, 4]
  }]
}
```

#### [series-bar.](https://echarts.apache.org/zh/option.html#series-bar) [data](https://echarts.apache.org/zh/option.html#series-bar.data) 

Array

系列中的数据内容数组。数组项通常为具体的数据项。

注意，如果系列没有指定 `data`，并且 option 有 [dataset](https://echarts.apache.org/zh/option.html#dataset)，那么默认使用第一个 [dataset](https://echarts.apache.org/zh/option.html#dataset)。如果指定了 `data`，则不会再使用 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

可以使用 `series.datasetIndex` 指定其他的 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

通常来说，数据用一个二维数组表示。如下，每一列被称为一个『维度』。

```ts
series: [{
    data: [
        // 维度X   维度Y   其他维度 ...
        [  3.4,    4.5,   15,   43],
        [  4.2,    2.3,   20,   91],
        [  10.8,   9.5,   30,   18],
        [  7.2,    8.8,   18,   57]
    ]
}]
```

- 在 [直角坐标系 (grid)](https://echarts.apache.org/zh/option.html#grid) 中『维度X』和『维度Y』会默认对应于 [xAxis](https://echarts.apache.org/zh/option.html#xAxis) 和 [yAxis](https://echarts.apache.org/zh/option.html#yAxis)。
- 在 [极坐标系 (polar)](https://echarts.apache.org/zh/option.html#polar) 中『维度X』和『维度Y』会默认对应于 [radiusAxis](https://echarts.apache.org/zh/option.html#radiusAxis) 和 [angleAxis](https://echarts.apache.org/zh/option.html#angleAxis)。
- 后面的其他维度是可选的，可以在别处被使用，例如：
  - 在 [visualMap](https://echarts.apache.org/zh/option.html#visualMap) 中可以将一个或多个维度映射到颜色，大小等多个图形属性上。
  - 在 [series.symbolSize](https://echarts.apache.org/zh/option.html#series.symbolSize) 中可以使用回调函数，基于某个维度得到 symbolSize 值。
  - 使用 [tooltip.formatter](https://echarts.apache.org/zh/option.html#tooltip.formatter) 或 [series.label.formatter](https://echarts.apache.org/zh/option.html#series.label.formatter) 可以把其他维度的值展示出来。

特别地，当只有一个轴为类目轴（axis.type 为 `'category'`）的时候，数据可以简化用一个一维数组表示。例如：

```ts
xAxis: {
    data: ['a', 'b', 'm', 'n']
},
series: [{
    // 与 xAxis.data 一一对应。
    data: [23,  44,  55,  19]
    // 它其实是下面这种形式的简化：
    // data: [[0, 23], [1, 44], [2, 55], [3, 19]]
}]
```

**『值』与 [轴类型](https://echarts.apache.org/zh/option.html#xAxis.type) 的关系：**

- 当某维度对应于数值轴（axis.type 为 `'value'` 或者 `'log'`）的时候：

  其值可以为 `number`（例如 `12`）。（也可以兼容 `string` 形式的 number，例如 `'12'`）

- 当某维度对应于类目轴（axis.type 为 `'category'`）的时候：

  其值须为类目的『序数』（从 `0` 开始）或者类目的『字符串值』。例如：

  ```ts
    xAxis: {
        type: 'category',
        data: ['星期一', '星期二', '星期三', '星期四']
    },
    yAxis: {
        type: 'category',
        data: ['a', 'b', 'm', 'n', 'p', 'q']
    },
    series: [{
        data: [
            // xAxis    yAxis
            [  0,        0,    2  ], // 意思是此点位于 xAxis: '星期一', yAxis: 'a'。
            [  '星期四',  2,    1  ], // 意思是此点位于 xAxis: '星期四', yAxis: 'm'。
            [  2,       'p',   2  ], // 意思是此点位于 xAxis: '星期三', yAxis: 'p'。
            [  3,        3,    5  ]
        ]
    }]
  ```

  双类目轴的示例可以参考 [Github Punchcard](https://echarts.apache.org/examples/zh/editor.html?c=scatter-punchCard) 示例。

- 当某维度对应于时间轴（type 为 `'time'`）的时候，值可以为：

  - 一个时间戳，如 `1484141700832`，表示 UTC 时间。
  - 或者字符串形式的时间描述：
    - ISO 8601 的子集，只包含这些形式（这几种格式，除非指明时区，否则均表示本地时间，与moment一致）：
      - 部分年月日时间: `'2012-03'`, `'2012-03-01'`, `'2012-03-01 05'`, `'2012-03-01 05:06'`.
      - 使用 `'T'` 或空格分割: `'2012-03-01T12:22:33.123'`, `'2012-03-01 12:22:33.123'`.
      - 时区设定: `'2012-03-01T12:22:33Z'`, `'2012-03-01T12:22:33+8000'`, `'2012-03-01T12:22:33-05:00'`.
    - 其他的时间字符串，包括（均表示本地时间）: `'2012'`, `'2012-3-1'`, `'2012/3/1'`, `'2012/03/01'`, `'2009/6/12 2:00'`, `'2009/6/12 2:05:08'`, `'2009/6/12 2:05:08.123'`
  - 或者用户自行初始化的 Date 实例：
    - 注意，用户自行初始化 Date 实例的时候，[浏览器的行为有差异，不同字符串的表示也不同](https://dygraphs.com/date-formats.html)。
    - 例如：在 chrome 中，`new Date('2012-01-01')` 表示 UTC 时间的 2012 年 1 月 1 日，而 `new Date('2012-1-1')` 和 `new Date('2012/01/01')` 表示本地时间的 2012 年 1 月 1 日。在 safari 中，不支持 `new Date('2012-1-1')` 这种表示方法。
    - 所以，使用 `new Date(dataString)` 时，可使用第三方库解析（如 [moment](https://momentjs.com/)），或者使用 `echarts.time.parse`，或者参见 [这里](https://dygraphs.com/date-formats.html)。

**当需要对个别数据进行个性化定义时：**

数组项可用对象，其中的 `value` 像表示具体的数值，如：

```ts
[
    12,
    34,
    {
        value : 56,
        //自定义标签样式，仅对该数据项有效
        label: {},
        //自定义特殊 itemStyle，仅对该数据项有效
        itemStyle:{}
    },
    10
]
// 或
[
    [12, 33],
    [34, 313],
    {
        value: [56, 44],
        label: {},
        itemStyle:{}
    },
    [10, 33]
]
```

**空值：**

当某数据不存在时（ps：*不存在*不代表值为 0），可以用 `'-'` 或者 `null` 或者 `undefined` 或者 `NaN` 表示。

例如，无数据在折线图中可表现为该点是断开的，在其它图中可表示为图形不存在。

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-bar.data.name) , [value](https://echarts.apache.org/zh/option.html#series-bar.data.value) , [groupId](https://echarts.apache.org/zh/option.html#series-bar.data.groupId) , [childGroupId](https://echarts.apache.org/zh/option.html#series-bar.data.childGroupId) , [label](https://echarts.apache.org/zh/option.html#series-bar.data.label) , [labelLine](https://echarts.apache.org/zh/option.html#series-bar.data.labelLine) , [itemStyle](https://echarts.apache.org/zh/option.html#series-bar.data.itemStyle) , [emphasis](https://echarts.apache.org/zh/option.html#series-bar.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-bar.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-bar.data.select) }

### series-pie 饼图

```ts
option = {
  legend: {
    orient: "vertical",
    left: "left",
    data: ["Apple", "Grapes", "Pineapples", "Oranges", "Bananas"]
  },
  series: [{
    type: "pie",
    data: [{
      value: 335,
      name: "Apple"
    }, {
      value: 310,
      name: "Grapes"
    }, {
      value: 234,
      name: "Pineapples"
    }, {
      value: 135,
      name: "Oranges"
    }, {
      value: 1548,
      name: "Bananas"
    }]
  }]
}
```

#### [series-pie.](https://echarts.apache.org/zh/option.html#series-pie) [data](https://echarts.apache.org/zh/option.html#series-pie.data) 

Array

系列中的数据内容数组。数组项可以为单个数值，如：

```ts
[12, 34, 56, 10, 23]
```

如果需要在数据中加入其它维度给 [visualMap](https://echarts.apache.org/zh/option.html#visualMap) 组件用来映射到颜色等其它图形属性。每个数据项也可以是数组，如：

```ts
[[12, 14], [34, 50], [56, 30], [10, 15], [23, 10]]
```

这时候可以将每项数组中的第二个值指定给 [visualMap](https://echarts.apache.org/zh/option.html#visualMap) 组件。

更多时候我们需要指定每个数据项的名称，这时候需要每个项为一个对象：

```ts
[{
    // 数据项的名称
    name: '数据1',
    // 数据项值8
    value: 10
}, {
    name: '数据2',
    value: 20
}]
```

需要对个别内容指定进行个性化定义时：

```ts
[{
    name: '数据1',
    value: 10
}, {
    // 数据项名称
    name: '数据2',
    value : 56,
    //自定义特殊 tooltip，仅对该数据项有效
    tooltip:{},
    //自定义特殊itemStyle，仅对该item有效
    itemStyle:{}
}]
```

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-pie.data.name) , [value](https://echarts.apache.org/zh/option.html#series-pie.data.value) , [groupId](https://echarts.apache.org/zh/option.html#series-pie.data.groupId) , [childGroupId](https://echarts.apache.org/zh/option.html#series-pie.data.childGroupId) , [selected](https://echarts.apache.org/zh/option.html#series-pie.data.selected) , [label](https://echarts.apache.org/zh/option.html#series-pie.data.label) , [labelLine](https://echarts.apache.org/zh/option.html#series-pie.data.labelLine) , [itemStyle](https://echarts.apache.org/zh/option.html#series-pie.data.itemStyle) , [emphasis](https://echarts.apache.org/zh/option.html#series-pie.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-pie.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-pie.data.select) , [tooltip](https://echarts.apache.org/zh/option.html#series-pie.data.tooltip) }

### series-scatter 散点图

```ts
option = {
  legend: {},
  grid: {
    left: "3%",
    right: "7%",
    bottom: "3%",
    containLabel: true
  },
  xAxis: {
    type: "value",
    scale: true,
    axisLabel: {
      formatter: "{value} cm"
    },
    splitLine: {
      show: false
    }
  },
  yAxis: {
    type: "value",
    scale: true,
    axisLabel: {
      formatter: "{value} kg"
    },
    splitLine: {
      show: false
    }
  },
  series: [{
    name: "Male",
    type: "scatter",
    data: [
      [174, 65.6],
      [175.3, 71.8],
      [193.5, 80.7],
      [186.5, 72.6],
      [187.2, 78.8],
      [181.5, 74.8],
      [184, 86.4],
      [184.5, 78.4],
      [175, 62],
      [184, 81.6],
      [180, 76.6],
      [177.8, 83.6],
      [192, 90],
      [176, 74.6],
      [174, 71],
      [184, 79.6],
      [192.7, 93.8],
      [171.5, 70],
      [173, 72.4],
      [176, 85.9],
      [176, 78.8],
      [180.5, 77.8],
      [172.7, 66.2],
      [176, 86.4],
      [173.5, 81.8],
      [178, 89.6],
      [180.3, 82.8],
      [180.3, 76.4],
      [164.5, 63.2],
      [173, 60.9],
      [183.5, 74.8],
      [175.5, 70],
      [188, 72.4],
      [189.2, 84.1],
      [172.8, 69.1],
      [170, 59.5],
      [182, 67.2],
      [170, 61.3],
      [177.8, 68.6],
      [184.2, 80.1],
      [186.7, 87.8],
      [171.4, 84.7],
      [172.7, 73.4],
      [175.3, 72.1],
      [180.3, 82.6],
      [182.9, 88.7],
      [188, 84.1],
      [177.2, 94.1],
      [172.1, 74.9],
      [167, 59.1],
      [169.5, 75.6],
      [174, 86.2],
      [172.7, 75.3],
      [182.2, 87.1],
      [164.1, 55.2],
      [163, 57],
      [171.5, 61.4],
      [184.2, 76.8],
      [174, 86.8],
      [174, 72.2],
      [177, 71.6],
      [186, 84.8],
      [167, 68.2],
      [171.8, 66.1],
      [182, 72],
      [167, 64.6],
      [177.8, 74.8],
      [164.5, 70],
      [192, 101.6],
      [175.5, 63.2],
      [171.2, 79.1],
      [181.6, 78.9],
      [167.4, 67.7],
      [181.1, 66],
      [177, 68.2],
      [174.5, 63.9],
      [177.5, 72],
      [170.5, 56.8],
      [182.4, 74.5],
      [197.1, 90.9],
      [180.1, 93],
      [175.5, 80.9],
      [180.6, 72.7],
      [184.4, 68],
      [175.5, 70.9],
      [180.6, 72.5],
      [177, 72.5],
      [177.1, 83.4],
      [181.6, 75.5],
      [176.5, 73],
      [175, 70.2],
      [174, 73.4],
      [165.1, 70.5],
      [177, 68.9],
      [192, 102.3],
      [176.5, 68.4],
      [169.4, 65.9],
      [182.1, 75.7],
      [179.8, 84.5],
      [175.3, 87.7],
      [184.9, 86.4],
      [177.3, 73.2],
      [167.4, 53.9],
      [178.1, 72],
      [168.9, 55.5],
      [157.2, 58.4],
      [180.3, 83.2],
      [170.2, 72.7],
      [177.8, 64.1],
      [172.7, 72.3],
      [165.1, 65],
      [186.7, 86.4],
      [165.1, 65],
      [174, 88.6],
      [175.3, 84.1],
      [185.4, 66.8],
      [177.8, 75.5],
      [180.3, 93.2],
      [180.3, 82.7],
      [177.8, 58],
      [177.8, 79.5],
      [177.8, 78.6],
      [177.8, 71.8],
      [177.8, 116.4],
      [163.8, 72.2],
      [188, 83.6],
      [198.1, 85.5],
      [175.3, 90.9],
      [166.4, 85.9],
      [190.5, 89.1],
      [166.4, 75],
      [177.8, 77.7],
      [179.7, 86.4],
      [172.7, 90.9],
      [190.5, 73.6],
      [185.4, 76.4],
      [168.9, 69.1],
      [167.6, 84.5],
      [175.3, 64.5],
      [170.2, 69.1],
      [190.5, 108.6],
      [177.8, 86.4],
      [190.5, 80.9],
      [177.8, 87.7],
      [184.2, 94.5],
      [176.5, 80.2],
      [177.8, 72],
      [180.3, 71.4],
      [171.4, 72.7],
      [172.7, 84.1],
      [172.7, 76.8],
      [177.8, 63.6],
      [177.8, 80.9],
      [182.9, 80.9],
      [170.2, 85.5],
      [167.6, 68.6],
      [175.3, 67.7],
      [165.1, 66.4],
      [185.4, 102.3],
      [181.6, 70.5],
      [172.7, 95.9],
      [190.5, 84.1],
      [179.1, 87.3],
      [175.3, 71.8],
      [170.2, 65.9],
      [193, 95.9],
      [171.4, 91.4],
      [177.8, 81.8],
      [177.8, 96.8],
      [167.6, 69.1],
      [167.6, 82.7],
      [180.3, 75.5],
      [182.9, 79.5],
      [176.5, 73.6],
      [186.7, 91.8],
      [188, 84.1],
      [188, 85.9],
      [177.8, 81.8],
      [174, 82.5],
      [177.8, 80.5],
      [171.4, 70],
      [185.4, 81.8],
      [185.4, 84.1],
      [188, 90.5],
      [188, 91.4],
      [182.9, 89.1],
      [176.5, 85],
      [175.3, 69.1],
      [175.3, 73.6],
      [188, 80.5],
      [188, 82.7],
      [175.3, 86.4],
      [170.5, 67.7],
      [179.1, 92.7],
      [177.8, 93.6],
      [175.3, 70.9],
      [182.9, 75],
      [170.8, 93.2],
      [188, 93.2],
      [180.3, 77.7],
      [177.8, 61.4],
      [185.4, 94.1],
      [168.9, 75],
      [185.4, 83.6],
      [180.3, 85.5],
      [174, 73.9],
      [167.6, 66.8],
      [182.9, 87.3],
      [160, 72.3],
      [180.3, 88.6],
      [167.6, 75.5],
      [186.7, 101.4],
      [175.3, 91.1],
      [175.3, 67.3],
      [175.9, 77.7],
      [175.3, 81.8],
      [179.1, 75.5],
      [181.6, 84.5],
      [177.8, 76.6],
      [182.9, 85],
      [177.8, 102.5],
      [184.2, 77.3],
      [179.1, 71.8],
      [176.5, 87.9],
      [188, 94.3],
      [174, 70.9],
      [167.6, 64.5],
      [170.2, 77.3],
      [167.6, 72.3],
      [188, 87.3],
      [174, 80],
      [176.5, 82.3],
      [180.3, 73.6],
      [167.6, 74.1],
      [188, 85.9],
      [180.3, 73.2],
      [167.6, 76.3],
      [183, 65.9],
      [183, 90.9],
      [179.1, 89.1],
      [170.2, 62.3],
      [177.8, 82.7],
      [179.1, 79.1],
      [190.5, 98.2],
      [177.8, 84.1],
      [180.3, 83.2],
      [180.3, 83.2]
    ]
  }]
}
```

#### [series-scatter.](https://echarts.apache.org/zh/option.html#series-scatter) [data](https://echarts.apache.org/zh/option.html#series-scatter.data) 

Array

系列中的数据内容数组。数组项通常为具体的数据项。

注意，如果系列没有指定 `data`，并且 option 有 [dataset](https://echarts.apache.org/zh/option.html#dataset)，那么默认使用第一个 [dataset](https://echarts.apache.org/zh/option.html#dataset)。如果指定了 `data`，则不会再使用 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

可以使用 `series.datasetIndex` 指定其他的 [dataset](https://echarts.apache.org/zh/option.html#dataset)。

通常来说，数据用一个二维数组表示。如下，每一列被称为一个『维度』。

```ts
series: [{
    data: [
        // 维度X   维度Y   其他维度 ...
        [  3.4,    4.5,   15,   43],
        [  4.2,    2.3,   20,   91],
        [  10.8,   9.5,   30,   18],
        [  7.2,    8.8,   18,   57]
    ]
}]
```

- 在 [直角坐标系 (grid)](https://echarts.apache.org/zh/option.html#grid) 中『维度X』和『维度Y』会默认对应于 [xAxis](https://echarts.apache.org/zh/option.html#xAxis) 和 [yAxis](https://echarts.apache.org/zh/option.html#yAxis)。
- 在 [极坐标系 (polar)](https://echarts.apache.org/zh/option.html#polar) 中『维度X』和『维度Y』会默认对应于 [radiusAxis](https://echarts.apache.org/zh/option.html#radiusAxis) 和 [angleAxis](https://echarts.apache.org/zh/option.html#angleAxis)。
- 后面的其他维度是可选的，可以在别处被使用，例如：
  - 在 [visualMap](https://echarts.apache.org/zh/option.html#visualMap) 中可以将一个或多个维度映射到颜色，大小等多个图形属性上。
  - 在 [series.symbolSize](https://echarts.apache.org/zh/option.html#series.symbolSize) 中可以使用回调函数，基于某个维度得到 symbolSize 值。
  - 使用 [tooltip.formatter](https://echarts.apache.org/zh/option.html#tooltip.formatter) 或 [series.label.formatter](https://echarts.apache.org/zh/option.html#series.label.formatter) 可以把其他维度的值展示出来。

特别地，当只有一个轴为类目轴（axis.type 为 `'category'`）的时候，数据可以简化用一个一维数组表示。例如：

```ts
xAxis: {
    data: ['a', 'b', 'm', 'n']
},
series: [{
    // 与 xAxis.data 一一对应。
    data: [23,  44,  55,  19]
    // 它其实是下面这种形式的简化：
    // data: [[0, 23], [1, 44], [2, 55], [3, 19]]
}]
```

**『值』与 [轴类型](https://echarts.apache.org/zh/option.html#xAxis.type) 的关系：**

- 当某维度对应于数值轴（axis.type 为 `'value'` 或者 `'log'`）的时候：

  其值可以为 `number`（例如 `12`）。（也可以兼容 `string` 形式的 number，例如 `'12'`）

- 当某维度对应于类目轴（axis.type 为 `'category'`）的时候：

  其值须为类目的『序数』（从 `0` 开始）或者类目的『字符串值』。例如：

  ```ts
    xAxis: {
        type: 'category',
        data: ['星期一', '星期二', '星期三', '星期四']
    },
    yAxis: {
        type: 'category',
        data: ['a', 'b', 'm', 'n', 'p', 'q']
    },
    series: [{
        data: [
            // xAxis    yAxis
            [  0,        0,    2  ], // 意思是此点位于 xAxis: '星期一', yAxis: 'a'。
            [  '星期四',  2,    1  ], // 意思是此点位于 xAxis: '星期四', yAxis: 'm'。
            [  2,       'p',   2  ], // 意思是此点位于 xAxis: '星期三', yAxis: 'p'。
            [  3,        3,    5  ]
        ]
    }]
  ```

  双类目轴的示例可以参考 [Github Punchcard](https://echarts.apache.org/examples/zh/editor.html?c=scatter-punchCard) 示例。

- 当某维度对应于时间轴（type 为 `'time'`）的时候，值可以为：

  - 一个时间戳，如 `1484141700832`，表示 UTC 时间。
  - 或者字符串形式的时间描述：
    - ISO 8601 的子集，只包含这些形式（这几种格式，除非指明时区，否则均表示本地时间，与moment一致）：
      - 部分年月日时间: `'2012-03'`, `'2012-03-01'`, `'2012-03-01 05'`, `'2012-03-01 05:06'`.
      - 使用 `'T'` 或空格分割: `'2012-03-01T12:22:33.123'`, `'2012-03-01 12:22:33.123'`.
      - 时区设定: `'2012-03-01T12:22:33Z'`, `'2012-03-01T12:22:33+8000'`, `'2012-03-01T12:22:33-05:00'`.
    - 其他的时间字符串，包括（均表示本地时间）: `'2012'`, `'2012-3-1'`, `'2012/3/1'`, `'2012/03/01'`, `'2009/6/12 2:00'`, `'2009/6/12 2:05:08'`, `'2009/6/12 2:05:08.123'`
  - 或者用户自行初始化的 Date 实例：
    - 注意，用户自行初始化 Date 实例的时候，[浏览器的行为有差异，不同字符串的表示也不同](https://dygraphs.com/date-formats.html)。
    - 例如：在 chrome 中，`new Date('2012-01-01')` 表示 UTC 时间的 2012 年 1 月 1 日，而 `new Date('2012-1-1')` 和 `new Date('2012/01/01')` 表示本地时间的 2012 年 1 月 1 日。在 safari 中，不支持 `new Date('2012-1-1')` 这种表示方法。
    - 所以，使用 `new Date(dataString)` 时，可使用第三方库解析（如 [moment](https://momentjs.com/)），或者使用 `echarts.time.parse`，或者参见 [这里](https://dygraphs.com/date-formats.html)。

**当需要对个别数据进行个性化定义时：**

数组项可用对象，其中的 `value` 像表示具体的数值，如：

```ts
[
    12,
    34,
    {
        value : 56,
        //自定义标签样式，仅对该数据项有效
        label: {},
        //自定义特殊 itemStyle，仅对该数据项有效
        itemStyle:{}
    },
    10
]
// 或
[
    [12, 33],
    [34, 313],
    {
        value: [56, 44],
        label: {},
        itemStyle:{}
    },
    [10, 33]
]
```

**空值：**

当某数据不存在时（ps：*不存在*不代表值为 0），可以用 `'-'` 或者 `null` 或者 `undefined` 或者 `NaN` 表示。

例如，无数据在折线图中可表现为该点是断开的，在其它图中可表示为图形不存在。

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-scatter.data.name) , [value](https://echarts.apache.org/zh/option.html#series-scatter.data.value) , [groupId](https://echarts.apache.org/zh/option.html#series-scatter.data.groupId) , [childGroupId](https://echarts.apache.org/zh/option.html#series-scatter.data.childGroupId) , [symbol](https://echarts.apache.org/zh/option.html#series-scatter.data.symbol) , [symbolSize](https://echarts.apache.org/zh/option.html#series-scatter.data.symbolSize) , [symbolRotate](https://echarts.apache.org/zh/option.html#series-scatter.data.symbolRotate) , [symbolKeepAspect](https://echarts.apache.org/zh/option.html#series-scatter.data.symbolKeepAspect) , [symbolOffset](https://echarts.apache.org/zh/option.html#series-scatter.data.symbolOffset) , [label](https://echarts.apache.org/zh/option.html#series-scatter.data.label) , [labelLine](https://echarts.apache.org/zh/option.html#series-scatter.data.labelLine) , [itemStyle](https://echarts.apache.org/zh/option.html#series-scatter.data.itemStyle) , [emphasis](https://echarts.apache.org/zh/option.html#series-scatter.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-scatter.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-scatter.data.select) , [tooltip](https://echarts.apache.org/zh/option.html#series-scatter.data.tooltip) }

### sereis-radar 雷达图

```ts
option = {
  title: {
    text: "基础雷达图"
  },
  tooltip: {},
  legend: {
    data: ["Allocated Budget", "Actual Spending"]
  },
  radar: {
    indicator: [{
      name: "sales",
      max: 6500
    }, {
      name: "Administration",
      max: 16000
    }, {
      name: "Information Techology",
      max: 30000
    }, {
      name: "Customer Support",
      max: 38000
    }, {
      name: "Development",
      max: 52000
    }, {
      name: "Marketing",
      max: 25000
    }]
  },
  series: [{
    name: "预算 vs 开销（Budget vs spending）",
    type: "radar",
    data: [{
      value: [4300, 10000, 28000, 35000, 50000, 19000],
      name: "Allocated Budget"
    }, {
      value: [5000, 14000, 28000, 31000, 42000, 21000],
      name: "Actual Spending"
    }]
  }]
}
```

#### [series-radar.](https://echarts.apache.org/zh/option.html#series-radar) [data](https://echarts.apache.org/zh/option.html#series-radar.data) 

Array

雷达图的数据是多变量（维度）的，如下示例：

```ts
data : [
    {
        value : [4300, 10000, 28000, 35000, 50000, 19000],
        name : '预算分配（Allocated Budget）'
    },
    {
        value : [5000, 14000, 28000, 31000, 42000, 21000],
        name : '实际开销（Actual Spending）'
    }
]
```

其中的`value`项数组是具体的数据，每个值跟 [radar.indicator](https://echarts.apache.org/zh/option.html#radar.indicator) 一一对应。

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-radar.data.name) , [value](https://echarts.apache.org/zh/option.html#series-radar.data.value) , [groupId](https://echarts.apache.org/zh/option.html#series-radar.data.groupId) , [childGroupId](https://echarts.apache.org/zh/option.html#series-radar.data.childGroupId) , [symbol](https://echarts.apache.org/zh/option.html#series-radar.data.symbol) , [symbolSize](https://echarts.apache.org/zh/option.html#series-radar.data.symbolSize) , [symbolRotate](https://echarts.apache.org/zh/option.html#series-radar.data.symbolRotate) , [symbolKeepAspect](https://echarts.apache.org/zh/option.html#series-radar.data.symbolKeepAspect) , [symbolOffset](https://echarts.apache.org/zh/option.html#series-radar.data.symbolOffset) , [label](https://echarts.apache.org/zh/option.html#series-radar.data.label) , [itemStyle](https://echarts.apache.org/zh/option.html#series-radar.data.itemStyle) , [lineStyle](https://echarts.apache.org/zh/option.html#series-radar.data.lineStyle) , [areaStyle](https://echarts.apache.org/zh/option.html#series-radar.data.areaStyle) , [emphasis](https://echarts.apache.org/zh/option.html#series-radar.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-radar.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-radar.data.select) , [tooltip](https://echarts.apache.org/zh/option.html#series-radar.data.tooltip) }

### series-tree 树图

```typescript
option = {
  series: [{
    type: "tree",
    data: [{
      name: "root",
      children: [{
        name: "Child A",
        children: [{
          name: "Leaf C"
        }, {
          name: "Leaf D"
        }, {
          name: "Leaf E"
        }, {
          name: "Leaf F"
        }]
      }, {
        name: "Child B",
        children: [{
          name: "Leaf G"
        }, {
          name: "Leaf H"
        }]
      }, {
        name: "Child D"
      }, {
        name: "Child F",
        children: [{
          name: "Leaf J"
        }, {
          name: "Leaf K"
        }]
      }]
    }],
    label: {
      position: "right"
    }
  }]
}
```

#### [series-tree.](https://echarts.apache.org/zh/option.html#series-tree) [data](https://echarts.apache.org/zh/option.html#series-tree.data)

Object

[series-tree.data](https://echarts.apache.org/zh/option.html#series-tree.data) 的数据格式是树状结构的，例如：

```javascript
{ // 注意，最外层是一个对象，代表树的根节点
    name: "flare",    // 节点的名称，当前节点 label 对应的文本
    label: {          // 此节点特殊的 label 配置（如果需要的话）。
        ...           // label的格式参见 series-tree.label。
    },
    itemStyle: {      // 此节点特殊的 itemStyle 配置（如果需要的话）。
        ...           // label的格式参见 series-tree.itemStyle。
    },
    children: [
        {
            name: "flex",
            value: 4116,    // value 值，只在 tooltip 中显示
            label: {
                ...
            },
            itemStyle: {
                ...
            },
            collapsed: null, // 如果为 true，表示此节点默认折叠。
            children: [...] // 叶子节点没有 children, 可以不写
        },
        ...
    ]
};
```

##### 所有属性

{ [name](https://echarts.apache.org/zh/option.html#series-tree.data.name) , [value](https://echarts.apache.org/zh/option.html#series-tree.data.value) , [collapsed](https://echarts.apache.org/zh/option.html#series-tree.data.collapsed) , [itemStyle](https://echarts.apache.org/zh/option.html#series-tree.data.itemStyle) , [lineStyle](https://echarts.apache.org/zh/option.html#series-tree.data.lineStyle) , [label](https://echarts.apache.org/zh/option.html#series-tree.data.label) , [emphasis](https://echarts.apache.org/zh/option.html#series-tree.data.emphasis) , [blur](https://echarts.apache.org/zh/option.html#series-tree.data.blur) , [select](https://echarts.apache.org/zh/option.html#series-tree.data.select) , [tooltip](https://echarts.apache.org/zh/option.html#series-tree.data.tooltip) , [animation](https://echarts.apache.org/zh/option.html#series-tree.data.animation) , [animationThreshold](https://echarts.apache.org/zh/option.html#series-tree.data.animationThreshold) , [animationDuration](https://echarts.apache.org/zh/option.html#series-tree.data.animationDuration) , [animationEasing](https://echarts.apache.org/zh/option.html#series-tree.data.animationEasing) , [animationDelay](https://echarts.apache.org/zh/option.html#series-tree.data.animationDelay) , [animationDurationUpdate](https://echarts.apache.org/zh/option.html#series-tree.data.animationDurationUpdate) , [animationEasingUpdate](https://echarts.apache.org/zh/option.html#series-tree.data.animationEasingUpdate) , [animationDelayUpdate](https://echarts.apache.org/zh/option.html#series-tree.data.animationDelayUpdate) }





# 3.进阶

## 3.1.异步数据加载与更新

ECharts 的异步数据加载与更新是动态可视化开发的核心功能之一，以下从基础到进阶的详细指南，包含代码示例和关键注意事项：

---

### **一、异步数据加载基础**
#### 1. 数据获取
使用 JavaScript 的 `fetch`、`axios` 或 `XMLHttpRequest` 获取远程数据：
```javascript
// 使用 fetch 示例
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    updateChart(data); // 处理数据并更新图表
  });
```

#### 2. 数据格式处理
将数据转换为 ECharts 所需的格式：
```javascript
function processData(rawData) {
  return {
    xAxis: { data: rawData.map(item => item.category) },
    series: [{
      data: rawData.map(item => item.value)
    }]
  };
}
```

#### 3. 图表更新
通过 `setOption` 动态更新配置：
```javascript
let chart = echarts.init(document.getElementById('chart'));
chart.setOption({
  xAxis: { type: 'category' },
  yAxis: { type: 'value' },
  series: [{ type: 'bar' }]
});

function updateChart(data) {
  const option = processData(data);
  chart.setOption(option); // 增量合并配置
}
```

---

### **二、实时数据更新**
#### 1. 定时轮询（Polling）
```javascript
// 每 5 秒更新一次数据
setInterval(() => {
  fetch('https://api.example.com/real-time-data')
    .then(response => response.json())
    .then(data => chart.setOption(processData(data)));
}, 5000);
```

#### 2. WebSocket 实时推送
```javascript
const ws = new WebSocket('wss://api.example.com/ws');
ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  chart.setOption(processData(data));
};
```

---

### **三、ECharts API 进阶技巧**
#### 1. 增量更新与性能优化
- **部分更新**：仅传递变化的数据部分，减少渲染开销。
  ```javascript
  chart.setOption({
    series: [{ id: 'sales', data: newDataArray }]
  }, { notMerge: false }); // notMerge: false 表示合并配置
  ```
- **大数据模式**：启用 `large: true` 和 `progressiveRender` 提升性能。
  ```javascript
  series: [{
    type: 'line',
    large: true,
    progressive: 2000 // 分片渲染
  }]
  ```

#### 2. 加载状态提示
```javascript
chart.showLoading('default', { 
  text: '疯狂加载中...',
  color: '#c23531',
  maskColor: 'rgba(0, 0, 0, 0.3)'
});

fetchData().then(() => chart.hideLoading());
```

---

### **四、完整示例：动态折线图**
```html
<div id="chart" style="width: 600px; height: 400px;"></div>
<script>
  const chart = echarts.init(document.getElementById('chart'));
  
  // 初始配置
  chart.setOption({
    xAxis: { type: 'time' },
    yAxis: { type: 'value' },
    series: [{ type: 'line', smooth: true }]
  });

  // 模拟实时数据
  function fetchData() {
    return Promise.resolve({
      timestamp: new Date().getTime(),
      value: Math.random() * 100
    });
  }

  // 每 2 秒追加新数据点
  setInterval(() => {
    fetchData().then(data => {
      const option = {
        xAxis: { data: [...chart.getOption().xAxis[0].data, data.timestamp] },
        series: [{ data: [...chart.getOption().series[0].data, data.value] }]
      };
      chart.setOption(option);
    });
  }, 2000);
</script>
```

---

### **五、注意事项**
1. **内存管理**：在 SPA（如 Vue/React）中，组件卸载时调用 `chart.dispose()` 释放资源。
2. **错误处理**：网络请求添加 `catch` 逻辑，避免静默失败。
3. **节流与防抖**：高频更新时限制渲染频率（如 Lodash 的 `throttle`）。
4. **SSR 兼容**：服务端渲染时确保 ECharts 在客户端初始化。

---

通过结合异步数据流和 ECharts 的动态配置，可轻松实现股票行情、实时监控等场景。根据需求选择轮询、WebSocket 或 Server-Sent Events（SSE），并合理优化渲染性能。



## 3.2.事件处理

ECharts 提供了丰富的事件处理机制，可以实现用户与图表的交互。以下是关于 ECharts 事件处理的详细介绍：

### 一、事件分类

ECharts 的事件分为两类：

1. **鼠标事件**：如 `click`、`dblclick`、`mouseover`、`mouseout` 等。
2. **组件交互事件**：如 `legendselectchanged`（图例选中状态改变）、`datazoom`（数据区域缩放）、`brushselected`（刷选区域）等。

### 二、绑定事件

ECharts 使用 `on` 方法绑定事件，格式如下：

JavaScript复制

```javascript
myChart.on(eventName, handler);
```

其中，`eventName` 是事件名称，`handler` 是回调函数。

#### 示例：绑定点击事件

以下代码展示了如何为柱状图绑定点击事件：

JavaScript复制

```javascript
var myChart = echarts.init(document.getElementById('chart'));
var option = {
    xAxis: { data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"] },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
    }]
};
myChart.setOption(option);

// 绑定点击事件
myChart.on('click', function(params) {
    alert('点击了柱状图，数值为：' + params.value);
});
```

当用户点击柱状图时，会弹出对应的数据值。

### 三、事件参数

事件回调函数中会传入一个 `params` 对象，包含以下常用属性：

- `componentType`：组件类型，如 `series`、`markLine` 等。
- `seriesType`：系列类型，如 `bar`、`line` 等。
- `name`：数据名称。
- `value`：数据值。
- `dataIndex`：数据索引。

### 四、高级用法

1. **指定组件绑定事件**
   可以通过 `query` 参数指定绑定事件的组件，例如：

   JavaScript复制

   ```javascript
   myChart.on('mouseover', {seriesName: '销量'}, function(params) {
       console.log('鼠标悬停在销量系列上');
   });
   ```

   这样可以只监听特定系列的事件。

2. **触发图表行为**
   使用 `dispatchAction` 方法可以程序化地触发图表行为，例如：

   JavaScript复制

   ```javascript
   myChart.dispatchAction({
       type: 'highlight',
       seriesIndex: 0,
       dataIndex: 2
   });
   ```

   这可以用于高亮指定的数据。

### 五、常见事件示例

1. **图例选中状态改变**：

   JavaScript复制

   ```javascript
   myChart.on('legendselectchanged', function(params) {
       console.log(params.selected); // 打印图例的选中状态
   });
   ```

2. **数据区域缩放**：

   JavaScript复制

   ```javascript
   myChart.on('datazoom', function(params) {
       console.log('数据区域缩放', params);
   });
   ```

3. **鼠标悬浮**：

   JavaScript复制

   ```javascript
   myChart.on('mouseover', function(params) {
       console.log('鼠标悬浮在', params.name);
   });
   ```

通过以上方式，你可以为 ECharts 图表添加丰富的交互功能。





