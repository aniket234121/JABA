# ConcurrentSkipListSet
ConcurrentSkipListSet is a thread-safe, sorted Set implementation in the Java Collections Framework.

* Package: java.util.concurrent
* Implements: NavigableSet
* Backed by: ConcurrentSkipListMap
* Maintains sorted order
* Designed for high concurrency

## Internal Working

👉 Internally uses:

    ConcurrentSkipListMap<E, Object>
Elements are stored as keys
Value is a dummy constant (PRESENT)

## Data Structure Used

👉 Skip List

A Skip List is a probabilistic data structure that:

Maintains elements in sorted order
Uses multiple levels of linked lists
Provides fast search, insertion, deletion

### 📌 Skip List Structure (Concept)
    
    Level 3:        -----------50---------
    Level 2:     ----20----40----50-------
    Level 1:  10----20----30----40----50--
    Level 0:  10----20----30----40----50--

👉 Higher levels skip more elements → faster traversal

Level 0 → full list (normal sorted linked list)
Higher levels → fewer elements (shortcuts)

### 📌 Key Concept: “Skip”

Instead of traversing one-by-one like a linked list,
👉 Skip list jumps across nodes using higher levels

### 📌 How Search Works
Example: Search for 30

Steps:

    Start at top level (Level 3)
    Move forward until next element > target
    Drop down one level
    Repeat until Level 0

Example:
```java
import java.util.concurrent.ConcurrentSkipListSet;

public class ConcurrentSkipListSetExample {
    public static void main(String[] args) {

        ConcurrentSkipListSet<Integer> set = new ConcurrentSkipListSet<>();

        set.add(30);
        set.add(10);
        set.add(20);
        set.add(40);

        System.out.println("Set: " + set);

        // Navigation
        System.out.println("First: " + set.first());
        System.out.println("Higher than 20: " + set.higher(20));

        // Remove
        set.remove(10);

        System.out.println("After removal: " + set);
    }
}
```