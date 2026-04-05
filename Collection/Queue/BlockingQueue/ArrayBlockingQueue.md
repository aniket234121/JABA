# ArrayBlockingQueue
ArrayBlockingQueue is a bounded, thread-safe, blocking queue backed by a fixed-size array.

This is a classic "bounded buffer", in which a fixed-sized array holds elements inserted by producers and extracted by consumers. 

**Once created, the capacity cannot be changed**. 

Attempts to put an element into a full queue will result in the operation blocking; attempts to take an element from an empty queue will similarly block.

It follows FIFO (First-In, First-Out) ordering and is widely used in producer-consumer systems.

## Constructors
    ArrayBlockingQueue(int capacity)
    ArrayBlockingQueue(int capacity, boolean fair)
    ArrayBlockingQueue(int capacity, boolean fair, Collection<? extends E> c)

ArrayBlockingQueue uses ONE lock for both producers and consumers.

Implication:

Simpler design

But:

Producer & consumer cannot work fully parallel

Slightly lower throughput

```java
import java.util.concurrent.ArrayBlockingQueue;

public class Main {
    public static void main(String[] args) {

        ArrayBlockingQueue<Integer> queue = new ArrayBlockingQueue<>(2);

        // Producer
        Runnable producer = () -> {
            try {
                for (int i = 1; i <= 5; i++) {
                    queue.put(i); // blocks if full
                    System.out.println("Produced: " + i);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        // Consumer
        Runnable consumer = () -> {
            try {
                while (true) {
                    int val = queue.take(); // blocks if empty
                    System.out.println("Consumed: " + val);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        new Thread(producer).start();
        new Thread(consumer).start();
    }
}
```