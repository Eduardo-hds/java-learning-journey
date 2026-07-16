# Chapter 2 — LocalDate

Now that you understand the philosophy of the `java.time` API, it's time to start using it.

We'll begin with the most commonly used class in business applications:

```java
LocalDate
```

This class represents **only a calendar date**.

No hours.

No minutes.

No seconds.

No time zone.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Create dates
* Obtain the current date
* Create specific dates
* Access year, month and day
* Perform date arithmetic
* Compare dates
* Calculate intervals
* Understand why `LocalDate` is immutable
* Apply `LocalDate` in business scenarios

---

# What is `LocalDate`?

`LocalDate` models a **calendar date**.

Example:

```text
2026-07-15
```

Internally it stores:

* Year
* Month
* Day

It **does not** store:

* Hour
* Minute
* Second
* Millisecond
* Time zone

Think of it as representing **a page on a calendar**.

---

# When Should You Use It?

Use `LocalDate` whenever the time of day is irrelevant.

Examples:

✔ Birthday

✔ Holiday

✔ Due date

✔ Invoice date

✔ Contract start date

✔ Graduation date

✔ Product expiration date

---

# When NOT to Use It

Don't use `LocalDate` if you need:

* Appointment at 15:00
* Login timestamp
* Flight departure time
* Event with hour and minute
* International timestamps

For those, use:

* `LocalDateTime`
* `Instant`
* `ZonedDateTime`

We'll study those later.

---

# Importing the Class

```java
import java.time.LocalDate;
```

---

# Creating the Current Date

The simplest way:

```java
LocalDate today = LocalDate.now();

System.out.println(today);
```

Example output:

```text
2026-07-15
```

---

## What Happens Internally?

When you call:

```java
LocalDate.now();
```

Java:

1. Reads the operating system clock.
2. Uses the system's default time zone.
3. Converts that information into a `LocalDate`.

Conceptually:

```text
Operating System Clock
          │
          ▼
 Current Date/Time
          │
          ▼
 Remove Time
          │
          ▼
    LocalDate
```

Notice that the **time portion is discarded**.

---

# Creating a Specific Date

Sometimes you don't want today's date.

Use:

```java
LocalDate birthday = LocalDate.of(1999, 8, 21);

System.out.println(birthday);
```

Output:

```text
1999-08-21
```

---

## Why Use `of()`?

Instead of many constructors, `java.time` uses **factory methods**.

```java
LocalDate.of(...)
```

is easier to read than:

```java
new LocalDate(...)
```

In fact, there is **no public constructor** for `LocalDate`.

This design:

* Improves readability
* Allows internal optimizations
* Prevents invalid object creation

---

# Month Constants

Using numbers:

```java
LocalDate.of(2026, 7, 15);
```

works, but this is clearer:

```java
import java.time.Month;

LocalDate vacation =
        LocalDate.of(2026, Month.JULY, 15);
```

Benefits:

* Easier to read
* Avoids confusing month numbers
* Prevents mistakes

---

# Getting Individual Fields

```java
LocalDate today = LocalDate.now();

System.out.println(today.getYear());
System.out.println(today.getMonth());
System.out.println(today.getMonthValue());
System.out.println(today.getDayOfMonth());
System.out.println(today.getDayOfWeek());
System.out.println(today.getDayOfYear());
```

Possible output:

```text
2026
JULY
7
15
WEDNESDAY
196
```

---

## Difference Between `getMonth()` and `getMonthValue()`

```java
today.getMonth();
```

Returns:

```text
JULY
```

(enum)

Whereas:

```java
today.getMonthValue();
```

Returns:

```text
7
```

(integer)

Whenever possible, prefer enums because they are more expressive and type-safe.

---

# Checking Leap Years

```java
LocalDate today = LocalDate.now();

System.out.println(today.isLeapYear());
```

Output:

```text
true
```

or

```text
false
```

Java handles all leap-year rules automatically.

You don't need to implement the logic yourself.

---

# Date Arithmetic

One of the strengths of `LocalDate` is its expressive arithmetic API.

Instead of manually calculating dates, you use methods that understand the calendar.

---

## Adding Days

```java
LocalDate today = LocalDate.now();

LocalDate future =
        today.plusDays(10);

System.out.println(future);
```

---

## Adding Weeks

```java
LocalDate nextMonth =
        today.plusWeeks(3);
```

---

## Adding Months

```java
LocalDate renewal =
        today.plusMonths(6);
```

---

## Adding Years

```java
LocalDate retirement =
        today.plusYears(30);
```

---

# Subtracting Time

The opposite methods also exist.

```java
today.minusDays(5);

today.minusWeeks(2);

today.minusMonths(1);

today.minusYears(10);
```

Again, these methods **do not modify** the original object.

---

# Immutability in Practice

Consider:

```java
LocalDate today = LocalDate.now();

today.plusDays(1);

System.out.println(today);
```

Many beginners expect tomorrow.

But the output is still today.

Why?

Because:

```java
plusDays()
```

