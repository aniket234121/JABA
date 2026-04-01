# WeakHashMap
The WeakHashMap is a hashtable-based implementation of the Map interface, with keys that are of a WeakReference type.

**An entry in a WeakHashMap will automatically be removed when its key is no longer in ordinary use, meaning that there is no single Reference that point to that key.**

When the garbage collection (GC) process discards a key, its entry is effectively removed from the map, so this class behaves somewhat differently from other Map implementations.

## Strong, Soft, and Weak References

### Strong References

The strong reference is the most common type of Reference that we use in our day to day programming:

    Integer prime = 1;
    String str=new String("hello")

The variable prime has a strong reference to an Integer object with value 1.

**Behavior**

Object is NOT eligible for GC as long as a strong reference exists

GC will never remove it automatically

### Weak Reference

A weak reference allows GC to collect the object as soon as no strong references exist.

```java
import java.lang.ref.WeakReference;

public class WeakExample {
    public static void main(String[] args) {
        String str = new String("Java");
        WeakReference<String> weakRef = new WeakReference<>(str);

        str = null; // remove strong reference

        System.gc();

        System.out.println(weakRef.get()); // may print null
    }
}
```

**Behavior**

* Object is collected immediately when GC runs
* Even if memory is sufficient

### Soft Reference
A soft reference keeps the object alive until memory becomes low.
```java

import java.lang.ref.SoftReference;

public class SoftExample {
    public static void main(String[] args) {
        SoftReference<String> softRef = new SoftReference<>(new String("Java"));

        System.out.println(softRef.get()); // usually not null

        System.gc();

        System.out.println(softRef.get()); // still likely not null
    }
}
```
**Behavior**

GC collects object ONLY when memory is insufficient
Otherwise, object remains

