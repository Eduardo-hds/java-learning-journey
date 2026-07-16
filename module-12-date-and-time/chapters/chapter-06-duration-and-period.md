# Chapter 6 — Duration & Period

So far, we've learned how to represent:

* Dates (`LocalDate`)
* Times (`LocalTime`)
* Date and time (`LocalDateTime`)
* Exact moments (`Instant`)

Now we'll answer a different question:

> **How much time exists between two temporal values?**

Java provides **two different classes** for this purpose:

```java
Duration
```

and

```java
Period
```

At first they seem similar.

In reality, they solve **completely different problems**.

Choosing the wrong one is one of the most common beginner mistakes.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Understand the difference between `Duration` and `Period`
* Know when to use each class
* Calculate elapsed time
* Measure business intervals
* Use `between()`
* Understand why two separate classes exist
* Avoid common mistakes

---

# The Big Difference

This is the most important concept in this chapter.

Think of it like this:

```text
Duration
↓

Measures TIME

Hours
Minutes
Seconds
Nanoseconds
```

While:

```text
Period
↓

Measures CALENDAR

Years
Months
Days
```

---

## Visual Comparison

```text
08:00 ------------------- 10:30

Elapsed?

2 hours 30 minutes

↓

Duration
```

---

```text
January 1 ---------------- March 15

Elapsed?

2 months 14 days

↓

Period
```

Notice that one thinks in **clock time**.

The other thinks in **calendar units**.

---

# Why Two Classes?

Suppose someone asks:

> "How old are you?"

Would you answer:

```text
864,000,000 seconds
```

Of course not.

You would say:

```text
27 years
```

Age is naturally measured using **calendar units**.

Now imagine:

> "How long did the download take?"

Would you answer:

```text
0 years
0 months
0 days
```

No.

You would say:

```text
12 seconds
```

Downloads are naturally measured using **time units**.

That's why Java separates these concepts.

---

# Duration

Import:

```java
import java.time.Duration;
```

A `Duration` represents an amount of **time**.

It works with:

* `Instant`
* `LocalTime`
* `LocalDateTime`

---

# Creating a Duration

Suppose we have:

```java
LocalTime start =
        LocalTime.of(9, 0);

LocalTime end =
        LocalTime.of(11, 30);
```

We can calculate:

```java
Duration duration =
        Duration.between(start, end);

System.out.println(duration);
```

Output:

```text
PT2H30M
```

This is ISO-8601 notation.

Meaning:

```text
Period of Time

2 Hours

30 Minutes
```

---

# Reading Duration Values

Instead of printing the object directly:

```java
System.out.println(duration.toHours());
```

Output:

```text
2
```

Notice something important.

The duration was:

```text
2 hours
30 minutes
```

But:

```java
toHours()
```

returns:

```text
2
```

because it returns **whole hours**.

---

Similarly:

```java
duration.toMinutes();
```

returns:

```text
150
```

which represents the **total elapsed minutes**.

This distinction is very important.

---

# Duration with LocalDateTime

```java
LocalDateTime start =
        LocalDateTime.of(
                2026,
                7,
                15,
                8,
                0
        );

LocalDateTime end =
        LocalDateTime.of(
                2026,
                7,
                15,
                17,
                30
        );

Duration work =
        Duration.between(start, end);

System.out.println(work.toHours());
```

Output:

```text
9
```

---

# Duration with Instant

This is extremely common.

```java
Instant start =
        Instant.now();

/* some task */

Instant end =
        Instant.now();

Duration execution =
        Duration.between(start, end);

System.out.println(
        execution.toMillis()
);
```

Perfect for measuring execution time.

---

# Useful Methods

```java
toHours()

toMinutes()

toSeconds()

toMillis()

toNanos()
```

Each returns the **total** amount in the requested unit.

---

# Period

Import:

```java
import java.time.Period;
```

A `Period` measures:

* Years
* Months
* Days

It works with:

```java
LocalDate
```

---

# Creating a Period

```java
LocalDate birth =
        LocalDate.of(1999, 8, 21);

LocalDate today =
        LocalDate.now();

Period age =
        Period.between(birth, today);

System.out.println(age);
```

Output:

```text
P26Y10M24D
```

Meaning:

```text
26 years

10 months

24 days
```

---

# Reading Individual Components

```java
System.out.println(age.getYears());

System.out.println(age.getMonths());

System.out.println(age.getDays());
```

Example:

```text
26
10
24
```

---

# Important Observation

Consider:

```java
Period age =
        Period.between(
                birth,
                today
        );
```

Suppose the result is:

```text
26 years

10 months

24 days
```

Calling:

```java
age.getDays();
```

returns:

```text
24
```

It **does not** return the total number of elapsed days.

It returns only the **days component** after years and months have already been accounted for.

If you need the total number of days between two dates, use:

```java
ChronoUnit.DAYS.between(start, end)
```

We'll cover `ChronoUnit` later in the module.

---

# Business Example 1 — Age Calculator

```java
LocalDate birthday =
        LocalDate.of(
                1999,
                8,
                21
        );

Period age =
        Period.between(
                birthday,
                LocalDate.now()
        );

System.out.println(
        age.getYears()
);
```

