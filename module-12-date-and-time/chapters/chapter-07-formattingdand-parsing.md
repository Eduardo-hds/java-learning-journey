# Chapter 7 — Formatting & Parsing

So far, we've learned how to create and manipulate date/time objects.

However, there is one problem.

Java displays dates using the **ISO-8601** standard.

Example:

```text
2026-07-15
```

This format is excellent for computers, but not always ideal for users.

Imagine a Brazilian application.

Users expect:

```text
15/07/2026
```

An American application often expects:

```text
07/15/2026
```

A report may require:

```text
Wednesday, July 15, 2026
```

This is where **`DateTimeFormatter`** comes in.

It allows us to:

* Format date/time objects into readable text.
* Parse text entered by users back into date/time objects.

This chapter is essential because almost every application displays dates or receives dates as input.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Understand what formatting and parsing are.
* Use `DateTimeFormatter`.
* Format dates and times using predefined formatters.
* Create custom formatting patterns.
* Parse user input safely.
* Handle invalid input gracefully.
* Apply formatting in business scenarios.

---

# What is Formatting?

Formatting means:

> **Converting a Java date/time object into text.**

Example:

```java
LocalDate date = LocalDate.of(2026, 7, 15);
```

Internally, Java stores this as a date object.

Formatting converts it into something like:

```text
15/07/2026
```

---

# What is Parsing?

Parsing is the opposite.

It means:

> **Converting text into a Java date/time object.**

Example:

User types:

```text
15/07/2026
```

Java converts it into:

```java
LocalDate
```

Formatting:

```text
Object → Text
```

Parsing:

```text
Text → Object
```

---

# Importing

```java
import java.time.format.DateTimeFormatter;
```

---

# Default Formatting

Every date/time class already has a default ISO-8601 representation.

```java
LocalDate today = LocalDate.now();

System.out.println(today);
```

Output:

```text
2026-07-15
```

The same applies to:

```java
LocalTime.now();
```

```text
09:45:18.532182900
```

and

```java
LocalDateTime.now();
```

```text
2026-07-15T09:45:18.532182900
```

---

# Using Predefined Formatters

Java provides several built-in formatters.

Example:

```java
LocalDate today = LocalDate.now();

DateTimeFormatter formatter =
        DateTimeFormatter.ISO_DATE;

System.out.println(today.format(formatter));
```

Output:

```text
2026-07-15
```

---

Other predefined formatters include:

```java
DateTimeFormatter.ISO_DATE

DateTimeFormatter.ISO_TIME

DateTimeFormatter.ISO_DATE_TIME
```

These are useful when communicating with APIs or storing standardized data.

---

# Creating a Custom Formatter

Most business applications require custom formats.

Example:

```java
DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern("dd/MM/yyyy");
```

Now:

```java
LocalDate today = LocalDate.now();

System.out.println(
        today.format(formatter)
);
```

Output:

```text
15/07/2026
```

---

# Understanding Pattern Symbols

The pattern language is simple but powerful.

| Pattern | Meaning              | Example |
| ------- | -------------------- | ------- |
| `d`     | Day                  | 5       |
| `dd`    | Day (2 digits)       | 05      |
| `M`     | Month                | 7       |
| `MM`    | Month (2 digits)     | 07      |
| `MMM`   | Abbreviated month    | Jul     |
| `MMMM`  | Full month           | July    |
| `yy`    | Two-digit year       | 26      |
| `yyyy`  | Four-digit year      | 2026    |
| `H`     | Hour (24h)           | 9       |
| `HH`    | Hour (24h, 2 digits) | 09      |
| `m`     | Minute               | 5       |
| `mm`    | Minute (2 digits)    | 05      |
| `s`     | Second               | 8       |
| `ss`    | Second (2 digits)    | 08      |

---

# Common Patterns

Brazilian format:

```java
"dd/MM/yyyy"
```

Example:

```text
15/07/2026
```

---

American format:

```java
"MM/dd/yyyy"
```

Example:

```text
07/15/2026
```

---

Date and time:

```java
"dd/MM/yyyy HH:mm"
```

Example:

```text
15/07/2026 14:30
```

---

Long format:

```java
"dd MMMM yyyy"
```

Example (English locale):

```text
15 July 2026
```

---

# Formatting `LocalDateTime`

```java
LocalDateTime meeting =
        LocalDateTime.of(
                2026,
                7,
                15,
                14,
                30
        );

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "dd/MM/yyyy HH:mm"
        );

System.out.println(
        meeting.format(formatter)
);
```

Output:

```text
15/07/2026 14:30
```

---

# Formatting `LocalTime`

```java
LocalTime time =
        LocalTime.of(9, 45);

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "HH:mm"
        );

System.out.println(
        time.format(formatter)
);
```

Output:

```text
09:45
```

---

# Parsing Dates

Suppose the user enters:

```text
15/07/2026
```

Java sees only a `String`.

We need to convert it into a `LocalDate`.

```java
String input = "15/07/2026";

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "dd/MM/yyyy"
        );

LocalDate date =
        LocalDate.parse(
                input,
                formatter
        );

System.out.println(date);
```

Output:

```text
2026-07-15
```

Notice that Java stores the date internally using ISO-8601, regardless of how the user entered it.

---

# Parsing `LocalDateTime`

```java
String input =
        "15/07/2026 14:30";

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "dd/MM/yyyy HH:mm"
        );

LocalDateTime meeting =
        LocalDateTime.parse(
                input,
                formatter
        );
```

---

# Parsing `LocalTime`

