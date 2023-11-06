# go修行之路

## 入门

Go，也称为Golang，是一种静态类型，编译型语言，它由Google开发，以其简洁的语法和强大的性能著称。

1. **变量和数据类型**：Go语言支持多种基本数据类型，包括整型（int）、浮点型（float32, float64）、字符串（string）、布尔型（bool）等。例如：
```go
var a int = 10 // int
var b float64 = 3.14 // float64
var c string = "hello" // string
var d bool = true // bool
```
另外，Go语言也支持复合类型，如数组（array）、切片（slice）、映射（map）和结构体（struct）等。

1. **控制结构**：Go语言的控制结构包括条件语句（if-else）、选择语句（switch）和循环语句（for）。例如：

```go
// if-else
num := 10
if num > 0 {
    fmt.Println("Positive")
} else {
    fmt.Println("Negative")
}

// switch
day := 5
switch day {
case 1:
    fmt.Println("Monday")
case 2:
    fmt.Println("Tuesday")
// other cases...
default:
    fmt.Println("Invalid day")
}

// for loop
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

3. **函数**：在Go语言中，你可以定义自己的函数来执行特定的任务。例如：

```go
func add(x int, y int) int {
    return x + y
}

fmt.Println(add(40, 2))  // prints 42
```

4. **结构体和方法**：Go语言支持创建自定义的数据类型，如结构体，并且可以为这些类型定义方法。例如：

```go
type Person struct {
    name string
    age  int
}

func (p Person) greet() string {
    return "Hello, my name is " + p.name
}

p := Person{"Bob", 30}
fmt.Println(p.greet())  // prints "Hello, my name is Bob"
```

5. **接口**：Go语言的接口是一种抽象类型，它定义了一组方法，但没有实现。任何实现了这些方法的类型都被认为实现了该接口。例如：

```go
type Shape interface {
    area() float64
}

type Circle struct {
    radius float64
}

func (c Circle) area() float64 {
    return math.Pi * c.radius * c.radius
}

c := Circle{5}
var s Shape = c
fmt.Println(s.area())  // prints 78.53981633974483
```

6. **并发**：Go语言的一个显著特性就是其对并发的支持，通过goroutine和通道（channel）可以方便地处理并发任务。例如：

```go
func hello() {
    fmt.Println("Hello from a goroutine!")
}

go hello()
fmt.Println("Hello from main!")
```
以上只是Go语言基础知识点的部分内容，实际上，Go语言的功能还包括错误处理、包和模块管理、内存管理、反射等更多特性。