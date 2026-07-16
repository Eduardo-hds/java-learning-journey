# Chapter 9 — Advanced Date & Time Operations

Throughout this module, you've already used many methods such as:

```java
plusDays()
minusMonths()
isBefore()
isAfter()
Duration.between()
Period.between()
```

Although these methods are convenient, the Java Time API provides a more **generic and flexible** way to work with temporal objects.

Many classes in `java.time` implement the **`Temporal`** and **`TemporalAccessor`** interfaces, allowing common operations to work consistently across different date/time types.

This chapter ties together everything you've learned so far and introduces utility methods you'll use frequently in real-world applications.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Understand generic temporal operations
* Use `plus()` and `minus()`
* Use `until()`
* Use `ChronoUnit.between()`
* Review comparison methods
* Choose the right approach for different scenarios
* Understand the common API design of `java.time`

---

# Why Generic Methods Exist

Earlier, we wrote code like this:

```java
LocalDate today = LocalDate.now();

LocalDate nextWeek =
        today.plusDays(7);
```

This is perfectly valid.

But what if the number of days is stored in a variable?

Or what if we want to switch between days, weeks, or months dynamically?

Instead of using a different method for each unit, Java allows us to write:

```java
today.plus(7, ChronoUnit.DAYS);
```

The operation becomes data-driven rather than method-driven.

---

# `ChronoUnit`

Import:

```java
import java.time.temporal.ChronoUnit;
```

`ChronoUnit` is an enum that represents standard units of time.

Some common values include:

```java
ChronoUnit.DAYS

ChronoUnit.WEEKS

ChronoUnit.MONTHS

ChronoUnit.YEARS

ChronoUnit.HOURS

ChronoUnit.MINUTES

ChronoUnit.SECONDS

ChronoUnit.MILLIS

ChronoUnit.NANOS
```

These units are used throughout the Date & Time API.

---

# `plus()`

Instead of:

```java
LocalDate tomorrow =
        LocalDate.now()
                .plusDays(1);
```

You can write:

```java
LocalDate tomorrow =
        LocalDate.now()
                .plus(1, ChronoUnit.DAYS);
```

Both produce the same result.

---

Another example:

```java
LocalDate vacation =
        LocalDate.now()
                .plus(3, ChronoUnit.MONTHS);
```

Instead of:

```java
.plusMonths(3)
```

---

With `LocalDateTime`:

```java
LocalDateTime meeting =
        LocalDateTime.now()
                .plus(2, ChronoUnit.HOURS);
```

---

# When to Prefer `plusDays()`

For simple, fixed operations:

```java
plusDays()

plusMonths()

plusYears()
```

are usually easier to read.

Example:

```java
invoice.plusDays(30);
```

is arguably clearer than:

```java
invoice.plus(30, ChronoUnit.DAYS);
```

---

# When to Prefer `plus()`

Imagine the user chooses a unit:

```text
Add:
10

Unit:
Months
```

Now we can write:

```java
date.plus(amount, unit);
```

without needing multiple `if` statements.

This flexibility makes `plus()` especially useful in reusable libraries and configurable applications.

---

# `minus()`

Works exactly the same way.

Instead of:

```java
today.minusDays(10);
```

we can write:

```java
today.minus(10, ChronoUnit.DAYS);
```

---

Example:

```java
LocalDate previousYear =
        LocalDate.now()
                .minus(1, ChronoUnit.YEARS);
```

---

# `until()`

Another powerful method is:

```java
until()
```

It calculates the amount of time **from the current object to another object**.

Example:

```java
LocalDate today =
        LocalDate.now();

LocalDate christmas =
        LocalDate.of(2026, 12, 25);

long days =
        today.until(
                christmas,
                ChronoUnit.DAYS
        );

System.out.println(days);
```

Possible output:

```text
163
```

Meaning:

```text
163 days remain.
```

---

# `until()` vs `between()`

These methods often confuse beginners.

Consider:

```java
today.until(christmas, ChronoUnit.DAYS);
```

and

```java
ChronoUnit.DAYS.between(
        today,
        christmas
);
```

They produce the same numeric result.

The difference is mostly stylistic.

One reads:

> "How many days until Christmas?"

The other reads:

> "How many days are between these dates?"

Both are correct.

---

# `ChronoUnit.between()`

Example:

```java
long days =
        ChronoUnit.DAYS.between(
                LocalDate.now(),
                LocalDate.of(2026, 12, 31)
        );
```

Another example:

```java
long hours =
        ChronoUnit.HOURS.between(
                LocalDateTime.now(),
                LocalDateTime.now()
                        .plusHours(5)
        );
```

Output:

```text
5
```

---

# Measuring Total Days

Earlier we learned that:

```java
Period
```

returns:

```text
Years

Months

Days
```

Suppose:

```text
2 years
3 months
10 days
```

Calling:

```java
period.getDays();
```

returns only:

```text
10
```

If your goal is:

> "How many total days have passed?"

use:

```java
ChronoUnit.DAYS.between(start, end);
```

This is one of the most common uses of `ChronoUnit`.

---

# Review — Comparison Methods

You've already seen these methods, but let's review them together.

---

## `isBefore()`

```java
LocalDate today =
        LocalDate.now();

LocalDate tomorrow =
        today.plusDays(1);

System.out.println(
        today.isBefore(tomorrow)
);
```

Output:

```text
true
```

