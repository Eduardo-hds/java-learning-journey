# Chapter 5 — Instant

Until now, we've worked with:

* `LocalDate`
* `LocalTime`
* `LocalDateTime`

These classes describe **local information**.

For example:

```text
2026-07-15T14:30
```

But there's an important question:

> **14:30 where?**

Brazil?

Japan?

London?

New York?

Without a time zone, the answer is unknown.

For applications that communicate across different regions, we need something different:

```java
Instant
```

An `Instant` represents **one exact moment on the global timeline**, independent of any local clock.

---

# Chapter Objectives

By the end of this chapter you will be able to:

* Understand UTC
* Understand the Unix Epoch
* Create `Instant` objects
* Convert between `Instant` and local date/time classes
* Compare instants
* Perform arithmetic
* Know when to use `Instant`
* Avoid common mistakes

---

# Why Do We Need `Instant`?

Imagine a user in Brazil buys a product at:

```text
15:00
```

A server in Germany receives the request.

What time was the purchase made?

If the application stores only:

```text
2026-07-15T15:00
```

the server has no idea which **15:00** this is.

Instead, we store an absolute point in time:

```text
2026-07-15T18:00:00Z
```

Every computer in the world interprets this as the **same instant**.

Each region can then display that instant in its own local time.

---

# Understanding UTC

Before learning `Instant`, you need to understand **UTC**.

UTC stands for:

> **Coordinated Universal Time**

It is the world's reference time standard.

Think of UTC as the "master clock."

Every time zone is defined as an offset from UTC.

Examples:

| Time Zone       | Offset |
| --------------- | -----: |
| UTC             | +00:00 |
| São Paulo       | -03:00 |
| London (winter) | +00:00 |
| Paris (winter)  | +01:00 |
| Tokyo           | +09:00 |

For example:

```text
UTC
18:00
```

becomes:

```text
São Paulo
15:00
```

and

```text
Tokyo
03:00 (next day)
```

The **instant never changes**—only its representation.

---

# The Unix Epoch

Computers often measure time from a fixed starting point called the **Unix Epoch**.

The epoch is:

```text
1970-01-01T00:00:00Z
```

This moment is considered **0 seconds**.

Examples:

```text
Epoch
↓

1970-01-01T00:00:00Z
```

```text
10 seconds later
↓

1970-01-01T00:00:10Z
```

```text
1000 seconds later
↓

1970-01-01T00:16:40Z
```

Internally, an `Instant` stores the number of seconds and nanoseconds relative to the Unix Epoch.

---

# Creating the Current Instant

```java
import java.time.Instant;

Instant now = Instant.now();

System.out.println(now);
```

Example output:

```text
2026-07-15T13:10:42.842517Z
```

Notice the final letter:

```text
Z
```

It means:

```text
UTC (+00:00)
```

---

# Creating a Specific Instant

You can create an `Instant` from an ISO-8601 string.

```java
Instant launch =
        Instant.parse("2026-08-01T15:00:00Z");

System.out.println(launch);
```

Output:

```text
2026-08-01T15:00:00Z
```

---

# Epoch Seconds

Every `Instant` can be converted into the number of seconds since the Unix Epoch.

```java
Instant now = Instant.now();

System.out.println(now.getEpochSecond());
```

Example:

```text
1784117442
```

This value is commonly stored in databases, logs, and distributed systems.

---

# Epoch Milliseconds

Many APIs use milliseconds instead of seconds.

```java
Instant now = Instant.now();

System.out.println(now.toEpochMilli());
```

Example:

```text
1784117442842
```

---

# Arithmetic

`Instant` supports arithmetic just like the other `java.time` classes.

## Adding Seconds

```java
Instant future =
        Instant.now()
                .plusSeconds(60);

System.out.println(future);
```

---

## Subtracting Seconds

```java
Instant past =
        Instant.now()
                .minusSeconds(120);
```

---

## Adding Hours

Since there isn't a dedicated `plusHours()` method on `Instant`, convert hours to seconds:

```java
Instant later =
        Instant.now()
                .plusSeconds(2 * 60 * 60);
```

Later in this module, you'll see a more expressive approach using `Duration`.

---

# Comparing Instants

## `isBefore()`

```java
Instant first =
        Instant.now();

Instant second =
        first.plusSeconds(10);

System.out.println(
        first.isBefore(second)
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
        second.isAfter(first)
);
```

---

## `equals()`

```java
Instant another = first;

System.out.println(
        first.equals(another)
);
```

---

# Why `isEqual()` Doesn't Exist

