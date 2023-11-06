# Java学习

## 理论

参考网站：
<https://www.runoob.com/java/java-tutorial.html>

Java是一种面向对象的编程语言，具有易用性、健壮性和安全性等特性。以下是Java的一些基础知识点：

1. **变量和数据类型**：Java有八种基本数据类型：byte, short, int, long, float, double, boolean 和 char。此外，您可以使用类创建自己的类型。

```java
int num = 10;  // 整型
double rate = 5.6;  // 浮点型
char letter = 'A';  // 字符型
boolean flag = true;  // 布尔型
String name = "John";  // 字符串型，String是Java的一个内置类
```

2. **操作符**：Java支持多种运算符，包括赋值、算数、关系、逻辑、位、三元等。

```java
int a = 5;
int b = 10;
int sum = a + b;  // 算数运算符
boolean result = (a == b);  // 关系运算符
result = !(a == b);  // 逻辑运算符
```

3. **控制流**：Java提供控制流结构，包括条件语句（if, switch）和循环语句（for, while, do while）。

```java
if (age >= 18) {
  System.out.println("Adult");
} else {
  System.out.println("Not adult");
}

for (int i = 0; i < 10; i++) {
  System.out.println(i);
}
```

4. **函数**：Java使用函数（在Java中称为方法）来封装可以重复使用的代码。

```java
public static void greet(String name) {
  System.out.println("Hello, " + name);
}
greet("John");
```

5. **数组**：Java数组是用来存储相同类型元素的容器。

```java
int[] numbers = new int[5];
numbers[0] = 1;
numbers[1] = 2;
// ...

String[] names = {"John", "Alice", "Bob"};
```

6. **对象和类**：Java是面向对象的语言，可以使用类创建对象。

```java
public class Dog {
  String name;

  public Dog(String name) {
    this.name = name;
  }

  public void bark(){
    System.out.println(name + " says: Woof!");
  }
}

Dog myDog = new Dog("Fido");
myDog.bark();
```

7. **继承和接口**：Java支持继承，一个类可以继承父类的属性和方法。Java也支持接口，接口定义了一种行为，一个类可以实现接口来表明它支持这种行为。

```java
public class Animal {
  public void eat() {
    System.out.println("The animal eats");
  }
}

public class Dog extends Animal {
  @Override
  public void eat() {
    System.out.println("The dog eats");
  }
}

Dog myDog = new Dog();
myDog.eat();

public interface Mammal {
  public void giveBirth();
}

public class Dog extends Animal implements Mammal {

  @Override
  public void giveBirth() {
    System.out.println("The dog gives birth");
  }
}

Dog myDog = new Dog();
myDog.giveBirth();
```

这些基础知识点只是入门Java的开始，要想深入学习Java，还需要掌握更多的知识，包括异常处理、多线程、泛型、集合框架、输入输出(IO)、网络编程、数据库连接(JDBC)以及Java的各种框架和类库。

## 环境准备

- jdk
- maven
- IDE

## 创建项目

## 项目配置

## 项目运行