---

## `isAfter()`

```java
System.out.println(
        tomorrow.isAfter(today)
);
```

---

## `isEqual()`

Available on:

* `LocalDate`
* `LocalTime`
* `LocalDateTime`
* `ZonedDateTime`

Example:

```java
LocalDate first =
        LocalDate.now();

LocalDate second =
        LocalDate.now();

System.out.println(
        first.isEqual(second)
);
```

Remember that `Instant` does **not** have `isEqual()`. Use `equals()` instead.

---

# Business Example 1 — Subscription Expiration

```java
LocalDate expiration =
        LocalDate.now()
                .plus(30, ChronoUnit.DAYS);

System.out.println(expiration);
```

---

# Business Example 2 — Days Until Vacation

```java
LocalDate vacation =
        LocalDate.of(2026, 12, 20);

long remaining =
        ChronoUnit.DAYS.between(
                LocalDate.now(),
                vacation
        );

System.out.println(
        remaining
);
```

---

# Business Example 3 — Appointment Reminder

```java
LocalDateTime appointment =
        LocalDateTime.of(
                2026,
                8,
                10,
                14,
                30
        );

if (appointment.isAfter(LocalDateTime.now())) {
    System.out.println(
            "Upcoming appointment."
    );
}
```

---

# Internal Behavior

Most `java.time` classes share a common design.

Conceptually:

```text
          Temporal
             ▲
             │
 ┌───────────┼────────────┐
 │           │            │
 ▼           ▼            ▼

LocalDate LocalTime LocalDateTime
     │          │           │
     └──────────┴───────────┘

Shared operations

plus()

minus()

until()
```

This consistent API makes it easier to learn new date/time classes.

---

# Common Mistakes

## Mistake 1

Using `Period` when you need total days.

Wrong:

```java
period.getDays();
```

Better:

```java
ChronoUnit.DAYS.between(...)
```

---

## Mistake 2

Confusing `until()` and `between()`.

Remember:

```text
today.until(christmas)
```

reads naturally from the starting object.

While:

```text
ChronoUnit.DAYS.between(today, christmas)
```

is a static utility method.

Choose whichever makes the code more expressive.

---

## Mistake 3

Forgetting immutability.

```java
date.plus(5, ChronoUnit.DAYS);
```

does not modify `date`.

Always assign the returned value.

---

# Performance Considerations

Methods like:

* `plus()`
* `minus()`
* `until()`
* `between()`

are optimized and inexpensive.

Choose the method that makes your code clearer.

Readability is generally more important than tiny performance differences.

---

# Best Practices

* Prefer specialized methods (`plusDays()`, `minusMonths()`) when the unit is fixed and readability benefits.
* Use `plus()` and `minus()` with `ChronoUnit` when the unit is dynamic or configurable.
* Use `ChronoUnit.between()` when you need a total amount in a specific unit.
* Use `until()` when the calculation reads naturally from the starting object.
* Continue relying on `isBefore()`, `isAfter()`, and `isEqual()` for comparisons.

---

# Guided Exercise 8 — Advanced Date & Time Operations

Create a class named `AdvancedOperationsExercises`.

---

## Step 1

Create today's date.

Using `plus()` and `ChronoUnit`, calculate:

* 15 days later
* 2 months later
* 1 year later

Print each result.

---

## Step 2

Using `minus()`, calculate:

* 7 days earlier
* 6 months earlier
* 5 years earlier

---

## Step 3

Create a future date.

Calculate the number of days until that date using:

```java
until(...)
```

Then perform the same calculation using:

```java
ChronoUnit.DAYS.between(...)
```

Compare the results.

---

## Step 4

Create two `LocalDateTime` objects.

Calculate:

* Total hours between them
* Total minutes between them

using `ChronoUnit`.

---

## Step 5

Create two appointments.

Use:

* `isBefore()`
* `isAfter()`
* `isEqual()`

to compare them.

Print clear messages describing the relationship.

---

## Step 6 (Challenge)

Build a simple **Date Calculator** class (which fits the `DateCalculator` service from the module's project structure).

Implement methods such as:

```java
LocalDate addDays(LocalDate date, int days)

LocalDate subtractMonths(LocalDate date, int months)

long daysBetween(LocalDate start, LocalDate end)

boolean isFuture(LocalDate date)
```

Use the generic methods (`plus()`, `minus()`, `ChronoUnit.between()`, and comparison methods) wherever appropriate.

This class will become part of the **Event Management System** in the final project.

---

# Chapter Summary

In this chapter, you learned:

* How generic temporal operations work across the `java.time` API.
* The role of `ChronoUnit`.
* When to use `plus()` and `minus()` instead of specialized methods.
* How `until()` and `ChronoUnit.between()` compare.
* How to calculate total units (days, hours, minutes) between temporal objects.
* Best practices for writing clear, flexible, and maintainable date/time code.

---

# ✔️ Next Step

The next chapter is the **Final Project** of Module 12.

You'll progressively build a **console-based Event Management System** using everything you've learned:

* `LocalDate`
* `LocalTime`
* `LocalDateTime`
* `Instant`
* `Duration`
* `Period`
* `DateTimeFormatter`
* `ZoneId`
* `ZonedDateTime`
* `ChronoUnit`

The focus will be on clean package organization, separating business logic from `Main.java`, and applying the Date & Time API to realistic scheduling and event management scenarios.
