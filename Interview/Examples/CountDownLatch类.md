`CountDownLatch`是Java并发包中的一个同步工具类，用于协调多个[[什么是线程？如何创建线程？|线程]]之间的同步操作。它的作用是允许一个或多个线程等待其他线程完成执行操作，然后再继续执行。

CountDownLatch的核心是一个计数器，该计数器初始化一个正整数，表示需要等待完成的线程数量。每个线程完成自己的任务时，计数器减1。当计数器值达到零时，所有等待的线程就会被唤醒，可以继续执行。

`CountDownLatch`的主要方法包括：

1. **`CountDownLatch(int count)`：** 构造函数，初始化计数器的值。

2. **`void await()`：** 调用此方法的线程会等待计数器减到零，即等待其他线程执行完毕。如果计数器已经是零，则该方法立即返回。

3. **`void countDown()`：** 计数器减1，表示一个线程已经执行完毕。

下面是一个简单的示例，演示了如何使用`CountDownLatch`：

```java
import java.util.concurrent.CountDownLatch;

public class CountDownLatchExample {

    public static void main(String[] args) throws InterruptedException {
        final int threadCount = 3;
        CountDownLatch countDownLatch = new CountDownLatch(threadCount);

        for (int i = 0; i < threadCount; i++) {
            new Thread(() -> {
                // 模拟线程执行一些操作
                System.out.println(Thread.currentThread().getName() + " is working");
                // 操作完成后调用countDown
                countDownLatch.countDown();
            }).start();
        }

        // 主线程等待所有线程执行完毕
        countDownLatch.await();

        System.out.println("All threads have finished their work. Continue with the main thread.");
    }
}
```

在这个例子中，主线程创建了3个子线程，并通过`countDownLatch.await()`等待这3个子线程执行完毕。每个子线程在完成工作后都会调用`countDown()`方法减小计数器。当计数器减到零时，主线程被唤醒，输出相应的信息。

`CountDownLatch`在并发编程中常用于等待一组线程执行完毕，然后执行下一步操作，或者等待多个任务完成后进行汇总处理。