# CopyOnWriteArrayList 
it is a thread-safe variant of ArrayList from java.util.concurrent.

It follows Copy-On-Write (COW) strategy:

Every write operation (add/remove/update) creates a new copy of the underlying array.

## Internal Working
Maintains an immutable snapshot array

On modification:

* Lock is acquired
* New array is created
* Old data is copied
* Modification applied
* Reference updated

### **📌 Read Operation:**

**No locking**

**Direct access to array**

### **📌 Write Operation:**

**Lock + full array copy → expensive**

```java
import java.util.concurrent.CopyOnWriteArrayList;

public class Demo {
    public static void main(String[] args) {
        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();

        list.add(1);
        list.add(2);
        list.add(3);

        for (Integer i : list) {
            if (i == 2) {
                list.add(4); // No ConcurrentModificationException
            }
            System.out.println(i);
        }

        System.out.println("Final List: " + list);
    }
}
```

Fail-Safe Iterator

Works on snapshot

No ConcurrentModificationException