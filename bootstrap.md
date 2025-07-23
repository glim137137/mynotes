# Bootstrap

文章参考：

[TOC]

## 简介

**Bootstrap** 是一个开源的前端开发框架，用于创建响应式和移动设备优先的网站和应用程序。它由 Twitter 的开发者 Mark Otto 和 Jacob Thornton 于 2011 年创建，并迅速成为最受欢迎的前端框架之一。

https://v5.bootcss.com/docs/getting-started/introduction/



## 引入Bootstrap

你可以通过两种方式来引入 Bootstrap：

### 通过 CDN 引入

这是最快的方法，不需要下载文件，只需要在 HTML 文件的 `<head>` 和 `<body>` 中添加以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bootstrap Demo</title>
  <!-- 引入 Bootstrap CSS -->
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

  <!-- 你的内容 -->

  <!-- 引入 jQuery 和 Bootstrap JS -->
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.2/dist/umd/popper.min.js"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
```

### 下载文件

如果你不想依赖 CDN，可以下载 Bootstrap 框架，解压后将 CSS 和 JS 文件添加到项目中，然后在 HTML 中引入。

## 常见的 Bootstrap 组件

Bootstrap 提供了很多现成的组件，可以让你快速构建响应式网页。以下是一些常用的组件和例子：

### 网格系统

Bootstrap 使用 12 栏栅格系统来创建布局。你可以通过类 `col-*` 来设置列的宽度。

```html
<div class="container">
  <div class="row">
    <div class="col-sm-4">Column 1</div>
    <div class="col-sm-4">Column 2</div>
    <div class="col-sm-4">Column 3</div>
  </div>
</div>
```

### 按钮

Bootstrap 提供了多种样式的按钮。

```html
<button type="button" class="btn btn-primary">Primary Button</button>
<button type="button" class="btn btn-secondary">Secondary Button</button>
```

### 导航栏

Bootstrap 可以帮助你快速创建响应式导航栏。

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Features</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Pricing</a>
      </li>
    </ul>
  </div>
</nav>
```

### 卡片

卡片是 Bootstrap 中常用的布局组件。

```html
<div class="card" style="width: 18rem;">
  <img src="https://via.placeholder.com/150" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

## 响应式设计

### 断点

Bootstrap 内置了 6 个默认断点，有时也被叫做 *grid tiers*, for building responsively. 如果你使用的是 Bootstrap 的 Sass 源文件，则可以自定义这些断点。

| Breakpoint        | Class infix | Dimensions |
| ----------------- | ----------- | ---------- |
| Extra small       | *None*      | <576px     |
| Small             | `sm`        | ≥576px     |
| Medium            | `md`        | ≥768px     |
| Large             | `lg`        | ≥992px     |
| Extra large       | `xl`        | ≥1200px    |
| Extra extra large | `xxl`       | ≥1400px    |

### 媒体查询 

由于 Bootstrap 是移动设备优先的，因此我们使用了一些 [媒体查询（media queries）](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) 功能来为我们的布局和视觉元素创建合理的断点。这些断点主要以最小的视口（viewport）宽度作为基准，并在视口尺寸改变时放大元素。

Bootstrap 提供了响应式设计支持，自动适应不同屏幕尺寸。通过使用 **媒体查询类**，可以让布局在不同设备上有不同的显示效果。

例如：

- `col-sm-4`：在小屏设备上占 4 列。
- `col-md-6`：在中等屏设备上占 6 列。

## 常见的工具类

Bootstrap 提供了很多实用的工具类，帮助你快速实现一些常见的样式和功能：

- **文本对齐**：`text-center`、`text-right`、`text-left`
- **背景颜色**：`bg-primary`、`bg-success`、`bg-danger`
- **边距和内边距**：`m-3`、`p-2`、`mt-4`（修改四周的外边距和内边距）

例如：

```html
<div class="text-center bg-primary text-white p-3">
  This is a centered text with a blue background.
</div>
```

