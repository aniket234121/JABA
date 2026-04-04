
## 3. Vector

Vector is a legacy class in Java that implements the List interface and is part of the Java Collections Framework.

It is synchronized, which means it is thread-safe but generally slower than ArrayList in single-threaded environments.

If you don’t specify capacityIncrement:

* Capacity doubles automatically

### Internal Working
same as arraylist backed by array of Object[]

when array is full create new array with capacity and copy previous element then add new one.

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
| **Grow policy**     | Doubles size when full               | Grows by 100% (2x size)         |
| **Legacy**          | ✅ Yes (older, before Java 1.2)       | ❌ No (modern, introduced in 1.2) |
| **Use in projects** | Rare, for old or multi-threaded code | Common, for modern Java apps     |
