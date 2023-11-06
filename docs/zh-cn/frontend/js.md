# js修行之路

## 学习路线

学习JavaScript的路线可能因人而异，但以下是一个推荐的学习路线：

**1. JavaScript 简介和基础知识**

在这个阶段，你需要学习 JavaScript 的基本语法，包括变量、数据类型、控制结构（如 if..else、for 循环）、函数等。

**2. 数据结构和算法**

理解数组、对象、树、图等基础数据结构，学习如何用 JavaScript 来操作这些数据结构。同时，基础的算法知识（如排序、搜索）也是必须掌握的。

**3. DOM 操作和事件处理**

DOM (Document Object Model) 是 JavaScript 与 HTML 交互的桥梁。学习如何选择（select）、更改（update）、增加（add）和删除（remove）HTML元素。同时，理解事件（event）如何工作，学会使用常见的事件（如 click、load、mouseover 等）。

**4. 常见的 Web API**

除了 DOM，Web 还有许多其他有用的 API，比如 Geolocation API、Web Storage API、Fetch API 等。学习这些 API 可以更好地为用户提供服务。

**5. 异步编程**

在 JavaScript 中，异步编程是必不可少的。学习回调函数（callback）、Promise、async/await 等异步处理方式。

**6. 深入 JavaScript**

理解 JavaScript 中的一些高级概念，比如闭包（closure）、原型链（prototype chain）、模块化（module）等。

**7. ES6 及其后的新特性**

ES6 （ES2015）引入了许多新特性，如 let/const、箭头函数、模块化等。后续的版本也持续增加了许多新特性。这一阶段需要了解和学习这些新特性。

**8. 前端框架**

学习像 React.js、Vue.js、Angular 这样的前端框架，可以提高编写复杂应用的效率。

**9. Node.js**

虽然不是必须的，但学习 Node.js 可以让你用 JavaScript 进行后端开发。对于全栈工程师来说这是必要的技能。

**10. 实践**

在整个学习过程中，动手实践、做项目非常重要。从简单的程序开始，慢慢增加复杂度，可以做一些实用工具、游戏、前端组件、甚至是完整的前后端应用。

同时，阅读他人的代码，参与开源项目也是提高的途径。编程是实践出真知，只要坚持学习和实践，你会在 JavaScript 的世界中找到属于你的一片天地。

## 入门

JavaScript 是Web开发中的一门重要语言，主要应用于浏览器端，让网页具有交互性。同时，随着Node.js的出现，JavaScript也可以用于服务器端开发。

以下是学习JavaScript的一些基础知识点：
 
1. **变量与数据类型**：JavaScript有六种数据类型：`string` (字符串), `number` (数字), `boolean` (布尔值)， `null` (空), `undefined` (未定义), 和 `object` (对象)。 

```javascript
let name = "John";  // 字符串
let age = 25;  // 数字
let isAdult = true;  // 布尔值
```

2. **数组和对象**：数组是一种特殊的对象，用于存储有序的数据集合。 对象则是键值对的集合，可用于存储更复杂的结构。

```javascript
let fruits = ["apple", "banana", "cherry"];  // 数组
let person = {name: "John", age: 25};  // 对象
```

3. **运算符**：JavaScript包括算术运算符(`+ - * /`等)，比较运算符(`== != > <`等), 逻辑运算符(`&& || !`等)等。

```javascript
let sum = 10 + 20;  // 算术运算符
let isEqual = sum == 30;  // 比较运算符
```

4. **条件语句**：`if`，`else if`，`else`，`switch`等用于进行条件判断。

```javascript
if (age >= 18) {
  console.log("You are an adult.");
} else {
  console.log("You are a minor.");
}
```

5. **循环**：`for`，`while`，和 `do while`等用于循环执行代码块。

```javascript
for(let i = 1; i <= 5; i++) {
  console.log(i);
}
```

6. **函数**：函数是执行特定任务的代码块。你可以自定义函数，也可以使用JavaScript内置的函数。

```javascript
function greet(name) {
  return "Hello, " + name;
}
console.log(greet("John"));  // 输出：Hello, John
```

7. **事件**：可以使你的网页对用户的行为做出响应，如点击，鼠标移动，键盘输入等。

```javascript
button.addEventListener("click", function() {
  alert("Button clicked!");
});
```

8. **DOM操作**：JavaScript可以用来改变网页内容和结构。这是通过操作DOM（Document Object Model）来实现的。

```javascript
let title = document.getElementById("title");
title.innerHTML = "New Title";
```

