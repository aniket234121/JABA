# Collectors Class

Collectors is a utility class in java.util.stream that provides static methods to accumulate elements of a stream into
various results, such as collections, strings, maps, statistics, etc.

### Methods

| Method                    | Signature                                                                                         | Return Type                                | Description                                                     |
|---------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------------------------------------|
| `toList()`                | `toList()`                                                                                        | `Collector<T, ?, List<T>>`                 | Collects elements into a `List`. Preserves order.               |
| `toSet()`                 | `toSet()`                                                                                         | `Collector<T, ?, Set<T>>`                  | Collects elements into a `Set`. Removes duplicates.             |
| `toMap()`                 | `toMap(Function<? super T, ? extends K> keyMapper, Function<? super T, ? extends U> valueMapper)` | `Collector<T, ?, Map<K,U>>`                | Collects elements into a map. Fails on duplicate keys.          |
|                           | `toMap(keyMapper, valueMapper, mergeFunction)`                                                    | `Collector<T, ?, Map<K,U>>`                | Handles duplicate keys with a merge function.                   |
|                           | `toMap(keyMapper, valueMapper, mergeFunction, mapSupplier)`                                       | `Collector<T, ?, M>`                       | Allows specifying a map type (like `LinkedHashMap`).            |
| `joining()`               | `joining()`                                                                                       | `Collector<CharSequence, ?, String>`       | Concatenates character sequences with no delimiter.             |
|                           | `joining(CharSequence delimiter)`                                                                 | `Collector<CharSequence, ?, String>`       | Concatenates with a delimiter.                                  |
|                           | `joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)`                       | `Collector<CharSequence, ?, String>`       | Concatenates with delimiter, prefix, and suffix.                |
| `groupingBy()`            | `groupingBy(Function<? super T, ? extends K>)`                                                    | `Collector<T, ?, Map<K, List<T>>>`         | Groups elements by a classifier function.                       |
|                           | `groupingBy(classifier, downstream)`                                                              | `Collector<T, ?, Map<K, D>>`               | Groups and collects using another collector.                    |
|                           | `groupingBy(classifier, supplier, downstream)`                                                    | `Collector<T, ?, M>`                       | Groups with a custom map supplier.                              |
| `partitioningBy()`        | `partitioningBy(Predicate<? super T>)`                                                            | `Collector<T, ?, Map<Boolean, List<T>>>`   | Partitions elements into two lists based on a predicate.        |
|                           | `partitioningBy(predicate, downstream)`                                                           | `Collector<T, ?, Map<Boolean, D>>`         | Partitions and collects using another collector.                |
| `counting()`              | `counting()`                                                                                      | `Collector<T, ?, Long>`                    | Counts the number of elements in the stream.                    |
| `summarizingInt()`        | `summarizingInt(ToIntFunction<? super T>)`                                                        | `Collector<T, ?, IntSummaryStatistics>`    | Collects count, sum, min, avg, and max of int values.           |
| `summarizingDouble()`     | `summarizingDouble(ToDoubleFunction<? super T>)`                                                  | `Collector<T, ?, DoubleSummaryStatistics>` | Same as above for `double`.                                     |
| `summarizingLong()`       | `summarizingLong(ToLongFunction<? super T>)`                                                      | `Collector<T, ?, LongSummaryStatistics>`   | Same as above for `long`.                                       |
| `mapping()`               | `mapping(Function<? super T, ? extends U>, Collector<? super U, A, R>)`                           | `Collector<T, A, R>`                       | Applies a function and collects using another collector.        |
| `reducing()`              | `reducing(BinaryOperator<T>)`                                                                     | `Collector<T, ?, Optional<T>>`             | Reduces elements using a binary operator.                       |
|                           | `reducing(U identity, Function<? super T, ? extends U>, BinaryOperator<U>)`                       | `Collector<T, ?, U>`                       | Maps elements and reduces them.                                 |
| `collectingAndThen()`     | `collectingAndThen(Collector<T, A, R>, Function<R, RR>)`                                          | `Collector<T, A, RR>`                      | Wraps another collector and applies a finishing transformation. |
| `filtering()` *(Java 9+)* | `filtering(Predicate<? super T>, Collector<? super T, A, R>)`                                     | `Collector<T, A, R>`                       | Filters stream elements before collecting.                      |

```java
package Java8.StreamAPI;

import java.util.*;
import java.util.stream.*;
import java.util.function.*;

public class CollectorsMethodsExamples   {

    static class Employee {
        String name;
        String department;
        int age;

        Employee(String name, String department, int age) {
            this.name = name;
            this.department = department;
            this.age = age;
        }

        String getName() { return name; }
        String getDepartment() { return department; }
        int getAge() { return age; }
    }

    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Bob");
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Employee> employees = Arrays.asList(
                new Employee("Alice", "HR", 30),
                new Employee("Bob", "IT", 25),
                new Employee("Charlie", "IT", 35),
                new Employee("David", "HR", 28),
                new Employee("Eve", "Sales", 40)
        );

        // 1. toList
        List<String> list = names.stream().collect(Collectors.toList());

        // 2. toSet
        Set<String> set = names.stream().collect(Collectors.toSet());

        // 3. toMap
        Map<String, Integer> nameLengthMap = names.stream()
                .collect(Collectors.toMap(Function.identity(), String::length, (a, b) -> a));

        // 4. joining
        String joined = names.stream().collect(Collectors.joining(", ", "[", "]"));

        // 5. groupingBy
        Map<String, List<Employee>> groupedByDept = employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));

        // 6. groupingBy with counting
        Map<String, Long> deptCount = employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment, Collectors.counting()));

        // 7. partitioningBy
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
                .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        // 8. counting
        long total = names.stream().collect(Collectors.counting());

        // 9. summarizingInt
        IntSummaryStatistics stats = names.stream()
                .collect(Collectors.summarizingInt(String::length));

        // 10. mapping
        Map<String, List<Integer>> deptAges = employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment,
                        Collectors.mapping(Employee::getAge, Collectors.toList())));

        // 11. reducing
        int sum = numbers.stream().collect(Collectors.reducing(0, Integer::sum));

        // 12. collectingAndThen
        List<String> unmodifiableNames = names.stream()
                .collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));

        // Output for visual verification
        System.out.println("List: " + list);
        System.out.println("Set: " + set);
        System.out.println("Map (toMap): " + nameLengthMap);
        System.out.println("Joined: " + joined);
        System.out.println("Grouped By Dept: " + groupedByDept);
        System.out.println("Dept Count: " + deptCount);
        System.out.println("Partitioned (Even/Odd): " + partitioned);
        System.out.println("Count: " + total);
        System.out.println("Summary Stats: " + stats);
        System.out.println("Mapped Dept Ages: " + deptAges);
        System.out.println("Sum (Reducing): " + sum);
        System.out.println("Unmodifiable Names: " + unmodifiableNames);
    }
}
```