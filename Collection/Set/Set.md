# Set
It is an unordered collection of objects in which duplicate values cannot be stored. It is an interface that implements the mathematical set. This interface adds a feature that restricts the insertion of duplicate elements.

No Specific Order: Does not maintain any specific order of elements (Exceptions: LinkedHashSet and TreeSet).

Allows One Null Element: Most Set implementations allow a single null element.

Implementation Classes: HashSet, LinkedHashSet, and TreeSet.

Thread-Safe Alternatives: For thread-safe operations, use ConcurrentSkipListSet or wrap a set using Collections.synchronizedSet().


Two interfaces extend the set implementation, that are, SortedSet and NavigableSet.

### implementations 
| Class           | Description                                                              |
| --------------- | ------------------------------------------------------------------------ |
| `HashSet`       | Backed by a `HashMap`; no ordering; allows one `null`                    |
| `LinkedHashSet` | Maintains insertion order; backed by a `LinkedHashMap`                   |
| `TreeSet`       | Sorted set based on natural order or a comparator; does not allow `null` |



| Use Case                                | Preferred Set   |
|-----------------------------------------|-----------------|
| No duplicates, no order required        | `HashSet`       |
| No duplicates, maintain insertion order | `LinkedHashSet` |
| No duplicates, sorted order required    | `TreeSet`       |


## 1. HashSet

* It ensures no duplicate elements are allowed.
* Backed by a HashMap internally
* Each element added is used as a key in the map, with a dummy value (PRESENT object).
* No guaranteed order of element
* Only one null is permitted since keys in HashMap allow one null.
* Constant-time performance for basic operations
* Average time complexity: add(), remove(), contains() = O(1)
* Worst-case = O(n) if hash collisions occur.
* Not synchronized 
It is not thread-safe; use Collections.synchronizedSet() or ConcurrentHashMap.newKeySet() for concurrent use.


1. Initial capacity and load factor affect performance
2. Default initial capacity = 16
3. Default load factor = 0.75
4. When size exceeds (capacity × load factor), it rehashes.


Uses hashCode() and equals() methods
Proper override of these methods is critical for correct behavior with custom objects.

### Constructors
| Constructor                                      | Description                                                                          |
|--------------------------------------------------|--------------------------------------------------------------------------------------|
| `HashSet()`                                      | Creates an empty `HashSet` with default capacity (16) and load factor (0.75)         |
| `HashSet(int initialCapacity)`                   | Creates a `HashSet` with specified initial capacity                                  |
| `HashSet(int initialCapacity, float loadFactor)` | Creates a `HashSet` with specified capacity and load factor                          |
| `HashSet(Collection<? extends E> c)`             | Creates a `HashSet` containing elements of the given collection (removes duplicates) |


## 2. TreeSet

* ✅ Implements Set, SortedSet, and NavigableSet
* ✅ Stores elements in sorted order (natural or using a custom comparator)
* ❌ Does not allow duplicate elements
* ❌ Does not allow null values (throws NullPointerException)
* ✅ Backed by a Red-Black Tree (self-balancing BST)

| Method                         | Description                                                               |
|--------------------------------|---------------------------------------------------------------------------|
| `add(E e)`                     | Adds the specified element in sorted order                                |
| `remove(Object o)`             | Removes the specified element if present                                  |
| `contains(Object o)`           | Returns `true` if the set contains the specified element                  |
| `clear()`                      | Removes all elements from the set                                         |
| `size()`                       | Returns the number of elements in the set                                 |
| `isEmpty()`                    | Checks if the set is empty                                                |
| `first()`                      | Returns the lowest (first) element                                        |
| `last()`                       | Returns the highest (last) element                                        |
| `higher(E e)`                  | Returns the least element strictly greater than `e`                       |
| `lower(E e)`                   | Returns the greatest element strictly less than `e`                       |
| `ceiling(E e)`                 | Returns the least element greater than or equal to `e`                    |
| `floor(E e)`                   | Returns the greatest element less than or equal to `e`                    |
| `pollFirst()`                  | Retrieves and removes the first (lowest) element                          |
| `pollLast()`                   | Retrieves and removes the last (highest) element                          |
| `descendingSet()`              | Returns a reverse order view of the elements in the set                   |
| `iterator()`                   | Returns an iterator over the elements                                     |
| `descendingIterator()`         | Returns an iterator over the elements in reverse order                    |
| `subSet(E from, E to)`         | Returns a view of the set between `from` (inclusive) and `to` (exclusive) |
| `headSet(E to)`                | Returns a view of elements strictly less than `to`                        |
| `tailSet(E from)`              | Returns a view of elements greater than or equal to `from`                |
| `forEach(Consumer<? super E>)` | Performs an action for each element in the set                            |


| Constructor                          | Description                                                                                    | Example                                                           |
|--------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `TreeSet()`                          | Creates an empty TreeSet sorted by natural order                                               | `TreeSet<Integer> set = new TreeSet<>();`                         |
| `TreeSet(Comparator<? super E> c)`   | Creates an empty TreeSet sorted using the specified comparator                                 | `TreeSet<String> set = new TreeSet<>(Comparator.reverseOrder());` |
| `TreeSet(Collection<? extends E> c)` | Creates a TreeSet containing the elements of the specified collection, sorted by natural order | `TreeSet<String> set = new TreeSet<>(List.of("a", "b", "a"));`    |
| `TreeSet(SortedSet<E> s)`            | Creates a TreeSet with the same elements and ordering as the given `SortedSet`                 | `TreeSet<Integer> set = new TreeSet<>(anotherSortedSet);`         |
