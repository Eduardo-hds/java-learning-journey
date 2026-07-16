# Chapter 3 — LocalTime

In the previous chapter, we learned how to work with **calendar dates** using `LocalDate`.

Now we'll study its counterpart:

```java
LocalTime
```

While `LocalDate` answers **"On which day?"**, `LocalTime` answers:

> **"At what time?"**

Many business applications need only a time of day:

* Store opening hours
* Class schedules
* Alarm clocks
* Daily meetings
* Restaurant reservations
* Office working hours

In all these situations, **the date doesn't matter**.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Create `LocalTime` objects
* Obtain the current time
* Create specific times
* Access hours, minutes, and seconds
* Perform time arithmetic
* Compare times
* Understand time precision
* Apply `LocalTime` in practical scenarios

---

# What is `LocalTime`?

`LocalTime` represents **only the time of day**.

Example:

```text
14:30:15
```

It stores:

* Hour
* Minute
* Second
* Nanosecond

It does **not** store:

* Year
* Month
* Day
* Time zone

Think of it as the time displayed on a wall clock.

---

# When Should You Use It?

Use `LocalTime` whenever the date is irrelevant.

Examples:

* A store opens at **09:00**
* Lunch starts at **12:30**
* A meeting happens every day at **08:00**
* An alarm rings at **07:15**
* A restaurant closes at **23:00**

---

# When NOT to Use It

Don't use `LocalTime` when the date matters.

Examples:

❌ Flight departure

❌ Appointment on July 20 at 14:00

❌ Login timestamp

❌ Event registration

These require:

* `LocalDateTime`
* `Instant`
* `ZonedDateTime`

---

# Importing the Class

```java
import java.time.LocalTime;
```

---

# Getting the Current Time

```java
LocalTime now = LocalTime.now();

System.out.println(now);
```

Possible output:

```text
09:42:18.513728900
```

You may notice many decimal places.

That's because `LocalTime` stores **nanoseconds**.

---

# Internal Precision

Internally, `LocalTime` stores four components:

```text
Hour
Minute
Second
Nanosecond
```

Example:

```text
09:42:18.513728900
```

Means:

```text
Hour:        09
Minute:      42
Second:      18
Nanosecond:  513728900
```

Java uses nanoseconds (1 billionth of a second) as its finest unit of precision for `LocalTime`.

In practice, the actual precision depends on the operating system and hardware clock, so the nanosecond value often contains less precise data.

---

# Creating a Specific Time

Use the factory method:

```java
LocalTime lunch = LocalTime.of(12, 30);

System.out.println(lunch);
```

Output:

```text
12:30
```

You can also specify seconds:

```java
LocalTime time =
        LocalTime.of(14, 45, 30);
```

Or even nanoseconds:

```java
LocalTime precise =
        LocalTime.of(14, 45, 30, 500_000_000);
```

---

# Accessing Individual Fields

```java
LocalTime now = LocalTime.now();

System.out.println(now.getHour());
System.out.println(now.getMinute());
System.out.println(now.getSecond());
System.out.println(now.getNano());
```

Example output:

```text
9
42
18
513728900
```

---

# Time Arithmetic

Like all `java.time` classes, `LocalTime` is immutable.

Operations return **new objects**.

---

## Adding Hours

```java
LocalTime meeting =
        LocalTime.of(9, 0);

LocalTime end =
        meeting.plusHours(2);

System.out.println(end);
```

Output:

```text
11:00
```

---

## Adding Minutes

```java
LocalTime departure =
        LocalTime.of(8, 15);

LocalTime arrival =
        departure.plusMinutes(45);

System.out.println(arrival);
```

Output:

```text
09:00
```

---

## Adding Seconds

```java
LocalTime countdown =
        LocalTime.of(10, 0);

countdown = countdown.plusSeconds(30);
```

---

## Subtracting Time

```java
LocalTime now =
        LocalTime.now();

LocalTime earlier =
        now.minusHours(1);

LocalTime breakTime =
        now.minusMinutes(15);
```

---

# Crossing Midnight

One interesting behavior is that `LocalTime` wraps around the 24-hour clock.

Example:

```java
LocalTime time =
        LocalTime.of(23, 30);

LocalTime result =
        time.plusHours(2);

System.out.println(result);
```

Output:

```text
01:30
```

Notice that `LocalTime` doesn't know about dates. It simply wraps to the next valid time within a 24-hour day.

If you need to know that the date changed, use `LocalDateTime`.

---

# Immutability Again

Consider:

```java
LocalTime now =
        LocalTime.now();

now.plusHours(1);

System.out.println(now);
```

Did the time change?

No.

Exactly like `LocalDate`, `LocalTime` is immutable.

Correct:

```java
LocalTime later =
        now.plusHours(1);
```

or

```java
now = now.plusHours(1);
```

---

# Comparing Times

## `isBefore()`

```java
LocalTime opening =
        LocalTime.of(8, 0);

LocalTime current =
        LocalTime.now();

System.out.println(
        current.isBefore(opening));
```

