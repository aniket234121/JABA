# Synchronous Queue
SynchronousQueue is a special BlockingQueue with zero capacity.

Package: java.util.concurrent

Implements: BlockingQueue<E>
Capacity: 0 (no storage at all)

It is not a queue in the traditional sense — it is a direct handoff mechanism between threads.

## SynchronousQueue works on producer–consumer rendezvous:

A producer thread must wait until a consumer takes the element
A consumer thread must wait until a producer provides the element

👉 No element is ever stored internally.

## Internal Working (Critical Understanding)

Unlike other queues:

    ❌ No array
    ❌ No linked list
    ❌ No buffering

Instead, it uses:

Thread-to-thread transfer mechanism

```java
import java.util.concurrent.*;

public class Example {
    public static void main(String[] args) {
        SynchronousQueue<Integer> queue = new SynchronousQueue<>();

        // Consumer
        new Thread(() -> {
            try {
                System.out.println("Waiting to consume...");
                int value = queue.take();
                System.out.println("Consumed: " + value);
            } catch (InterruptedException e) {}
        }).start();

        // Producer
        new Thread(() -> {
            try {
                Thread.sleep(2000);
                System.out.println("Producing 10...");
                queue.put(10);
            } catch (InterruptedException e) {}
        }).start();
    }
}
```

### Output

    Waiting to consume...
    (after 2 sec)
    Producing 10...
    Consumed: 10