returns a **new object**.

Correct:

```java
today = today.plusDays(1);
```

or

```java
LocalDate tomorrow =
        today.plusDays(1);
```

---

# Chaining Operations

Since every method returns a new `LocalDate`, chaining is natural.

```java
LocalDate result =
        LocalDate.now()
                .plusMonths(2)
                .minusDays(5)
                .plusYears(1);
```

This style is concise and readable.

---

# Comparing Dates

Dates are objects.

Never compare them using:

```java
==
```

This compares object references, not the dates they represent.

---

## `isBefore()`

```java
LocalDate today = LocalDate.now();

LocalDate christmas =
        LocalDate.of(2026, 12, 25);

System.out.println(
        today.isBefore(christmas));
```

Output:

```text
true
```

---

## `isAfter()`

```java
System.out.println(
        christmas.isAfter(today));
```

---

## `isEqual()`

```java
LocalDate anotherToday =
        LocalDate.now();

System.out.println(
        today.isEqual(anotherToday));
```

---

# Ordering Dates

`LocalDate` implements `Comparable`.

That means you can sort lists of dates.

```java
Collections.sort(dateList);
```

The dates are sorted chronologically.

---

# Calculating the Difference Between Dates

One simple approach is:

```java
long days =
        start.until(end).getDays();
```

However, this only returns the **days component** of the period between two dates, not necessarily the total number of elapsed days.

A more reliable approach for total days will be introduced later with `ChronoUnit.DAYS.between(...)`.

We'll explore `Period` and `ChronoUnit` in dedicated chapters.

---

# Business Example 1 — Expiration Date

```java
LocalDate manufacture =
        LocalDate.now();

LocalDate expiration =
        manufacture.plusYears(2);

System.out.println(expiration);
```

---

# Business Example 2 — Membership Renewal

```java
LocalDate subscription =
        LocalDate.now();

LocalDate renewal =
        subscription.plusMonths(1);
```

---

# Business Example 3 — Warranty

```java
LocalDate purchase =
        LocalDate.of(2026, 7, 15);

LocalDate warranty =
        purchase.plusYears(3);
```

---

# Business Example 4 — Is the Product Expired?

```java
LocalDate expiration =
        LocalDate.of(2026, 8, 15);

if (LocalDate.now().isAfter(expiration)) {
    System.out.println("Expired");
} else {
    System.out.println("Valid");
}
```

---

# Common Mistakes

## Mistake 1

Ignoring immutability.

```java
date.plusDays(3);
```

Nothing changes.

---

## Mistake 2

Using `==`.

Wrong:

```java
date1 == date2
```

Correct:

```java
date1.isEqual(date2)
```

or

```java
date1.equals(date2)
```

* `equals()` checks if the two objects represent the same date.
* `isEqual()` is part of the temporal API and expresses the same intent for dates in a more domain-specific way.

For `LocalDate`, both methods produce the same result.

---

## Mistake 3

Using `LocalDate` for appointments.

Appointments need time.

Use:

```java
LocalDateTime
```

instead.

---

# Performance Considerations

`LocalDate` objects are:

* Small
* Immutable
* Lightweight
* Efficient

Creating new instances is inexpensive.

Don't try to optimize by reusing mutable objects—that's exactly what the old API did, and it led to many bugs.

---

# Best Practices

* Use `LocalDate` only when you don't need a time.
* Prefer `Month` enums over numeric month values for readability.
* Store the result of `plus...()` and `minus...()` methods.
* Use `isBefore()`, `isAfter()`, and `isEqual()` instead of comparing references.
* Let the API handle leap years and month lengths instead of writing your own calculations.

---

# Guided Exercise 1 — Working with `LocalDate`

Create a new class named `LocalDateExercises`.

### Step 1

Create a variable with today's date and print it.

Expected output (example):

```text
Today: 2026-07-15
```

---

### Step 2

Create your birth date using `LocalDate.of(...)` and print:

```text
Birth date: 1999-08-21
```

(Replace with your actual birth date.)

---

### Step 3

Print the following information about your birth date:

* Year
* Month
* Month number
* Day of month
* Day of week
* Day of year
* Whether it was a leap year

---

### Step 4

Calculate and print:

* 30 days from today
* 6 months from today
* 1 year from today

---

### Step 5

Check whether your birthday is before today's date:

```text
Is birthday before today? true
```

---

### Step 6 (Challenge)

Create an expiration date one year from today. Then simulate checking the product after adding two years to today's date and print whether the product would be expired.

---

# Chapter Summary

In this chapter you learned:

* How to create `LocalDate` instances.
* The difference between the current date and a specific date.
* How to access date fields.
* How to perform date arithmetic.
* Why `LocalDate` is immutable.
* How to compare dates safely.
* Practical business scenarios where `LocalDate` is the right choice.

In the next chapter, we'll explore **`LocalTime`**, which represents the time of day independently of any date. There you'll learn how to work with hours, minutes, seconds, time arithmetic, and common scheduling scenarios.
