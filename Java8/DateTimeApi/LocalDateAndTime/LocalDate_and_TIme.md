# Local DateAndTime

## Methods
| Function          | Description                                                       | Syntax                                        |
|-------------------|-------------------------------------------------------------------|-----------------------------------------------|
| now()             | Gets the current date-time from the system clock                  | `LocalDateTime.now()`                         |
| of()              | Creates a LocalDateTime from year, month, day, hour, minute, etc. | `LocalDateTime.of(2025, 6, 8, 14, 30)`        |
| parse()           | Parses a LocalDateTime from a string                              | `LocalDateTime.parse("2025-06-08T14:30")`     |
| getYear()         | Gets the year                                                     | `dt.getYear()`                                |
| getMonth()        | Gets the month as a `Month` enum                                  | `dt.getMonth()`                               |
| getMonthValue()   | Gets the month as a number (1-12)                                 | `dt.getMonthValue()`                          |
| getDayOfMonth()   | Gets the day of the month                                         | `dt.getDayOfMonth()`                          |
| getDayOfWeek()    | Gets the day of the week as `DayOfWeek` enum                      | `dt.getDayOfWeek()`                           |
| getDayOfYear()    | Gets the day of the year                                          | `dt.getDayOfYear()`                           |
| getHour()         | Gets the hour-of-day (0–23)                                       | `dt.getHour()`                                |
| getMinute()       | Gets the minute-of-hour                                           | `dt.getMinute()`                              |
| getSecond()       | Gets the second-of-minute                                         | `dt.getSecond()`                              |
| getNano()         | Gets the nanosecond part of the time                              | `dt.getNano()`                                |
| plusDays(n)       | Returns copy with n days added                                    | `dt.plusDays(2)`                              |
| minusDays(n)      | Returns copy with n days subtracted                               | `dt.minusDays(2)`                             |
| plusHours(n)      | Returns copy with n hours added                                   | `dt.plusHours(3)`                             |
| minusHours(n)     | Returns copy with n hours subtracted                              | `dt.minusHours(1)`                            |
| plusMinutes(n)    | Returns copy with n minutes added                                 | `dt.plusMinutes(15)`                          |
| minusMinutes(n)   | Returns copy with n minutes subtracted                            | `dt.minusMinutes(15)`                         |
| plusSeconds(n)    | Returns copy with n seconds added                                 | `dt.plusSeconds(10)`                          |
| minusSeconds(n)   | Returns copy with n seconds subtracted                            | `dt.minusSeconds(5)`                          |
| withYear(n)       | Returns copy with altered year                                    | `dt.withYear(2030)`                           |
| withMonth(n)      | Returns copy with altered month                                   | `dt.withMonth(12)`                            |
| withDayOfMonth(n) | Returns copy with altered day                                     | `dt.withDayOfMonth(20)`                       |
| withHour(n)       | Returns copy with altered hour                                    | `dt.withHour(10)`                             |
| withMinute(n)     | Returns copy with altered minute                                  | `dt.withMinute(45)`                           |
| withSecond(n)     | Returns copy with altered second                                  | `dt.withSecond(30)`                           |
| withNano(n)       | Returns copy with altered nanosecond                              | `dt.withNano(123000000)`                      |
| truncatedTo(unit) | Truncates the datetime to the given unit                          | `dt.truncatedTo(ChronoUnit.HOURS)`            |
| isBefore(other)   | Checks if this datetime is before another                         | `dt.isBefore(other)`                          |
| isAfter(other)    | Checks if this datetime is after another                          | `dt.isAfter(other)`                           |
| equals(other)     | Checks if this datetime equals another                            | `dt.equals(other)`                            |
| format(formatter) | Formats this datetime using a DateTimeFormatter                   | `dt.format(DateTimeFormatter.ofPattern(...))` |
| toLocalDate()     | Returns only the date part as LocalDate                           | `dt.toLocalDate()`                            |
| toLocalTime()     | Returns only the time part as LocalTime                           | `dt.toLocalTime()`                            |
| toString()        | Returns ISO-8601 string representation                            | `dt.toString()`                               |

```java
package Java8.DateTimeApi.LocalDateAndTime;

import java.time.*;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;

public class LocalDateTimeExamples {
    public static void main(String[] args) {
        // Static Factory Methods
        LocalDateTime now = LocalDateTime.now();
        System.out.println("Now: " + now); // Output: Current system date-time

        LocalDateTime specific = LocalDateTime.of(2025, 6, 8, 14, 30);
        System.out.println("Specific: " + specific); // Output: 2025-06-08T14:30

        LocalDate date = LocalDate.of(2025, 6, 8);
        LocalTime time = LocalTime.of(14, 30);
        LocalDateTime combined = LocalDateTime.of(date, time);
        System.out.println("Combined DateTime: " + combined); // Output: 2025-06-08T14:30

        // Parsing
        LocalDateTime parsed = LocalDateTime.parse("2025-06-08T14:30");
        System.out.println("Parsed ISO: " + parsed); // Output: 2025-06-08T14:30

        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm");
        LocalDateTime parsedCustom = LocalDateTime.parse("08-06-2025 14:30", formatter);
        System.out.println("Parsed Custom: " + parsedCustom); // Output: 2025-06-08T14:30

        // Getters
        System.out.println("Year: " + now.getYear());                 // e.g., 2025
        System.out.println("Month: " + now.getMonth());               // e.g., JUNE
        System.out.println("Month Value: " + now.getMonthValue());    // e.g., 6
        System.out.println("Day of Month: " + now.getDayOfMonth());   // e.g., 8
        System.out.println("Day of Year: " + now.getDayOfYear());     // e.g., 160
        System.out.println("Day of Week: " + now.getDayOfWeek());     // e.g., SUNDAY
        System.out.println("Hour: " + now.getHour());                 // e.g., 20
        System.out.println("Minute: " + now.getMinute());             // e.g., 15
        System.out.println("Second: " + now.getSecond());             // e.g., 10
        System.out.println("Nano: " + now.getNano());                 // e.g., 123456789

        // Plus / Minus
        System.out.println("Plus 2 days: " + now.plusDays(2));
        System.out.println("Minus 3 hours: " + now.minusHours(3));
        System.out.println("Plus 10 minutes: " + now.plusMinutes(10));

        // With methods
        System.out.println("With year 2030: " + now.withYear(2030));
        System.out.println("With month 12: " + now.withMonth(12));
        System.out.println("With day of month 15: " + now.withDayOfMonth(15));
        System.out.println("With hour 10: " + now.withHour(10));
        System.out.println("With minute 45: " + now.withMinute(45));

        // Truncate to unit
        System.out.println("Truncated to HOURS: " + now.truncatedTo(ChronoUnit.HOURS));

        // Comparison
        LocalDateTime future = now.plusDays(1);
        System.out.println("Is now before future? " + now.isBefore(future)); // true
        System.out.println("Is now after future? " + now.isAfter(future));   // false
        System.out.println("Equals itself? " + now.equals(now));             // true

        // Format
        String formatted = now.format(DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss"));
        System.out.println("Formatted: " + formatted); // e.g., 2025/06/08 20:15:30

        // To LocalDate and LocalTime
        System.out.println("To LocalDate: " + now.toLocalDate()); // e.g., 2025-06-08
        System.out.println("To LocalTime: " + now.toLocalTime()); // e.g., 20:15:30
    }
}
```