---

## `isAfter()`

```java
System.out.println(
        current.isAfter(opening));
```

---

## `isEqual()`

```java
LocalTime lunch =
        LocalTime.of(12, 0);

LocalTime anotherLunch =
        LocalTime.of(12, 0);

System.out.println(
        lunch.isEqual(anotherLunch));
```

---

# Business Example 1 — Is the Store Open?

```java
LocalTime opening =
        LocalTime.of(8, 0);

LocalTime closing =
        LocalTime.of(18, 0);

LocalTime current =
        LocalTime.now();

boolean open =
        !current.isBefore(opening)
        && current.isBefore(closing);

System.out.println(open);
```

Why use:

```java
!current.isBefore(opening)
```

instead of:

```java
current.isAfter(opening)
```

Because `isAfter()` is **strict**.

If the store opens exactly at **08:00**, then:

```java
current.isAfter(opening)
```

returns:

```text
false
```

But the store should be considered open at exactly **08:00**.

Using:

```java
!current.isBefore(opening)
```

means:

* after the opening time ✅
* exactly at the opening time ✅

This is a common pattern when checking inclusive ranges.

---

# Business Example 2 — Office Hours

```java
LocalTime workStart =
        LocalTime.of(9, 0);

LocalTime workEnd =
        LocalTime.of(17, 0);

LocalTime employeeTime =
        LocalTime.now();

if (employeeTime.isAfter(workEnd)) {
    System.out.println("Late checkout.");
}
```

---

# Business Example 3 — Daily Alarm

```java
LocalTime alarm =
        LocalTime.of(6, 30);

System.out.println(
        "Alarm set for " + alarm);
```

---

# Method Chaining

```java
LocalTime result =
        LocalTime.now()
                .plusHours(1)
                .minusMinutes(15)
                .plusSeconds(10);
```

Each operation returns a new `LocalTime`.

---

# Common Mistakes

## Mistake 1 — Forgetting Immutability

```java
time.plusHours(2);
```

The original object doesn't change.

---

## Mistake 2 — Using `==`

Wrong:

```java
time1 == time2
```

Correct:

```java
time1.equals(time2)
```

or

```java
time1.isEqual(time2)
```

---

## Mistake 3 — Using `LocalTime` for Appointments

Imagine:

```text
Doctor appointment
09:30
```

Which day?

`LocalTime` cannot answer.

Use:

```java
LocalDateTime
```

instead.

---

## Mistake 4 — Assuming Time Arithmetic Changes the Date

This code:

```java
LocalTime.of(23, 30).plusHours(2);
```

returns:

```text
01:30
```

It does **not** tell you that a new day has started.

If crossing midnight is important, use `LocalDateTime`.

---

# Performance Considerations

`LocalTime` is:

* Immutable
* Lightweight
* Thread-safe
* Optimized for frequent use

Creating new instances is inexpensive and should not be avoided in normal applications.

---

# Best Practices

* Use `LocalTime` only when the date is irrelevant.
* Always remember that methods like `plusHours()` return a new object.
* Use `isBefore()`, `isAfter()`, and `isEqual()` for comparisons.
* Be aware that `LocalTime` wraps around midnight.
* Prefer `LocalDateTime` when both date and time are required.

---

# Guided Exercise 2 — Working with `LocalTime`

Create a new class named `LocalTimeExercises`.

### Step 1

Create a variable with the current time and print it.

Example:

```text
Current time: 09:42:18
```

---

### Step 2

Create the following times:

* Breakfast: **07:30**
* Lunch: **12:00**
* Dinner: **19:00**

Print all of them.

---

### Step 3

Print the following information about the current time:

* Hour
* Minute
* Second
* Nanosecond

---

### Step 4

Starting from **09:15**, calculate:

* +2 hours
* +45 minutes
* -30 minutes

Print each result.

---

### Step 5

Check whether the current time is before or after **18:00**.

Print an appropriate message:

```text
The workday is still in progress.
```

or

```text
The workday has ended.
```

---

### Step 6 (Challenge)

Implement a simple "store open" check.

Rules:

* Opens at **08:00**
* Closes at **18:00**

Use the current time and determine whether the store is open.

**Bonus challenge:** Modify the logic for a store that operates overnight, for example:

* Opens at **22:00**
* Closes at **06:00**

Think carefully about why the previous range check no longer works. We'll revisit this kind of scenario later in the module.

---

# Chapter Summary

In this chapter, you learned:

* What `LocalTime` represents.
* How to create current and specific times.
* How to access hours, minutes, seconds, and nanoseconds.
* How to perform time arithmetic.
* How `LocalTime` behaves when crossing midnight.
* How to compare times correctly.
* Practical business use cases and common pitfalls.

In the next chapter, we'll combine everything you've learned so far with **`LocalDateTime`**, allowing us to represent complete timestamps without a time zone—the most common choice for appointments, schedules, and calendar events.
