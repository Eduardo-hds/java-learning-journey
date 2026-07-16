# Chapter 4 — LocalDateTime

So far, we've learned two separate concepts:

* `LocalDate` → **When is the day?**
* `LocalTime` → **What is the time?**

Most real-world events require **both**.

Examples:

* Doctor appointment
* Job interview
* Flight departure
* Restaurant reservation
* Calendar event
* School class
* Meeting

This is exactly why Java provides:

```java
LocalDateTime
```

It combines a **date** and a **time** into a single immutable object.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Understand what `LocalDateTime` represents
* Create current and specific date-time values
* Combine `LocalDate` and `LocalTime`
* Access date and time components
* Perform arithmetic
* Compare date-time values
* Understand when `LocalDateTime` should and should not be used
* Apply it to common business scenarios

---

# What is `LocalDateTime`?

`LocalDateTime` represents:

* Date
* Time

Example:

```text
2026-07-15T14:30:00
```

It contains:

* Year
* Month
* Day
* Hour
* Minute
* Second
* Nanosecond

It does **NOT** contain:

* UTC offset
* Time zone

Think of it as saying:

> "July 15th at 2:30 PM"

But **where?**

Brazil?

Japan?

London?

The object doesn't know.

---

# When Should You Use It?

`LocalDateTime` is ideal when the event happens in **one local context**.

Examples:

✔ Doctor appointment

✔ Gym class

✔ Restaurant reservation

✔ School timetable

✔ Company meeting in the same office

✔ Reminder

---

# When NOT to Use It

Don't use it when the exact moment in the world matters.

Examples:

* Server logs
* API timestamps
* Distributed systems
* International flights
* Cloud applications
* Global scheduling

These should use:

* `Instant`
* `ZonedDateTime`

We'll study them later.

---

# Importing

```java
import java.time.LocalDateTime;
```

---

# Creating the Current Date and Time

```java
LocalDateTime now =
        LocalDateTime.now();

System.out.println(now);
```

Example output:

```text
2026-07-15T09:45:21.315820900
```

Notice the letter:

```text
T
```

This follows the ISO-8601 standard and separates the date from the time.

It is **not** a time zone indicator.

---

# Creating a Specific Date and Time

```java
LocalDateTime meeting =
        LocalDateTime.of(
                2026,
                8,
                10,
                14,
                30
        );

System.out.println(meeting);
```

Output:

```text
2026-08-10T14:30
```

You can also include seconds and nanoseconds:

```java
LocalDateTime precise =
        LocalDateTime.of(
                2026,
                8,
                10,
                14,
                30,
                45,
                250_000_000
        );
```

---

# Creating from Existing Objects

Often you already have a `LocalDate` and a `LocalTime`.

Instead of recreating everything:

```java
LocalDate date =
        LocalDate.of(2026, 8, 10);

LocalTime time =
        LocalTime.of(14, 30);

LocalDateTime meeting =
        LocalDateTime.of(date, time);
```

This is one of the most common ways to build a `LocalDateTime`.

---

# Extracting the Date

```java
LocalDateTime meeting =
        LocalDateTime.now();

LocalDate date =
        meeting.toLocalDate();

System.out.println(date);
```

Output:

```text
2026-07-15
```

---

# Extracting the Time

```java
LocalTime time =
        meeting.toLocalTime();

System.out.println(time);
```

Output:

```text
09:45:21.315820900
```

---

# Accessing Individual Fields

Everything available in `LocalDate` and `LocalTime` is also available here.

```java
LocalDateTime now =
        LocalDateTime.now();

System.out.println(now.getYear());

System.out.println(now.getMonth());

System.out.println(now.getDayOfMonth());

System.out.println(now.getHour());

System.out.println(now.getMinute());

System.out.println(now.getSecond());
```

---

# Date-Time Arithmetic

Like every class in `java.time`, `LocalDateTime` is immutable.

Operations return new objects.

---

## Adding Days

```java
LocalDateTime tomorrow =
        LocalDateTime.now()
                .plusDays(1);
```

---

## Adding Hours

```java
LocalDateTime later =
        LocalDateTime.now()
                .plusHours(3);
```

---

## Adding Months

```java
LocalDateTime renewal =
        LocalDateTime.now()
                .plusMonths(6);
```

---

## Combining Operations

```java
LocalDateTime result =
        LocalDateTime.now()
                .plusYears(1)
                .minusMonths(2)
                .plusDays(5)
                .plusHours(4)
                .plusMinutes(20);
```

The API remains fluent and readable even with multiple operations.

---

# Crossing Midnight

Unlike `LocalTime`, `LocalDateTime` keeps track of the date.

Example:

```java
LocalDateTime dateTime =
        LocalDateTime.of(
                2026,
                7,
                15,
                23,
                30
        );

LocalDateTime result =
        dateTime.plusHours(2);

System.out.println(result);
```

Output:

```text
2026-07-16T01:30
```

Notice that **both the time and the date changed automatically**.

This is one of the major advantages over using `LocalDate` and `LocalTime` separately.

---

# Comparing Date-Time Values

## `isBefore()`

