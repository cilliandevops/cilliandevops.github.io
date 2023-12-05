# CSS修行之路

## 入门

CSS (Cascading Style Sheets) 是一种样式表语言，用于描述HTML或XML（包括SVG、MathML等）文档的呈现方式。CSS描述了如何将元素在屏幕、纸、音频等媒体上进行布局。

以下是一些入门CSS的重点知识点：

1. CSS 选择器：选择器用于选定你想要应用样式的元素。如元素选择器（p），类选择器（.classname），ID选择器（#idname），属性选择器（[attr=value]）等。

2. CSS 声明：CSS声明由属性和对应的值组成，例如 `color: red;` 中的 `color` 是属性，`red` 是值。

3. CSS 盒模型：盒模型由内容（content）、内边距（padding）、边界（border）和外边距（margin）组成，是布局的基础。

4. CSS 布局：CSS提供了多种布局模型，如流动模型（Normal Flow）、浮动模型（Float）、定位模型（Positioning）、弹性盒布局（Flexbox）和网格布局（Grid）等。

5. CSS 颜色和背景：颜色可以用名称、十六进制、RGB或HSL表示。背景相关属性有 `background-color`, `background-image`, `background-repeat`, `background-position` 等。

6. CSS 字体和文本：有关文本样式的属性值有 `font-family`, `font-size`, `font-weight`, `text-align`, `text-decoration`, `line-height` 等。

7. CSS 伪类和伪元素：伪类（如 `:hover`, `:active`, `:first-child`）和伪元素（如 `::after`, `::before`）允许你设置元素的特殊状态的样式。

8. CSS 转换和过渡：`transform` 属性允许你旋转、缩放、倾斜或平移元素。`transition` 属性用于元素间的平滑过渡。

9. CSS 动画：`animation` 属性可以创建复杂的动画，它是一个复合属性，包含子属性如 `animation-name`, `animation-duration`, `animation-timing-function` 等。

10. CSS 响应式设计：响应式设计是使你的网页在不同尺寸的屏幕上都有良好的布局和性能。使用媒体查询（Media Query）来为不同尺寸的设备应用不同的CSS样式。

下面我们来看一些基础的CSS示例：

```css
/* 元素选择器，选择所有p元素 */
p {
  color: red;                 /* 文字颜色为红色 */
  background-color: #ffffee;  /* 背景颜色为浅黄色 */
}

/* 类选择器，选择类名为highlight的元素 */
.highlight {
  background-color: yellow;   /* 背景色为黄色 */
  font-weight: bold;          /* 文字加粗 */
}

/* ID选择器，选择ID为main-title的元素 */
#main-title {
  text-align: center;         /* 文字居中对齐 */
  font-size: 24px;            /* 字体大小为24像素 */
}

/* 伪类选择器，选择鼠标悬停在链接上的状态 */
a:hover {
  color: orange;              /* 文字颜色为橙色 */
}

/* 转换和过渡 */
.box {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  transition: width 2s;       /* 2秒内变换宽度 */
}

.box:hover {
  width: 200px;               /* 鼠标悬停时宽度变为200px */
}
```

以上只是一些基本示例，实际上CSS的能力远不止于此。在学习的过程中，理论知识和实践应该结合，这样可以更好地理解并掌握CSS。

## 进阶

让我们深入探索一些更复杂的CSS示例:

1. CSS盒模型：

```css
.box {
  border: 2px solid black;  /* 边框宽度为2px，风格为实线，颜色为黑色 */
  padding: 10px;  /* 内边距为10px */
  margin: 20px;  /* 外边距为20px */
  width: 300px;  /* 内容区宽度为300px */
}
```

2. CSS布局使用浮动：

```css
.left {
  float: left;  /* 左浮动 */
  width: 50%;
}

.right {
  float: right;  /* 右浮动 */
  width: 50%;
}
```

3. CSS布局使用Flexbox：

```css
.container {
  display: flex;  /* 设置容器为Flex布局 */
  justify-content: space-between;  /* 项目之间的间隔尽可能大 */
}

.item {
  flex: 1;  /* 所有项目都将等分空间 */
}
```

4. 响应式设计使用媒体查询：

```css
/* 当屏幕宽度小于600px时，改变背景颜色和字体大小 */
@media (max-width: 600px) {
  body {
    background-color: lightblue;
    font-size: 18px;
  }
}
```

5. CSS动画：

```css
@keyframes slidein {
  from {transform: translateX(100%);}
  to {transform: translateX(0);}
}

.box {
  animation: slidein 3s ease-in-out infinite alternate;  /* 使用动画 */
}
```

这些例子涵盖了CSS的一些基本知识，但还有更多需要学习的内容。可以通过创建自己的网页并尝试使用这些代码来更深入地理解它们。

## 布局

学习网址 <https://www.runoob.com/css/css-tutorial.html>

在 CSS 中，有许多用于控制布局的属性。以下列举了一些常见的属性：

width 和 height：用于设置元素的宽度和高度。

display：这是一个非常重要的属性，它确定了一个元素如何在页面上展示。常见的值有 block，inline，inline-block，flex，grid 等。

position：控制元素的定位方式。它的值可以是 static，relative，absolute，fixed 或 sticky。

top，right，bottom 和 left：当 position 的值不是 static 时，这些属性决定了元素从其定位点的位置。

margin：定义元素四周的外边距。可以用像素、百分比或 em 等单位表示。

padding：定义元素边框以内的空间。同样可以使用像素、百分比或 em 等单位表示。

border：定义元素的边框。你可以定义边框的宽度、样式（如实线、虚线等）和颜色。

box-sizing：该属性决定宽度和高度的计算方式。content-box 是默认值，意味着宽度和高度分别应用于元素的内容框。在此模式下，元素的总宽度/高度是内容、内边距和边框的总和。border-box 让元素具有指定的宽度和高度，内边距和边框的宽度在已经设定的宽度和高度内，这样会更直观和方便。

flex：一个在 flex 容器内的快捷属性，用于设置元素如何分配空间和对齐内容。

grid：用于布局的二维系统，可以处理列和行。
