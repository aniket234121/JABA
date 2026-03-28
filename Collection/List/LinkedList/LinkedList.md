
## 2. Linked List

LinkedList is a part of the Java Collections Framework under the java.util package. It implements the List, Deque, and
Queue interfaces and is doubly-linked by default.

#### Characteristics

* **Linked list class has Doubly linked list implementation.**
* **Allows null elements.**
* **Maintains insertion order.**

* Not synchronized (use Collections.synchronizedList() for thread safety).
* Allows duplicate elements.

| Constructor                             | Description                                                                  |
|-----------------------------------------|------------------------------------------------------------------------------|
| `LinkedList()`                          | Creates an empty linked list.                                                |
| `LinkedList(Collection<? extends E> c)` | Creates a linked list with elements from the specified collection, in order. |

## Extra methods than other List implementations

| Category             | Method / Feature        | Defined In        | Description                                                          |
|----------------------|------------------------|-------------------|----------------------------------------------------------------------|
| Extra Method         | addFirst(E e)          | LinkedList/Deque  | Inserts the element at the beginning of the list                     |
| Extra Method         | addLast(E e)           | LinkedList/Deque  | Appends the element to the end of the list                           |
| Extra Method         | offerFirst(E e)        | LinkedList/Deque  | Inserts at the beginning (returns true if successful)                |
| Extra Method         | offerLast(E e)         | LinkedList/Deque  | Inserts at the end (returns true if successful)                      |
| Extra Method         | getFirst()             | LinkedList/Deque  | Returns the first element (throws NoSuchElementException if empty)   |
| Extra Method         | getLast()              | LinkedList/Deque  | Returns the last element                                             |
| Extra Method         | peekFirst()            | LinkedList/Deque  | Retrieves, but does not remove, the first element (or null)          |
| Extra Method         | peekLast()             | LinkedList/Deque  | Retrieves, but does not remove, the last element (or null)           |
| Extra Method         | removeFirst()          | LinkedList/Deque  | Removes and returns the first element                                |
| Extra Method         | removeLast()           | LinkedList/Deque  | Removes and returns the last element                                 |
| Extra Method         | pollFirst()            | LinkedList/Deque  | Retrieves and removes the first element (or null)                    |
| Extra Method         | pollLast()             | LinkedList/Deque  | Retrieves and removes the last element (or null)                     |
| Extra Method         | push(E e)              | LinkedList/Deque  | Pushes element onto the stack (same as addFirst())                   |
| Extra Method         | pop()                  | LinkedList/Deque  | Pops element from the stack (same as removeFirst())                  |
| Extra Method         | descendingIterator()   | LinkedList        | Returns an iterator over elements in reverse order                   |
| Behavior Difference  | Doubly Linked Structure| LinkedList        | Uses nodes with prev/next references (non-contiguous memory)         |
| Behavior Difference  | Fast Insert/Delete     | LinkedList        | O(1) at ends, no shifting required                                  |
| Behavior Difference  | Slow Random Access     | LinkedList        | O(n) traversal required for index-based access                       |
| Behavior Difference  | Implements Deque       | LinkedList        | Supports queue, deque, and stack operations                          |
| Behavior Difference  | Not Synchronized       | LinkedList        | Not thread-safe by default                                           |

```java
import java.util.*;

public class SimpleLinkedList {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();

        // Adding elements
        list.add(10);
        list.add(20);
        list.add(30);

        // Display list
        System.out.println("List: " + list);

        // Access elements
        System.out.println("First: " + list.getFirst());
        System.out.println("Last: " + list.getLast());

        // Remove element
        list.removeFirst();

        System.out.println("After removal: " + list);
    }
}
```