```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class LinkedListVsArrayList {
    public static void main(String[] args) {
        // ArrayList 随机访问性能演示
        List<Integer> arrayList = new ArrayList<>();
        for (int i = 0; i < 1000000; i++) {
            arrayList.add(i);
        }

        long startTime = System.nanoTime();
        int randomIndex = 500000;
        int element = arrayList.get(randomIndex);
        long endTime = System.nanoTime();

        System.out.println("ArrayList Random Access Time: " + (endTime - startTime) + " ns");

        // LinkedList 随机访问性能演示
        List<Integer> linkedList = new LinkedList<>(arrayList);

        startTime = System.nanoTime();
        element = linkedList.get(randomIndex);
        endTime = System.nanoTime();

        System.out.println("LinkedList Random Access Time: " + (endTime - startTime) + " ns");

        // ArrayList 插入性能演示
        startTime = System.nanoTime();
        arrayList.add(500000, 9999);
        endTime = System.nanoTime();

        System.out.println("ArrayList Insertion Time: " + (endTime - startTime) + " ns");

        // LinkedList 插入性能演示
        startTime = System.nanoTime();
        linkedList.add(500000, 9999);
        endTime = System.nanoTime();

        System.out.println("LinkedList Insertion Time: " + (endTime - startTime) + " ns");

        // ArrayList 删除性能演示
        startTime = System.nanoTime();
        arrayList.remove(500000);
        endTime = System.nanoTime();

        System.out.println("ArrayList Deletion Time: " + (endTime - startTime) + " ns");

        // LinkedList 删除性能演示
        startTime = System.nanoTime();
        linkedList.remove(500000);
        endTime = System.nanoTime();

        System.out.println("LinkedList Deletion Time: " + (endTime - startTime) + " ns");
    }
}

```
## 结果：
![[Pasted image 20240203101709.png]]