# Enum map
EnumMap<K extends Enum<K>, V> is a specialized Map implementation designed exclusively for enum keys.

* Located in: java.util
* Internally optimized for enum-based key access

## Key Characteristics
Keys must be from a single enum type

Maintains natural order of enum constants (declaration order)

Not synchronized

Allows:
* ❌ Null keys → NOT allowed
* ✔ Null values → allowed
* Extremely fast and memory-efficient

### Internal Working
Internally backed by an array
Each enum constant has a fixed ordinal index

Mapping:

    enumKey.ordinal() → array index

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
```java
import java.util.EnumMap;

public class Main {
    enum Day {
        MONDAY, TUESDAY, WEDNESDAY
    }

    public static void main(String[] args) {

        EnumMap<Day, String> map = new EnumMap<>(Day.class);

        map.put(Day.MONDAY, "Work");
        map.put(Day.TUESDAY, "Gym");
        map.put(Day.WEDNESDAY, "Study");

        System.out.println("EnumMap: " + map);

        // Access
        System.out.println("Monday plan: " + map.get(Day.MONDAY));
    }
}
```
