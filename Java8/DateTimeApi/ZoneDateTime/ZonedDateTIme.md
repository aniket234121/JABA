# ZonedDateTime

ZonedDateTime is part of the Java 8 Date-Time API (java.time package) and represents a date and time with a time zone.

## Methods

| Method Signature                                                                                                                       | Return Type     | Description                                                                            |
|----------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------------------------------------------------------------|
| `public static ZonedDateTime now()`                                                                                                    | `ZonedDateTime` | Returns the current date-time using the system default time-zone.                      |
| `public static ZonedDateTime now(ZoneId zone)`                                                                                         | `ZonedDateTime` | Returns the current date-time in the given time-zone.                                  |
| `public static ZonedDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond, ZoneId zone)` | `ZonedDateTime` | Obtains an instance using year, month, day, time, and zone.                            |
| `public static ZonedDateTime of(LocalDate date, LocalTime time, ZoneId zone)`                                                          | `ZonedDateTime` | Combines a `LocalDate`, `LocalTime`, and `ZoneId` into a `ZonedDateTime`.              |
| `public static ZonedDateTime of(LocalDateTime localDateTime, ZoneId zone)`                                                             | `ZonedDateTime` | Creates a `ZonedDateTime` from `LocalDateTime` and zone.                               |
| `public static ZonedDateTime parse(CharSequence text)`                                                                                 | `ZonedDateTime` | Parses a `ZonedDateTime` from a string in ISO-8601 format.                             |
| `public static ZonedDateTime parse(CharSequence text, DateTimeFormatter formatter)`                                                    | `ZonedDateTime` | Parses using a custom formatter.                                                       |
| `public ZonedDateTime withZoneSameInstant(ZoneId zone)`                                                                                | `ZonedDateTime` | Returns a copy of this datetime with a different time zone, keeping the same instant.  |
| `public ZonedDateTime withZoneSameLocal(ZoneId zone)`                                                                                  | `ZonedDateTime` | Returns a copy with a different time zone, but same local date-time (changes instant). |
| `public LocalDateTime toLocalDateTime()`                                                                                               | `LocalDateTime` | Converts to a `LocalDateTime`, discarding the time-zone.                               |
| `public ZonedDateTime plusDays(long days)`                                                                                             | `ZonedDateTime` | Returns a copy with the specified number of days added.                                |
| `public ZonedDateTime minusHours(long hours)`                                                                                          | `ZonedDateTime` | Returns a copy with the specified number of hours subtracted.                          |
| `public boolean isBefore(ChronoZonedDateTime<?> other)`                                                                                | `boolean`       | Checks if this date-time is before the specified date-time.                            |
| `public boolean isAfter(ChronoZonedDateTime<?> other)`                                                                                 | `boolean`       | Checks if this date-time is after the specified date-time.                             |
| `public ZoneId getZone()`                                                                                                              | `ZoneId`        | Returns the time-zone.                                                                 |
| `public ZoneOffset getOffset()`                                                                                                        | `ZoneOffset`    | Returns the zone offset from UTC.                                                      |
| `public LocalDate getDate()`                                                                                                           | `LocalDate`     | Gets only the date portion.                                                            |
| `public LocalTime getTime()`                                                                                                           | `LocalTime`     | Gets only the time portion.                                                            |
| `public ZonedDateTime truncatedTo(TemporalUnit unit)`                                                                                  | `ZonedDateTime` | Returns a copy with time truncated to the specified unit.                              |
| `public String format(DateTimeFormatter formatter)`                                                                                    | `String`        | Formats the date-time using the provided formatter.                                    |

```java
package Java8.DateTimeApi.ZoneDateTime;

import java.time.*;
import java.time.format.DateTimeFormatter;

public class ZonedDateTimeExample {

    public static void main(String[] args) {
        // Current ZonedDateTime
        ZonedDateTime zdtNow = ZonedDateTime.now();
        System.out.println("Current ZonedDateTime: " + zdtNow); // Current system zone time

        // Specific ZonedDateTime
        ZonedDateTime zdt = ZonedDateTime.of(2025, 6, 9, 10, 30, 0, 0, ZoneId.of("Asia/Kolkata"));
        System.out.println("ZonedDateTime.of(): " + zdt);

        // Parsing from String
        ZonedDateTime parsed = ZonedDateTime.parse("2025-06-09T10:15:30+05:30[Asia/Kolkata]");
        System.out.println("Parsed ZonedDateTime: " + parsed);

        // Converting time zone
        ZonedDateTime utcTime = zdt.withZoneSameInstant(ZoneId.of("UTC"));
        System.out.println("Converted to UTC: " + utcTime);

        // Formatting
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss z VV");
        String formatted = zdt.format(formatter);
        System.out.println("Formatted: " + formatted);

        // Getting LocalDateTime
        LocalDateTime localDateTime = zdt.toLocalDateTime();
        System.out.println("LocalDateTime from ZonedDateTime: " + localDateTime);
    }
}

```