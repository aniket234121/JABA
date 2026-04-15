# DateTimeFormatter

## Formatter 

| Symbol | Meaning             | Example    |
|--------|---------------------|------------|
| yyyy   | Year                | 2025       |
| MM     | Month (2 digits)    | 06         |
| MMM    | Month (short name)  | Jun        |
| dd     | Day of month        | 08         |
| EEEE   | Day of week (full)  | Sunday     |
| E      | Day of week (short) | Sun        |
| HH     | Hour (0-23)         | 14         |
| hh     | Hour (1-12)         | 02         |
| mm     | Minute              | 30         |
| ss     | Second              | 15         |
| a      | AM/PM marker        | PM         |
| SSS    | Milliseconds        | 123        |
| z      | Time zone           | IST        |
| X      | ISO 8601 time zone  | +05, +0530 |


## common Methods
| Method Signature                                                                | Description                           |
|---------------------------------------------------------------------------------|---------------------------------------|
| static DateTimeFormatter ofPattern(String pattern)                              | Creates a formatter using a pattern   |
| static DateTimeFormatter ofPattern(String pattern, Locale l)                    | Creates a locale-sensitive formatter  |
| String format(TemporalAccessor temporal)                                        | Formats a date/time object to string  |
| TemporalAccessor parse(CharSequence text)                                       | Parses a string to a date/time object |
| <T extends TemporalAccessor> T parse(CharSequence text, TemporalQuery<T> query) | Parses with a query                   |

```java
package Java8.DateTimeApi.DateTimeFormatter;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.*;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class DateTimeFormatterExample {

    public static void another() {

        LocalDateTime dateTime = LocalDateTime.of(2025, 6, 8, 14, 30, 15);

        // 1. Built-in ISO Formatters


        System.out.println("ISO_DATE: " + dateTime.format(DateTimeFormatter.ISO_DATE));
        // Output: 2025-06-08

        System.out.println("ISO_TIME: " + dateTime.format(DateTimeFormatter.ISO_TIME));
        // Output: 14:30:15

        System.out.println("ISO_DATE_TIME: " + dateTime.format(DateTimeFormatter.ISO_DATE_TIME));
        // Output: 2025-06-08T14:30:15

        System.out.println("BASIC_ISO_DATE: " + dateTime.format(DateTimeFormatter.BASIC_ISO_DATE));
        // Output: 20250608

        ZonedDateTime zonedDateTime = dateTime.atZone(ZoneId.of("Asia/Kolkata"));
        System.out.println("RFC_1123_DATE_TIME: " + zonedDateTime.format(DateTimeFormatter.RFC_1123_DATE_TIME));
        // Output: Sun, 8 Jun 2025 14:30:15 GMT+05:30





        // 2. Custom Pattern Formatting


        DateTimeFormatter custom1 = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
        System.out.println("Custom 1: " + dateTime.format(custom1));
        // Output: 08-06-2025 14:30:15

        DateTimeFormatter custom2 = DateTimeFormatter.ofPattern("EEEE, MMM dd yyyy hh:mm:ss a");
        System.out.println("Custom 2: " + dateTime.format(custom2));
        // Output: Sunday, Jun 08 2025 02:30:15 PM

        DateTimeFormatter custom3 = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss z").withZone(ZoneId.of("Asia/Kolkata"));
        System.out.println("Zoned Format: " + custom3.format(zonedDateTime));
        // Output: 2025/06/08 14:30:15 IST

        // 3. Parsing with ISO and custom formatters
        String isoInput = "2025-06-08T14:30:15";
        LocalDateTime parsedISO = LocalDateTime.parse(isoInput);
        System.out.println("Parsed ISO: " + parsedISO);
        // Output: 2025-06-08T14:30:15

        String customInput = "08-06-2025 14:30:15";
        LocalDateTime parsedCustom = LocalDateTime.parse(customInput, custom1);
        System.out.println("Parsed Custom: " + parsedCustom);
        // Output: 2025-06-08T14:30:15

        // 4. Locale-sensitive formatting
        DateTimeFormatter localeFormatter = DateTimeFormatter.ofPattern("dd MMMM yyyy", Locale.FRENCH);
        System.out.println("French format: " + dateTime.format(localeFormatter));
        // Output: 08 juin 2025


    }

    public static void main(String[] args) {
        String date = "19-09-2002";
        DateTimeFormatter df = DateTimeFormatter.ofPattern("d-M-y");
        LocalDate localDate = LocalDate.parse(date, df);
        System.out.println(localDate);
    }
}
```