# DelayQueue
DelayQueue is a thread-safe, unbounded blocking queue where elements can only be taken after a specified delay has expired.

Package: java.util.concurrent
Implements: BlockingQueue<E>
Requirement: Elements must implement Delayed

It is essentially a time-based priority queue.

## Core Concept (Most Important)

Each element has:

A delay time
It becomes available only after delay expires

👉 Retrieval rule:

Only elements whose delay ≤ 0 can be removed

## Internal Working (Critical Section)
Data Structure

Internally uses a PriorityQueue (min-heap)

Ordering based on:

    getDelay(TimeUnit unit)
How ordering works

* Element with least remaining delay stays at head
* But even if it’s at head → it cannot be removed until delay expires

```java
import java.util.concurrent.*;

class Task implements Delayed {
    private long startTime;
    private String name;

    public Task(String name, long delayMillis) {
        this.name = name;
        this.startTime = System.currentTimeMillis() + delayMillis;
    }

    public long getDelay(TimeUnit unit) {
        long diff = startTime - System.currentTimeMillis();
        return unit.convert(diff, TimeUnit.MILLISECONDS);
    }

    public int compareTo(Delayed other) {
        return Long.compare(this.getDelay(TimeUnit.MILLISECONDS),
                            other.getDelay(TimeUnit.MILLISECONDS));
    }

    public String getName() {
        return name;
    }
}

public class Example {
    public static void main(String[] args) throws Exception {
        DelayQueue<Task> queue = new DelayQueue<>();

        queue.put(new Task("Task1", 3000));
        queue.put(new Task("Task2", 1000));

        while (!queue.isEmpty()) {
            System.out.println(queue.take().getName());
        }
    }
}
```
### Output:
    Task2
    Task1