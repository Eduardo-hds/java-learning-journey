# Module 12 — Date & Time API

Welcome to **Module 12** of the Java Bootcamp.

This module marks another important milestone. Until now, we've worked mostly with data that doesn't naturally change over time. Real-world applications, however, almost always involve dates and times:

* Scheduling meetings
* User birthdays
* Payment due dates
* Event expiration
* Login timestamps
* Logs
* File creation times
* Time zone conversion
* Age calculation

Java's modern **`java.time` API** (introduced in Java 8 via JSR-310) was specifically designed to solve these problems safely, clearly, and efficiently.

Unlike previous modules, this one is less about algorithms and more about correctly modeling one of the most difficult domains in software engineering: **time**.

---

# Module Index

## Chapter 1 — Understanding Time in Software

* Why dates and times are difficult
* Calendars are human inventions
* Time zones
* UTC
* Leap years
* Daylight Saving Time
* Why "adding one day" isn't always 24 hours

---

## Chapter 2 — Legacy Date APIs

* `Date`
* `Calendar`
* Problems with the old API
* Mutability
* Thread safety
* Poor design
* Why Java introduced `java.time`

---

## Chapter 3 — Introduction to `java.time`

* Package overview
* Design philosophy
* Immutability
* Thread safety
* Main classes
* Choosing the correct class

---

## Chapter 4 — LocalDate

* Current date
* Specific dates
* Date arithmetic
* Comparisons
* Useful methods

Exercises included.

---

## Chapter 5 — LocalTime

* Current time
* Specific times
* Arithmetic
* Comparisons

Exercises included.

---

## Chapter 6 — LocalDateTime

* Combining date and time
* Scheduling
* Arithmetic
* Comparing timestamps

Exercises included.

---

## Chapter 7 — Instant

* UTC
* Epoch time
* Current instant
* Machine timestamps

Exercises included.

---

## Chapter 8 — Duration & Period

* Measuring elapsed time
* Difference between Duration and Period
* Calculating intervals
* Business use cases

Exercises included.

---

## Chapter 9 — Formatting & Parsing

* `DateTimeFormatter`
* Built-in formats
* Custom patterns
* Parsing
* Input validation

Exercises included.

---

## Chapter 10 — Time Zones

* `ZoneId`
* `ZonedDateTime`
* UTC vs Local Time
* Conversions
* Global applications

Exercises included.

---

## Chapter 11 — Advanced Operations

* `plus()`
* `minus()`
* `until()`
* `between()`
* `isBefore()`
* `isAfter()`
* `isEqual()`

Practical examples.

---

## Chapter 12 — Guided Exercises

We'll build several independent mini-projects:

### Exercise 1

Age Calculator

### Exercise 2

Days Until Event

### Exercise 3

Appointment Scheduler

### Exercise 4

Date Formatter

### Exercise 5

Safe Date Parser

### Exercise 6

World Clock

### Exercise 7

Duration Calculator

---

## Chapter 13 — Final Project

Build a complete console application:

# Event Management System

The project will be developed progressively throughout the module.

Features include:

* Register events
* Event scheduling
* Date formatting
* Remaining time calculation
* Multiple time zones
* Organized packages
* Separation of responsibilities
* Clean architecture

Project structure:

```text
src/
 ├── Main.java
 ├── model/
 │    ├── Appointment.java
 │    ├── Event.java
 │    └── Reminder.java
 ├── service/
 │    ├── DateCalculator.java
 │    ├── EventScheduler.java
 │    └── FormatterService.java
 └── util/
```

As in previous modules, **`Main.java`** will only coordinate the application. Business logic belongs in the service layer.

---

# Learning Goals

By the end of this module you will be able to:

* Understand how computers represent time.
* Choose the correct Java date/time class.
* Perform date arithmetic correctly.
* Work with immutable temporal objects.
* Format dates for users.
* Parse user input safely.
* Calculate ages and intervals.
* Work with UTC.
* Convert between time zones.
* Build scheduling systems.
* Avoid common mistakes involving mutable dates and time zones.

---

# Why Date and Time Are Surprisingly Difficult

At first glance, dates seem simple.

Imagine writing:

```java
tomorrow = today + 1;
```

Easy, right?

