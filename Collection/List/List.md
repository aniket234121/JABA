# List

The List interface is part of the Java Collections Framework and represents an ordered collection (also known as a
sequence).
Elements can be accessed by their index, and duplicates are allowed.

### Key Characteristics:

* Maintains insertion order
* Allows duplicate elements
* Supports positional access via index (0-based)
* Can include null elements

### Additional methods in list

| Method Signature                                       | Return Type       | Description                                                             |
|--------------------------------------------------------|-------------------|-------------------------------------------------------------------------|
| `void add(int index, E element)`                       | `void`            | Inserts element at the specified position                               |
| `boolean addAll(int index, Collection<? extends E> c)` | `boolean`         | Inserts all elements starting at the specified index                    |
| `E get(int index)`                                     | `E`               | Returns the element at the specified position                           |
| `E set(int index, E element)`                          | `E`               | Replaces element at the specified index                                 |
| `E remove(int index)`                                  | `E`               | Removes and returns element at the specified position                   |
| `int indexOf(Object o)`                                | `int`             | Returns the index of the first occurrence of the specified element      |
| `int lastIndexOf(Object o)`                            | `int`             | Returns the index of the last occurrence of the specified element       |
| `ListIterator<E> listIterator()`                       | `ListIterator<E>` | Returns a list iterator over the elements                               |
| `ListIterator<E> listIterator(int index)`              | `ListIterator<E>` | Returns a list iterator starting at the specified index                 |
| `List<E> subList(int fromIndex, int toIndex)`          | `List<E>`         | Returns a view of the portion of the list between the specified indices |

## 1. ArrayList

ArrayList is a resizable array implementation of the List interface in Java. It is part of the java.util package and
allows dynamic array operations (unlike arrays with fixed size).

* Implements List Interface
* Maintains insertion order
* Allows duplicate elements
* Supports random access via index (O(1) time)
* Grows automatically when elements are added beyond its capacity
* Multiple null values can be stored
* Not thread-safe by default. Use Collections.synchronizedList() for thread safety.
* Fast for random access (get(), set())
* Slower for insertions/removals in the middle (O(n) time)
* Default is 10; increases by 50% when resized

### Internal Working:

* Backed by an array of type Object [ ].
* When capacity is exceeded:
* A new larger array is created
* All old elements are copied to the new array

#### Constructors

| Constructor                            | Description                                          |
|----------------------------------------|------------------------------------------------------|
| `ArrayList()`                          | Creates an empty list with default capacity (10)     |
| `ArrayList(int initialCapacity)`       | Creates a list with specified initial capacity       |
| `ArrayList(Collection<? extends E> c)` | Creates a list with elements of the given collection |

## 2. Linked List

LinkedList is a part of the Java Collections Framework under the java.util package. It implements the List, Deque, and
Queue interfaces and is doubly-linked by default.

#### Characteristics

* Linked list class has Doubly linked list implementation.
* Allows null elements.
* Maintains insertion order.
* Not synchronized (use Collections.synchronizedList() for thread safety).
* Allows duplicate elements.

| Constructor                             | Description                                                                  |
|-----------------------------------------|------------------------------------------------------------------------------|
| `LinkedList()`                          | Creates an empty linked list.                                                |
| `LinkedList(Collection<? extends E> c)` | Creates a linked list with elements from the specified collection, in order. |

### Extra methods than other List implementations

| Method                 | Description                                                          |
|------------------------|----------------------------------------------------------------------|
| `addFirst(E e)`        | Inserts the element at the beginning of the list                     |
| `addLast(E e)`         | Appends the element to the end of the list                           |
| `getFirst()`           | Returns the first element (throws `NoSuchElementException` if empty) |
| `getLast()`            | Returns the last element                                             |
| `removeFirst()`        | Removes and returns the first element                                |
| `removeLast()`         | Removes and returns the last element                                 |
| `offerFirst(E e)`      | Inserts at the beginning (returns `true` if successful)              |
| `offerLast(E e)`       | Inserts at the end (returns `true` if successful)                    |
| `peekFirst()`          | Retrieves, but does not remove, the first element (or `null`)        |
| `peekLast()`           | Retrieves, but does not remove, the last element (or `null`)         |
| `pollFirst()`          | Retrieves and removes the first element (or `null`)                  |
| `pollLast()`           | Retrieves and removes the last element (or `null`)                   |
| `push(E e)`            | Pushes element onto the stack (same as `addFirst()`)                 |
| `pop()`                | Pops element from the stack (same as `removeFirst()`)                |
| `descendingIterator()` | Returns an iterator over the elements in reverse order               |

## 3. Vector

Vector is a legacy class in Java that implements the List interface and is part of the Java Collections Framework.
It is synchronized, which means it is thread-safe but generally slower than ArrayList in single-threaded environments.

### constructors

| Constructor                                          | Description                                                                               |
|------------------------------------------------------|-------------------------------------------------------------------------------------------|
| `Vector()`                                           | Creates a vector with initial capacity of 10.                                             |
| `Vector(int initialCapacity)`                        | Creates a vector with specified initial capacity.                                         |
| `Vector(int initialCapacity, int capacityIncrement)` | Creates a vector with specified capacity and increment size (how much to grow when full). |
| `Vector(Collection<? extends E> c)`                  | Creates a vector containing elements from a given collection.                             |

### unique methods in vector than other list implementations

| Method                              | Description                                                  |
|-------------------------------------|--------------------------------------------------------------|
| `addElement(E obj)`                 | Legacy method; adds element to the end (similar to `add()`). |
| `removeElement(Object obj)`         | Removes first occurrence of specified object.                |
| `removeElementAt(int index)`        | Removes the element at the specified index.                  |
| `insertElementAt(E obj, int index)` | Inserts element at specified index.                          |
| `elementAt(int index)`              | Returns the element at the specified index.                  |
| `firstElement()`                    | Returns the first element of the vector.                     |
| `lastElement()`                     | Returns the last element of the vector.                      |
| `setElementAt(E obj, int index)`    | Replaces element at the specified index.                     |
| `elements()`                        | Returns an `Enumeration` of the vector elements.             |
| `capacity()`                        | Returns the current capacity of the vector.                  |
| `ensureCapacity(int minCapacity)`   | Increases capacity if needed.                                |
| `trimToSize()`                      | Reduces internal array size to current number of elements.   |

### Difference between Vector and ArrayList

| Feature             | **Vector**                           | **ArrayList**                    |
|---------------------|--------------------------------------|----------------------------------|
| **Thread-safe**     | ✅ Yes (synchronized)                 | ❌ No (not synchronized)          |
| **Performance**     | ❌ Slower (due to synchronization)    | ✅ Faster (no sync overhead)      |
| **Grow policy**     | Doubles size when full               | Grows by 50% (1.5x size)         |
| **Legacy**          | ✅ Yes (older, before Java 1.2)       | ❌ No (modern, introduced in 1.2) |
| **Use in projects** | Rare, for old or multi-threaded code | Common, for modern Java apps     |

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
