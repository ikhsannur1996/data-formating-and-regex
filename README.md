# PostgreSQL Data Formatting and Regular Expressions (Regex) Guide

## Introduction

PostgreSQL is a powerful, open-source relational database management system that supports advanced data formatting and manipulation. This guide provides an overview of key techniques for formatting data and using regular expressions (regex) within PostgreSQL. Whether you're working with dates, times, or strings, PostgreSQL offers a robust set of functions to handle various data transformation tasks.

### **A. Data Formatting**

Data formatting in PostgreSQL allows you to convert and display information in a variety of formats. This section covers essential functions such as `TO_CHAR` for formatting dates and times, `TO_DATE` for converting strings to dates, and various casting techniques to handle different data types. You'll learn how to:

- Format dates and times in different styles.
- Convert between strings, integers, floats, and dates.
- Adjust date values by adding or subtracting intervals.
- Handle locale-specific date formats and time zones.

### 1. Date Formatting

#### Format Date

```sql
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD') AS formatted_date;
```
- **Explanation**: Converts the current date and time into the format `YYYY-MM-DD`.

#### Convert String to Date (DD-MM-YYYY)

```sql
SELECT TO_DATE('08-09-2024', 'DD-MM-YYYY') AS converted_date;
```
- **Explanation**: Converts the string `'08-09-2024'` into a date, based on the format `DD-MM-YYYY`. The result will be `2024-09-08` in PostgreSQL's standard date format.

#### Additional TO_DATE Example (YYYY/MM/DD)

```sql
SELECT TO_DATE('2024/09/08', 'YYYY/MM/DD') AS formatted_date;
```
- **Explanation**: Converts the string `'2024/09/08'` into the corresponding date format, `YYYY-MM-DD`.

#### Format Date with Day Name

```sql
SELECT TO_CHAR(NOW(), 'Day, DD Month YYYY') AS formatted_date;
```
- **Explanation**: Adds the day name and formats the date like `Sunday, 08 September 2024`.

#### Format Date to 'MM/DD/YYYY'

```sql
SELECT TO_CHAR(NOW(), 'MM/DD/YYYY') AS formatted_date;
```
- **Explanation**: Formats the current date to `MM/DD/YYYY`.

#### Format Time to 'HH24:MI:SS'

```sql
SELECT TO_CHAR(NOW(), 'HH24:MI:SS') AS formatted_time;
```
- **Explanation**: Formats the current time to a 24-hour format, like `13:45:30`.

#### Format Date and Time Together

```sql
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD HH24:MI:SS') AS formatted_date_time;
```
- **Explanation**: Combines date and time in the format `YYYY-MM-DD HH24:MI:SS`.

#### Convert String to Date (Month Day, Year)

```sql
SELECT TO_DATE('September 08, 2024', 'Month DD, YYYY') AS converted_date;
```
- **Explanation**: Converts the string `'September 08, 2024'` into a `DATE` object.

#### Adding Days to a Date

```sql
SELECT NOW() + INTERVAL '5 days' AS future_date;
```
- **Explanation**: Adds 5 days to the current date.

#### Subtracting Days from a Date

```sql
SELECT NOW() - INTERVAL '5 days' AS past_date;
```
- **Explanation**: Subtracts 5 days from the current date.

### 2. Cast String

#### Cast Integer to String

```sql
SELECT CAST(12345 AS VARCHAR) AS string_value;
```
- **Explanation**: Casts the integer `12345` into a string.

#### Cast Date to String

```sql
SELECT CAST(NOW() AS VARCHAR) AS date_string;
```
- **Explanation**: Casts the current date and time to a string.

### 3. Integer Cast

#### Convert String to Integer

```sql
SELECT '12345'::INTEGER AS int_value;
```
- **Explanation**: Converts the string `'12345'` to an integer.

#### Convert Float to Integer

```sql
SELECT FLOOR(123.45) AS int_value;
```
- **Explanation**: Converts the float `123.45` to an integer by flooring it to `123`.

### 4. Float Cast

#### Convert String to Float