Exactly what we'll build in Exercise 1.

---

# Business Example 2 — Employee Seniority

```java
LocalDate hired =
        LocalDate.of(
                2020,
                2,
                10
        );

Period seniority =
        Period.between(
                hired,
                LocalDate.now()
        );

System.out.println(
        seniority.getYears()
);
```

---

# Business Example 3 — Measuring Program Execution

```java
Instant start =
        Instant.now();

/* process */

Instant end =
        Instant.now();

Duration elapsed =
        Duration.between(
                start,
                end
        );

System.out.println(
        elapsed.toMillis()
);
```

---

# `between()`

Both classes provide the static method:

```java
between()
```

Examples:

```java
Duration.between(start, end);
```

and

```java
Period.between(start, end);
```

The meaning is always:

```text
end - start
```

If the first argument is later than the second, the result will be negative.

---

# Negative Intervals

Example:

```java
Duration result =
        Duration.between(
                LocalTime.of(12, 0),
                LocalTime.of(10, 0)
        );

System.out.println(result);
```

Output:

```text
PT-2H
```

Similarly:

```java
Period result =
        Period.between(
                LocalDate.of(2026, 7, 20),
                LocalDate.of(2026, 7, 15)
        );
```

Produces a negative period.

---

# Internal Behavior

Conceptually:

```text
Duration

↓

Elapsed time

↓

Seconds
+
Nanoseconds
```

---

While:

```text
Period

↓

Calendar

↓

Years
Months
Days
```

Different internal models.

Different purposes.

---

# Common Mistakes

## Mistake 1

Using `Duration` for age.

Wrong:

```java
Duration.between(
        birthday,
        today
);
```

`Duration` requires time-based values, not `LocalDate`.

Use:

```java
Period
```

instead.

---

## Mistake 2

Using `Period` for execution time.

Wrong:

```java
Period.between(
        start,
        end
);
```

Use:

```java
Duration
```

---

## Mistake 3

Confusing total values with components.

Example:

```java
Period
↓

2 years

5 months

10 days
```

Calling:

```java
getDays()
```

returns:

```text
10
```

not the total number of elapsed days.

Similarly:

```java
Duration

2 hours

30 minutes
```

Calling:

```java
toHours()
```

returns:

```text
2
```

not **2.5**.

Remember:

* `Period` getters return **components**.
* `Duration.to...()` methods return **totals**, truncated to whole units.

---

# Performance Considerations

Both classes are:

* Immutable
* Thread-safe
* Lightweight

Creating them is inexpensive.

The calculations are handled internally using optimized algorithms.

---

# Best Practices

* Use `Period` for dates.
* Use `Duration` for time.
* Measure execution time with `Instant` + `Duration`.
* Calculate age with `LocalDate` + `Period`.
* Be aware of the difference between total values and component values.
* Remember that `between(start, end)` computes `end - start`.

---

# Guided Exercise 5 — Working with `Duration` and `Period`

Create a class named `DurationPeriodExercises`.

---

## Step 1 — Age Calculator

Create your birth date using `LocalDate`.

Calculate your age with:

```java
Period.between(...)
```

Print:

* Years
* Months
* Days

Example:

```text
Age:

26 years

10 months

24 days
```

---

## Step 2 — Employee Seniority

Create a hiring date.

Calculate how long the employee has worked.

Print:

* Years
* Months
* Days

---

## Step 3 — Meeting Duration

Create:

* Start: **09:15**
* End: **11:45**

Calculate:

```java
Duration.between(...)
```

Print:

* Hours
* Minutes
* Seconds

Observe that:

* `toHours()` returns total whole hours.
* `toMinutes()` returns total whole minutes.

---

## Step 4 — Measure Execution Time

Record:

```java
Instant start = Instant.now();
```

Perform a simple task, such as a loop:

```java
for (int i = 0; i < 5_000_000; i++) {
    Math.sqrt(i);
}
```

Then record:

```java
Instant end = Instant.now();
```

Calculate the elapsed `Duration`.

Print the execution time in:

* Milliseconds
* Nanoseconds

---

## Step 5 (Challenge)

Create two `LocalDateTime` values representing:

* Meeting start
* Meeting end

Calculate how long the meeting lasted using `Duration`.

Then create two `LocalDate` values representing:

* Contract start
* Contract end

Calculate the contract length using `Period`.

Explain **why** one problem uses `Duration` and the other uses `Period`.

---

# Chapter Summary

In this chapter, you learned:

* Why Java provides both `Duration` and `Period`.
* The conceptual difference between elapsed **time** and elapsed **calendar** units.
* How to calculate time intervals with `Duration`.
* How to calculate calendar intervals with `Period`.
* How to use `between()` correctly.
* The difference between total values and component values.
* Common pitfalls when choosing the wrong class.

In the next chapter, we'll learn how to **format and parse** date/time objects using `DateTimeFormatter`. This is where you'll start converting Java's internal date/time representations into user-friendly formats and safely reading dates entered by users.
