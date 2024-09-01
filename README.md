# Java
前言：三狗狗的Java杂记，希望所有笔记都成为我前进的脚印。

---

## Javaの日常

### 1.sort() 方法：Arrays.sort() 是 Arrays 类中的一个静态方法，用于对数组进行排序。默认情况下，它对数组中的元素进行升序排序。
eg:
```Java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] nums1 = {5, 2, 9, 1, 5, 6};
        Arrays.sort(nums1);
        System.out.println(Arrays.toString(nums1)); // 输出: [1, 2, 5, 5, 6, 9]
    }
}
```

---

### 2.final 变量：被 final 修饰的变量在赋值之后，就不能再被重新赋值了。这种特性常用于定义常量。

---

### 3.用 boolean 命名的函数通常表示该函数会返回一个布尔值（true 或 false）。这类函数的主要目的是执行某种逻辑判断或条件验证，然后根据结果返回布尔类型的值。带有布尔返回类型的函数通常用于做逻辑判断，并根据条件返回 true 或 false。这种命名方式使代码更具可读性，开发者在调用这些函数时，可以直观地理解其功能与返回值的含义。

---

### 4.在 Java 中，双引号 (" ") 是用来表示字符串 (String) 的，而单引号 (' ') 是用来表示字符 (char) 的。

---

### 5.在 Java 中，字符用单引号表示，而字符串用双引号表示。== 可以用于比较两个 char 类型的值，但对于 String 类型的值，应使用 .equals() 方法进行比较。

---

### 6.静态上下文（例如静态方法或静态块）不能直接访问类的非静态成员（包括非静态方法和变量），因为静态成员属于类本身，而非静态成员属于类的实例。

#### 例子：

假设你有以下代码：
```Java
public class Main {
    public void judgment(char[][] grid) {
        // Some code
    }

    public static void main(String[] args) {
        judgment(grid);  // Error: Non-static method 'judgment(char[][])' cannot be referenced from a static context
    }
}
```
#### 问题

在 main 方法中，你尝试调用非静态的 judgment 方法，但 main 是静态方法。静态方法无法直接访问非静态方法，因为非静态方法依赖于类的具体实例。

#### 解决方案

有两种常见的解决方案：

1）将方法变为静态方法

如果该方法不依赖类的实例，可以将其声明为静态方法：
```Java
public class Main {
    public static void judgment(char[][] grid) {
        // Some code
    }

    public static void main(String[] args) {
        char[][] grid = {{'B', 'W'}, {'W', 'B'}};
        judgment(grid);  // Now it works
    }
}
```

2)创建类的实例并调用非静态方法

如果 judgment 方法依赖于类的实例，则在 main 方法中创建类的实例，并通过该实例调用非静态方法：
```Java
public class Main {
    public void judgment(char[][] grid) {
        // Some code
    }

    public static void main(String[] args) {
        Main mainInstance = new Main();
        char[][] grid = {{'B', 'W'}, {'W', 'B'}};
        mainInstance.judgment(grid);  // No error now
    }
}
``` 

---

### 7.类的实例和静态的区别

*实例成员（非静态成员）：每个类的实例（对象）都有自己独立的一份数据或方法。这些成员依赖于类的具体对象来访问或调用。例如，普通的类变量和方法通常是非静态的，属于类的实例。

*静态成员：静态成员是属于类本身的，不依赖于类的实例。静态成员可以直接通过类名调用，无需创建类的对象。

#### 例子说明

1)实例成员
```Java
public class Person {
    // 实例成员变量
    private String name;

    // 构造器用于初始化类的实例
    public Person(String name) {
        this.name = name;
    }

    // 实例方法
    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }

    public static void main(String[] args) {
        // 创建类的实例（对象）
        Person person = new Person("Alice");
        
        // 调用实例方法
        person.sayHello();  // 输出: Hello, my name is Alice
    }
}
```
在这个例子中，name 和 sayHello() 方法都是依赖于类的实例的。我们不能直接通过类名 Person 来调用 sayHello()，必须先创建 Person 类的对象 person，再通过这个对象调用该方法。

2)静态成员
```Java
public class Person {
    // 静态成员变量
    private static String species = "Homo sapiens";

    // 静态方法
    public static void showSpecies() {
        System.out.println("Species: " + species);
    }

    public static void main(String[] args) {
        // 可以直接通过类名调用静态方法
        Person.showSpecies();  // 输出: Species: Homo sapiens
    }
}
```
在这个例子中，species 和 showSpecies() 是静态的，它们属于类本身，和任何特定的实例无关。我们可以直接通过类名 Person 调用 showSpecies()，无需创建类的实例。
