# Chapter 1 — Introduction to `java.time`

In the previous chapter, we learned **why** Java introduced a completely new Date & Time API.

Now we'll start learning the API itself.

This chapter is one of the most important in the module because it establishes the mental model you'll use for every other date/time class.

---

# Chapter Objectives

By the end of this chapter you will understand:

* What the `java.time` package is
* The philosophy behind its design
* Why its classes are immutable
* Why immutability makes them thread-safe
* How to choose the correct date/time class
* The hierarchy and relationship between the main classes
* Common beginner mistakes
* Best practices

---

# What is `java.time`?

`java.time` is Java's modern API for representing and manipulating dates and times.

It was introduced in **Java 8** (2014) and has been the recommended approach ever since.

Unlike the old APIs (`Date` and `Calendar`), it was designed from the ground up with modern software engineering principles:

* Clear responsibilities
* Immutable objects
* Thread safety
* Fluent methods
* Better readability
* Better maintainability

The package contains dozens of classes, but in practice you'll use a relatively small core set.

---

# The Core Philosophy

The biggest design change is this:

> **One class should represent one concept.**

Instead of a single "date" object trying to represent everything, Java provides specialized classes.

For example:

| Concept            | Class           |
| ------------------ | --------------- |
| Date only          | `LocalDate`     |
| Time only          | `LocalTime`     |
| Date + Time        | `LocalDateTime` |
| Absolute instant   | `Instant`       |
| Time Zone          | `ZoneId`        |
| Date + Time + Zone | `ZonedDateTime` |
| Date difference    | `Period`        |
| Time difference    | `Duration`      |

This separation greatly reduces ambiguity and bugs.

---

# Understanding the Main Classes

Let's examine each one conceptually before using them.

---

## `LocalDate`

Represents **only a calendar date**.

Example:

```text
2026-07-15
```

Contains:

* year
* month
* day

Does **NOT** contain:

* hour
* minute
* second
* time zone

Business examples:

* Birthday
* Holiday
* Due date
* Invoice date
* Employment start date

Use it whenever the time of day doesn't matter.

---

## `LocalTime`

Represents **only a time of day**.

Example:

```text
14:30:15
```

Contains:

* hour
* minute
* second
* nanosecond

Does **NOT** contain:

* year
* month
* day
* time zone

Business examples:

* Store opening hours
* Alarm clock
* Lunch break
* Daily meeting at 09:00

---

## `LocalDateTime`

Represents:

* date
* time

Example:

```text
2026-07-15 14:30
```

Still does **NOT** know:

* country
* city
* time zone

Business examples:

* Appointment
* Reservation
* Calendar event
* Class schedule

---

## `Instant`

Represents a single exact moment in time.

Think of it as the timestamp computers use internally.

Example:

```text
2026-07-15T12:30:15Z
```

Notice the `Z`.

`Z` means:

```text
UTC (Coordinated Universal Time)
```

An `Instant` always refers to the exact same point in time, no matter where you are.

Business examples:

* Database timestamps
* API communication
* Audit logs
* Authentication tokens

---

## `ZoneId`

Represents a geographic time zone.

Examples:

```text
America/Sao_Paulo
```

```text
Europe/London
```

```text
Asia/Tokyo
```

A `ZoneId` contains the rules needed to convert between UTC and local time.

---

## `ZonedDateTime`

Combines:

* date
* time
* time zone

Example:

```text
2026-07-15T09:00-03:00[America/Sao_Paulo]
```

This object knows:

* the date
* the clock time
* the region
* the UTC offset
* daylight saving rules (if applicable)

This is essential for international applications.

---

## `Duration`

Represents an amount of **time**.

Measured using:

* hours
* minutes
* seconds
* nanoseconds

Examples:

```text
2 hours
```

```text
15 minutes
```

```text
90 seconds
```

Good for measuring elapsed time.

Examples:

* Video duration
* Request processing time
* Stopwatch
* Flight time

---

## `Period`

Represents an amount of **calendar time**.

Measured using:

* years
* months
* days

Examples:

```text
2 years
```

```text
3 months
```

```text
10 days
```

Useful for:

* Age calculation
* Subscription periods
* Rental contracts
* Warranty duration

---

# Choosing the Correct Class

This is one of the most important skills in this module.

Imagine you need to store someone's birthday.

Should you use:

```java
LocalDateTime
```

No.

Birthdays don't have a time.

The correct choice is:

```java
LocalDate
```

---

Imagine a cinema session.

You need:

* date
* hour

Use:

```java
LocalDateTime
```

---

