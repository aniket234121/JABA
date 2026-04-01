# HashMap
HashMap is a hash table–based implementation of Map used for storing key-value pairs with O(1) average time complexity.

    Map<K, V> map = new HashMap<>();

* Internally uses Hashing

## Internal Data Structure (Java 8+)

**🧠 Core Structure:**

Array (Bucket) → LinkedList → Red-Black Tree (if needed)

    transient Node<K,V>[] table;

**📦 Node Structure:**

```java
static class Node<K,V> {
    final int hash;
    final K key;
    V value;
    Node<K,V> next;
}
```

## How HashMap Works (Step-by-Step)
### **🔁 put(K key, V value)**

Compute hash:

    int hash = key.hashCode();
    Improve hash (to reduce collisions):
    hash = hash ^ (hash >>> 16);

Find bucket index:

    index = (n - 1) & hash;
Insert logic:

If bucket empty → insert node

If same key → replace value

If collision → add to linked list

If list becomes large → convert to tree

🔍 get(K key)

### **Compute hash**
Find bucket

Traverse:

Linked list OR
Tree (log n lookup)

# Buckets & Collision Handling
**📦 Bucket Concept:**

Each array index = bucket

Multiple entries can exist in same bucket

**⚠️ Collision:**

Occurs when:

    hash(key1) == hash(key2)

**🔧 Handling Strategy:**

    Java 7:

    LinkedList only

    Java 8+:

    LinkedList → Red-Black Tree (if threshold crossed)

### Treeification (Java 8 Feature)
**🔁 When does LinkedList become Tree?**

    Condition	Value
    Bucket size ≥	8
    Table size ≥	64
Untreeify:

If size drops below 6 → back to LinkedList

## Collisions
For this to work correctly, equal keys must have the same hash, however, different keys can have the same hash. If two different keys have the same hash, the two values belonging to them will be stored in the same bucket. Inside a bucket, values are stored in a list and retrieved by looping over all elements. The cost of this is O(n).

As of Java 8 (see JEP 180), the data structure in which the values inside one bucket are stored is changed from a list to a balanced tree if a bucket contains 8 or more values, and it’s changed back to a list if, at some point, only 6 values are left in the bucket. This improves the performance to be O(log n).

## Capacity and Load Factor
To avoid having many buckets with multiple values, the capacity is doubled if 75% (the load factor) of the buckets become non-empty. The default value for the load factor is 75%, and the default initial capacity is 16. Both can be set in the constructor.
### 📊 Load Factor:
    loadFactor = 0.75 (default)
### 📦 Capacity:
    Initial: 16
### 🔥 Resize Trigger:
    size > capacity * loadFactor

Example:

    16 * 0.75 = 12 → resize at 13th element


### Using object as key (Important)

while using object as key we must override hashcode and equals method in the new class which object we are creating because map uses these class internally for all the functionality.

```java
import java.util.Objects;

class Person {
    private int id;
    private String name;

    public Person(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // ✅ Override equals()
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return id == person.id && Objects.equals(name, person.name);
    }

    // ✅ Override hashCode()
    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }
}
--- -----------------------------------------------
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {

        Map<Person, String> map = new HashMap<>();

        Person p1 = new Person(1, "Aniket");
        Person p2 = new Person(2, "Rahul");

        map.put(p1, "Engineer");
        map.put(p2, "Doctor");

        // 🔍 Retrieve using new object (same data)
        Person search = new Person(1, "Aniket");

        System.out.println(map.get(search)); // ✅ Engineer
    }
}
```

### What Happens If You DO NOT Override? 

**🚫 Default Behavior (Object class)**

* equals() → compares memory reference

* hashCode() → based on memory address
------

# 📘 HashMap Methods (Java)

## 🔹 Basic Operations

| Method | Return Type | Description |
|--------|------------|------------|
| put(K key, V value) | V | Inserts or updates key-value pair |
| get(Object key) | V | Returns value for given key or null |
| remove(Object key) | V | Removes mapping for key |
| containsKey(Object key) | boolean | Checks if key exists |
| containsValue(Object value) | boolean | Checks if value exists |
| size() | int | Returns number of entries |
| isEmpty() | boolean | Checks if map is empty |
| clear() | void | Removes all entries |

---

## 🔹 Bulk Operations

| Method | Return Type | Description |
|--------|------------|------------|
| putAll(Map<? extends K, ? extends V> m) | void | Copies all mappings from another map |

---

## 🔹 Collection Views

| Method | Return Type | Description |
|--------|------------|------------|
| keySet() | Set<K> | Returns all keys |
| values() | Collection<V> | Returns all values |
| entrySet() | Set<Map.Entry<K, V>> | Returns all key-value pairs |

---

## 🔹 Java 8+ Functional Methods

| Method | Return Type | Description |
|--------|------------|------------|
| getOrDefault(Object key, V defaultValue) | V | Returns value or default if key not found |
| putIfAbsent(K key, V value) | V | Inserts only if key is absent |
| compute(K key, BiFunction) | V | Recomputes value for key |
| computeIfAbsent(K key, Function) | V | Computes value if key not present |
| computeIfPresent(K key, BiFunction) | V | Updates value if key exists |
| merge(K key, V value, BiFunction) | V | Merges values for key |
| replace(K key, V value) | V | Replaces value if key exists |
| replace(K key, V oldVal, V newVal) | boolean | Replaces only if old value matches |
| forEach(BiConsumer) | void | Iterates over entries |

---

## 🔹 Utility Methods

| Method | Return Type | Description |
|--------|------------|------------|
| clone() | Object | Returns shallow copy |
| equals(Object o) | boolean | Compares maps |
| hashCode() | int | Returns hash code of map |

---

## 🔹 Important Notes

- `put()` returns **previous value** (important for interviews)
- `get()` returns **null if key not found**
- `entrySet()` is **most efficient for iteration**
- Functional methods are **preferred in modern Java (8+)**

Iterate with entry on map
```java
for(Map.Entry<String, Product> entry : productsByName.entrySet()) {
    Product product =  entry.getValue();
    String key = entry.getKey();
    //do something with the key and value
}
```