```sql
SELECT CAST('123.45' AS FLOAT) AS float_value;
```
- **Explanation**: Converts the string `'123.45'` into a floating-point number.

#### Convert Integer to Float

```sql
SELECT 12345::FLOAT AS float_value;
```
- **Explanation**: Converts the integer `12345` to a float.

#### Convert Date to Float (Timestamp)

```sql
SELECT EXTRACT(EPOCH FROM NOW()) AS timestamp_seconds;
```
- **Explanation**: Converts the current date and time to a float representing the number of seconds since the Unix epoch.

### 5. Date Formatting with Locale

#### Format Date with Locale Specifics

```sql
SELECT TO_CHAR(NOW(), 'TMDay, DD TMMonth YYYY', 'nls_date_language=english') AS formatted_date;
```
- **Explanation**: Formats the current date according to locale-specific settings.

### 6. Formatting Time Zone

#### Format Date and Time with Time Zone

```sql
SELECT TO_CHAR(NOW() AT TIME ZONE 'UTC', 'YYYY-MM-DD HH24:MI:SS TZ') AS formatted_date_time_utc;
```
- **Explanation**: Formats the current date and time including the time zone.

### 7. Custom Date and Time Format

#### Custom Format Date and Time

```sql
SELECT TO_CHAR(NOW(), 'Dy, DD Mon YYYY HH12:MI AM') AS custom_format_date_time;
```
- **Explanation**: Formats the current date and time in a custom format like `Sun, 08 Sep 2024 01:45 PM`.

### 8. Extracting Date Components

#### Extract Year from Date

```sql
SELECT EXTRACT(YEAR FROM NOW()) AS year;
```
- **Explanation**: Extracts the year from the current date.

#### Extract Month from Date

```sql
SELECT EXTRACT(MONTH FROM NOW()) AS month;
```
- **Explanation**: Extracts the month from the current date.

### 9. Format Currency

#### Format as Currency

```sql
SELECT TO_CHAR(12345.6789, 'L9,999.99') AS currency_formatted;
```
- **Explanation**: Formats the number as currency with a locale-specific currency symbol.

### 10. Format Interval

#### Format Interval as String

```sql
SELECT TO_CHAR(INTERVAL '1 year 2 months 3 days', 'YY "years" MM "months" DD "days"') AS interval_formatted;
```
- **Explanation**: Formats an interval in a human-readable string format.

---

## **B. Regular Expressions (Regex)**
Regular expressions are powerful tools for pattern matching and text manipulation. PostgreSQL's support for regex allows you to search for, extract, and replace text based on specific patterns. In this section, you'll explore how to:
- Perform basic and case-insensitive pattern matching.
- Extract substrings, domains, and numbers from strings.
- Validate formats such as emails, phone numbers, and IP addresses.
- Replace characters and remove unwanted text using regex.

### 1. Basic Pattern Matching

```sql
SELECT 'abcdef' ~ 'abc' AS is_match;
```
- **Explanation**: Checks if `'abcdef'` contains `'abc'`. The result is `TRUE`.

### 2. Case-Insensitive Pattern Matching

```sql
SELECT 'AbCdef' ~* 'abc' AS is_case_insensitive_match;
```
- **Explanation**: Performs a case-insensitive match, returning `TRUE` if `'abc'` is found in `'AbCdef'`.

### 3. Match Full Word

```sql
SELECT 'hello world' ~ '\yworld\y' AS full_word_match;
```
- **Explanation**: Matches the full word `'world'`. `\y` denotes word boundaries.

### 4. Extract Substring with Regex

```sql
SELECT SUBSTRING('john.doe@example.com' FROM '[a-z]+') AS extracted_string;
```
- **Explanation**: Extracts the first sequence of lowercase letters, in this case, `'john'`.

### 5. Extract Domain from Email

```sql
SELECT SUBSTRING('john.doe@example.com' FROM '@(.+)$') AS domain;
```
- **Explanation**: Extracts the domain part of the email, resulting in `'example.com'`.

### 6. Replace Characters Using Regex