Imagine storing when a user logged into your server.

Should you use `LocalDateTime`?

Usually **no**.

Servers often communicate globally.

Use:

```java
Instant
```

because it represents the exact same moment for every machine.

---

# Decision Guide

```text
Do you only need a date?

        YES
         │
         ▼
   LocalDate

----------------------------

Do you only need a time?

        YES
         │
         ▼
   LocalTime

----------------------------

Need both?

        YES
         │
         ▼
 LocalDateTime

----------------------------

Need an exact global timestamp?

        YES
         │
         ▼
    Instant

----------------------------

Need a timezone?

        YES
         │
         ▼
 ZonedDateTime
```

A good rule of thumb is to choose the **simplest class that accurately models your data**.

---

# Immutability

One of the defining characteristics of `java.time` is that **all core classes are immutable**.

Once created, an object cannot change.

Example:

```java
LocalDate today = LocalDate.now();

today.plusDays(1);

System.out.println(today);
```

Many beginners expect `today` to become tomorrow.

It doesn't.

The output is still today's date because `plusDays()` returns a **new** object.

To keep the result:

```java
LocalDate today = LocalDate.now();

LocalDate tomorrow = today.plusDays(1);
```

Now:

```text
today
```

and

```text
tomorrow
```

are two different objects.

---

# Why Immutability?

Imagine two variables referencing the same mutable object:

```text
A ----\
       \
        Date Object
       /
B ----/
```

If A changes it:

```text
A -> tomorrow
```

Then B also sees the modified value.

This can create subtle bugs.

With immutable objects, every modification creates a new instance:

```text
today ---------> 2026-07-15

plusDays(1)

tomorrow ------> 2026-07-16
```

The original object remains unchanged.

---

# Thread Safety

Because immutable objects never change after creation, multiple threads can safely share the same instance without synchronization.

For example, imagine hundreds of threads reading the same `LocalDate` object. Since no thread can modify it, there is no risk of one thread affecting another.

This makes `java.time` classes naturally thread-safe, unlike the legacy `Date` and `Calendar` classes.

---

# Method Chaining

Most methods return a new object, which allows chaining.

Example:

```java
LocalDate result = LocalDate.now()
        .plusMonths(2)
        .minusDays(5)
        .plusYears(1);
```

This style is called a **fluent API**.

Benefits:

* Easier to read
* Less temporary variables
* Expressive code
* Encourages immutability

---

# Performance Considerations

A common question is:

> "Does creating new objects every time hurt performance?"

In most applications, **no**.

Reasons:

* Date/time objects are lightweight.
* The JVM is highly optimized for allocating and garbage-collecting short-lived objects.
* The safety and readability gained from immutability far outweigh the small allocation cost.

Only in extremely performance-sensitive systems (such as some high-frequency trading applications) might object creation become a consideration.

---

# Common Mistakes

### Mistake 1 — Choosing the Wrong Class

```java
LocalDateTime birthday;
```

Better:

```java
LocalDate birthday;
```

---

### Mistake 2 — Ignoring the Returned Object

```java
date.plusDays(3);
```

Nothing changes.

Correct:

```java
date = date.plusDays(3);
```

or

```java
LocalDate future = date.plusDays(3);
```

---

### Mistake 3 — Using `LocalDateTime` Everywhere

Many beginners use `LocalDateTime` for every situation.

Ask yourself:

* Do I need only a date?
* Do I need only a time?
* Do I need an exact global timestamp?
* Do I need a time zone?

Using the most appropriate class makes your code clearer and prevents logical errors.

---

# Best Practices

* Use the simplest date/time class that fits the problem.
* Remember that all `java.time` objects are immutable.
* Store the result of methods like `plus()` and `minus()`.
* Use `Instant` for machine timestamps and distributed systems.
* Use `LocalDate` for dates without a time.
* Use `LocalTime` for times without a date.
* Use `LocalDateTime` only when both date and time are required and no time zone is involved.
* Use `ZonedDateTime` when working across regions or countries.

---

# Chapter Summary

In this chapter, you learned:

* The philosophy behind the `java.time` API.
* The purpose of each core date/time class.
* How to choose the right class for different scenarios.
* Why immutability is a central design principle.
* How immutability leads to thread safety.
* Why methods return new objects instead of modifying existing ones.
* Common mistakes and recommended best practices.

You now have the conceptual foundation needed to start working with the API. In the next chapter, we'll begin with the first and one of the most commonly used classes: **`LocalDate`**, where you'll learn to create dates, perform date arithmetic, compare dates, and use them in practical business scenarios.
