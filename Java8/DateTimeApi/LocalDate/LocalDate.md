# LocalDate

* **now()** -> gives current date.
* **of(2000,06,09)** -> to create any date object. ( inbuilt validation for dates create using of)
* **isAfter(date obj)**  ->check is called Date obj is after passed date obj.
* **isBefore(date obj)** ->check is called Date obj is before passed date obj.
* **plusMongths(long no. of month to add)** add the month to the old date and return new date object.

| Function                             | Description                                                   | Syntax                          |
|--------------------------------------|---------------------------------------------------------------|---------------------------------|
| `now()`                              | Gets the current date from the system clock                   | `LocalDate.now()`               |
| `of(int year, int month, int day)`   | Obtains an instance of `LocalDate` from year, month, and day  | `LocalDate.of(2025, 6, 4)`      |
| `parse(CharSequence text)`           | Parses a `LocalDate` from a text string                       | `LocalDate.parse("2025-06-04")` |
| `getYear()`                          | Gets the year field                                           | `date.getYear()`                |
| `getMonth()`                         | Gets the month as a `Month` enum                              | `date.getMonth()`               |
| `getMonthValue()`                    | Gets the month as an int from 1 to 12                         | `date.getMonthValue()`          |
| `getDayOfMonth()`                    | Gets the day of the month                                     | `date.getDayOfMonth()`          |
| `getDayOfWeek()`                     | Gets the day of the week as a `DayOfWeek` enum                | `date.getDayOfWeek()`           |
| `getDayOfYear()`                     | Gets the day of the year                                      | `date.getDayOfYear()`           |
| `isLeapYear()`                       | Checks if the year is a leap year                             | `date.isLeapYear()`             |
| `lengthOfMonth()`                    | Returns the length of the month in days                       | `date.lengthOfMonth()`          |
| `lengthOfYear()`                     | Returns the length of the year in days                        | `date.lengthOfYear()`           |
| `plusDays(long daysToAdd)`           | Returns a copy with the specified number of days added        | `date.plusDays(5)`              |
| `minusDays(long daysToSubtract)`     | Returns a copy with the specified number of days subtracted   | `date.minusDays(3)`             |
| `plusMonths(long monthsToAdd)`       | Returns a copy with the specified number of months added      | `date.plusMonths(2)`            |
| `minusMonths(long monthsToSubtract)` | Returns a copy with the specified number of months subtracted | `date.minusMonths(1)`           |
| `plusYears(long yearsToAdd)`         | Returns a copy with the specified number of years added       | `date.plusYears(1)`             |
| `minusYears(long yearsToSubtract)`   | Returns a copy with the specified number of years subtracted  | `date.minusYears(1)`            |
| `withDayOfMonth(int dayOfMonth)`     | Returns a copy with the day of month altered                  | `date.withDayOfMonth(15)`       |
| `withMonth(int month)`               | Returns a copy with the month altered                         | `date.withMonth(12)`            |
| `withYear(int year)`                 | Returns a copy with the year altered                          | `date.withYear(2030)`           |
| `until(ChronoLocalDate endDate)`     | Calculates the period between two dates                       | `date.until(otherDate)`         |
| `isBefore(ChronoLocalDate other)`    | Checks if this date is before the specified date              | `date.isBefore(otherDate)`      |
| `isAfter(ChronoLocalDate other)`     | Checks if this date is after the specified date               | `date.isAfter(otherDate)`       |
| `equals(Object otherDate)`           | Checks if this date is equal to the specified date            | `date.equals(otherDate)`        |
| `toString()`                         | Converts the date to a string                                 | `date.toString()`               |


# Java `LocalDate` Task List (Easy to Hard)

A series of tasks to practice and master the `LocalDate` class in Java.

---

## ✅ Task 1: Basic LocalDate Creation and Formatting (Easy)

Write a method to:

- Create today’s date.
- Create a specific date (e.g., `1995-08-20`).
- Format both dates in the `"dd-MM-yyyy"` pattern.

---

## ✅ Task 2: Date Arithmetic (Moderate)

Write a method that:

- Takes a `LocalDate` input.
- Adds 45 days.
- Subtracts 3 months.
- Returns the resulting date.

---

## ✅ Task 3: Check for Recurring Events (Moderate)

Write a method that:

- Takes two inputs: a `LocalDate` of a birthday and today’s date.
- Checks if today is that birthday (ignoring the year).
- Returns `true` if it is, otherwise `false`.

---

## ✅ Task 4: List All Mondays in a Given Month (Intermediate)

Write a method that:

- Takes a year and month as input.
- Returns a list of all dates that fall on a **Monday** in that month.

💡 *Hint*: Use `TemporalAdjusters` and `DayOfWeek.MONDAY`.

