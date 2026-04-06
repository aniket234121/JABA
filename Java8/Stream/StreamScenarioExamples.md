# 🧪 Java Stream API Practice Problems (10 Exercises)

| #  | Problem Title                     | Description                                                                                                                                        |
|----|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 1  | Filter Even Numbers               | Given a `List<Integer>`, return a new list containing only even numbers. <br>**Input**: `[1, 2, 3, 4]` → **Output**: `[2, 4]`                      |
| 2  | Find Unique Words from Sentences  | Given a `List<String>` (each element is a sentence), extract **unique words** (case-insensitive) using `flatMap`.                                  |
| 3  | Square and Remove Duplicates      | Given a `List<Integer>`, square each number and remove duplicates. <br>**Input**: `[1, 2, 3, 2]` → **Output**: `[1, 4, 9]`                         |
| 4  | Find the Maximum Salary           | Given a list of `Employee(name, salary)`, find the employee with the **maximum salary** using `max()` and return the name.                         |
| 5  | Group Students by Grade           | Given a list of `Student(name, grade)`, group students by their grade into a `Map<String, List<Student>>`.                                         |
| 6  | Partition Numbers by Even and Odd | Given a `List<Integer>`, partition them into even and odd using `partitioningBy`. Return `Map<Boolean, List<Integer>>`.                            |
| 7  | Sum of All Digits                 | Given a `List<Integer>`, flatten all digits and return their total sum. <br>**Input**: `[12, 34]` → **Output**: `10`                               |
| 8  | Word Count Map                    | Given a `List<String>` of words, return a `Map<String, Long>` that counts how many times each word occurs.                                         |
| 9  | Sort by Multiple Fields           | Given a list of `Person(name, age)`, sort them first by age, then by name (lexicographically). Return sorted list.                                 |
| 10 | Find First Palindrome             | Given a `List<String>`, return the **first word that is a palindrome** (case-insensitive). <br>**Input**: `["cat", "noon"]` → **Output**: `"noon"` |

> 💡 **Bonus:** Flatten a `List<int[]>` and return only **prime numbers** using `flatMapToInt()` + custom prime logic.

```java
package Java8.StreamAPI;

import UtilityClasses.Employee;
import UtilityClasses.Person;
import UtilityClasses.Student;

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamPracticeProblemsSolutions {


    //filter even no. from list....
    public static List<Integer> filterEven(List<Integer> list) {
        return list.stream().filter(x -> x % 2 == 0).collect(Collectors.toList());
    }

    // from list of sentences extract unique words
    public static List<String> ExtractUniqueWords(List<String> list) {
        return list.stream()
                .flatMap(item -> Arrays.stream(item.split(" ")))
                .distinct()
                .collect(Collectors.toList());
    }

    // Square and Remove Duplicates from list
    public static List<Integer> squareAndRemoveDuplicates(List<Integer> list) {
        return list.stream().map(x -> x * x).distinct().collect(Collectors.toList());
    }

    //return name of employee having maximum salary from list of employees
    public static String empHavingMaxSalary(List<Employee> list) {
        return list.stream()
                .max((a, b) -> (int) (a.getSalary() - b.getSalary()))
                .get().getName();
    }

    //from list of students group them into grades
    //Given a list of Student(name, grade), group students by their grade into a Map<String, List<Student>>.
    public static Map<String, List<Student>> groupStudentsByGrade(List<Student> list) {
        return list.stream().collect(Collectors.groupingBy(item -> item.getGrade(), Collectors.toList()));
    }

    //sum of all digits in list
    public static int sumOfElements(List<Integer> list) {
        return list.stream().mapToInt(x -> x).reduce((acc, val) -> acc += val).getAsInt();
    }

    //count how many times each word occurs
    public static Map<String, Integer> getWordFrequency(List<String> list) {
        return list.stream().collect(Collectors.groupingBy(item -> item, Collectors.collectingAndThen(Collectors.counting(), Long::intValue)));
    }

//    Sort by Multiple Fields	Given a list of Person(name, age),
//    sort them first by age, then by name (lexicographically). Return sorted list.
    public static List<Person> Sort(List<Person> list)
    {
        return list.stream().sorted((a,b)->a.getAge()- b.getAge()).sorted((a,b)->a.getName().compareTo(b.getName())).collect(Collectors.toList());
    }

    // from a list of String find firsPalindrome
    public static String findFirstPalindrom(List<String> list)
    {
        return list.stream().filter(x->{
            StringBuilder sb=new StringBuilder(x);
            StringBuilder sb2=sb.reverse();
            return sb.equals(sb2);
        }).findFirst().get();
    }

    public static void main(String[] args) {

        // Test 1: Filter Even Numbers
        List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);
        System.out.println(nums);
        System.out.println("Even Numbers: " + StreamPracticeProblemsSolutions.filterEven(nums));

        // Test 2: Extract Unique Words

        List<String> sentences = Arrays.asList("Java is great", "Streams are great", "Java Streams");
        System.out.println(sentences);
        System.out.println("Unique Words: " + StreamPracticeProblemsSolutions.ExtractUniqueWords(sentences));

        // Test 3: Square and Remove Duplicates
        List<Integer> sqList = Arrays.asList(1, 2, 3, 2, 4);
        System.out.println(sqList);
        System.out.println("Squared Unique: " + StreamPracticeProblemsSolutions.squareAndRemoveDuplicates(sqList));

        // Test 4: Employee with Max Salary
        List<Employee> employees = Arrays.asList(
                new Employee("Alice", 50000),
                new Employee("Bob", 70000),
                new Employee("Charlie", 65000)
        );
        System.out.println(employees);
        System.out.println("Max Salary Employee: " + StreamPracticeProblemsSolutions.empHavingMaxSalary(employees));

        // Test 5: Group Students by Grade
        List<Student> students = Arrays.asList(
                new Student("Aman", "A"),
                new Student("Neha", "B"),
                new Student("Ravi", "A"),
                new Student("Sita", "C"),
                new Student("John", "B")
        );
        System.out.println(students);
        Map<String, List<Student>> grouped = StreamPracticeProblemsSolutions.groupStudentsByGrade(students);
        grouped.forEach((grade, group) -> System.out.println("Grade " + grade + ": " + group));
    }
}
```