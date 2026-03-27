# Queue < Interface >

The Queue Interface is a part of java.util package and extends the Collection interface. It stores and processes the
data in order means elements are inserted at the end and removed from the front.

### Queue Interface Methods

| Method Signature     | Return Type | Description                                                               | Behavior on Failure            |
|----------------------|-------------|---------------------------------------------------------------------------|--------------------------------|
| `boolean add(E e)`   | boolean     | Inserts element into the queue. Throws `IllegalStateException` if full.   | Exception if capacity exceeded |
| `boolean offer(E e)` | boolean     | Inserts element if possible. Returns false if the queue is full.          | `false` if full                |
| `E remove()`         | E           | Retrieves and removes the head. Throws `NoSuchElementException` if empty. | Exception if empty             |
| `E poll()`           | E           | Retrieves and removes the head. Returns `null` if empty.                  | `null` if empty                |
| `E element()`        | E           | Retrieves but does not remove the head. Throws `NoSuchElementException`.  | Exception if empty             |
| `E peek()`           | E           | Retrieves but does not remove the head. Returns `null` if empty.          | `null` if empty                |

**Note:- the implementing class of queue interface will have all the methods from collection interface and also these 6
methods in queue interface. i.e.**

### All the Methods that are present inside implementing classes of queue.

| Method Signature                            | Defined In | Description                                                    |
|---------------------------------------------|------------|----------------------------------------------------------------|
| `boolean add(E e)`                          | Queue      | Inserts element. Throws if queue is full.                      |
| `boolean offer(E e)`                        | Queue      | Inserts element if possible. Returns false if full.            |
| `E remove()`                                | Queue      | Removes and returns head. Throws if empty.                     |
| `E poll()`                                  | Queue      | Removes and returns head. Returns null if empty.               |
| `E element()`                               | Queue      | Peeks head. Throws if empty.                                   |
| `E peek()`                                  | Queue      | Peeks head. Returns null if empty.                             |
| `int size()`                                | Collection | Returns number of elements in the queue.                       |
| `boolean isEmpty()`                         | Collection | Checks if the queue is empty.                                  |
| `boolean contains(Object o)`                | Collection | Checks if queue contains the specified element.                |
| `Iterator<E> iterator()`                    | Collection | Returns an iterator over the elements.                         |
| `Object[] toArray()`                        | Collection | Returns array of all elements.                                 |
| `<T> T[] toArray(T[] a)`                    | Collection | Returns array of elements in specified array type.             |
| `boolean remove(Object o)`                  | Collection | Removes a single instance of specified element.                |
| `boolean containsAll(Collection<?> c)`      | Collection | Checks if queue contains all elements in specified collection. |
| `boolean addAll(Collection<? extends E> c)` | Collection | Adds all elements from specified collection.                   |
| `boolean removeAll(Collection<?> c)`        | Collection | Removes all queue elements also in specified collection.       |
| `boolean retainAll(Collection<?> c)`        | Collection | Retains only elements also in specified collection.            |
| `void clear()`                              | Collection | Removes all elements.                                          |
| `boolean equals(Object o)`                  | Collection | Compares the queue to another object.                          |
| `int hashCode()`                            | Collection | Returns hash code of the queue.                                |

## 1. Priority Queue

A PriorityQueue is a special type of queue where elements are ordered according to their natural ordering (if they
implement Comparable) or by a custom Comparator provided at queue construction.

* It is not a FIFO queue like LinkedList or ArrayDeque.

* The head of the queue is the least element based on the ordering.

* Internally implemented using a binary heap (usually a Min-Heap).

* Stored as an array and satisfies the heap property: the parent is less than or equal to the children.

* Uses a Min-Heap by default, where the smallest element has the highest priority.

* Can use a custom Comparator to define a Max-Heap or other custom ordering.

* PriorityQueue does not allow null elements. Inserting null will throw NullPointerException.

* PriorityQueue is not thread-safe. Use PriorityBlockingQueue for concurrent scenarios.

* Allows duplicate elements.

### Constructors

| Constructor Signature            | Description                     |
|----------------------------------|---------------------------------|
| `PriorityQueue()`                | Natural order, default capacity |
| `PriorityQueue(int)`             | Natural order, custom capacity  |
| `PriorityQueue(int, Comparator)` | Custom comparator and capacity  |
| `PriorityQueue(Collection)`      | Initialize from a collection    |
| `PriorityQueue(PriorityQueue)`   | Copy another priority queue     |
| `PriorityQueue(SortedSet)`       | Initialize from sorted set      |

## Deque < Interface>

The Deque interface in Java is a part of the Java Collections Framework and is used to represent a double-ended queue.

This means you can insert and remove elements from both ends — front and rear.

Key Features of Deque

* Extends Queue interface.
* Allows insertion and removal at both ends.
* Supports LIFO (stack) and FIFO (queue) operations.
* Can be bounded (capacity-limited) or unbounded.
* Null elements are not allowed in most implementations like ArrayDeque

### Common Implementations

1. ArrayDeque (most used, fast and efficient)
2. LinkedList (also implements Deque)
3. ConcurrentLinkedDeque (for concurrent access)

#### Methods

| Method                            | Description                                                                |
|-----------------------------------|----------------------------------------------------------------------------|
| `addFirst(E e)`                   | Inserts the specified element at the front of the deque                    |
| `addLast(E e)`                    | Inserts the specified element at the rear of the deque                     |
| `offerFirst(E e)`                 | Offers to insert the element at the front; returns `false` on failure      |
| `offerLast(E e)`                  | Offers to insert the element at the rear; returns `false` on failure       |
| `removeFirst()`                   | Removes and returns the first element of the deque                         |
| `removeLast()`                    | Removes and returns the last element of the deque                          |
| `pollFirst()`                     | Removes and returns the first element, or returns `null` if empty          |
| `pollLast()`                      | Removes and returns the last element, or returns `null` if empty           |
| `getFirst()`                      | Retrieves the first element without removing it; throws exception if empty |
| `getLast()`                       | Retrieves the last element without removing it; throws exception if empty  |
| `peekFirst()`                     | Retrieves the first element or `null` if empty                             |
| `peekLast()`                      | Retrieves the last element or `null` if empty                              |
| `removeFirstOccurrence(Object o)` | Removes the first occurrence of the specified element                      |
| `removeLastOccurrence(Object o)`  | Removes the last occurrence of the specified element                       |
| `push(E e)`                       | Pushes an element onto the stack represented by the deque (front)          |
| `pop()`                           | Pops an element from the stack represented by the deque (front)            |
| `descendingIterator()`            | Returns an iterator over elements in reverse order                         |

## 1. ArrayDeque

In Java, the ArrayDeque is a resizable array implementation of the Deque interface, which stands for double-ended queue.
It allows elements to be added or removed from both ends efficiently. It can be used as a stack (LIFO) or a queue (
FIFO).

* ArrayDeque grows dynamically.
* It generally provides faster operations than LinkedList because it does not have the overhead of node management.
* Operations like addFirst(), addLast(), removeFirst(), removeLast() are all done in constant time O(1).
* The ArrayDeque class implements these two interfaces Queue interface and Deque interface. support concurrent access by
  multiple threads

| Constructor                             | Description                                                     |
|-----------------------------------------|-----------------------------------------------------------------|
| `ArrayDeque()`                          | Creates an empty deque with default capacity                    |
| `ArrayDeque(int numElements)`           | Creates a deque with initial capacity                           |
| `ArrayDeque(Collection<? extends E> c)` | Creates a deque containing the elements of the given collection |