---

## ✅ Task 5: Date Range Validation & Counting (Hard)

Write a method that:

- Takes two `LocalDate` inputs: `startDate` and `endDate`.
- Validates that `startDate` is before `endDate`.
- Counts how many **Saturdays** and **Sundays** fall within the date range.
- Returns the counts using either a custom class or a `Map<String, Integer>`.

---
```java
package Java8.DateTimeApi.LocalDate;

import java.time.*;
import java.time.format.DateTimeFormatter;
import java.time.temporal.TemporalAdjusters;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class LocalDateExample {

    /*task list methods from localDate.md file
    Write a method to:

            - Create today’s date.
            - Create a specific date (e.g., `1995-08-20`).
            - Format both dates in the `"dd-MM-yyyy"` pattern.*/
    public static void basicLocalDate() {
        //create today date
        LocalDate today = LocalDate.now();
        LocalDate specificDate = LocalDate.of(1995, 8, 20);

        System.out.println("today date: " + today);
        System.out.println("specific date: " + specificDate);

        //formatter to "dd-MM-yyyy"
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("d-M-y");

        // format() returns string....
        String formattedDate = specificDate.format(formatter);
        System.out.println("formatter date: " + formattedDate);
    }


    /*
    Write a method that:

    - Takes a `LocalDate` input.
    - Adds 45 days.
    - Subtracts 3 months.
    - Returns the resulting date.
     */
    public static LocalDate DateArithmetic(LocalDate dateArg)
    {
        return dateArg.plusDays(45).minusMonths(3);
    }

    /*
    Write a method that:

    - Takes two inputs: a `LocalDate` of a birthday and today’s date.
    - Checks if today is that birthday (ignoring the year).
    - Returns `true` if it is, otherwise `false`.

     */
    public static boolean checkBirthday(LocalDate birthday,LocalDate today)
    {
        return birthday.getMonthValue()==today.getMonthValue()&&birthday.getDayOfMonth()==today.getDayOfMonth();
    }


    /*

    Write a method that:

    - Takes a year and month as input.
    - Returns a list of all dates that fall on a **Monday** in that month.

    *Hint* Use `TemporalAdjusters` and `DayOfWeek.MONDAY`

    */
    public static List<LocalDate> MondayDates(int year,int month){

        List<LocalDate> mondays=new ArrayList<>();
        LocalDate date=LocalDate.of(year,month,1);
        LocalDate monday=date.with(TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY));


        while(monday.getMonthValue()==month)
        {
            mondays.add(monday);
            monday=monday.plusDays(7);
        }
        return mondays;
    }
/*

    Write a method that:

    - Takes two `LocalDate` inputs: `startDate` and `endDate`.
    - Validates that `startDate` is before `endDate`.
    - Counts how many **Saturdays** and **Sundays** fall within the date range.
    - Returns the counts using either a custom class or a `Map<String, Integer>`.
*/
    public static Map<String,Integer> countSatandSundays(LocalDate startDate,LocalDate endDate){
        if(!startDate.isBefore(endDate))
            return new HashMap<>();
        LocalDate Saturday =startDate.with(TemporalAdjusters.nextOrSame(DayOfWeek.SATURDAY));
        LocalDate Sunday =startDate.with(TemporalAdjusters.nextOrSame(DayOfWeek.SUNDAY));
        Map<String,Integer> count=new HashMap<>();
        count.put("Saturday",0);
        count.put("Sunday",0);
        while(Saturday.isBefore(endDate)||Saturday.isEqual(endDate))
        {
            count.put("Saturday",count.get("Saturday")+1);
            Saturday=Saturday.plusDays(7);
        }
        while(Sunday.isBefore(endDate)||Sunday.isEqual(endDate))
        {
            count.put("Sunday",count.get("Sunday")+1);
            Sunday=Sunday.plusDays(7);
        }
        return count;
    }


    public static void sirExamplesOfLocalDate() {
        LocalDate currentDate = LocalDate.now();
        LocalDate randomDate = LocalDate.of(2000, 9, 8);
        System.out.println(currentDate);
        System.out.println(randomDate);

        System.out.println(currentDate.isAfter(randomDate));
        System.out.println(currentDate.plusMonths(4));
        System.out.println(currentDate.minusDays(2));

        System.out.println("parse the string date to local date" + LocalDate.parse("2000-09-08"));

        //zoned date

        ZoneId zoneid = ZoneId.of("America/Los_Angeles");
        LocalDate localDateofZone = LocalDate.now(zoneid);
        System.out.println(localDateofZone + " this is localDateofZOne");

    }


    public static void main(String[] args) {
//        sirExamplesOfLocalDate();
        basicLocalDate();
        LocalDate ld=LocalDate.now();
        System.out.println(ld+" return date by adding 45Days and subtract 3 month: "+DateArithmetic(ld));
        //check today birthday ignore year
        System.out.println(checkBirthday(LocalDate.of(2002,9,3),LocalDate.now()));
        System.out.println(MondayDates(2002,3));

    }
}
```
---

