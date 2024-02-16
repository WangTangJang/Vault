ArrayList和普通数组有一些重要的区别，主要体现在灵活性、扩容机制、方法支持等方面。以下是它们之间的主要区别：
## 大小固定 vs. 动态扩容：
- 普通数组的大小是固定的，一旦创建后无法改变。如果需要更多的空间，必须创建一个新数组并手动复制元素。
- ArrayList可以动态扩容，当元素数量超过当前容量时，会自动创建一个更大的数组，并将元素复制到新数组中
## 自动装箱和拆箱：
- 普通数组可以存储基本数据类型（如int、char等），但不能存储对象。在需要使用基本数据类型时，必须使用其包装类。
- ArrayList只能存储对象，因此当存储基本数据类型时，会自动进行装箱和拆箱的操作。
## 灵活性和便利性：
- 普通数组在长度固定的情况下比较简单，但在动态增加或缩减元素时需要手动处理。
- ArrayList提供了一系列的方法和操作，使得在动态操作元素时更加方便，例如add、remove、get等方法。
## 方法支持：
- ArrayList类提供了一系列丰富的方法，使得操作元素更加方便，例如添加、删除、查找等。
- 普通数组只提供了有限的方法，操作相对较为简单，需要[[#example|手动]]实现大部分的操作。
## 性能差异：
- 在随机访问元素时，普通数组由于是连续内存，访问速度相对较快。
- 在插入和删除元素时，ArrayList由于动态扩容和元素移动，性能可能较普通数组差。
## 总结
总体而言，ArrayList提供了更多的灵活性和便利性，适用于需要动态管理元素数量的场景。普通数组在长度不变的情况下可能更加高效，但缺乏ArrayList提供的便利方法。选择使用哪种数据结构取决于具体的需求和使用场景。

## example
在 Java 中，普通数组（即原始的数组，如`int[]`、`double[]`等）没有内建的 `remove` 方法。如果需要从数组中删除元素，你需要手动实现这个操作，包括找到要删除的元素的位置，并将数组中的其他元素移动以填补空缺。
```java
public class ArrayRemoveExample {
    public static void main(String[] args) {
        int[] originalArray = {1, 2, 3, 4, 5};
        int elementToRemove = 3;

        // 找到要删除的元素的位置
        int indexToRemove = -1;
        for (int i = 0; i < originalArray.length; i++) {
            if (originalArray[i] == elementToRemove) {
                indexToRemove = i;
                break;
            }
        }

        // 如果找到要删除的元素，则进行删除操作
        if (indexToRemove != -1) {
            // 移动数组元素以填补空缺
            for (int i = indexToRemove; i < originalArray.length - 1; i++) {
                originalArray[i] = originalArray[i + 1];
            }

            // 缩小数组长度
            int[] newArray = new int[originalArray.length - 1];
            System.arraycopy(originalArray, 0, newArray, 0, newArray.length);

            // 更新原始数组的引用
            originalArray = newArray;
        }

        // 打印删除元素后的数组
        for (int value : originalArray) {
            System.out.print(value + " ");
        }
    }
}
```