以上是JavaScript的一些基础知识点，但这只是冰山一角。JavaScript还有更多的高级主题，如异步编程、原型链、闭包、模块化、ES6新功能等。在学习的过程中，不断实践和尝试解决实际问题非常重要。

## 进阶


1. **变量**：变量用来储存数据。在JavaScript中，我们使用var，let，const来声明变量。

```js
var name = "John";  // 可重复声明，可更改值
let age = 25;  // 不可重复声明，可更改值
const isAdult = true;  // 不可重复声明，不可更改值
```

2. **数据类型**：JavaScript有七种数据类型：Number、String、Boolean、Object、Null、Undefined、Symbol。

```js
let num = 25; // Number
let str = "Hello World"; // String
let flag = true; // Boolean
let student = {name: "John", age: 25}; // Object
let empty = null; // Null
let notAssigned; // Undefined
let syb = Symbol("id"); // Symbol
```

3. **运算符**：JavaScript运算符包括算术运算符、赋值运算符、比较运算符、逻辑运算符等。

```js
let a = 5; let b = 3;
console.log(a + b); // 算术运算符
console.log(a = b); // 赋值运算符
console.log(a == b); // 比较运算符
console.log(a && b); // 逻辑运算符
```

4. **控制结构**：包括条件语句和循环语句。

```js
//条件语句
if (age > 18) {
  console.log("Adult");
} else {
  console.log("Not adult");
}

//循环语句
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

5. **函数**：函数是包含一些代码的可重复使用的代码块。

```js
function greet(name) {
  return "Hello" + name;
}
greet("John"); // "Hello John"
```

6. **数组**：数组是用来储存一系列值的数据结构。

```js
let fruits = ["Apple", "Banana", "Cherry"];
console.log(fruits[0]); // "Apple"
```

7. **对象**：对象是包围在花括号{}中的键值对（name: value）集合。

```js
let student = {
  name: "John",
  age: 25,
  isAdult: function() {
    return this.age > 18;
  }
};
console.log(student.isAdult()); // true
```

8. **事件**：事件是当事情发生时可以触发 JavaScript 函数/代码的 HTML。

```js
document.querySelector("button").addEventListener("click", function() {
  console.log("Button clicked!");
});
```

9. **错误处理**：使用try...catch...来处理可能引发错误的代码块。

```js
try {
  callAFunctionThatDoesntExist();
} catch(error) {
  console.log("An error occurred: ", error.message);
}
```

10. **异步编程**：在JavaScript中，异步编程是关键，包括回调函数、Promises和async/await。

```js
// 回调函数
setTimeout(function() {
  console.log('After 1 second');
}, 1000);

// Promise
let promise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve('Promise resolved');
  }, 1000);
});

promise.then(function(value) {
  console.log(value);
});

// async/await
async function asyncFunc() {
  // wait until the promise resolves
  let result = await promise;
  console.log(result);
}

asyncFunc();
```
## let与var的区别

`let`和`var`都是用于声明变量的关键字，但它们之间存在一些重要的差异：

1. **作用域**：`var`声明的变量具有函数作用域，这意味着如果变量在函数内部声明，那么它只能在该函数内部被访问。`let`声明的变量具有块作用域，也就是说，如果变量在一个块（如if语句或for循环等）内部声明，那么它只能在该块内部被访问。

```js
function testVar() {
  var x = 1;
  if (true) {
    var x = 2;  // 同一个变量，值被改写
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function testLet() {
  let x = 1;
  if (true) {
    let x = 2;  // 不同的变量，语句块内的x与函数内的x不同
    console.log(x);  // 2
  }
  console.log(x);  // 1
}

testVar();
testLet();
```

2. **提升**：JavaScript引擎会“提升”所有的`var`声明（不包括赋值），将它们移到当前作用域的顶部。这意味着你可以在声明前使用`var`变量，虽然这并不是好的实践。`let`声明不会被提升，若在声明之前使用`let`变量，会抛出错误。

```js
console.log(x);  // undefined
var x = 5;

console.log(y);  // ReferenceError: y is not defined
let y = 5;
```

3. **重复声明**：在同一个作用域内，`var`允许你重复声明同一个变量，而`let`不允许。

```js
var x = 1;
var x = 2;  // 没有问题

let y = 1;
let y = 2;  // SyntaxError: Identifier 'y' has already been declared
```

总的来说，`let`提供了更好的变量作用域控制，减少了一些常见的JavaScript错误，因此推荐在现代JavaScript开发中使用`let`代替`var`。