Unfortunately, the real world isn't that simple.

Software must deal with questions such as:

* How many days are in February?
* Is this year a leap year?
* What happens when daylight saving time begins?
* Which country's calendar is being used?
* Is the time stored in UTC or local time?
* Is this timestamp before or after a time-zone conversion?
* What if a meeting is scheduled simultaneously in Brazil, Japan, and the United States?

Even experienced developers frequently make mistakes with dates and times because time is governed by **human conventions**, not just mathematics.

Some examples of real-world complexity include:

* Months have different lengths.
* Leap years add an extra day.
* Some countries observe Daylight Saving Time, while others do not.
* Time zones change due to political decisions.
* The same instant can have different local times depending on the region.

Because of these complexities, date and time handling is considered one of the most error-prone areas in software engineering.

---

# The Legacy APIs (`Date` and `Calendar`)

Before Java 8, developers primarily used two classes:

```java
Date
```

and

```java
Calendar
```

These APIs worked, but they accumulated design problems over many years.

Some of the biggest issues were:

### Mutable Objects

Changing a date modified the existing object, making bugs easier to introduce.

### Poor API Design

Methods were confusing.

Example:

```java
getMonth()
```

returned values from **0 to 11** instead of **1 to 12**.

---

### Thread Safety Issues

Sharing `Date` or `Calendar` instances across multiple threads could produce unexpected behavior because the objects were mutable.

---

### Difficult to Read

Simple operations often required many lines of code.

Example:

```java
Calendar calendar = Calendar.getInstance();

calendar.add(Calendar.DAY_OF_MONTH, 5);
```

Compared to the modern API:

```java
LocalDate.now().plusDays(5);
```

The newer version is shorter, clearer, and less error-prone.

---

### Mixed Responsibilities

The legacy API mixed concepts such as:

* dates
* times
* time zones
* formatting
* calculations

into classes that were difficult to understand and maintain.

---

# Why `java.time` Replaced the Legacy APIs

Java 8 introduced the **`java.time`** package to address these shortcomings.

Its design focused on several key principles:

## 1. Immutability

Date/time objects cannot be modified after creation.

```java
LocalDate today = LocalDate.now();

LocalDate tomorrow = today.plusDays(1);
```

`today` remains unchanged.

This eliminates many subtle bugs.

---

## 2. Thread Safety

Because objects are immutable, they can safely be shared between threads without synchronization.

---

## 3. Clear Separation of Responsibilities

Instead of one large, multipurpose class, the API provides specialized types:

| Class           | Responsibility           |
| --------------- | ------------------------ |
| `LocalDate`     | Date only                |
| `LocalTime`     | Time only                |
| `LocalDateTime` | Date + time              |
| `Instant`       | Exact UTC timestamp      |
| `Duration`      | Time-based interval      |
| `Period`        | Date-based interval      |
| `ZoneId`        | Time zone identifier     |
| `ZonedDateTime` | Date/time with time zone |

Each class has a single, well-defined purpose, making code easier to understand and maintain.

---

## 4. Fluent API

Operations read almost like natural language.

```java
LocalDate.now()
         .plusWeeks(2)
         .minusDays(3);
```

This fluent style improves readability and reduces boilerplate.

---

## 5. Better Performance

Creating immutable objects does allocate new instances, but these classes are lightweight and optimized by the JVM. In most business applications, the benefits of correctness, readability, and safety far outweigh the small allocation cost.

---

## 6. International Standards

The API is based on the ISO-8601 standard and inspired by the highly regarded Joda-Time library, resulting in consistent and predictable behavior.

---

# The Big Picture of `java.time`

You can think of the main classes as follows:

```text
                java.time

                  LocalDate
                 (date only)

                     │

                  LocalTime
                 (time only)

                     │

               LocalDateTime
             (date + time)

                     │

                  ZonedDateTime
         (date + time + timezone)

                     │

                  Instant
          (absolute UTC timestamp)
```

Each class models a different concept. Choosing the right one is an important design decision that we'll explore throughout this module.

---

# What Comes Next

In the next chapter, we'll begin using the API by exploring **`LocalDate`**, the foundation for working with calendar dates. You'll learn how to create dates, perform arithmetic, compare values, and understand why immutability changes how date operations are written.
