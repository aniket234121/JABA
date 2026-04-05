# Blocking Queue
BlockingQueue is a thread-safe queue interface that supports blocking operations for both insertion and removal.

It is designed for producer-consumer scenarios, where:

* Producers wait if the queue is full
* Consumers wait if the queue is empty
## heirarchy

    Queue
    └── BlockingQueue
            ├── ArrayBlockingQueue
            ├── LinkedBlockingQueue
            ├── PriorityBlockingQueue
            ├── DelayQueue
            └── SynchronousQueue

### In multithreading:

Without coordination → race conditions / busy waiting
Threads may:
* Try to consume when no data exists
* Overproduce → overflow

### BlockingQueue:

* Automatically handles synchronization
* Eliminates need for wait() / notify()
* Prevents CPU wastage (no busy spinning)
### Blocking Behavior
#### ➤ Producer (put)
    If queue is full → thread waits (blocked)
    When space frees → thread resumes
#### ➤ Consumer (take)
    If queue is empty → thread waits
    When element added → thread resumes

