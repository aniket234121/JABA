# Immutable Map
It is sometimes preferable to disallow modifications to the java.util.Map such as sharing read-only data across threads. For this purpose, we can use either an Unmodifiable Map or an Immutable Map.

An Immutable Map is a map whose contents cannot be modified after creation.

* No addition, deletion, or update of entries
* Any modification attempt results in:
    * UnsupportedOperationException or
    * Creation of a new map (depending on implementation)

## Why Use Immutable Maps

* Thread-safe by design (no synchronization required)
* Prevents accidental modification
* Improves data integrity
* Suitable for constants and configuration data
* Often more memory efficient

## Ways to Create Immutable Maps in Java

### Using Map.of() (Java 9+)

```java
import java.util.Map;

Map<Integer, String> map = Map.of(
    1, "A",
    2, "B",
    3, "C"
);
```
#### Characteristics
* Immutable
* No null keys/values
* Throws UnsupportedOperationException on modification

### Using Map.ofEntries()
```java
import java.util.Map;

Map<Integer, String> map = Map.ofEntries(
    Map.entry(1, "A"),
    Map.entry(2, "B"),
    Map.entry(3, "C")
);
```

### Using Collections.unmodifiableMap()
```java
import java.util.*;

Map<Integer, String> temp = new HashMap<>();
temp.put(1, "A");
temp.put(2, "B");

Map<Integer, String> map = Collections.unmodifiableMap(temp);
```
#### Important
* Creates a read-only view, NOT truly immutable
* If temp changes → map also reflects changes