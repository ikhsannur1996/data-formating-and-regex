# PostgreSQL Data Formatting and Regular Expressions (Regex) Guide

## **Table of Contents**
1. [Introduction](#introduction)
2. [Data Formatting](#data-formatting)
   - [1. Formatting Date to 'YYYY-MM-DD'](#1-formatting-date-to-yyyy-mm-dd)
   - [2. Formatting Date to 'MM/DD/YYYY'](#2-formatting-date-to-mmddyyyy)
   - [3. Formatting Date with Day Name](#3-formatting-date-with-day-name)
   - [4. Formatting Date to 'DD-MM-YYYY'](#4-formatting-date-to-dd-mm-yyyy)
   - [5. Formatting Time to 'HH24:MI:SS'](#5-formatting-time-to-hh24miss)
   - [6. Formatting Date and Time Together](#6-formatting-date-and-time-together)
   - [7. Convert String to Date 'DD-MM-YYYY'](#7-convert-string-to-date-dd-mm-yyyy)
   - [8. Convert String to Date 'YYYY/MM/DD'](#8-convert-string-to-date-yyyymmdd)
   - [9. Convert String to Date 'Month Day, Year'](#9-convert-string-to-date-month-day-year)
   - [10. Adding or Subtracting Days to a Date](#10-adding-or-subtracting-days-to-a-date)
3. [Regular Expressions (Regex)](#regular-expressions-regex)
   - [1. Basic Pattern Matching](#1-basic-pattern-matching)
   - [2. Case-Insensitive Pattern Matching](#2-case-insensitive-pattern-matching)
   - [3. Match Full Word](#3-match-full-word)
   - [4. Extract Substring with Regex](#4-extract-substring-with-regex)
   - [5. Extract Domain from Email](#5-extract-domain-from-email)
   - [6. Replace Characters Using Regex](#6-replace-characters-using-regex)
   - [7. Match a Sequence of Digits](#7-match-a-sequence-of-digits)
   - [8. Validate Email Format](#8-validate-email-format)
   - [9. Replace Multiple Spaces with a Single Space](#9-replace-multiple-spaces-with-a-single-space)
   - [10. Extract Numbers from a String](#10-extract-numbers-from-a-string)
   - [11. Check if String Contains Only Numbers](#11-check-if-string-contains-only-numbers)
   - [12. Extract First Word from a Sentence](#12-extract-first-word-from-a-sentence)
   - [13. Remove Non-Alphanumeric Characters](#13-remove-non-alphanumeric-characters)
   - [14. Find Words Starting with a Specific Letter](#14-find-words-starting-with-a-specific-letter)
   - [15. Extract File Extension from Filename](#15-extract-file-extension-from-filename)
   - [16. Check if String Ends with a Number](#16-check-if-string-ends-with-a-number)
   - [17. Match Phone Number Format](#17-match-phone-number-format)
   - [18. Match IPv4 Address Format](#18-match-ipv4-address-format)
   - [19. Find All Words in a String](#19-find-all-words-in-a-string)
   - [20. Remove HTML Tags](#20-remove-html-tags)

---

## **Introduction**

PostgreSQL provides a powerful set of tools for managing, formatting, and manipulating data in your database. This guide covers two key concepts:

### **Data Formatting**
Data formatting in PostgreSQL allows you to present and manipulate data (especially dates and times) in various formats to meet application or reporting needs. Whether you want to change how dates are displayed, convert between data types, or apply precise formatting for complex reports, PostgreSQL's functions like `TO_CHAR()` and `TO_DATE()` make it easy.

This section will demonstrate how to:
- Format dates in various ways.
- Convert strings to dates and vice versa.
- Manipulate and format both date and time components.
  
Understanding these functions helps ensure that your data is displayed in the correct format for users and applications.

### **Regular Expressions (Regex)**
Regular expressions are a powerful tool for pattern matching and string manipulation. PostgreSQL provides robust support for regex, allowing you to find, extract, and modify data based on complex patterns. Regex can be used to validate data formats (such as email addresses and phone numbers), extract meaningful substrings, and replace unwanted characters.

In this section, you will explore:
- Pattern matching for strings.
- Extracting data using regex.
- Validating and cleaning data with regular expressions.

Mastering regex in PostgreSQL enables efficient text searching, validation, and manipulation within the database.

---

## **Data Formatting**

### 1. Formatting Date to 'YYYY-MM-DD'

```sql
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD') AS formatted_date;
```
- **Explanation**: Formats the current date to `'YYYY-MM-DD'`.

### 2. Formatting Date to 'MM/DD/YYYY'

```sql
SELECT TO_CHAR(NOW(), 'MM/DD/YYYY') AS formatted_date;
```
- **Explanation**: Formats the current date to `'MM/DD/YYYY'`.

### 3. Formatting Date with Day Name

```sql
SELECT TO_CHAR(NOW(), 'Day, DD Month YYYY') AS formatted_date;
```
- **Explanation**: Adds the day name and formats the date like `'Sunday, 08 September 2024'`.

### 4. Formatting Date to 'DD-MM-YYYY'

```sql
SELECT TO_CHAR(NOW(), 'DD-MM-YYYY') AS formatted_date;
```
- **Explanation**: Formats the current date to `'DD-MM-YYYY'`.

### 5. Formatting Time to 'HH24:MI:SS'

```sql
SELECT TO_CHAR(NOW(), 'HH24:MI:SS') AS formatted_time;
```
- **Explanation**: Formats the current time to a 24-hour format, like `'13:45:30'`.

### 6. Formatting Date and Time Together

```sql
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD HH24:MI:SS') AS formatted_date_time;
```
- **Explanation**: Combines date and time in the format `'YYYY-MM-DD HH24:MI:SS'`.

### 7. Convert String to Date 'DD-MM-YYYY'

```sql
SELECT TO_DATE('08-09-2024', 'DD-MM-YYYY') AS converted_date;
```
- **Explanation**: Converts the string `'08-09-2024'` to a `DATE` object.

### 8. Convert String to Date 'YYYY/MM/DD'

```sql
SELECT TO_DATE('2024/09/08', 'YYYY/MM/DD') AS converted_date;
```
- **Explanation**: Converts the string `'2024/09/08'` to a `DATE` object.

### 9. Convert String to Date 'Month Day, Year'

```sql
SELECT TO_DATE('September 08, 2024', 'Month DD, YYYY') AS converted_date;
```
- **Explanation**: Converts the string `'September 08, 2024'` to a `DATE` object.

### 10. Adding or Subtracting Days to a Date

```sql
SELECT NOW() + INTERVAL '5 days' AS future_date;
```
- **Explanation**: Adds 5 days to the current date.

---

## **Regular Expressions (Regex)**

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
- **

Explanation**: Checks if the string is in a valid email format. Returns `TRUE`.

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
SELECT REGEXP_REPLACE('Hello@World!', '[^A-Za-z0-9]', '', 'g') AS cleaned_string;
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
