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
