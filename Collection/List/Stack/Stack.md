
## 4. Stack

Stack is a legacy class in Java that represents a Last-In-First-Out (LIFO) data structure.

It is used when elements need to be accessed in reverse order (last inserted, first removed)

* Thread-safe because it inherits all methods from Vector.
* Maintains insertion order, like a list.
* Not recommended for high-performance, single-threaded applications.
* Considered legacy but still usable.

### unique methods in Stack

| Stack's Own Method | Description                                  |
|--------------------|----------------------------------------------|
| `push(E item)`     | Adds to top of stack                         |
| `pop()`            | Removes and returns top                      |
| `peek()`           | Returns top without removing                 |
| `empty()`          | Checks if stack is empty                     |
| `search(Object o)` | 1-based position from top, `-1` if not found |


**Note:- Stack gets:**
* All Vector methods
* All List methods
* All Collection methods
* All Iterable methods
* Plus: It defines its own 5 unique methods.

### Constructors
| Constructor | Description                                                                              |
|-------------|------------------------------------------------------------------------------------------|
| `Stack()`   | Creates an **empty stack** with an initial capacity of **10** (inherited from `Vector`). |

```java
public static void main(String [] args){
    Stack<Integer> stack=new Stack();
    stack.push(1);
    stack.push(2);
    stack.push(3);
    System.out.println(stack)
    stack.pop()
    System.out.println(stack)

}
```