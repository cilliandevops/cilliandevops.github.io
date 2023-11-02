# 基础知识点必备

## 入门

HTML (HyperText Markup Language) 是用于创建网页的标准标记语言。它用于描述网页的结构和内容，包括文本，图片，链接等等。

以下是入门HTML的重点知识点：

1. HTML文档的基本结构：HTML 文档以 <!DOCTYPE html> 开头，来声明文档类型，然后是 <html> 标签，结束在 </html>标签。文档内主要包含<head> 和 <body> 两个部分。

2. HTML 元素和标签：HTML元素通常由开始标签和结束标签组成。例如：`<p>这是一个段落</p>`，其中 "p" 是元素名称。

3. HTML 属性：HTML元素可以有许多属性，它们为元素提供额外信息，如 id、class、style、src等。

4. 注释：HTML注释是被浏览器忽略的部分，其语法是 <!-- 这是注释 -->。

5. 标题：在HTML中，有六级标题，从 `<h1>` 到 `<h6>`。

6. 段落：`<p>` 标签用于定义段落。

7. 链接：`<a>` 标签用于定义链接。

8. 图像：`<img>` 标签用于插入图像。

9. 列表：在HTML中有两种列表，无序列表`<ul>`和有序列表`<ol>`。

10. 表格：`<table>`标签用于创建表格。

11. 表单：表单用于收集用户输入，可使用 `<form>` 标签。

12. 样式和颜色：可以使用 "style" 属性来设置元素的样式。

13. 打包下载和分发页面：要将你的页面放在web上，你需要将它发布到一个web服务器上。

14. 语义化标签：HTML5 引入了一些语义化的新标签，如 `<header>`, `<footer>`, `<section>`, `<article>`, `<nav>`, `<aside>` 等，它们提供了更明确的结构语义。

学习HTML的过程中，建议手动编写代码进行实践，同时参考互联网上的教程和文档，如W3Schools和MDN Web Docs。

## 进阶

当然，我们可以进一步深入到一些更具体的HTML知识点：

1. HTML元素和标签：
    - 块级元素（Block-level Element）：如 `<div>`, `<p>`, `<h1>` - `<h6>`, `<ul>`, `<li>`, `<table>`等，这些元素在显示时通常会以新行来开始和结束。
    - 内联元素（Inline Element）：如 `<span>`, `<a>`, `<img>`, `<button>`等，这些元素在显示时不会以新行开始，它们通常出现在块级元素中。

2. HTML属性：
    - id属性：可以为HTML元素提供唯一id，通常用于CSS样式或JavaScript引用。
    - class属性：可以为HTML元素提供一个或多个类名，用于CSS样式或JavaScript引用。
    - src属性：定义嵌入内容的地址，如 `<img>`, `<audio>`, `<video>`, `<script>`, `<iframe>`等。
    - href属性：定义超链接的目标地址。

3. HTML文本格式化：
    - `<strong>` 标签表示强调的文本。
    - `<em>` 标签表示斜体的文本。
    - `<mark>` 标签定义带有背景色的文本。

4. HTML链接：
    - 外部链接：使用完整的URL路径。
    - 内部链接：链接到同一页面的不同部分，通常用id属性来实现。

5. HTML图片：`<img>` 标签的主要属性有src（源地址）、alt（替代文本）、width（宽度）和height（高度）。

6. HTML列表：除了无序和有序列表之外，还有定义列表`<dl>`，其中包含`<dt>`（定义术语）和`<dd>`（描述术语）。

7. HTML表格：除了 `<table>` 标签，还有 `<tr>`（行）、`<td>`（数据单元格）和 `<th>`（表头）等。

8. HTML表单：包含了`<input>`元素（可以有不同的类型如text, password, radio, checkbox, submit等）、`<label>`元素（定义输入元素的标签）、`<textarea>`元素（定义多行的文本输入字段）、`<button>`元素（定义一个可点击的按钮）、`<select>`元素（创建一个下拉列表）等。

9. HTML5新元素：HTML5引入了许多新标签，如`<canvas>`（用于图形的绘制）、`<video>`和`<audio>`（用于视频和音频媒体）、`<svg>`（用于矢量图形），以及一系列语义元素如`<section>`, `<article>`, `<aside>`, `<nav>`, `<header>`, `<footer>`, `<figure>`, `<figcaption>`等。

10. HTML响应式：使Web页面在不同的设备（桌面，平板，手机等）上看起来都优雅，可以使用 media query（媒体查询）和 viewport（视口）等技术。

在学习的过程中，应多动手实践以更好地理解和记忆知识点。

## 示例

1. 基本HTML模板：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!-- 在此处插入内容 -->
</body>
</html>
```

2. 文本格式化示例：

```html
<strong>这是加粗的文本</strong>
<em>这是斜体的文本</em>
<mark>这是带有背景色的文本</mark>
```

3. 创建链接：

```html
<!-- 外部链接 -->
<a href="https://www.example.com">访问example网站</a>
<!-- 内部链接 -->
<a href="#section1">跳转到第一部分</a>
```

4. 插入图片：

```html
<img src="path/to/image.jpg" alt="描述图片的文本" width="300" height="200">
```

5. 创建列表：

```html
<!-- 无序列表 -->
<ul>
  <li>列表项1</li>
  <li>列表项2</li>
</ul>

<!-- 有序列表 -->
<ol>
  <li>列表项1</li>
  <li>列表项2</li>
</ol>

<!-- 定义列表 -->
<dl>
  <dt>术语1</dt>
  <dd>术语1的描述</dd>
  <dt>术语2</dt>
  <dd>术语2的描述</dd>
</dl>
```

6. 表格示例：

```html
<table>
  <tr>
    <th>表头1</th>
    <th>表头2</th>
  </tr>
  <tr>
    <td>行1，列1</td>
    <td>行1，列2</td>
  </tr>
  <tr>
    <td>行2，列1</td>
    <td>行2，列2</td>
  </tr>
</table>
```

7. 表单示例：

```html
<form>
  <label for="name">用户名：</label>
  <input type="text" id="name" name="name">

  <label for="password">密码：</label>
  <input type="password" id="password" name="password">

  <label for="gender">性别：</label>
  <input type="radio" id="male" name="gender" value="male">
  <label for="male">男</label>
  <input type="radio" id="female" name="gender" value="female">
  <label for="female">女</label>

  <input type="submit" value="提交">
</form>
```

8. HTML5新增元素示例：

```html
<canvas id="myCanvas"></canvas>
<video src="path/to/video.mp4" controls>您的浏览器不支持视频播放</video>
<audio src="path/to/audio.mp3" controls>您的浏览器不支持音频播放</audio>
<figure>
  <img src="path/to/image.jpg" alt="描述图片的文本">
  <figcaption>图片说明文字</figcaption>
</figure>
```

9. 响应式布局示例：

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
  /* 设置基本样式 */
  body {font-family: Arial, sans-serif;}

  /* 当屏幕宽度大于等于600px时，改变布局 */
  @media (min-width: 600px) {
    .container {
      display: flex;
    }
    .left {
      width: 70%;
    }
    .right {
      width: 30%;
    }
  }
</style>

<div class="container">
  <div class="left">左侧内容</div>
  <div class="right">右侧内容</div>
</div>
```

使用这些示例作为学习HTML的参考，并在编写代码的过程中逐步实践。