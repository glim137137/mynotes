# Swing

[TOC]

**Swing** 是 Java 提供的一套用于构建图形用户界面(GUI)的工具包，是 Java Foundation Classes (JFC)的一部分。他的核心特点为：

1. **跨平台**：在所有支持 Java 的平台上表现一致
2. **轻量级组件**：不依赖本地操作系统的原生组件
3. **丰富的组件库**：提供按钮、文本框、表格等完整组件
4. **可扩展性**：可以自定义组件外观和行为
5. **双缓冲技术**：减少图形闪烁

## 主要组件

### 顶层容器

| 组件      | 描述                           |
| :-------- | :----------------------------- |
| `JFrame`  | 主窗口，带标题栏、边框和菜单栏 |
| `JDialog` | 对话框窗口                     |

### 常用组件

| 组件           | 描述         |
| :------------- | :----------- |
| `JButton`      | 按钮         |
| `JLabel`       | 文本标签     |
| `JTextField`   | 单行文本框   |
| `JTextArea`    | 多行文本区域 |
| `JCheckBox`    | 复选框       |
| `JRadioButton` | 单选按钮     |
| `JComboBox`    | 下拉列表     |
| `JList`        | 列表组件     |
| `JTable`       | 表格         |
| `JTree`        | 树形结构     |

### 容器组件

| 组件          | 描述           |
| :------------ | :------------- |
| `JPanel`      | 通用容器       |
| `JScrollPane` | 带滚动条的容器 |
| `JTabbedPane` | 选项卡面板     |
| `JSplitPane`  | 分割面板       |

## 屏幕坐标体系

**原点(0,0)**：位于屏幕的左上角

**X轴**：向右为正方向

**Y轴**：向下为正方向

**单位**：像素(pixel)

**坐标范围**：

- 水平坐标范围：0 到 (水平分辨率-1)
- 垂直坐标范围：0 到 (垂直分辨率-1)

> 例如1920×1080分辨率的屏幕：
>
> - X轴坐标范围：0-1919
> - Y轴坐标范围：0-1079

## 简单绘图

```java
import javax.swing.*;
import java.awt.*; // Abstract Window Toolkit

@SuppressWarnings({"all"})
public class DrawPanel extends JFrame {

    private MyPanel mp = null;

    public DrawPanel() {
        mp = new MyPanel();
        this.add(mp);
        this.setSize(400, 300);
        // 点击窗口退出按钮，程序自动退出
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setVisible(true);
    }

    public static void main(String[] args) {
        new DrawPanel();
    }
}

class MyPanel extends JPanel {
    @Override
    public void paint(Graphics g) {
        super.paint(g);
        System.out.println("paint 被调用了");
        g.drawOval(10, 10, 100, 100);
    }
}
```

**`paint`** 方法是从 **Java AWT/Swing 组件继承体系** 中继承而来的。最初定义在 **`java.awt.Component`** 类中。

### 继承链分析

```
java.lang.Object
  └─ java.awt.Component
      └─ java.awt.Container
          └─ javax.swing.JComponent
              └─ javax.swing.JPanel (您的 MyPanel 父类)
```

### 绘图原理

**`java.awt.Component`** 类提供了两个和绘图相关的重要方法

1. `paint(Graphics g)`绘制组件的外观
2. `repaint()`刷新组件的外观

当组件第一次在屏幕显示的时候,程序会自动的调用`paint()`方法来绘制组件。

在以下情况 `paint()` 将会被调用:

1. 窗口最小化，再最大化
2. 窗口的大小发生变化
3. `repaint()` 方法被调用

### `Graphics` 类

`Graphics` 是 Java AWT (Abstract Window Toolkit) 中的一个核心抽象类，用于所有 2D 图形绘制操作。它提供了在组件上绘制图形、文本和图像的基本方法。

```
java.lang.Object
  └─ java.awt.Graphics (抽象类)
      └─ java.awt.Graphics2D (更强大的子类)
```

##### 绘制图形

| 方法                                                         | 描述         |
| :----------------------------------------------------------- | :----------- |
| `drawLine(int x1, int y1, int x2, int y2)`                   | 绘制直线     |
| `drawRect(int x, int y, int width, int height)`              | 绘制矩形边框 |
| `fillRect(int x, int y, int width, int height)`              | 填充矩形     |
| `drawOval(int x, int y, int width, int height)`              | 绘制椭圆边框 |
| `fillOval(int x, int y, int width, int height)`              | 填充椭圆     |
| `drawArc(int x, int y, int width, int height, int startAngle, int arcAngle)` | 绘制圆弧     |
| `fillArc(int x, int y, int width, int height, int startAngle, int arcAngle)` | 填充圆弧     |
| `drawPolygon(int[] xPoints, int[] yPoints, int nPoints)`     | 绘制多边形   |
| `fillPolygon(int[] xPoints, int[] yPoints, int nPoints)`     | 填充多边形   |

##### 绘制文本

| 方法                                   | 描述         |
| :------------------------------------- | :----------- |
| `drawString(String str, int x, int y)` | 绘制文本     |
| `setFont(Font font)`                   | 设置字体     |
| `getFont()`                            | 获取当前字体 |
| `getFontMetrics()`                     | 获取字体度量 |

##### 颜色控制

| 方法                | 描述         |
| :------------------ | :----------- |
| `setColor(Color c)` | 设置绘图颜色 |
| `getColor()`        | 获取当前颜色 |

##### 图像操作

| 方法                                                         | 描述     |
| :----------------------------------------------------------- | :------- |
| `drawImage(Image i mg, int x, int y, ImageObserver observer)` | 绘制图像 |
| `drawImage(Image img, int x, int y, int width, int height, ImageObserver observer)` |          |

### `Image` 类

`Image` 类是 Java AWT (Abstract Window Toolkit) 中用于表示图形图像的抽象类，是所有图像表示类的超类。

```
java.lang.Object
  └─ java.awt.Image (抽象类)
      ├─ java.awt.image.BufferedImage
      └─ java.awt.image.VolatileImage
```

##### 核心方法

| 方法                                                  | 描述                                    |
| :---------------------------------------------------- | :-------------------------------------- |
| `getWidth(ImageObserver observer)`                    | 获取图像宽度                            |
| `getHeight(ImageObserver observer)`                   | 获取图像高度                            |
| `getScaledInstance(int width, int height, int hints)` | 创建缩放后的图像版本                    |
| `getGraphics()`                                       | 获取图像的绘图上下文 (仅适用于缓冲图像) |
| `flush()`                                             | 释放图像占用的资源                      |

##### 使用 `Toolkit` 加载图像

```java
import java.awt.*;
import javax.swing.*;

public class ImageExample {
    public static void main(String[] args) {
        Image image = Toolkit.getDefaultToolkit().getImage("path/to/image.jpg");
        
        // 或者用相对路径
        Image image2 = Toolkit.getDefaultToolkit().getImage(Panel.getClass().getResource("/bg.png"));
        
        // 使用Swing的ImageIcon也可以加载图像
        ImageIcon icon = new ImageIcon("path/to/image.png");
        Image image3 = icon.getImage();
    }
}
```

##### 使用 `ImageIO` 加载图像

```java
import javax.imageio.ImageIO;
import java.awt.Image;
import java.io.File;
import java.io.IOException;

public class ImageIOExample {
    public static void main(String[] args) {
        try {
            Image image = ImageIO.read(new File("path/to/image.jpg"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