```sql
SELECT REGEXP_REPLACE('2024-09-08', '-', '/') AS formatted_date;
```
- **Explanation**: Replaces hyphens (`-`) with slashes (`/`), resulting in `'2024/09/08'`.

### 7. Match a Sequence of Digits

```sql
SELECT 'abc123def' ~ '\d+' AS has_digits;
```
- **Explanation**: Checks if the string contains a sequence of digits. Returns `TRUE` if digits are found.

### 8. Validate Email Format

```sql
SELECT 'john.doe@example.com' ~ '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$' AS is_valid_email;
```
- **Explanation**: Checks if the string is in a valid email format. Returns `TRUE`.

### 9. Replace Multiple Spaces with a Single Space

```sql
SELECT REGEXP_REPLACE('Hello    World', '\s+', ' ', 'g') AS single_spaced_string;
```
- **Explanation**: Replaces multiple spaces with a single space, resulting in `'Hello World'`.

### 10. Extract Numbers from a String

```sql
SELECT REGEXP_REPLACE('Order123', '\D', '', 'g') AS extracted_numbers;
```
- **Explanation**: Removes all non-digit characters, resulting in `'123'`.

### 11. Check if String Contains Only Numbers

```sql
SELECT '12345' ~ '^\d+$' AS is_only_numbers;
```
- **Explanation**: Checks if the string contains only numbers. Returns `TRUE`.

### 12. Extract First Word from a Sentence

```sql
SELECT SUBSTRING('Hello World' FROM '^\w+') AS first_word;
```
- **Explanation**: Extracts the first word `'Hello'` from the string.

### 13. Remove Non-Alphanumeric Characters

```sql
SELECT REGEXP_REPLACE('Hello@World

!', '[^A-Za-z0-9]', '', 'g') AS cleaned_string;
```
- **Explanation**: Removes all non-alphanumeric characters, resulting in `'HelloWorld'`.

### 14. Find Words Starting with a Specific Letter

```sql
SELECT 'Apple Banana Cherry' ~ '\bA\w+' AS starts_with_A;
```
- **Explanation**: Checks if there is a word starting with the letter `'A'`. Returns `TRUE`.

### 15. Extract File Extension from Filename

```sql
SELECT SUBSTRING('report.pdf' FROM '\.(\w+)$') AS file_extension;
```
- **Explanation**: Extracts the file extension, resulting in `'pdf'`.

### 16. Check if String Ends with a Number

```sql
SELECT 'invoice123' ~ '\d+$' AS ends_with_number;
```
- **Explanation**: Checks if the string ends with a number. Returns `TRUE`.

### 17. Match Phone Number Format

```sql
SELECT '123-456-7890' ~ '^\d{3}-\d{3}-\d{4}$' AS is_valid_phone;
```
- **Explanation**: Checks if the string matches the format of a phone number (`123-456-7890`). Returns `TRUE`.

### 18. Match IPv4 Address Format

```sql
SELECT '192.168.1.1' ~ '^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$' AS is_valid_ip;
```
- **Explanation**: Checks if the string is a valid IPv4 address. Returns `TRUE`.

### 19. Find All Words in a String

```sql
SELECT REGEXP_SPLIT_TO_ARRAY('apple, banana, cherry', '\s*,\s*') AS words;
```
- **Explanation**: Splits the string into an array of words based on commas and spaces, resulting in `{'apple', 'banana', 'cherry'}`.

### 20. Remove HTML Tags

```sql
SELECT REGEXP_REPLACE('<p>Hello</p>', '<[^>]*>', '', 'g') AS no_html;
```
- **Explanation**: Removes HTML tags from the string, resulting in `'Hello'`.

---

### **Summary**

- **Data Formatting**: Includes 10 sections covering the use of `TO_CHAR`, `TO_DATE`, and handling date/time manipulations.
- **Regular Expressions**: Demonstrates 20 examples of regex usage in PostgreSQL, such as pattern matching, extracting substrings, and validating formats like emails or phone numbers.

---
### **Reference**
- https://www.postgresql.org/docs/current/functions-formatting.html
- https://www.postgresql.org/docs/current/functions-matching.html