Unlike `LocalDate`, `LocalTime`, and `LocalDateTime`, the `Instant` class does **not** provide an `isEqual()` method.

That's because an `Instant` already represents an exact point in time with no calendar-system ambiguity.

To test equality, use:

```java
instant1.equals(instant2)
```

---

# Converting an `Instant` to Local Time

An `Instant` has **no time zone**.

To display it as a local date and time, Java needs a `ZoneId`.

Example:

```java
import java.time.*;

Instant now = Instant.now();

ZoneId zone =
        ZoneId.systemDefault();

LocalDateTime local =
        LocalDateTime.ofInstant(now, zone);

System.out.println(local);
```

The same `Instant` can produce different local times depending on the chosen time zone.

We'll explore this in detail in the Time Zones chapter.

---

# Business Example 1 — User Login

```java
Instant loginTime =
        Instant.now();

System.out.println(loginTime);
```

Store the login time in UTC.

When displaying it to users, convert it to their local time zone.

---

# Business Example 2 — Audit Logs

```java
Instant created =
        Instant.now();

System.out.println(
        "Record created at: " + created
);
```

Every server around the world records the same global timeline.

---

# Business Example 3 — API Communication

Two servers:

* Brazil
* Japan

Both exchange timestamps using:

```text
2026-07-15T18:00:00Z
```

No ambiguity.

Each server converts the instant to its own local time for display if needed.

---

# Internal Behavior

Conceptually, an `Instant` is stored like this:

```text
Seconds since Epoch

+

Nanoseconds adjustment
```

Illustration:

```text
1970-01-01T00:00:00Z
        │
        ▼
   + 1,784,117,442 seconds
        │
        ▼
2026-07-15T13:10:42Z
```

This numeric representation makes `Instant` ideal for calculations, comparisons, and storage.

---

# Common Mistakes

## Mistake 1 — Using `LocalDateTime` for Server Timestamps

Wrong:

```java
LocalDateTime.now();
```

Better:

```java
Instant.now();
```

Why?

`LocalDateTime` depends on the server's local clock and time zone.

`Instant` is universal.

---

## Mistake 2 — Expecting Local Time

Printing an `Instant`:

```java
System.out.println(Instant.now());
```

returns UTC, not your local time.

That's expected.

Convert it using a `ZoneId` if you need local representation.

---

## Mistake 3 — Forgetting Immutability

```java
instant.plusSeconds(60);
```

Nothing changes.

Always store the returned object.

---

# Performance Considerations

`Instant` is:

* Immutable
* Lightweight
* Thread-safe
* Optimized for timestamp calculations

It is one of the most commonly used classes in backend development because it provides an efficient, unambiguous representation of time.

---

# Best Practices

* Use `Instant` for machine-generated timestamps.
* Store timestamps in UTC.
* Convert to local time only when displaying information to users.
* Use `equals()`, `isBefore()`, and `isAfter()` for comparisons.
* Remember that an `Instant` is not intended for direct user-facing display.

---

# Guided Exercise 4 — Working with `Instant`

Create a new class named `InstantExercises`.

### Step 1

Create a variable with the current `Instant` and print it.

Example:

```text
Current instant:
2026-07-15T13:10:42.842517Z
```

---

### Step 2

Print:

* The current `Instant`
* The number of epoch seconds
* The number of epoch milliseconds

---

### Step 3

Create an `Instant` from the following string:

```text
2026-12-25T00:00:00Z
```

Print the result.

---

### Step 4

Starting from the current instant, create:

* One minute in the future
* Five minutes in the past

Print all three values.

---

### Step 5

Compare the three instants using:

* `isBefore()`
* `isAfter()`
* `equals()`

---

### Step 6 (Challenge)

Convert the current `Instant` into a `LocalDateTime` using your system's default time zone.

Print both values and observe:

* The `Instant` remains in UTC (`Z`).
* The `LocalDateTime` shows your local date and time.

---

# Chapter Summary

In this chapter, you learned:

* Why UTC is the global reference for time.
* What the Unix Epoch is.
* How `Instant` represents an exact point on the global timeline.
* How to create and compare `Instant` objects.
* How to perform arithmetic with instants.
* Why `Instant` is the preferred choice for server timestamps and distributed systems.
* How to convert an `Instant` into a local date and time using a `ZoneId`.

In the next chapter, we'll study **`Duration`** and **`Period`**, two classes that answer a different question: **"How much time has passed?"** You'll learn why Java provides two separate types for elapsed time and when each should be used.
