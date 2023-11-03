# Essential Basic Knowledge

## Introduction

HTML (HyperText Markup Language) is the standard markup language for creating web pages. It is used to describe the structure and content of web pages, including text, images, links, etc.

Here are the key knowledge points to get started with HTML:

1. Basic structure of HTML documents: HTML documents start with <!DOCTYPE html> to declare the document type, followed by the <html> tag, ending at the </html> tag. The document mainly contains two parts: <head> and <body>.

2. HTML elements and tags: HTML elements are typically composed of a start tag and an end tag. For example: `<p>This is a paragraph</p>`, where "p" is the element name.

3. HTML attributes: HTML elements can have many attributes, providing extra information for the elements, such as id, class, style, src, etc.

4. Comments: HTML comments are parts that are ignored by the browser, with the syntax being <!-- This is a comment -->.

5. Headings: In HTML, there are six levels of headings, from `<h1>` to `<h6>`.

6. Paragraphs: The `<p>` tag is used to define paragraphs.

7. Links: The `<a>` tag is used to define links.

8. Images: The `<img>` tag is used to insert images.

9. Lists: In HTML, there are two types of lists, unordered lists `<ul>` and ordered lists `<ol>`.

10. Tables: The `<table>` tag is used to create tables.

11. Forms: Forms are used to collect user input, which can be done using the `<form>` tag.

12. Styles and Colors: The "style" attribute can be used to set the style of elements.

13. Packaging, Downloading, and Distributing Pages: To put your page on the web, you need to publish it to a web server.

14. Semantic Tags: HTML5 introduced some new semantic tags, such as `<header>`, `<footer>`, `<section>`, `<article>`, `<nav>`, `<aside>`, etc., which provide a clearer structural semantics.

During the process of learning HTML, it is recommended to write code manually for practice, while referring to online tutorials and documents, such as W3Schools and MDN Web Docs.

## Advanced

Of course, we can delve further into some more specific HTML knowledge points:

1. HTML elements and tags:
    - Block-level Elements: Such as `<div>`, `<p>`, `<h1>` - `<h6>`, `<ul>`, `<li>`, `<table>`, etc., these elements usually start and end on a new line when displayed.
    - Inline Elements: Such as `<span>`, `<a>`, `<img>`, `<button>`, etc., these elements do not start on a new line when displayed, they usually appear within block-level elements.

2. HTML attributes:
    - id attribute: Can provide a unique id for HTML elements, usually used for CSS styling or JavaScript reference.
    - class attribute: Can provide one or more class names for HTML elements, used for CSS styling or JavaScript reference.
    - src attribute: Define embedded content address, such as `<img>`, `<audio>`, `<video>`, `<script>`, `<iframe>`, etc.
    - href attribute: Define the target address of the hyperlink.

3. HTML text formatting:
    - `<strong>` tag represents emphasized text.
    - `<em>` tag represents italic text.
    - `<mark>` tag defines text with a background color.

4. HTML links:
    - External links: Use the full URL path.
    - Internal links: Link to different parts of the same page, usually achieved with the id attribute.

5. HTML images: The main attributes of the `<img>` tag are src (source address), alt (alternative text), width, and height.

6. HTML lists: In addition to unordered and ordered lists, there are definition lists `<dl>`, which include `<dt>` (define terms) and `<dd>` (describe terms).

7. HTML tables: In addition to the `<table>` tag, there are also `<tr>` (row), `<td>` (data cell), and `<th>` (table header), etc.

8. HTML forms: Includes `<input>` elements (which can have different types such as text, password, radio, checkbox, submit, etc.), `<label>` elements (define labels for input elements), `<textarea>` elements (define multi-line text input fields), `<button>` elements (define a clickable button), `<select>` elements (create a drop-down list), etc.

9. HTML5 new elements: HTML5 introduced many new tags, such as `<canvas>` (for drawing graphics), `<video>` and `<audio>` (for video and audio media), `<svg>` (for vector graphics), as well as a series of semantic elements like `<section>`, `<article>`, `<aside>`, `<nav>`, `<header>`, `<footer>`, `<figure>`, `<figcaption>`, etc.

10. HTML responsive: To make web pages look elegant on different devices (desktop, tablet, mobile, etc.), technologies such as media query and viewport can be used.

During the learning process, one should practice more to better understand and memorize the knowledge points.

## Examples

1. Basic HTML template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!-- Insert content here -->
</body>
</html>
```

2. Text formatting example:

```html
<strong>This is bold text</strong>
<em>This is italic text</em>
<mark>This is text with a background color</mark>
```

3. Creating links:

```html
<!-- External link -->
<a href="https://www.example.com">Visit example website</a>
<!-- Internal link -->
<a href="#section1">Jump to the first section</a>
```

4. Inserting images:

```html
<img src="path/to/image.jpg" alt="Text describing the image" width="300" height="200">
```

5. Creating lists:

```html
<!-- Unordered list -->
<ul>
  <li>List item 1</li>
  <li>List item 2</li>
</ul>

<!-- Ordered list -->
<ol>
  <li>List item 1</li>
  <li>List item 2</li>
</ol>

<!-- Definition list -->
<dl>
  <dt>Term 1</dt>
  <dd>Description of Term 1</dd>
  <dt>Term 2</dt>
  <dd>Description of Term 2</dd>
</dl>
```

6. Table example:

```html
<table>
  <tr>
    <th>Header 1</th>
    <th>Header 2</th>
  </tr>
  <tr>
    <td>Row 1, Column 1</td>
    <td>Row 1, Column 2</td>
  </tr>
  <tr>
    <td>Row 2, Column 1</td>
    <td>Row 2, Column 2</td>
  </tr>
</table>
```

7. Form example:

```html
<form>
  <label for="name">Username:</label>
  <input type="text" id="name" name="name">

  <label for="password">Password:</label>
  <input type="password" id="password" name="password">

  <label for="gender">Gender:</label>
  <input type="radio" id="male" name="gender" value="male">
  <label for="male">Male</label>
  <input type="radio" id="female" name="gender" value="female">
  <label for="female">Female</label>

  <input type="submit" value="Submit">
</form>
```

8. New HTML5 elements example:

```html
<canvas id="myCanvas"></canvas>
<video src="path/to/video.mp4" controls>Your browser does not support video playback</video>
<audio src="path/to/audio.mp3" controls>Your browser does not support audio playback</audio>
<figure>
  <img src="path/to/image.jpg" alt="Text describing the image">
  <figcaption>Image description text</figcaption>
</figure>
```

9. Responsive layout example:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
  /* Set basic styles */
  body {font-family: Arial, sans-serif;}

  /* Change layout when the screen width is greater than or equal to 600px */
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
  <div class="left">Left content</div>
  <div class="right">Right content</div>
</div>
```

Use these examples as references for learning HTML, and gradually practice in the process of writing code.