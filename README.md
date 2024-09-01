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