```java
String input = "09:45";

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern("HH:mm");

LocalTime time =
        LocalTime.parse(input, formatter);
```

---

# What Happens with Invalid Input?

Suppose the user types:

```text
31/02/2026
```

February 31st does not exist.

Java throws:

```text
DateTimeParseException
```

Example:

```java
try {
    LocalDate date =
            LocalDate.parse(
                    "31/02/2026",
                    formatter
            );
} catch (DateTimeParseException e) {
    System.out.println("Invalid date.");
}
```

Always validate user input when parsing dates.

---

# Business Example 1 — Displaying a Due Date

```java
LocalDate dueDate =
        LocalDate.of(2026, 8, 5);

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "dd/MM/yyyy"
        );

System.out.println(
        "Due: " +
        dueDate.format(formatter)
);
```

Output:

```text
Due: 05/08/2026
```

---

# Business Example 2 — Reading a Birthday

```java
Scanner scanner =
        new Scanner(System.in);

System.out.print("Birth date: ");

String input =
        scanner.nextLine();

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "dd/MM/yyyy"
        );

LocalDate birth =
        LocalDate.parse(input, formatter);
```

Later, we'll combine this with `try/catch` to repeatedly ask the user until a valid date is entered.

---

# Business Example 3 — Event Schedule

```java
LocalDateTime event =
        LocalDateTime.of(
                2026,
                10,
                3,
                19,
                30
        );

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "EEEE, dd MMMM yyyy HH:mm"
        );

System.out.println(
        event.format(formatter)
);
```

Possible output (depending on the default locale):

```text
Thursday, 03 October 2026 19:30
```

---

# Locales

Notice the previous example.

The names of months and weekdays depend on the **Locale**.

If your system is configured for Portuguese (Brazil), you might see:

```text
quinta-feira, 03 outubro 2026 19:30
```

If it's configured for English:

```text
Thursday, 03 October 2026 19:30
```

You can explicitly choose a locale:

```java
import java.util.Locale;

DateTimeFormatter formatter =
        DateTimeFormatter.ofPattern(
                "EEEE, dd MMMM yyyy",
                Locale.US
        );
```

Or:

```java
Locale.forLanguageTag("pt-BR")
```

Using an explicit locale is recommended when your application must produce consistent output regardless of the user's operating system.

---

# Common Mistakes

## Mistake 1 — Wrong Pattern

Input:

```text
15/07/2026
```

Pattern:

```java
"MM/dd/yyyy"
```

Result:

Parsing fails because the pattern doesn't match the input.

---

## Mistake 2 — Using `mm` Instead of `MM`

This is one of the most common errors.

Correct:

```java
MM
```

means:

```text
Month
```

Wrong:

```java
mm
```

means:

```text
Minute
```

Similarly:

* `HH` = hour (24-hour clock)
* `hh` = hour (12-hour clock, usually combined with `a` for AM/PM)

---

## Mistake 3 — Forgetting That Formatting Doesn't Change the Object

```java
LocalDate date =
        LocalDate.now();

date.format(formatter);
```

The date itself is unchanged.

Formatting simply returns a `String`.

---

# Performance Considerations

`DateTimeFormatter` objects are:

* Immutable
* Thread-safe

If you use the same formatter repeatedly, it's a good idea to create it once and reuse it.

Example:

```java
private static final DateTimeFormatter FORMATTER =
        DateTimeFormatter.ofPattern("dd/MM/yyyy");
```

Avoid creating identical formatter instances inside loops when performance matters.

---

# Best Practices

* Always use `DateTimeFormatter` instead of manually building date strings.
* Match the parsing pattern exactly to the expected user input.
* Handle `DateTimeParseException` when reading external data.
* Use explicit locales for predictable month and weekday names.
* Reuse formatter instances when possible.

---

# Guided Exercise 6 — Formatting & Parsing

Create a new class named `FormatterExercises`.

---

## Step 1

Create today's date.

Display it using:

* Default format
* `dd/MM/yyyy`
* `MM/dd/yyyy`

---

## Step 2

Create a `LocalDateTime`.

Display it as:

```text
15/07/2026 14:30
```

---

## Step 3

Create a `LocalTime`.

Display it as:

```text
09:45
```

---

## Step 4

Read a date from the user using `Scanner`.

Expected format:

```text
dd/MM/yyyy
```

Convert it into a `LocalDate` and print the parsed value.

---

## Step 5

Protect the parsing code with a `try/catch`.

If the input is invalid, display:

```text
Invalid date. Please use the format dd/MM/yyyy.
```

---

## Step 6 (Challenge)

Ask the user for:

* Event date (`dd/MM/yyyy`)
* Event time (`HH:mm`)

Parse both values and combine them into a `LocalDateTime`.

Finally, display the event in this format:

```text
Saturday, 03 October 2026 19:30
```

Use an explicit `Locale` (for example, `Locale.US` or `Locale.forLanguageTag("pt-BR")`) so the output is predictable.

---

# Chapter Summary

In this chapter, you learned:

* The difference between formatting and parsing.
* How to use `DateTimeFormatter`.
* How to create custom formatting patterns.
* The meaning of common pattern symbols.
* How to parse user input safely.
* How locales affect month and weekday names.
* How to handle invalid date input gracefully.
* Best practices for reusable, thread-safe formatters.

In the next chapter, we'll explore **Time Zones** using `ZoneId` and `ZonedDateTime`. You'll learn how Java represents the same instant in different parts of the world, how to convert between time zones correctly, and why storing timestamps in UTC is a best practice for global applications.
