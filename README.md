# Java
前言：三狗狗的Java杂记，希望所有笔记都成为我前进的脚印。

---

# Javaの日常

# 1.sort() 方法：Arrays.sort() 是 Arrays 类中的一个静态方法，用于对数组进行排序。默认情况下，它对数组中的元素进行升序排序。

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
<br>

## 降序排序

对于对象数组（如 Integer[]），可以直接使用 Arrays.sort() 结合 __Collections.reverseOrder()__ 实现降序排列：
```Java
Integer[] nums1 = {5, 2, 9, 1, 5, 6};
Arrays.sort(nums1, Collections.reverseOrder());
// 排序后，nums1 = [9, 6, 5, 5, 2, 1]
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

---

### 8.`@Data` 是 Lombok 库中的一个注解，用于简化 Java 类中常见的样板代码。它会自动生成以下常用的代码：

1. **Getter 和 Setter 方法**：
   - 为类中的所有字段自动生成相应的 `get` 和 `set` 方法。

2. **`toString()` 方法**：
   - 自动生成 `toString()` 方法，输出对象的字段值，便于调试和日志记录。

3. **`equals()` 和 `hashCode()` 方法**：
   - 自动生成 `equals()` 和 `hashCode()` 方法，用于对象比较和散列操作。

4. **`RequiredArgsConstructor`**：
   - 生成一个包含所有 `final` 字段的构造方法，以及所有标记了 `@NonNull` 注解的字段。

使用 `@Data` 可以避免手动编写重复的代码，从而使代码更简洁、更易维护。它通常适用于简单的数据传输对象（DTO）或实体类中。

**示例**：
```java
@Data
public class User {
    private Long id;
    private String name;
    private String email;
}
```
这个注解将会自动生成 `id`、`name` 和 `email` 的 Getter、Setter、`toString()`、`equals()` 和 `hashCode()` 方法。

### 注意：
- 如果你需要定制某些方法，可能需要自己手动编写这些方法，避免 Lombok 的自动生成与手动代码冲突。

---

# 9.Java集合框架体系

![image](https://github.com/user-attachments/assets/c130884c-092a-412a-851f-2003f86fe172)

---

# 10.算法复杂度分析

![image](https://github.com/user-attachments/assets/b24dd79c-fda8-4995-a8d0-59ce1e512207)

![image](https://github.com/user-attachments/assets/38d5ab68-f092-4114-95a8-fc2b575c7f11)

![image](https://github.com/user-attachments/assets/e8ec847c-0e0b-47db-b0de-7c07c8358a6a)

![image](https://github.com/user-attachments/assets/2454800a-6a22-4cc2-aa23-fb5dd87bdc9e)

![image](https://github.com/user-attachments/assets/6b3146b4-d079-4da3-97f6-f12457ffcf5e)

![image](https://github.com/user-attachments/assets/cca71d64-e3c5-4622-a68b-a47e14f908b5)

![image](https://github.com/user-attachments/assets/70d052ab-942c-4f50-9724-193eac9a7b00)

![image](https://github.com/user-attachments/assets/2b1f154d-bfdb-44c3-93cb-4c085c910b31)

---

# 11.ArrayList数据结构——数组

![image](https://github.com/user-attachments/assets/c149df34-b089-4c48-956b-1662872cb627)

![image](https://github.com/user-attachments/assets/8b593442-95f3-4ea6-ab05-26fa129ab5dd)

![image](https://github.com/user-attachments/assets/7b1a4fff-3480-4f4e-982b-93c2d55bd169)

![image](https://github.com/user-attachments/assets/000093b7-5d7a-4344-beaf-63161780956b)

![image](https://github.com/user-attachments/assets/411443fc-285d-4e6e-b20a-c17821b3204e)

---

# 12.ArrayList源码分析

![image](https://github.com/user-attachments/assets/e85ca02c-d7c5-4450-8c9e-c547fdd1331e)

---

# 13.ArrayList底层原理及构造函数相关面试题回答

![image](https://github.com/user-attachments/assets/96358e7d-0e64-43c7-a899-5613c8751189)

![image](https://github.com/user-attachments/assets/9515752e-1648-4c60-96ce-74ae6e80f058)

---

# 14.ArrayList如何实现数组和List之间的转换

![image](https://github.com/user-attachments/assets/117872ad-806b-48b4-8c8e-f87ba08891c9)

![image](https://github.com/user-attachments/assets/a82868e9-0feb-4bfa-8cdf-c7be3845f1ba)

---

# 15.LinkedList数据结构——链表

![image](https://github.com/user-attachments/assets/22496283-df8c-447b-b7a1-8ed5f03656ab)

![image](https://github.com/user-attachments/assets/e7aacd26-3669-47ed-a061-bc6c47abd36b)

![image](https://github.com/user-attachments/assets/b04e644a-a5c5-4e03-85a4-bac4f1959e66)

![image](https://github.com/user-attachments/assets/f39bb9c7-395b-4eec-863e-62f4a37068a6)

![image](https://github.com/user-attachments/assets/b79e1702-da3d-4313-afb3-7e6c8132d69c)

![image](https://github.com/user-attachments/assets/1f968946-18f9-46f7-a0d2-eba8b6de5189)

---

# 16.ArrayList和LinkedList的区别是什么

![image](https://github.com/user-attachments/assets/56165176-10ae-42d4-abae-0284aa99c84e)

![image](https://github.com/user-attachments/assets/c8be56d8-a2a7-49e1-90ab-1bc724e198db)

![image](https://github.com/user-attachments/assets/03aab92b-512f-4bfa-a589-63ef9d92c41b)

---

# 17.二叉树

![image](https://github.com/user-attachments/assets/6f328667-9130-4b11-add7-1c10319918a8)

![image](https://github.com/user-attachments/assets/105e0f90-78e5-45e4-9bb6-9ca7164f5070)

![image](https://github.com/user-attachments/assets/0d6e4f58-3e69-4db2-a73f-6fdf181675e1)

---

# 18.红黑树

![image](https://github.com/user-attachments/assets/7912423e-fdaa-4f36-a18e-50144feba170)

![image](https://github.com/user-attachments/assets/8eb4dcec-4ddf-45e6-9b0e-cd029b687323)

![image](https://github.com/user-attachments/assets/4396d47d-9124-4106-91d5-9f321cce9efb)

---

# 19.散列表

![image](https://github.com/user-attachments/assets/99ed0ab3-d8b5-4916-a254-3440018fdb96)

![image](https://github.com/user-attachments/assets/18db2142-1e24-4ad4-a8c2-ffb944b8532d)

![image](https://github.com/user-attachments/assets/5691fcfc-3715-4743-9de2-dd98f2e30a10)

![image](https://github.com/user-attachments/assets/ee98ae94-6e40-43fa-95a4-e481eb3927ee)

![image](https://github.com/user-attachments/assets/fee2abb2-f04d-48c5-8377-8e023f52f866)

![image](https://github.com/user-attachments/assets/0f965297-9a1a-44a2-a812-bab5c6de1427)

![image](https://github.com/user-attachments/assets/9f8061f7-6444-4413-9481-a57033070173)

---

# 20.HashMap的实现原理

![image](https://github.com/user-attachments/assets/63cf993d-7054-46e0-b9c1-4102a34394bc)

![image](https://github.com/user-attachments/assets/9dd41c28-89a3-4ede-8f8f-0a6d5464302f)

![image](https://github.com/user-attachments/assets/ded0cdf2-f845-40b0-9f8a-529f8be78974)

---

# 21.HashMap的put方法的具体流程

![image](https://github.com/user-attachments/assets/941ff22a-e11b-4c1e-aa2a-6b8114b53d4d)

![image](https://github.com/user-attachments/assets/84437aaa-718f-41b2-87b5-a8372ec5da0b)

![image](https://github.com/user-attachments/assets/b500233a-9c43-4b7b-b6ac-29afa62a88a9)

![image](https://github.com/user-attachments/assets/5f1e5ce3-438d-4e98-aa47-b09889f87478)

---

# 22.HashMap的扩容机制

![image](https://github.com/user-attachments/assets/eb8d5408-e163-4b4c-849f-a42d1b9502b4)

![image](https://github.com/user-attachments/assets/bf6edbd7-da4a-4ed8-98c0-841ba21aedb2)

---

# 23.HashMap的寻址算法和数组长度为什么是2的n次幂

![image](https://github.com/user-attachments/assets/ca0a0fed-3cd4-47cc-ab83-f73aea34d8c1)

![image](https://github.com/user-attachments/assets/abe2b51d-d933-4a94-93d3-48e8ff6c5e0b)

![image](https://github.com/user-attachments/assets/a5429e88-8312-46e1-9d66-62f1c3182269)

---

# 24.HashMap在1.7情况下的多线程死循环问题

![image](https://github.com/user-attachments/assets/cd476948-48cb-4d2a-b725-e6e68169ccd8)

![image](https://github.com/user-attachments/assets/efcc55f5-f89a-4e56-b34f-833ab7ccffbb)

![image](https://github.com/user-attachments/assets/35f90070-8e42-411c-9077-710804744346)

---

# 25.JVM介绍、运行流程

![image](https://github.com/user-attachments/assets/b600c3e8-2b66-44d3-b359-61256595ec97)

![image](https://github.com/user-attachments/assets/e195f4dd-22bb-4d7e-8b26-c8df118bf12a)

![image](https://github.com/user-attachments/assets/afd11942-682d-49ab-9539-e47d85a38aa3)

![image](https://github.com/user-attachments/assets/56780185-e8da-4e80-b43c-ce22fa4b226d)

---

# 26.什么是程序计数器

![image](https://github.com/user-attachments/assets/87bff5bc-91a0-4fae-87e4-9bb7f5eb271a)

![image](https://github.com/user-attachments/assets/c9702a39-9053-4113-a5de-72a65ba813a6)

![image](https://github.com/user-attachments/assets/14a9a71d-b6b4-432b-94d9-352e7c5b7f0c)

---

# 27.详细介绍下Java堆

![image](https://github.com/user-attachments/assets/41ea3023-4af2-4241-9182-d5fcce119d4f)

![image](https://github.com/user-attachments/assets/5f12a701-b650-4b9f-a8d2-1b03773794fb)

![image](https://github.com/user-attachments/assets/e89a749a-dabe-425a-96df-bc42338ffe8b)

---

# 28.什么是虚拟机栈