```java
LocalDateTime now =
        LocalDateTime.now();

LocalDateTime meeting =
        LocalDateTime.of(
                2026,
                8,
                1,
                14,
                0
        );

System.out.println(
        now.isBefore(meeting)
);
```

---

## `isAfter()`

```java
System.out.println(
        now.isAfter(meeting)
);
```

---

## `isEqual()`

```java
LocalDateTime first =
        LocalDateTime.now();

LocalDateTime second =
        first;

System.out.println(
        first.isEqual(second)
);
```

---

# Business Example 1 — Appointment

```java
LocalDateTime appointment =
        LocalDateTime.of(
                2026,
                9,
                3,
                15,
                30
        );

if (appointment.isAfter(LocalDateTime.now())) {
    System.out.println("Upcoming appointment.");
}
```

---

# Business Example 2 — Deadline

```java
LocalDateTime deadline =
        LocalDateTime.of(
                2026,
                12,
                31,
                23,
                59
        );

boolean expired =
        LocalDateTime.now().isAfter(deadline);

System.out.println(expired);
```

---

# Business Example 3 — Class Schedule

```java
LocalDate date =
        LocalDate.of(2026, 8, 20);

LocalTime time =
        LocalTime.of(19, 0);

LocalDateTime classStart =
        LocalDateTime.of(date, time);

System.out.println(classStart);
```

---

# Immutability Revisited

This still doesn't work:

```java
LocalDateTime meeting =
        LocalDateTime.now();

meeting.plusHours(1);

System.out.println(meeting);
```

The original object is unchanged.

Correct:

```java
meeting = meeting.plusHours(1);
```

or

```java
LocalDateTime updated =
        meeting.plusHours(1);
```

---

# Method Chaining

```java
LocalDateTime event =
        LocalDateTime.now()
                .plusWeeks(2)
                .plusHours(3)
                .minusMinutes(15);
```

This style is encouraged because every method returns a new object.

---

# Internal Behavior

Internally, `LocalDateTime` is essentially a composition of:

```text
LocalDate
        +
LocalTime
```

Conceptually:

```text
        LocalDate
      (2026-07-15)

            +

        LocalTime
        (14:30)

            │
            ▼

      LocalDateTime
 2026-07-15T14:30
```

It **does not** calculate UTC offsets or know anything about time zones.

---

# Common Mistakes

## Mistake 1 — Using `LocalDateTime` for Global Timestamps

Suppose a server in Brazil stores:

```text
2026-07-15T10:00
```

Another server in Japan reads it.

What does **10:00** mean?

Without a time zone, there is no way to know.

For globally shared timestamps, use `Instant` or `ZonedDateTime`.

---

## Mistake 2 — Forgetting Immutability

```java
meeting.plusDays(2);
```

Nothing changes.

Always assign the returned object.

---

## Mistake 3 — Using `==`

Wrong:

```java
meeting1 == meeting2
```

Correct:

```java
meeting1.equals(meeting2)
```

or

```java
meeting1.isEqual(meeting2)
```

---

# Performance Considerations

`LocalDateTime` is:

* Immutable
* Lightweight
* Thread-safe
* Efficient

The JVM handles the creation of these small objects very efficiently.

Favor clarity and correctness over trying to reuse objects.

---

# Best Practices

* Use `LocalDateTime` when both date and time are needed but no time zone is involved.
* Use `LocalDate` and `LocalTime` separately if they naturally represent independent concepts.
* Store the result of arithmetic methods.
* Use `isBefore()`, `isAfter()`, and `isEqual()` for comparisons.
* Switch to `Instant` or `ZonedDateTime` when dealing with distributed or international systems.

---

# Guided Exercise 3 — Appointment Scheduler

Create a new class named `LocalDateTimeExercises`.

### Step 1

Create a variable with the current date and time.

Print:

```text
Current date and time:
2026-07-15T09:45:21
```

---

### Step 2

Create an appointment for a specific date and time.

Example:

* Date: August 20, 2026
* Time: 14:30

Print the appointment.

---

### Step 3

Create the appointment by combining a `LocalDate` and a `LocalTime` using `LocalDateTime.of(date, time)`.

Verify that the result matches the one from Step 2.

---

### Step 4

Extract and print:

* Date
* Time
* Year
* Month
* Day
* Hour
* Minute

---

### Step 5

Create a new `LocalDateTime` that is:

* 7 days later
* 2 hours later
* 30 minutes earlier

Print both the original and the modified values to confirm that the original object did not change.

---

### Step 6

Check whether the appointment is:

* In the future
* In the past
* Exactly equal to the current date and time

Use `isBefore()`, `isAfter()`, and `isEqual()`.

---

### Step 7 (Mini Challenge)

Simulate an appointment reminder.

If the appointment is in the future, print:

```text
Your appointment is scheduled for:
2026-08-20T14:30
```

Otherwise, print:

```text
This appointment has already passed.
```

> **Preparation for the Final Project:** The logic you implemented here will later be moved into the `Appointment` model and an `EventScheduler` service. This exercise introduces the core functionality you'll progressively build into the **Event Management System**.