```java
package Java8.DateTimeApi.LocalDate;

import java.time.LocalDate;
import java.time.Month;
import java.time.DayOfWeek;
import java.time.Period;
import java.time.format.DateTimeFormatter;

public class LocalDateMethodExamples {

    public static void main(String[] args) {
        // 1. now()
        LocalDate today = LocalDate.now();
        System.out.println("now(): " + today); // now(): 2025-06-08

        // 2. of()
        LocalDate customDate = LocalDate.of(2025, 6, 4);
        System.out.println("of(): " + customDate); // of(): 2025-06-04

        // 3. parse()
        LocalDate parsedDate = LocalDate.parse("2025-06-04");
        System.out.println("parse(): " + parsedDate); // parse(): 2025-06-04

        //custom Parsed Date
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
        LocalDate customParsed = LocalDate.parse("04-06-2025", formatter);
        System.out.println("Custom parsed: " + customParsed); // Output: Custom parsed: 2025-06-04

        // 4. getYear()
        System.out.println("getYear(): " + customDate.getYear()); // getYear(): 2025

        // 5. getMonth()
        Month month = customDate.getMonth();
        System.out.println("getMonth(): " + month); // getMonth(): JUNE

        // 6. getMonthValue()
        System.out.println("getMonthValue(): " + customDate.getMonthValue()); // getMonthValue(): 6

        // 7. getDayOfMonth()
        System.out.println("getDayOfMonth(): " + customDate.getDayOfMonth()); // getDayOfMonth(): 4

        // 8. getDayOfWeek()
        DayOfWeek dayOfWeek = customDate.getDayOfWeek();
        System.out.println("getDayOfWeek(): " + dayOfWeek); // getDayOfWeek(): WEDNESDAY

        // 9. getDayOfYear()
        System.out.println("getDayOfYear(): " + customDate.getDayOfYear()); // getDayOfYear(): 155

        // 10. isLeapYear()
        System.out.println("isLeapYear(): " + customDate.isLeapYear()); // isLeapYear(): false

        // 11. lengthOfMonth()
        System.out.println("lengthOfMonth(): " + customDate.lengthOfMonth()); // lengthOfMonth(): 30

        // 12. lengthOfYear()
        System.out.println("lengthOfYear(): " + customDate.lengthOfYear()); // lengthOfYear(): 365

        // 13. plusDays()
        System.out.println("plusDays(5): " + customDate.plusDays(5)); // plusDays(5): 2025-06-09

        // 14. minusDays()
        System.out.println("minusDays(3): " + customDate.minusDays(3)); // minusDays(3): 2025-06-01

        // 15. plusMonths()
        System.out.println("plusMonths(2): " + customDate.plusMonths(2)); // plusMonths(2): 2025-08-04

        // 16. minusMonths()
        System.out.println("minusMonths(1): " + customDate.minusMonths(1)); // minusMonths(1): 2025-05-04

        // 17. plusYears()
        System.out.println("plusYears(1): " + customDate.plusYears(1)); // plusYears(1): 2026-06-04

        // 18. minusYears()
        System.out.println("minusYears(1): " + customDate.minusYears(1)); // minusYears(1): 2024-06-04

        // 19. withDayOfMonth()
        System.out.println("withDayOfMonth(15): " + customDate.withDayOfMonth(15)); // withDayOfMonth(15): 2025-06-15

        // 20. withMonth()
        System.out.println("withMonth(12): " + customDate.withMonth(12)); // withMonth(12): 2025-12-04

        // 21. withYear()
        System.out.println("withYear(2030): " + customDate.withYear(2030)); // withYear(2030): 2030-06-04

        // 22. until()
        LocalDate endDate = LocalDate.of(2026, 6, 4);
        Period period = customDate.until(endDate);
        System.out.println("until(2026-06-04): " + period); // until(2026-06-04): P1Y

        // 23. isBefore()
        System.out.println("isBefore(2026-06-04): " + customDate.isBefore(endDate)); // isBefore(2026-06-04): true

        // 24. isAfter()
        System.out.println("isAfter(2026-06-04): " + customDate.isAfter(endDate)); // isAfter(2026-06-04): false

        // 25. equals()
        System.out.println("equals(LocalDate.of(2025, 6, 4)): " + customDate.equals(LocalDate.of(2025, 6, 4))); // true

        // 26. toString()
        System.out.println("toString(): " + customDate.toString()); // toString(): 2025-06-04
    }
}
```