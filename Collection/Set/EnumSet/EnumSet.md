# EnumSet
EnumSet is a specialized Set implementation for enum types only.

* Package: java.util
* Works only with enum elements
* Extremely fast and memory-efficient

## Internal Working

Internally implemented using bit vectors (bit masks)

How it works:
* Each enum constant is assigned a bit position
* Presence of element = bit = 1
* Absence = bit = 0

### Example

    enum Day {
        MON, TUE, WED, THU, FRI, SAT, SUN
    }

If set contains:

    [MON, WED, FRI]

Internally stored as:

    1 0 1 0 1 0 0   (bit vector)

👉 This makes operations extremely fast (bitwise operations)

## Types of EnumSet
### 1. RegularEnumSet

* Used when enum has ≤ 64 elements
* Uses single long (64-bit)
### 2. JumboEnumSet
* Used when enum has > 64 elements
* Uses long array

```java
import java.util.EnumSet;

enum Day {
    MON, TUE, WED, THU, FRI, SAT, SUN
}

public class EnumSetExample {
    public static void main(String[] args) {

        EnumSet<Day> set = EnumSet.of(Day.MON, Day.WED, Day.FRI);

        System.out.println("EnumSet: " + set);

        // Add element
        set.add(Day.SUN);

        // Check element
        System.out.println("Contains MON? " + set.contains(Day.MON));

        // Remove element
        set.remove(Day.WED);

        System.out.println("After removal: " + set);
    }
}
```
### Output:

    EnumSet: [MON, WED, FRI]
    Contains MON? true
    After removal: [MON, FRI, SUN]