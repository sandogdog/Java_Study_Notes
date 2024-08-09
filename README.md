# Java
前言：三狗狗的Java杂记，希望所有笔记都成为我前进的脚印。

Javaの日常

1.sort() 方法：Arrays.sort() 是 Arrays 类中的一个静态方法，用于对数组进行排序。默认情况下，它对数组中的元素进行升序排序。
eg:
```
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] nums1 = {5, 2, 9, 1, 5, 6};
        Arrays.sort(nums1);
        System.out.println(Arrays.toString(nums1)); // 输出: [1, 2, 5, 5, 6, 9]
    }
}
